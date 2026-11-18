# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: journeys/fhir-diagnostic-report.spec.ts >> the standards screen shows lab and imaging reports offered as FHIR
- Location: e2e/journeys/fhir-diagnostic-report.spec.ts:9:1

# Error details

```
Error: expect(locator).toContainText(expected) failed

Locator: getByText('FHIR R4 EHR Exchange').locator('xpath=ancestor::*[contains(., \'DiagnosticReport\')][1]')
Expected substring: "DiagnosticReport"
Timeout: 10000ms
Error: element(s) not found

Call log:
  - Expect "toContainText" getByText('FHIR R4 EHR Exchange').locator('xpath=ancestor::*[contains(., \'DiagnosticReport\')][1]') with timeout 10000ms
  - waiting for getByText('FHIR R4 EHR Exchange').locator('xpath=ancestor::*[contains(., \'DiagnosticReport\')][1]')

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
  2  |  * An integration officer checks what the hospital's FHIR server offers an
  3  |  * ABDM health-information user (#225): the Standards screen reads the live
  4  |  * CapabilityStatement, and released lab and imaging reports are now on it as
  5  |  * DiagnosticReport, alongside Observation.
  6  |  */
  7  | import { expect, test } from "./support/world";
  8  | 
  9  | test("the standards screen shows lab and imaging reports offered as FHIR", async ({ hospital }) => {
  10 |   const page = await hospital.asAdmin();
  11 |   await page.goto("/admin/settings#standards");
  12 |   const card = page.getByText("FHIR R4 EHR Exchange").locator("xpath=ancestor::*[contains(., 'DiagnosticReport')][1]");
> 13 |   await expect(card).toContainText("DiagnosticReport");
     |                      ^ Error: expect(locator).toContainText(expected) failed
  14 |   await expect(card).toContainText("Observation");
  15 | });
  16 | 
```