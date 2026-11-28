# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: forms/patient-register.spec.ts >> PatientRegisterForm field validation >> registration context exposes all canonical patient types and sources
- Location: e2e/forms/patient-register.spec.ts:28:3

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByText('Patient registration')
Expected: visible
Timeout: 10000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" getByText('Patient registration') with timeout 10000ms
  - waiting for getByText('Patient registration')

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
  2  | import type { Locator, Page } from "@playwright/test";
  3  | import { navigateTo, routeApiDirect } from "../helpers";
  4  | import { patientRegisterSchema } from "./schemas/patient-register";
  5  | 
  6  | test.describe("PatientRegisterForm field validation", () => {
  7  |   test.beforeEach(async ({ page }) => {
  8  |     await routeApiDirect(page);
  9  |     await navigateTo(page, patientRegisterSchema.navigatePath);
> 10 |     await expect(page.getByText("Patient registration")).toBeVisible();
     |                                                          ^ Error: expect(locator).toBeVisible() failed
  11 |   });
  12 | 
  13 |   test.afterEach(async ({ page }) => {
  14 |     await page.unrouteAll({ behavior: "ignoreErrors" });
  15 |   });
  16 | 
  17 |   test("required fields reject blank submission", async ({ page }) => {
  18 |     await page.getByRole("button", { name: /Save now/i }).click();
  19 | 
  20 |     // The shared registration rules (#4668): a first name, a sex, and a phone
  21 |     // or "Has no phone". A last name is not required — one name is a whole name.
  22 |     await expect(page.getByText("First name is required")).toBeVisible();
  23 |     await expect(page.getByText("Choose the patient's sex")).toBeVisible();
  24 |     await expect(page.getByText("Enter a phone number, or tick Has no phone")).toBeVisible();
  25 |     await expect(page.getByText("Last name is required")).toHaveCount(0);
  26 |   });
  27 | 
  28 |   test("registration context exposes all canonical patient types and sources", async ({ page }) => {
  29 |     await expectSelectOptions(page, page.getByRole("combobox", { name: "Registration type" }), [
  30 |       "New",
  31 |       "Revisit",
  32 |       "Transfer in",
  33 |       "Referral",
  34 |       "Emergency",
  35 |       "Camp",
  36 |       "Telemedicine",
  37 |       "Pre-registration",
  38 |     ]);
  39 | 
  40 |     await expectSelectOptions(page, page.getByRole("combobox", { name: "Registration source" }), [
  41 |       "Walk-in",
  42 |       "Phone",
  43 |       "Online portal",
  44 |       "Mobile app",
  45 |       "Kiosk",
  46 |       "Referral",
  47 |       "Ambulance",
  48 |       "Camp",
  49 |       "Telemedicine",
  50 |     ]);
  51 |   });
  52 | 
  53 |   test("DOB, age hint, calendar popover, and phone prefix stay usable", async ({ page }) => {
  54 |     await expect(page.locator('input[aria-label="Primary phone country"]')).toHaveValue(/\+\d+/);
  55 |     await expect(page.locator('input[aria-label="Phone (primary) Phone Primary"]')).toBeVisible();
  56 | 
  57 |     await page.locator('input[aria-label="Age years"]').fill("25");
  58 |     await expect(page.getByText(/As of today: 25 years/i)).toBeVisible();
  59 | 
  60 |     await page.getByLabel("Date of birth").click();
  61 |     await expect(page.getByRole("dialog")).toBeVisible();
  62 |   });
  63 | });
  64 | 
  65 | test.describe("PatientRegisterForm mobile viewport", () => {
  66 |   test.use({ viewport: { width: 390, height: 844 }, isMobile: true, hasTouch: true });
  67 | 
  68 |   test.beforeEach(async ({ page }) => {
  69 |     await routeApiDirect(page);
  70 |     await navigateTo(page, patientRegisterSchema.navigatePath);
  71 |     await expect(page.getByText("Patient registration")).toBeVisible();
  72 |   });
  73 | 
  74 |   test.afterEach(async ({ page }) => {
  75 |     await page.unrouteAll({ behavior: "ignoreErrors" });
  76 |   });
  77 | 
  78 |   test("keeps registration context usable on a mobile-sized device", async ({ page }) => {
  79 |     // Qualify by role. Mantine's Select renders the visible combobox *and* a
  80 |     // hidden input carrying the value for form submission, and both inherit
  81 |     // the label — so a bare getByLabel matches two elements and fails strict
  82 |     // mode. The field was visible the whole time; the locator was ambiguous.
  83 |     await expect(page.getByRole("combobox", { name: "Registration type" })).toBeVisible();
  84 |     await expect(page.getByRole("combobox", { name: "Registration source" })).toBeVisible();
  85 |     await expect(page.getByRole("combobox", { name: "Camp reference" })).toBeVisible();
  86 |     await expect(page.locator('input[aria-label="Primary phone country"]')).toBeVisible();
  87 |     await expect(page.locator('input[aria-label="Phone (primary) Phone Primary"]')).toBeVisible();
  88 |   });
  89 | });
  90 | 
  91 | async function expectSelectOptions(page: Page, trigger: Locator, labels: string[]) {
  92 |   await trigger.click();
  93 |   for (const label of labels) {
  94 |     await expect(page.getByRole("option", { name: label, exact: true })).toBeVisible();
  95 |   }
  96 |   await page.keyboard.press("Escape");
  97 | }
  98 | 
```