# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: robustness/crawl.spec.ts >> front_office_staff: every page in their sidebar opens and works
- Location: e2e/robustness/crawl.spec.ts:77:3

# Error details

```
Error: front_office_staff: problems a user would meet

expect(received).toEqual(expected) // deep equality

- Expected  -  1
+ Received  + 16

- Array []
+ Array [
+   Object {
+     "page": "/front-office › Queue Metrics",
+     "what": "console error: %o
+
+ %s
+
+ %s
+  TypeError: Cannot read properties of undefined (reading 'toFixed')
+     at Object.render (http://localhost:5173/src/pages/front-office/queue-metrics-",
+   },
+   Object {
+     "page": "/front-office › Queue Metrics",
+     "what": "error screen (Screen unavailable)",
+   },
+ ]
```

# Page snapshot

```yaml
- generic [ref=f11e3]:
  - banner [ref=f11e4]:
    - generic [ref=f11e5]:
      - paragraph [ref=f11e9] [cursor=pointer]: MedBrains HMS
      - generic [ref=f11e10]:
        - separator [ref=f11e11]
        - button "Search... ⌘K" [ref=f11e12] [cursor=pointer]:
          - generic [ref=f11e13]:
            - paragraph [ref=f11e18]: Search...
            - generic [ref=f11e19]: ⌘K
        - button "Help" [ref=f11e20] [cursor=pointer]
        - button "Notes" [ref=f11e25] [cursor=pointer]
        - button "Notifications" [ref=f11e31] [cursor=pointer]
        - generic [ref=f11e36] [cursor=pointer]:
          - checkbox "Switch to light mode" [checked]
        - button "Language" [ref=f11e47] [cursor=pointer]
        - separator [ref=f11e55]
        - generic [ref=f11e56] [cursor=pointer]:
          - generic [ref=f11e57]: E
          - generic [ref=f11e59]:
            - paragraph [ref=f11e60]: E2E Front Office Staff mx0c6a29
            - paragraph [ref=f11e61]: front office staff
  - navigation [ref=f11e62]:
    - generic [ref=f11e65]:
      - generic [ref=f11e66]:
        - paragraph [ref=f11e67]: Core
        - link [ref=f11e68] [cursor=pointer]:
          - /url: /dashboard
          - generic [aria-hidden] [ref=f11e71]: DB
          - generic [ref=f11e72]: Dashboard
          - button "Pin to favorites" [ref=f11e74]
        - link [ref=f11e78] [cursor=pointer]:
          - /url: /approvals
          - generic [ref=f11e84]: Approvals
          - button "Pin to favorites" [ref=f11e86]
        - link [ref=f11e90] [cursor=pointer]:
          - /url: /health-pulse
          - generic [aria-hidden] [ref=f11e93]: HP
          - generic [ref=f11e94]: Health Pulse
          - button "Pin to favorites" [ref=f11e96]
        - link [ref=f11e100] [cursor=pointer]:
          - /url: /token-board
          - generic [aria-hidden] [ref=f11e103]: TB
          - generic [ref=f11e104]: Token Board
          - button "Pin to favorites" [ref=f11e106]
        - link [ref=f11e110] [cursor=pointer]:
          - /url: /token-console
          - generic [aria-hidden] [ref=f11e113]: TC
          - generic [ref=f11e114]: Token Console
          - button "Pin to favorites" [ref=f11e116]
      - generic [ref=f11e120]:
        - separator [ref=f11e121]
        - paragraph [ref=f11e122]: Operations
        - link [ref=f11e123] [cursor=pointer]:
          - /url: /front-office
          - generic [aria-hidden] [ref=f11e126]: FO
          - generic [ref=f11e127]: Front Office
          - button "Pin to favorites" [ref=f11e129]
        - link [ref=f11e133] [cursor=pointer]:
          - /url: /communications
          - generic [aria-hidden] [ref=f11e136]: Com
          - generic [ref=f11e137]: Communications
          - button "Pin to favorites" [ref=f11e139]
      - generic [ref=f11e143]:
        - separator [ref=f11e144]
        - paragraph [ref=f11e145]: Network
        - link [ref=f11e146] [cursor=pointer]:
          - /url: /uhi-requests
          - generic [ref=f11e152]: UHI requests
          - button "Pin to favorites" [ref=f11e154]
      - generic [ref=f11e158]:
        - separator [ref=f11e159]
        - paragraph [ref=f11e160]: Marketing & Web
        - link [ref=f11e161] [cursor=pointer]:
          - /url: /marketing
          - generic [ref=f11e168]: Marketing
          - button "Pin to favorites" [ref=f11e170]
      - generic [ref=f11e174]:
        - separator [ref=f11e175]
        - paragraph [ref=f11e176]: Administration
        - generic [ref=f11e177]:
          - button "Admin" [expanded] [ref=f11e178] [cursor=pointer]:
            - generic [aria-hidden] [ref=f11e181]: Usr
          - link "Queues" [ref=f11e188] [cursor=pointer]:
            - /url: /admin/queues
    - generic [ref=f11e199]:
      - separator
      - button "Collapse" [ref=f11e201] [cursor=pointer]:
        - paragraph [ref=f11e206]: Collapse
      - paragraph [ref=f11e208]: v3.33.2 · bd8151a · Nov 28, 2026
  - main [ref=f11e209]:
    - alert "Verify your email" [ref=f11e210]:
      - generic [ref=f11e215]:
        - generic [ref=f11e216]: Verify your email
        - generic [ref=f11e219]:
          - paragraph [ref=f11e220]: Confirm e2e_frontofficesta_mx0c6a29@e2e.medbrains.localhost to secure your account — check your inbox for the link.
          - button "Resend" [ref=f11e221] [cursor=pointer]
    - navigation "Breadcrumb" [ref=f11e225]:
      - list [ref=f11e226]:
        - listitem [ref=f11e227]:
          - link "Administration" [ref=f11e228] [cursor=pointer]:
            - /url: /admin
          - generic [aria-hidden] [ref=f11e229]: /
        - listitem [ref=f11e230]:
          - generic [ref=f11e231]: Queues
    - generic [ref=f11e233]:
      - generic [ref=f11e237]:
        - heading "Queues" [level=1] [ref=f11e238]
        - paragraph [ref=f11e239]: How each desk, room and camp numbers and admits tokens.
      - generic [ref=f11e240]:
        - textbox "Search table" [ref=f11e250]:
          - /placeholder: Find a queue or place
        - separator [ref=f11e251]
        - generic [ref=f11e254]:
          - heading "No queues set up yet" [level=4] [ref=f11e255]
          - paragraph [ref=f11e256]: Every place uses the standard numbering (T-001, P-001…) until you set up a queue for it.
      - paragraph [ref=f11e257]: Only a hospital administrator can change queues.
  - button "Open MedBrains assistant (drag to reposition)" [ref=f11e258]
```

# Test source

```ts
  20  |   "nurse",
  21  |   "pharmacist",
  22  |   "lab_technician",
  23  |   "billing_clerk",
  24  |   "camp_coordinator",
  25  |   "super_admin",
  26  | ];
  27  | 
  28  | /** Development noise, not something a user of the product would meet. */
  29  | const NOISE = [/\[vite\]/i, /WebSocket closed without opened/i, /Download the React DevTools/i];
  30  | 
  31  | interface Problem {
  32  |   page: string;
  33  |   what: string;
  34  | }
  35  | 
  36  | function watch(page: Page, problems: Problem[], current: () => string) {
  37  |   page.on("pageerror", (error) =>
  38  |     problems.push({ page: current(), what: `JS error: ${error.message.slice(0, 160)}` }),
  39  |   );
  40  |   page.on("console", (message) => {
  41  |     if (message.type() !== "error") return;
  42  |     const text = message.text();
  43  |     if (NOISE.some((pattern) => pattern.test(text))) return;
  44  |     problems.push({ page: current(), what: `console error: ${text.slice(0, 160)}` });
  45  |   });
  46  |   page.on("response", (response) => {
  47  |     const url = new URL(response.url());
  48  |     if (!url.pathname.startsWith("/api/")) return;
  49  |     const status = response.status();
  50  |     if (status >= 500 || status === 403) {
  51  |       problems.push({
  52  |         page: current(),
  53  |         what: `${status} ${response.request().method()} ${url.pathname}`,
  54  |       });
  55  |     }
  56  |   });
  57  | }
  58  | 
  59  | async function checkScreen(page: Page, problems: Problem[], where: string): Promise<void> {
  60  |   await waitForSettledScreen(page);
  61  |   if (await page.getByRole("heading", { name: "Screen unavailable" }).count()) {
  62  |     problems.push({ page: where, what: "error screen (Screen unavailable)" });
  63  |   }
  64  |   // Full-screen pages (the waiting-room display, kiosk) have no <main>.
  65  |   const region = (await page.locator("main").count()) > 0 ? page.locator("main") : page.locator("body");
  66  |   const text = ((await region.first().textContent({ timeout: 5_000 })) ?? "").trim();
  67  |   if (text.length < 20) problems.push({ page: where, what: "blank page" });
  68  |   const toasts = page.locator(
  69  |     '.mantine-Notification-root[style*="danger"], .mantine-Notification-root[style*="-red-"]',
  70  |   );
  71  |   for (const toast of await toasts.all()) {
  72  |     problems.push({ page: where, what: `error toast: ${(await toast.innerText()).slice(0, 120)}` });
  73  |   }
  74  | }
  75  | 
  76  | for (const role of ROLES) {
  77  |   test(`${role}: every page in their sidebar opens and works`, async ({ page }) => {
  78  |     test.setTimeout(600_000);
  79  |     const problems: Problem[] = [];
  80  |     let current = "(login)";
  81  |     watch(page, problems, () => current);
  82  |     await routeApiDirect(page);
  83  |     const identity = getE2EIdentity(role);
  84  |     await loginAsRole(page, identity.username, identity.password);
  85  |     await page.goto("/dashboard");
  86  |     await waitForSettledScreen(page);
  87  | 
  88  |     // Their sidebar is the list — collapsed groups included.
  89  |     const paths = await page.evaluate(() => [
  90  |       ...new Set(
  91  |         [...document.querySelectorAll("nav a[href]")]
  92  |           .map((a) => a.getAttribute("href") ?? "")
  93  |           .filter((href) => href.startsWith("/")),
  94  |       ),
  95  |     ]);
  96  |     expect(paths.length, `${role} sees a sidebar`).toBeGreaterThan(0);
  97  | 
  98  |     for (const path of paths) {
  99  |       current = path;
  100 |       const before = problems.length;
  101 |       await page.goto(path);
  102 |       await checkScreen(page, problems, path);
  103 |       const tabs = page.locator("main").getByRole("tab");
  104 |       const count = await tabs.count();
  105 |       for (let i = 0; i < count; i += 1) {
  106 |         const tab = tabs.nth(i);
  107 |         if (!(await tab.isVisible()) || (await tab.isDisabled())) continue;
  108 |         const name = ((await tab.innerText()) || `tab ${i + 1}`).trim().slice(0, 40);
  109 |         current = `${path} › ${name}`;
  110 |         await tab.click();
  111 |         await checkScreen(page, problems, current);
  112 |       }
  113 |       // One line per page as it goes, so a hang later loses nothing.
  114 |       // biome-ignore lint/suspicious/noConsole: report output
  115 |       console.log(`CRAWLED ${role} ${path} ${JSON.stringify(problems.slice(before))}`);
  116 |     }
  117 | 
  118 |     // biome-ignore lint/suspicious/noConsole: report output
  119 |     console.log(`ROBUSTNESS ${role} ${JSON.stringify({ pages: paths.length, problems })}`);
> 120 |     expect(problems, `${role}: problems a user would meet`).toEqual([]);
      |                                                             ^ Error: front_office_staff: problems a user would meet
  121 |   });
  122 | }
  123 | 
```