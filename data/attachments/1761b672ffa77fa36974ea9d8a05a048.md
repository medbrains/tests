# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: forms/patient-edit.spec.ts >> Patient edit route >> loads the edit form for an existing patient
- Location: e2e/forms/patient-edit.spec.ts:13:3

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByText('Update demographic, contact, and clinical-safety fields')
Expected: visible
Timeout: 10000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" getByText('Update demographic, contact, and clinical-safety fields') with timeout 10000ms
  - waiting for getByText('Update demographic, contact, and clinical-safety fields')

```

```yaml
- complementary "About MedBrains":
  - paragraph: MedBrains
  - paragraph: For Indian hospitals · NABH · ABDM
  - heading "The whole hospital. One system." [level=2]
  - paragraph: From the front desk to the discharge summary — OPD, wards, lab, pharmacy and billing, with every rule built in.
  - list:
    - listitem:
      - paragraph: One patient, one record
      - paragraph: A UHID at the front desk and the same chart in OPD, wards, lab, pharmacy and billing.
    - listitem:
      - paragraph: The rules are in the screens
      - paragraph: NABH workflows, Schedule H and NDPS at the counter, and every access on record.
    - listitem:
      - paragraph: Web and native apps
      - paragraph: Staff and patient apps for iPhone and Android, token boards for the waiting room.
    - listitem:
      - paragraph: Your hospital's data, sealed
      - paragraph: Each hospital is isolated in the database itself, and its data is kept in India.
  - region "Health tips":
    - paragraph: Health tip
    - paragraph: Fill half your plate with fruit & veg
    - paragraph: Five servings a day supports immunity, digestion and long-term health.
    - paragraph: "Source: ICMR–NIN Dietary Guidelines"
    - button "Pause health tips":
      - img
    - tablist "Choose a health tip":
      - tab "Tip 1 of 6"
      - tab "Tip 2 of 6" [selected]
      - tab "Tip 3 of 6"
      - tab "Tip 4 of 6"
      - tab "Tip 5 of 6"
      - tab "Tip 6 of 6"
    - button "Previous tip":
      - img
    - button "Next tip":
      - img
- main:
  - heading "Sign in" [level=1]
  - paragraph: Start with your hospital
  - text: Hospital code
  - paragraph: The code your hospital gave you, e.g. CITYHOSP.
  - img
  - textbox "Hospital code"
  - alert:
    - img
    - text: Couldn't reach the hospital server. This is a connection problem, not a wrong code — try again in a moment.
  - button "Continue" [disabled]
  - button "Dev credentials"
  - text: MedBrains v3.33.2
  - paragraph:
    - link "Terms":
      - /url: /terms
    - text: ·
    - link "Privacy":
      - /url: /privacy
```

# Test source

```ts
  1  | import { expect, test } from "@playwright/test";
  2  | import { BACKEND_URL, getAuthToken, navigateTo, routeApiDirect } from "../helpers";
  3  | 
  4  | test.describe("Patient edit route", () => {
  5  |   test.beforeEach(async ({ page }) => {
  6  |     await routeApiDirect(page);
  7  |   });
  8  | 
  9  |   test.afterEach(async ({ page }) => {
  10 |     await page.unrouteAll({ behavior: "ignoreErrors" });
  11 |   });
  12 | 
  13 |   test("loads the edit form for an existing patient", async ({ page, request }) => {
  14 |     const { cookies } = await getAuthToken(request);
  15 |     const resp = await request.get(`${BACKEND_URL}/api/patients?per_page=1`, {
  16 |       headers: { Cookie: cookies },
  17 |     });
  18 |     expect(resp.ok()).toBeTruthy();
  19 | 
  20 |     const body = (await resp.json()) as { patients?: Array<{ id: string }> };
  21 |     const patient = body.patients?.[0];
  22 |     test.skip(!patient, "no seeded patient available");
  23 | 
  24 |     await navigateTo(page, `/patients/${patient.id}/edit`);
  25 | 
  26 |     await expect(
  27 |       page.getByText("Update demographic, contact, and clinical-safety fields"),
> 28 |     ).toBeVisible();
     |       ^ Error: expect(locator).toBeVisible() failed
  29 |     await expect(page.getByPlaceholder("Prefix")).toBeVisible();
  30 |   });
  31 | });
  32 | 
```