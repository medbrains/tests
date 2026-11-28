# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: crud/patient-scores.spec.ts >> patient assessment scores >> a patient's recorded scores are on their admission
- Location: e2e/crud/patient-scores.spec.ts:13:3

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByText('Aldrete recovery score')
Expected: visible
Timeout: 15000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" getByText('Aldrete recovery score') with timeout 15000ms
  - waiting for getByText('Aldrete recovery score')

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
  2  | import { navigateTo } from "../helpers";
  3  | 
  4  | /**
  5  |  * A score that belongs to the patient.
  6  |  *
  7  |  * Care View carries twenty of these as ward-level calculators: pick five
  8  |  * values, read a number, keep nothing. An Aldrete IS the record that a
  9  |  * patient was fit to leave recovery, and NEWS2 exists to show deterioration —
  10 |  * neither survives being arithmetic.
  11 |  */
  12 | test.describe("patient assessment scores", () => {
  13 |   test("a patient's recorded scores are on their admission", async ({ page }) => {
  14 |     await navigateTo(page, "/ipd/admissions/b052afe0-bc1c-48e2-9260-a7ead7a48ab0#scores");
> 15 |     await expect(page.getByText("Aldrete recovery score")).toBeVisible({ timeout: 15000 });
     |                                                            ^ Error: expect(locator).toBeVisible() failed
  16 |     // Recorded earlier against this admission — proving the history reads
  17 |     // back, which is the whole difference from a calculator.
  18 |     await expect(page.getByText("Recorded scores")).toBeVisible();
  19 |   });
  20 | 
  21 |   test("the discharge threshold is stated, not left to memory", async ({ page }) => {
  22 |     await navigateTo(page, "/ipd/admissions/b052afe0-bc1c-48e2-9260-a7ead7a48ab0#scores");
  23 |     // Defaults are 2 across five parameters, so the total is 10 — at or above
  24 |     // the threshold of 9.
  25 |     await expect(page.getByText(/Total 10 of 10/)).toBeVisible({ timeout: 15000 });
  26 |   });
  27 | });
  28 | 
```