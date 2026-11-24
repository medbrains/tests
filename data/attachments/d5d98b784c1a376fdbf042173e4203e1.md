# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: journeys/mlc-injuries.spec.ts >> a doctor records an injury on an MLC by its site on the body
- Location: e2e/journeys/mlc-injuries.spec.ts:10:1

# Error details

```
Test timeout of 120000ms exceeded.
```

```
Error: locator.click: Target page, context or browser has been closed
Call log:
  - waiting for getByRole('tab', { name: /MLC/ })

```

# Page snapshot

```yaml
- generic [ref=e3]:
  - complementary "About MedBrains" [ref=e4]:
    - generic [ref=e5]:
      - paragraph [ref=e7]: MedBrains
      - generic [ref=e8]:
        - paragraph [ref=e9]: For Indian hospitals · NABH · ABDM
        - heading "The whole hospital. One system." [level=2] [ref=e10]:
          - text: The whole hospital.
          - generic [ref=e11]: One system.
        - paragraph [ref=e12]: From the front desk to the discharge summary — OPD, wards, lab, pharmacy and billing, with every rule built in.
      - list [ref=e13]:
        - listitem [ref=e14]:
          - generic [ref=e20]:
            - paragraph [ref=e21]: One patient, one record
            - paragraph [ref=e22]: A UHID at the front desk and the same chart in OPD, wards, lab, pharmacy and billing.
        - listitem [ref=e23]:
          - generic [ref=e28]:
            - paragraph [ref=e29]: The rules are in the screens
            - paragraph [ref=e30]: NABH workflows, Schedule H and NDPS at the counter, and every access on record.
        - listitem [ref=e31]:
          - generic [ref=e35]:
            - paragraph [ref=e36]: Web and native apps
            - paragraph [ref=e37]: Staff and patient apps for iPhone and Android, token boards for the waiting room.
        - listitem [ref=e38]:
          - generic [ref=e44]:
            - paragraph [ref=e45]: Your hospital's data, sealed
            - paragraph [ref=e46]: Each hospital is isolated in the database itself, and its data is kept in India.
      - region "Health tips" [ref=e48]:
        - generic [ref=e49]:
          - paragraph [ref=e50]: Health tip
          - paragraph [ref=e51]: Know your numbers
          - paragraph [ref=e52]: Regular blood-pressure, sugar and cholesterol checks catch silent risks early.
          - paragraph [ref=e53]: "Source: Indian Heart Association"
        - generic [ref=e54]:
          - generic [ref=e55]:
            - button "Pause health tips" [ref=e56] [cursor=pointer]
            - tablist "Choose a health tip" [ref=e61]:
              - tab "Tip 1 of 6" [ref=e62] [cursor=pointer]
              - tab "Tip 2 of 6" [ref=e63] [cursor=pointer]
              - tab "Tip 3 of 6" [ref=e64] [cursor=pointer]
              - tab "Tip 4 of 6" [ref=e65] [cursor=pointer]
              - tab "Tip 5 of 6" [selected] [ref=e66] [cursor=pointer]
              - tab "Tip 6 of 6" [ref=e67] [cursor=pointer]
          - generic [ref=e68]:
            - button "Previous tip" [ref=e69] [cursor=pointer]
            - button "Next tip" [ref=e73] [cursor=pointer]
  - main [ref=e77]:
    - generic [ref=e78]:
      - generic [ref=e79]:
        - heading "Sign in" [level=1] [ref=e81]
        - paragraph [ref=e82]: Start with your hospital
      - generic [ref=e83]:
        - generic [ref=e84]:
          - generic [ref=e85]: Hospital code *
          - paragraph [ref=e86]: The code your hospital gave you, e.g. CITYHOSP.
          - textbox "Hospital code" [active] [ref=e92]
        - button "Continue" [disabled] [ref=e93]
      - generic [ref=e96]:
        - button "Dev credentials" [ref=e98] [cursor=pointer]
        - generic [ref=e99]: MedBrains v3.33.2
        - paragraph [ref=e100]:
          - link "Terms" [ref=e101] [cursor=pointer]:
            - /url: /terms
          - text: ·
          - link "Privacy" [ref=e102] [cursor=pointer]:
            - /url: /privacy
```

# Test source

```ts
  1  | /**
  2  |  * An injury on a medico-legal case is recorded from the case page — site
  3  |  * picked on the body — and listed numbered, with its printed size, the way
  4  |  * the injury certificate reads it.
  5  |  */
  6  | import { api } from "../helpers/api";
  7  | import { createPatientApi } from "../helpers/journey-steps";
  8  | import { expect, test } from "./support/world";
  9  | 
  10 | test("a doctor records an injury on an MLC by its site on the body", async ({ hospital }) => {
  11 |   test.setTimeout(120_000); // the anatomy model is ~33 MB on first open
  12 |   const patient = await createPatientApi(hospital.admin);
  13 |   const mlc = await api<{ id: string; mlc_number: string }>(
  14 |     hospital.admin,
  15 |     "POST",
  16 |     "/api/emergency/mlc",
  17 |     { patient_id: patient.id, case_type: "assault" },
  18 |   );
  19 | 
  20 |   const page = await hospital.asAdmin();
  21 |   await page.goto("/emergency");
> 22 |   await page.getByRole("tab", { name: /MLC/ }).click();
     |                                                ^ Error: locator.click: Target page, context or browser has been closed
  23 |   await page
  24 |     .getByRole("button", { name: `View MLC case ${mlc.mlc_number}: details and documents` })
  25 |     .click();
  26 | 
  27 |   const injuries = page.getByRole("form", { name: "Record an injury" });
  28 |   await injuries.getByRole("button", { name: "Pick injury site on the body" }).click();
  29 |   const picker = page.getByRole("dialog", { name: "Pick injury site" });
  30 |   await picker.getByLabel("Find a region or structure").fill("Left patella");
  31 |   await page.getByRole("option", { name: "Left patella", exact: true }).click();
  32 |   await picker.getByRole("button", { name: "Use this site" }).click();
  33 |   await injuries.getByRole("textbox", { name: "length (cm)" }).fill("4.5");
  34 |   await injuries.getByRole("textbox", { name: "width (cm)" }).fill("0.5");
  35 |   await injuries.getByRole("button", { name: "Record injury" }).click();
  36 | 
  37 |   const row = page.getByRole("row", { name: /Left patella/ });
  38 |   await expect(row).toBeVisible();
  39 |   await expect(row).toContainText("4.5 × 0.5 cm");
  40 |   await expect(row.getByRole("cell").first()).toHaveText("1");
  41 | });
  42 | 
```