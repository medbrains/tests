# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: journeys/patient-notices.spec.ts >> the administrator switches a patient notice off and it stays off
- Location: e2e/journeys/patient-notices.spec.ts:18:1

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByRole('row').filter({ hasText: 'Tell the patient their lab report is ready' })
Expected: visible
Timeout: 10000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" getByRole('row').filter({ hasText: 'Tell the patient their lab report is ready' }) with timeout 10000ms
  - waiting for getByRole('row').filter({ hasText: 'Tell the patient their lab report is ready' })

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
  1  | /**
  2  |  * The hospital decides which notices go out (#205). The administrator sees
  3  |  * every notice the system can send — report ready, claim approved,
  4  |  * prescription expiring, low stock, serious incident — on the Integration Hub,
  5  |  * switches one off, and finds it still off when they come back.
  6  |  */
  7  | import { expect, test } from "./support/world";
  8  | 
  9  | const NOTICES = [
  10 |   "Tell the patient their lab report is ready",
  11 |   "Tell the patient their imaging report is ready",
  12 |   "SMS the patient when the insurer approves their claim",
  13 |   "SMS the patient three days before a prescription with refills left expires",
  14 |   "Email the pharmacists when a drug falls to its reorder level",
  15 |   "Email quality and administration about a major or sentinel incident",
  16 | ];
  17 | 
  18 | test("the administrator switches a patient notice off and it stays off", async ({ hospital }) => {
  19 |   test.setTimeout(90_000);
  20 |   const page = await hospital.asAdmin();
  21 |   await page.goto("/admin/integration-hub");
  22 |   for (const notice of NOTICES) {
> 23 |     await expect(page.getByRole("row").filter({ hasText: notice })).toBeVisible();
     |                                                                     ^ Error: expect(locator).toBeVisible() failed
  24 |   }
  25 | 
  26 |   const row = page.getByRole("row").filter({ hasText: NOTICES[2] });
  27 |   const toggle = row.getByRole("switch");
  28 |   await expect(toggle).toBeChecked();
  29 |   await toggle.click({ force: true });
  30 |   await expect(row).toContainText("Disabled");
  31 | 
  32 |   await page.reload();
  33 |   const again = page.getByRole("row").filter({ hasText: NOTICES[2] });
  34 |   await expect(again).toContainText("Disabled");
  35 |   await expect(again.getByRole("switch")).not.toBeChecked();
  36 | 
  37 |   // Put it back for the rest of the suite.
  38 |   await again.getByRole("switch").click({ force: true });
  39 |   await expect(again).toContainText("Active");
  40 | });
  41 | 
```