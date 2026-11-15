# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: linkages/bed-lifecycle.spec.ts >> A bed follows the admission through transfer and discharge >> occupied → transferred → released, with a turnaround entry per release
- Location: e2e/linkages/bed-lifecycle.spec.ts:32:3

# Error details

```
Error: expect(received).not.toContain(expected) // indexOf

Expected value: not "6111c2dd-bef7-41c8-b206-74ceeafff85b"
Received array:     ["af1f5190-84cf-407f-b2f1-f485efe8f5cb", "0712125a-49e9-41c3-8ed4-1ce284c38d2e", "6111c2dd-bef7-41c8-b206-74ceeafff85b", "d346f4ef-34d9-449e-9006-9f4d372d388f", "56868e22-1679-44f2-9ea7-3da24095654c", "1d1c0af4-17ce-4677-9285-c121e7bb1f3f", "6c7d2f2a-35c6-4eb0-91d4-ce12525d17d7", "97a29523-a931-4cb8-ba6d-ba8419100dd1", "7b384287-c46c-454b-8993-7a0ef04b9410", "e59a6d1c-8ff6-48cc-892c-21b0b8ffc7cd", "128e1650-6ccb-43ef-a693-147d613fb316", "5c9a4281-eb5e-4d06-80f6-32d67b383906", "e61a1ca5-3e0c-4346-8e3e-51fd47b06535", "a3edafba-158b-4cd2-a609-369ee5bd7367", "5f985544-fd09-409f-ab55-d7a9e9e08e4e", "17b3ee63-3347-47b5-9eff-503c161603e0", "e7e15121-2855-442c-8e99-c0fc4bc0573b", "e477144d-e53c-4c32-9b9b-262edfc3011d", "7b49a489-758a-4d31-a488-54d3dbef525a", "d38e09e6-d73c-4ced-85bb-9220bc351a76", "6ec11dda-931c-4e63-9f00-69eb9a61acda", "94185c70-1523-49f6-bf8a-a39cd9ab1d9e", "9784512f-092d-40c8-aad9-f88db2ab08b9", "f34dcbc1-6b76-4f8f-830e-a76c4aa6e5cd", "8823076a-5435-4486-9376-9b3bb906af39", "a4f41c82-7f41-4831-9f8e-fb33b1bee289", "8f305ee9-8713-4412-a4a7-4019483d8a96", "30edf8fa-324d-44a3-91df-1cf202b4d3d3", "5b77d226-b660-4a3f-9758-b164229bd29b", "5782d2e1-d592-4811-b799-d81eeacf90d9", "88aa0435-e555-4359-9db8-fe56b87900b2"]
```

# Test source

```ts
  1  | /**
  2  |  * Bed lifecycle — admit, transfer, discharge, turnaround.
  3  |  *
  4  |  * A bed is a location row with one bed_states row. Admission takes it
  5  |  * (occupied, and gone from the available list), a transfer hands the old
  6  |  * bed to housekeeping (vacant_dirty) and takes the new one, discharge hands
  7  |  * the last bed over the same way. Every release writes a turnaround entry;
  8  |  * completing it stamps ready_at, and only a status change to vacant_clean
  9  |  * puts the bed back in the available list.
  10 |  *
  11 |  * The negatives are what keep two patients out of one bed: a second
  12 |  * admission into an occupied bed and a transfer onto the bed already held
  13 |  * are both refused.
  14 |  */
  15 | 
  16 | import { expect, test } from "@playwright/test";
  17 | import { api, getAuthContextFromCookies } from "../helpers/api";
  18 | import { freshWardBeds,
  19 |   admitToIpd,
  20 |   completeBedTurnaround,
  21 |   createPatientApi,
  22 |   dischargeAdmission,
  23 |   getBedDashboardBeds,
  24 |   listAvailableBeds,
  25 |   listBedTurnaround,
  26 |   setBedStatus,
  27 |   transferAdmissionBed,
  28 | } from "../helpers/journey-steps";
  29 | import { getIpdDept } from "../helpers/seed-resolvers";
  30 | 
  31 | test.describe("A bed follows the admission through transfer and discharge", () => {
  32 |   test("occupied → transferred → released, with a turnaround entry per release", async ({ request }) => {
  33 |     const admin = await getAuthContextFromCookies(request);
  34 |     const [bedA, bedB] = await freshWardBeds(admin, 2);
  35 |     if (!bedA || !bedB) throw new Error("two beds of this run's own");
  36 |     const patient = await createPatientApi(admin);
  37 | 
  38 |     const admissionId = await admitToIpd(admin, { patientId: patient.id, bedId: bedA.bed_id });
  39 | 
  40 |     const bedRow = async (bedId: string) => {
  41 |       const row = (await getBedDashboardBeds(admin)).find((b) => b.bed_location_id === bedId);
  42 |       expect(row, `dashboard row for ${bedId}`).toBeDefined();
  43 |       return row as NonNullable<typeof row>;
  44 |     };
  45 | 
  46 |     expect(await bedRow(bedA.bed_id)).toMatchObject({ bed_status: "occupied", admission_id: admissionId });
  47 |     expect((await listAvailableBeds(admin)).map((b) => b.bed_id)).not.toContain(bedA.bed_id);
  48 | 
  49 |     // Negative: nobody else gets that bed.
  50 |     const second = await createPatientApi(admin);
  51 |     await api(
  52 |       admin,
  53 |       "POST",
  54 |       "/api/ipd/admissions",
  55 |       { patient_id: second.id, department_id: (await getIpdDept(admin)).id, bed_id: bedA.bed_id },
  56 |       { expectStatus: 400 },
  57 |     );
  58 | 
  59 |     await transferAdmissionBed(admin, admissionId, bedB.bed_id, "Isolation required");
  60 |     expect(await bedRow(bedA.bed_id)).toMatchObject({ bed_status: "vacant_dirty", admission_id: null });
  61 |     expect(await bedRow(bedB.bed_id)).toMatchObject({ bed_status: "occupied", admission_id: admissionId });
  62 |     const afterTransfer = (await listBedTurnaround(admin)).find(
  63 |       (t) => t.bed_id === bedA.bed_id && t.admission_id === admissionId,
  64 |     );
  65 |     expect(afterTransfer, "the released bed is on housekeeping's list").toBeDefined();
  66 |     expect(afterTransfer?.ready_at).toBeNull();
  67 | 
  68 |     // Negative: a transfer onto the bed already held is refused.
  69 |     await transferAdmissionBed(admin, admissionId, bedB.bed_id, "Same bed", { expectStatus: 400 });
  70 | 
  71 |     await dischargeAdmission(admin, admissionId);
  72 |     const detail = await api<{ admission: { status: string; bed_id: string | null } }>(
  73 |       admin,
  74 |       "GET",
  75 |       `/api/ipd/admissions/${admissionId}`,
  76 |     );
  77 |     expect(detail.admission.status).toBe("discharged");
  78 |     expect(await bedRow(bedB.bed_id)).toMatchObject({ bed_status: "vacant_dirty", admission_id: null });
  79 | 
  80 |     const afterDischarge = (await listBedTurnaround(admin)).find(
  81 |       (t) => t.bed_id === bedB.bed_id && t.admission_id === admissionId,
  82 |     );
  83 |     expect(afterDischarge).toBeDefined();
  84 |     const done = await completeBedTurnaround(admin, (afterDischarge as { id: string }).id);
  85 |     expect(done.ready_at).not.toBeNull();
  86 |     expect(typeof done.turnaround_minutes).toBe("number");
  87 | 
  88 |     // Cleaning done is not the same as ready for the next patient: the bed
  89 |     // returns to the available list only when its status says vacant_clean.
> 90 |     expect((await listAvailableBeds(admin)).map((b) => b.bed_id)).not.toContain(bedB.bed_id);
     |                                                                       ^ Error: expect(received).not.toContain(expected) // indexOf
  91 |     await setBedStatus(admin, bedB.bed_id, "vacant_clean");
  92 |     await setBedStatus(admin, bedA.bed_id, "vacant_clean");
  93 |     expect((await listAvailableBeds(admin)).map((b) => b.bed_id)).toEqual(
  94 |       expect.arrayContaining([bedA.bed_id, bedB.bed_id]),
  95 |     );
  96 |   });
  97 | });
  98 | 
```