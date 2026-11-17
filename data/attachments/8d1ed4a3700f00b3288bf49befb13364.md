# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: journeys/grn-receiving-store.spec.ts >> a store keeper receives a purchase order into a store
- Location: e2e/journeys/grn-receiving-store.spec.ts:16:1

# Error details

```
Error: the seed has a store to receive into
```

# Test source

```ts
  1  | /**
  2  |  * Goods received go into a store. A store keeper receives a purchase order
  3  |  * on screen and the stock lands in the store they chose; a receipt naming no
  4  |  * store is refused, because stock no store owns can be neither issued nor
  5  |  * moved.
  6  |  */
  7  | import { api, getAuthContextFromCookies, loginAsRoleApi } from "../helpers/api";
  8  | import {
  9  |   approvePurchaseOrder,
  10 |   createProcurementVendor,
  11 |   createPurchaseOrder,
  12 |   sendPurchaseOrderToVendor,
  13 | } from "../helpers/journey-steps";
  14 | import { expect, test } from "./support/world";
  15 | 
  16 | test("a store keeper receives a purchase order into a store", async ({ hospital, request }) => {
  17 |   test.setTimeout(120_000);
  18 |   const admin = await getAuthContextFromCookies(request);
  19 |   // Separation of duties: the officer raises the order, someone else approves.
  20 |   const officer = await loginAsRoleApi(request, "procurement_officer");
  21 |   const vendor = await createProcurementVendor(officer, {});
  22 |   const created = await createPurchaseOrder(officer, { vendorId: vendor.id, quantity: 4 });
  23 |   const po = { ...created.purchase_order, items: created.items };
  24 |   await approvePurchaseOrder(admin, po.id);
  25 |   await sendPurchaseOrderToVendor(officer, po.id);
  26 |   const stores = await api<{ id: string; name: string; is_active: boolean }[]>(
  27 |     admin,
  28 |     "GET",
  29 |     "/api/procurement/store-locations",
  30 |   );
  31 |   const store = stores.find((s) => s.is_active);
> 32 |   if (!store) throw new Error("the seed has a store to receive into");
     |                     ^ Error: the seed has a store to receive into
  33 | 
  34 |   // Refused without a store, whoever calls.
  35 |   await expect(
  36 |     api(admin, "POST", "/api/procurement/grns", {
  37 |       po_id: po.id,
  38 |       items: [
  39 |         {
  40 |           po_item_id: po.items[0]?.id,
  41 |           item_name: po.items[0]?.item_name,
  42 |           quantity_received: 1,
  43 |           quantity_accepted: 1,
  44 |           quantity_rejected: 0,
  45 |           unit_price: "1.00",
  46 |         },
  47 |       ],
  48 |     }),
  49 |   ).rejects.toThrow(/422/);
  50 | 
  51 |   const page = await hospital.as("store_keeper");
  52 |   await page.goto("/materials");
  53 |   await page.getByRole("tab", { name: "Procurement" }).click();
  54 |   await page.getByRole("tab", { name: "GRN" }).click();
  55 |   await page.getByRole("button", { name: "New GRN" }).click();
  56 |   const drawer = page.getByRole("dialog", { name: "Create GRN" });
  57 |   await drawer.getByRole("combobox", { name: "Purchase Order" }).click();
  58 |   await page.getByRole("option", { name: new RegExp(po.po_number) }).click();
  59 |   const storePicker = drawer.getByRole("combobox", { name: "Receive into store" });
  60 |   if (stores.filter((s) => s.is_active).length > 1) {
  61 |     await storePicker.click();
  62 |     await page.getByRole("option", { name: store.name, exact: true }).click();
  63 |   }
  64 |   await expect(storePicker).toHaveValue(store.name);
  65 |   await drawer.getByRole("button", { name: "Save draft GRN", exact: true }).click();
  66 |   await expect(drawer).toBeHidden();
  67 | 
  68 |   // A draft moves nothing; the store keeper posts it and only then is it stock.
  69 |   const detail = page.getByRole("dialog", { name: "GRN Details" });
  70 |   await expect(detail.getByText("No stock has moved")).toBeVisible();
  71 |   await detail.getByRole("button", { name: "Post to stock" }).click();
  72 |   await expect(detail.getByText("posted", { exact: true })).toBeVisible();
  73 |   await expect(detail.getByRole("button", { name: "Post to stock" })).toBeHidden();
  74 | 
  75 |   const grns = await api<{ grns: { po_id: string; store_location_id: string | null }[] }>(
  76 |     admin,
  77 |     "GET",
  78 |     "/api/procurement/grns?page=1&per_page=100",
  79 |   );
  80 |   const grn = grns.grns.find((g) => g.po_id === po.id);
  81 |   expect(grn?.store_location_id, "the receipt names its store").toBe(store.id);
  82 | });
  83 | 
```