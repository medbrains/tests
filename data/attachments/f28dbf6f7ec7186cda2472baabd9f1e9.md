# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: journeys/dashboard-widget-picker.spec.ts >> a manager hides and restores a widget from the widget menu
- Location: e2e/journeys/dashboard-widget-picker.spec.ts:8:1

# Error details

```
Error: expect(locator).toBeChecked() failed

Locator:  getByRole('dialog', { name: 'Widgets' }).getByRole('group', { name: 'IPD' }).getByRole('checkbox', { name: 'Mortality' })
Expected: checked
Received: unchecked
Timeout:  10000ms

Call log:
  - Expect "toBeChecked" getByRole('dialog', { name: 'Widgets' }).getByRole('group', { name: 'IPD' }).getByRole('checkbox', { name: 'Mortality' }) with timeout 10000ms
  - waiting for getByRole('dialog', { name: 'Widgets' }).getByRole('group', { name: 'IPD' }).getByRole('checkbox', { name: 'Mortality' })
    23 × locator resolved to <input type="checkbox" id="mantine-d1viegwbt" data-with-error-styles="true" aria-describedby="mantine-d1viegwbt-description" class="mantine-focus-auto m_26063560 mantine-Checkbox-input"/>
       - unexpected value "unchecked"

```

```yaml
- checkbox "Mortality"
```

# Test source

```ts
  1  | /**
  2  |  * A viewer chooses their dashboard's widgets from a menu of what their
  3  |  * access allows: a manager takes the mortality tile off and puts it back; a
  4  |  * nurse is never offered management KPIs.
  5  |  */
  6  | import { expect, test } from "./support/world";
  7  | 
  8  | test("a manager hides and restores a widget from the widget menu", async ({ hospital }) => {
  9  |   const page = await hospital.as("hospital_admin");
  10 |   await page.goto("/dashboard");
  11 |   const mortality = page.locator(".stat-card").filter({ hasText: "Mortality" });
  12 |   await expect(mortality).toBeVisible();
  13 | 
  14 |   await page.getByRole("button", { name: "Choose dashboard widgets" }).click();
  15 |   const menu = page.getByRole("dialog", { name: "Widgets" });
  16 |   const ipd = menu.getByRole("group", { name: "IPD" });
  17 |   const box = ipd.getByRole("checkbox", { name: "Mortality" });
> 18 |   await expect(box).toBeChecked();
     |                     ^ Error: expect(locator).toBeChecked() failed
  19 | 
  20 |   await box.click();
  21 |   await expect(mortality).toHaveCount(0);
  22 |   await expect(box).not.toBeChecked();
  23 | 
  24 |   await box.click();
  25 |   await expect(mortality).toBeVisible();
  26 |   await expect(box).toBeChecked();
  27 | });
  28 | 
  29 | test("a nurse is offered only widgets her access allows", async ({ hospital }) => {
  30 |   const page = await hospital.as("nurse");
  31 |   await page.goto("/dashboard");
  32 |   await page.getByRole("button", { name: "Choose dashboard widgets" }).click();
  33 |   const menu = page.getByRole("dialog", { name: "Widgets" });
  34 |   await expect(menu.getByRole("checkbox").first()).toBeVisible();
  35 |   for (const area of ["Doctors' documentation", "Department efficiency"]) {
  36 |     await expect(menu.getByRole("group", { name: area })).toHaveCount(0);
  37 |   }
  38 |   await expect(menu.getByRole("checkbox", { name: "Mortality" })).toHaveCount(0);
  39 | });
  40 | 
```