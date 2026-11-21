# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: journeys/onboarding-workbook.spec.ts >> an admin sets the hospital up from the onboarding workbook
- Location: e2e/journeys/onboarding-workbook.spec.ts:38:1

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByRole('heading', { name: 'Onboarding workbook' })
Expected: visible
Timeout: 10000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" getByRole('heading', { name: 'Onboarding workbook' }) with timeout 10000ms
  - waiting for getByRole('heading', { name: 'Onboarding workbook' })

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
  1  | /**
  2  |  * The hospital's admin sets up departments, a ward, its beds and staff from
  3  |  * the onboarding workbook: downloads it, fills it, uploads it. A mistake is
  4  |  * shown by sheet, row and column with nothing changed; the corrected file is
  5  |  * checked, then applied, and the new ward's beds are there.
  6  |  */
  7  | import { mkdtempSync } from "node:fs";
  8  | import { tmpdir } from "node:os";
  9  | import { join } from "node:path";
  10 | import writeXlsxFile from "write-excel-file/node";
  11 | import { expect, test } from "./support/world";
  12 | 
  13 | type Cells = (string | null)[][];
  14 | 
  15 | async function writeBook(path: string, t: string, role: string) {
  16 |   const sheet = (title: string, rows: Cells) => ({
  17 |     sheet: title,
  18 |     data: rows.map((r) => r.map((value) => ({ value }))),
  19 |   });
  20 |   await writeXlsxFile([
  21 |       sheet("Departments", [["Code", "Name", "Type"], [`ORT${t}`, "Orthopaedics", "clinical"]]),
  22 |       sheet("Wards", [
  23 |         ["Code", "Name", "Ward type", "Admits", "Department code"],
  24 |         [`OW${t}`, `Ortho Ward ${t}`, "general", "any", `ORT${t}`],
  25 |       ]),
  26 |       sheet("Beds", [
  27 |         ["Bed code", "Ward code", "Room"],
  28 |         [`OB${t}1`, `OW${t}`, `OR${t}`],
  29 |         [`OB${t}2`, `OW${t}`, `OR${t}`],
  30 |       ]),
  31 |       sheet("Staff", [
  32 |         ["Username", "Full name", "Email", "Role", "Departments"],
  33 |         [`ortho_${t.toLowerCase()}`, "Dr Arjun Rao", `arjun.${t.toLowerCase()}@example.test`, role, `ORT${t}`],
  34 |       ]),
  35 |   ]).toFile(path);
  36 | }
  37 | 
  38 | test("an admin sets the hospital up from the onboarding workbook", async ({ hospital }) => {
  39 |   const t = `${Date.now().toString(36)}`.toUpperCase().slice(-6);
  40 |   const dir = mkdtempSync(join(tmpdir(), "workbook-"));
  41 |   const page = await hospital.asAdmin();
  42 |   await page.goto("/admin/workbook");
> 43 |   await expect(page.getByRole("heading", { name: "Onboarding workbook" })).toBeVisible();
     |                                                                            ^ Error: expect(locator).toBeVisible() failed
  44 | 
  45 |   const [download] = await Promise.all([
  46 |     page.waitForEvent("download"),
  47 |     page.getByRole("button", { name: "Blank workbook" }).click(),
  48 |   ]);
  49 |   expect(download.suggestedFilename()).toMatch(/onboarding-workbook-blank\.xlsx$/);
  50 | 
  51 |   const wrong = join(dir, "wrong.xlsx");
  52 |   await writeBook(wrong, t, "surgeon");
  53 |   const chooser = page.waitForEvent("filechooser");
  54 |   await page.getByRole("button", { name: "Choose workbook (.xlsx)" }).click();
  55 |   await (await chooser).setFiles(wrong);
  56 |   const result = page.getByTestId("workbook-result");
  57 |   await expect(result.getByText("1 problem(s) to fix")).toBeVisible();
  58 |   const problem = result.getByRole("table", { name: "Problems" }).getByRole("row").nth(1);
  59 |   await expect(problem).toContainText("Staff");
  60 |   await expect(problem).toContainText("2");
  61 |   await expect(problem).toContainText("Role");
  62 |   await expect(result.getByRole("button", { name: "Apply workbook" })).toHaveCount(0);
  63 | 
  64 |   const right = join(dir, "right.xlsx");
  65 |   await writeBook(right, t, "doctor");
  66 |   const again = page.waitForEvent("filechooser");
  67 |   await page.getByRole("button", { name: "Choose workbook (.xlsx)" }).click();
  68 |   await (await again).setFiles(right);
  69 |   await expect(result.getByText("Checked — ready to apply")).toBeVisible();
  70 |   const beds = result.getByRole("table", { name: "Changes by sheet" }).getByRole("row", { name: /Beds/ });
  71 |   await expect(beds).toContainText("2");
  72 |   await result.getByRole("button", { name: "Apply workbook" }).click();
  73 |   await expect(result.getByText("Applied")).toBeVisible();
  74 |   await expect(result.getByText("1 new staff have been emailed how to set their password.")).toBeVisible();
  75 | 
  76 |   const [filled] = await Promise.all([
  77 |     page.waitForEvent("download"),
  78 |     page.getByRole("button", { name: "With current data" }).click(),
  79 |   ]);
  80 |   expect(filled.suggestedFilename()).toMatch(/onboarding-workbook\.xlsx$/);
  81 | });
  82 | 
```