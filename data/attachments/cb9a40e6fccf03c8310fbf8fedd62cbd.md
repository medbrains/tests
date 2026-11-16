# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: robustness/crawl.spec.ts >> doctor: every page in their sidebar opens and works
- Location: e2e/robustness/crawl.spec.ts:77:3

# Error details

```
Error: doctor: problems a user would meet

expect(received).toEqual(expected) // deep equality

- Expected  -   1
+ Received  + 106

- Array []
+ Array [
+   Object {
+     "page": "/front-office › Token Boards",
+     "what": "403 GET /api/tokens/board",
+   },
+   Object {
+     "page": "/front-office › Token Boards",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/front-office › Token Boards",
+     "what": "403 GET /api/tv/queue/pharmacy",
+   },
+   Object {
+     "page": "/front-office › Token Boards",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/front-office › Token Boards",
+     "what": "403 GET /api/tv/queue/lab",
+   },
+   Object {
+     "page": "/front-office › Token Boards",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/front-office › Token Boards",
+     "what": "403 GET /api/tv/queue/er",
+   },
+   Object {
+     "page": "/front-office › Token Boards",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/front-office › Token Boards",
+     "what": "403 GET /api/tv/queue/radiology/xray",
+   },
+   Object {
+     "page": "/front-office › Token Boards",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/mrd",
+     "what": "403 GET /api/mrd/storage-locations",
+   },
+   Object {
+     "page": "/mrd",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/mrd",
+     "what": "403 GET /api/mrd/storage-locations",
+   },
+   Object {
+     "page": "/mrd",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/regulatory › Checklists",
+     "what": "403 GET /api/regulatory/checklists",
+   },
+   Object {
+     "page": "/regulatory › Checklists",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/regulatory › ADR & Device Reports",
+     "what": "403 GET /api/regulatory/materiovigilance",
+   },
+   Object {
+     "page": "/regulatory › ADR & Device Reports",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/regulatory › Submissions",
+     "what": "403 GET /api/regulatory/submissions",
+   },
+   Object {
+     "page": "/regulatory › Submissions",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/reports",
+     "what": "403 GET /api/reports/occupancy-queue-pressure/data",
+   },
+   Object {
+     "page": "/reports",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/reports",
+     "what": "403 GET /api/reports/occupancy-queue-pressure/data",
+   },
+   Object {
+     "page": "/reports",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+   Object {
+     "page": "/admin/documents › Review Schedule",
+     "what": "403 GET /api/documents/review-schedule",
+   },
+   Object {
+     "page": "/admin/documents › Review Schedule",
+     "what": "console error: Failed to load resource: the server responded with a status of 403 (Forbidden)",
+   },
+ ]
```

# Page snapshot

```yaml
- generic [ref=f49e3]:
  - banner [ref=f49e4]:
    - generic [ref=f49e5]:
      - paragraph [ref=f49e9] [cursor=pointer]: MedBrains HMS
      - generic [ref=f49e10]:
        - separator [ref=f49e11]
        - button "Search... ⌘K" [ref=f49e12] [cursor=pointer]:
          - generic [ref=f49e13]:
            - paragraph [ref=f49e18]: Search...
            - generic [ref=f49e19]: ⌘K
        - button "Help" [ref=f49e20] [cursor=pointer]
        - button "Notes" [ref=f49e25] [cursor=pointer]
        - generic [ref=f49e30]:
          - generic [ref=f49e31]: "1"
          - button "Notifications" [ref=f49e32] [cursor=pointer]
        - generic [ref=f49e37] [cursor=pointer]:
          - checkbox "Switch to light mode" [checked]
        - button "Language" [ref=f49e48] [cursor=pointer]
        - separator [ref=f49e56]
        - generic [ref=f49e57] [cursor=pointer]:
          - generic [ref=f49e58]: E
          - generic [ref=f49e60]:
            - paragraph [ref=f49e61]: E2E Doctor mwj1yll3
            - paragraph [ref=f49e62]: doctor
  - navigation [ref=f49e63]:
    - generic [ref=f49e66]:
      - generic [ref=f49e67]:
        - paragraph [ref=f49e68]: Core
        - link [ref=f49e69] [cursor=pointer]:
          - /url: /dashboard
          - generic [aria-hidden] [ref=f49e72]: DB
          - generic [ref=f49e73]: Dashboard
          - button "Pin to favorites" [ref=f49e75]
        - link [ref=f49e79] [cursor=pointer]:
          - /url: /approvals
          - generic [ref=f49e85]: Approvals
          - button "Pin to favorites" [ref=f49e87]
        - link [ref=f49e91] [cursor=pointer]:
          - /url: /my-earnings
          - generic [aria-hidden] [ref=f49e94]: Ern
          - generic [ref=f49e95]: My Earnings
          - button "Pin to favorites" [ref=f49e97]
        - link [ref=f49e101] [cursor=pointer]:
          - /url: /health-pulse
          - generic [aria-hidden] [ref=f49e104]: HP
          - generic [ref=f49e105]: Health Pulse
          - button "Pin to favorites" [ref=f49e107]
        - link [ref=f49e111] [cursor=pointer]:
          - /url: /health-intel
          - generic [aria-hidden] [ref=f49e114]: HI
          - generic [ref=f49e115]: Health intelligence
          - button "Pin to favorites" [ref=f49e117]
      - generic [ref=f49e121]:
        - separator [ref=f49e122]
        - paragraph [ref=f49e123]: Clinical
        - link [ref=f49e124] [cursor=pointer]:
          - /url: /patients
          - generic [aria-hidden] [ref=f49e127]: Pt
          - generic [ref=f49e128]: Patients
          - button "Pin to favorites" [ref=f49e130]
        - link [ref=f49e134] [cursor=pointer]:
          - /url: /immunization-clinic
          - generic [aria-hidden] [ref=f49e137]: Imm
          - generic [ref=f49e138]: Immunisation clinic
          - button "Pin to favorites" [ref=f49e140]
        - link [ref=f49e144] [cursor=pointer]:
          - /url: /opd
          - generic [aria-hidden] [ref=f49e147]: OPD
          - generic [ref=f49e148]: OPD Queue
          - button "Pin to favorites" [ref=f49e150]
        - link [ref=f49e154] [cursor=pointer]:
          - /url: /telemedicine
          - generic [aria-hidden] [ref=f49e157]: Tel
          - generic [ref=f49e158]: Telemedicine
          - button "Pin to favorites" [ref=f49e160]
        - link [ref=f49e164] [cursor=pointer]:
          - /url: /doctor/signoffs
          - generic [aria-hidden] [ref=f49e167]: Sig
          - generic [ref=f49e168]: Doctor Sign-offs
          - button "Pin to favorites" [ref=f49e170]
        - link [ref=f49e174] [cursor=pointer]:
          - /url: /emergency
          - generic [aria-hidden] [ref=f49e177]: ER
          - generic [ref=f49e178]: Emergency
          - button "Pin to favorites" [ref=f49e180]
        - link [ref=f49e184] [cursor=pointer]:
          - /url: /order-sets
          - generic [aria-hidden] [ref=f49e187]: OS
          - generic [ref=f49e188]: Order Sets
          - button "Pin to favorites" [ref=f49e190]
        - link [ref=f49e194] [cursor=pointer]:
          - /url: /chronic-care
          - generic [aria-hidden] [ref=f49e197]: CC
          - generic [ref=f49e198]: Chronic Care
          - button "Pin to favorites" [ref=f49e200]
        - link [ref=f49e204] [cursor=pointer]:
          - /url: /home-healthcare
          - generic [ref=f49e212]: Home healthcare
          - button "Pin to favorites" [ref=f49e214]
        - link [ref=f49e218] [cursor=pointer]:
          - /url: /home-visits
          - generic [ref=f49e224]: Home visits
          - button "Pin to favorites" [ref=f49e226]
      - generic [ref=f49e230]:
        - separator [ref=f49e231]
        - paragraph [ref=f49e232]: Diagnostics
        - link [ref=f49e233] [cursor=pointer]:
          - /url: /lab
          - generic [aria-hidden] [ref=f49e236]: Lab
          - generic [ref=f49e237]: Lab
          - button "Pin to favorites" [ref=f49e239]
        - link [ref=f49e243] [cursor=pointer]:
          - /url: /pharmacy
          - generic [aria-hidden] [ref=f49e246]: Rx
          - generic [ref=f49e247]: Pharmacy
          - button "Pin to favorites" [ref=f49e249]
      - generic [ref=f49e253]:
        - separator [ref=f49e254]
        - paragraph [ref=f49e255]: Inpatient
        - link [ref=f49e256] [cursor=pointer]:
          - /url: /ipd
          - generic [aria-hidden] [ref=f49e259]: IPD
          - generic [ref=f49e260]: IPD
          - button "Pin to favorites" [ref=f49e262]
        - link [ref=f49e266] [cursor=pointer]:
          - /url: /care-view
          - generic [aria-hidden] [ref=f49e269]: CV
          - generic [ref=f49e270]: Care View
          - button "Pin to favorites" [ref=f49e272]
        - link [ref=f49e276] [cursor=pointer]:
          - /url: /case-sheet-review
          - generic [ref=f49e282]: Case sheet review
          - button "Pin to favorites" [ref=f49e284]
        - link [ref=f49e288] [cursor=pointer]:
          - /url: /icu
          - generic [aria-hidden] [ref=f49e291]: ICU
          - generic [ref=f49e292]: ICU
          - button "Pin to favorites" [ref=f49e294]
        - link [ref=f49e298] [cursor=pointer]:
          - /url: /nurse
          - generic [aria-hidden] [ref=f49e301]: Nur
          - generic [ref=f49e302]: Nurse Activities
          - button "Pin to favorites" [ref=f49e304]
        - link [ref=f49e308] [cursor=pointer]:
          - /url: /ot
          - generic [aria-hidden] [ref=f49e311]: OT
          - generic [ref=f49e312]: Operation Theatre
          - button "Pin to favorites" [ref=f49e314]
        - link [ref=f49e318] [cursor=pointer]:
          - /url: /bedside-portal
          - generic [aria-hidden] [ref=f49e321]: BP
          - generic [ref=f49e322]: Bedside Portal
          - button "Pin to favorites" [ref=f49e324]
      - generic [ref=f49e328]:
        - separator [ref=f49e329]
        - paragraph [ref=f49e330]: Finance
        - link [ref=f49e331] [cursor=pointer]:
          - /url: /insurance
          - generic [aria-hidden] [ref=f49e334]: Ins
          - generic [ref=f49e335]: Insurance & TPA
          - button "Pin to favorites" [ref=f49e337]
        - link [ref=f49e341] [cursor=pointer]:
          - /url: /indent
          - generic [aria-hidden] [ref=f49e344]: Ind
          - generic [ref=f49e345]: Indent & Store
          - button "Pin to favorites" [ref=f49e347]
        - link [ref=f49e351] [cursor=pointer]:
          - /url: /materials
          - generic [aria-hidden] [ref=f49e354]: Mat
          - generic [ref=f49e355]: Materials
          - button "Pin to favorites" [ref=f49e357]
      - generic [ref=f49e361]:
        - separator [ref=f49e362]
        - paragraph [ref=f49e363]: Operations
        - link [ref=f49e364] [cursor=pointer]:
          - /url: /front-office
          - generic [aria-hidden] [ref=f49e367]: FO
          - generic [ref=f49e368]: Front Office
          - button "Pin to favorites" [ref=f49e370]
        - link [ref=f49e374] [cursor=pointer]:
          - /url: /lms
          - generic [aria-hidden] [ref=f49e377]: LMS
          - generic [ref=f49e378]: Learning (LMS)
          - button "Pin to favorites" [ref=f49e380]
        - link [ref=f49e384] [cursor=pointer]:
          - /url: /mrd
          - generic [aria-hidden] [ref=f49e387]: MRD
          - generic [ref=f49e388]: Medical Records
          - button "Pin to favorites" [ref=f49e390]
      - generic [ref=f49e394]:
        - separator [ref=f49e395]
        - paragraph [ref=f49e396]: Network
        - link [ref=f49e397] [cursor=pointer]:
          - /url: /inter-hospital-transfers
          - generic [ref=f49e405]: Inter-hospital transfers
          - button "Pin to favorites" [ref=f49e407]
        - link [ref=f49e411] [cursor=pointer]:
          - /url: /inter-hospital-stock
          - generic [ref=f49e419]: Inter-hospital stock
          - button "Pin to favorites" [ref=f49e421]
      - generic [ref=f49e425]:
        - separator [ref=f49e426]
        - paragraph [ref=f49e427]: Compliance
        - link [ref=f49e428] [cursor=pointer]:
          - /url: /consent
          - generic [aria-hidden] [ref=f49e431]: Cns
          - generic [ref=f49e432]: Consent Management
          - button "Pin to favorites" [ref=f49e434]
        - link [ref=f49e438] [cursor=pointer]:
          - /url: /regulatory
          - generic [aria-hidden] [ref=f49e441]: Reg
          - generic [ref=f49e442]: Regulatory Compliance
          - button "Pin to favorites" [ref=f49e444]
        - link [ref=f49e448] [cursor=pointer]:
          - /url: /reports
          - generic [aria-hidden] [ref=f49e451]: Rep
          - generic [ref=f49e452]: Reports Center
          - button "Pin to favorites" [ref=f49e454]
      - generic [ref=f49e458]:
        - separator [ref=f49e459]
        - paragraph [ref=f49e460]: Specialty
        - link [ref=f49e461] [cursor=pointer]:
          - /url: /specialty/ophthalmology
          - generic [aria-hidden] [ref=f49e464]: Eye
          - generic [ref=f49e465]: Ophthalmology
          - button "Pin to favorites" [ref=f49e467]
        - link [ref=f49e471] [cursor=pointer]:
          - /url: /specialty/dental
          - generic [aria-hidden] [ref=f49e474]: Dnt
          - generic [ref=f49e475]: Dental
          - button "Pin to favorites" [ref=f49e477]
        - link [ref=f49e481] [cursor=pointer]:
          - /url: /specialty/cath-lab
          - generic [aria-hidden] [ref=f49e484]: CL
          - generic [ref=f49e485]: Cath Lab
          - button "Pin to favorites" [ref=f49e487]
        - link [ref=f49e491] [cursor=pointer]:
          - /url: /specialty/endoscopy
          - generic [aria-hidden] [ref=f49e494]: End
          - generic [ref=f49e495]: Endoscopy
          - button "Pin to favorites" [ref=f49e497]
        - link [ref=f49e501] [cursor=pointer]:
          - /url: /specialty/psychiatry
          - generic [aria-hidden] [ref=f49e504]: Psy
          - generic [ref=f49e505]: Psychiatry
          - button "Pin to favorites" [ref=f49e507]
        - link [ref=f49e511] [cursor=pointer]:
          - /url: /specialty/pmr
          - generic [aria-hidden] [ref=f49e514]: PMR
          - generic [ref=f49e515]: Physical Medicine
          - button "Pin to favorites" [ref=f49e517]
        - link [ref=f49e521] [cursor=pointer]:
          - /url: /specialty/palliative
          - generic [aria-hidden] [ref=f49e524]: Pal
          - generic [ref=f49e525]: Palliative Care
          - button "Pin to favorites" [ref=f49e527]
        - link [ref=f49e531] [cursor=pointer]:
          - /url: /specialty/maternity
          - generic [aria-hidden] [ref=f49e534]: Mat
          - generic [ref=f49e535]: Maternity
          - button "Pin to favorites" [ref=f49e537]
        - link [ref=f49e541] [cursor=pointer]:
          - /url: /specialty/other
          - generic [aria-hidden] [ref=f49e544]: Spc
          - generic [ref=f49e545]: Other Specialties
          - button "Pin to favorites" [ref=f49e547]
        - link [ref=f49e551] [cursor=pointer]:
          - /url: /specialty/cancer-registry
          - generic [aria-hidden] [ref=f49e554]: CR
          - generic [ref=f49e555]: Cancer registry
          - button "Pin to favorites" [ref=f49e557]
        - link [ref=f49e561] [cursor=pointer]:
          - /url: /clinical-trials
          - generic [ref=f49e566]: Clinical trials
          - button "Pin to favorites" [ref=f49e568]
      - generic [ref=f49e572]:
        - separator [ref=f49e573]
        - paragraph [ref=f49e574]: Administration
        - generic [ref=f49e575]:
          - button "Admin" [expanded] [ref=f49e576] [cursor=pointer]:
            - generic [aria-hidden] [ref=f49e579]: Usr
          - generic [ref=f49e585]:
            - link "Doctor Schedules" [ref=f49e586] [cursor=pointer]:
              - /url: /admin/doctor-schedules
              - generic [aria-hidden] [ref=f49e589]: DS
            - link "Documents & Printing" [ref=f49e591] [cursor=pointer]:
              - /url: /admin/documents
              - generic [aria-hidden] [ref=f49e594]: Dcs
    - generic [ref=f49e596]:
      - separator
      - button "Collapse" [ref=f49e598] [cursor=pointer]:
        - paragraph [ref=f49e603]: Collapse
      - paragraph [ref=f49e605]: v3.33.2 · b266fbb · Nov 16, 2026
  - main [ref=f49e606]:
    - alert "Verify your email" [ref=f49e607]:
      - generic [ref=f49e612]:
        - generic [ref=f49e613]: Verify your email
        - generic [ref=f49e616]:
          - paragraph [ref=f49e617]: Confirm e2e_doctor_mwj1yll3@e2e.medbrains.localhost to secure your account — check your inbox for the link.
          - button "Resend" [ref=f49e618] [cursor=pointer]
    - navigation "Breadcrumb" [ref=f49e622]:
      - list [ref=f49e623]:
        - listitem [ref=f49e624]:
          - link "Administration" [ref=f49e625] [cursor=pointer]:
            - /url: /admin
          - generic [aria-hidden] [ref=f49e626]: /
        - listitem [ref=f49e627]:
          - generic [ref=f49e628]: Documents & Printing
    - generic [ref=f49e630]:
      - generic [ref=f49e633]:
        - generic [aria-hidden] [ref=f49e634]: Dcs
        - generic [ref=f49e635]:
          - heading "Documents & Printing" [level=1] [ref=f49e636]
          - paragraph [ref=f49e637]: Manage templates, generated outputs, print queues, and copy/printer routing
      - generic [ref=f49e638]:
        - tablist [ref=f49e639]:
          - tab "Templates" [ref=f49e640] [cursor=pointer]
          - tab "Generated Documents" [ref=f49e646] [cursor=pointer]
          - tab "Review Schedule" [active] [selected] [ref=f49e652] [cursor=pointer]
        - tabpanel "Review Schedule" [ref=f49e658]:
          - generic [ref=f49e659]:
            - paragraph [ref=f49e661]: NABH-mandated annual form/document review tracking
            - table [ref=f49e663]:
              - rowgroup [ref=f49e664]:
                - row [ref=f49e665]:
                  - columnheader "Template" [ref=f49e666]
                  - columnheader "Cycle" [ref=f49e668]
                  - columnheader "Last Reviewed" [ref=f49e670]
                  - columnheader "Next Due" [ref=f49e672]
                  - columnheader "Status" [ref=f49e674]
                  - columnheader [ref=f49e676]
              - rowgroup [ref=f49e677]:
                - row [ref=f49e678]:
                  - cell [ref=f49e679]
                  - cell [ref=f49e681]
                  - cell [ref=f49e683]
                  - cell [ref=f49e685]
                  - cell [ref=f49e687]
                  - cell [ref=f49e689]
                - row [ref=f49e691]:
                  - cell [ref=f49e692]
                  - cell [ref=f49e694]
                  - cell [ref=f49e696]
                  - cell [ref=f49e698]
                  - cell [ref=f49e700]
                  - cell [ref=f49e702]
                - row [ref=f49e704]:
                  - cell [ref=f49e705]
                  - cell [ref=f49e707]
                  - cell [ref=f49e709]
                  - cell [ref=f49e711]
                  - cell [ref=f49e713]
                  - cell [ref=f49e715]
                - row [ref=f49e717]:
                  - cell [ref=f49e718]
                  - cell [ref=f49e720]
                  - cell [ref=f49e722]
                  - cell [ref=f49e724]
                  - cell [ref=f49e726]
                  - cell [ref=f49e728]
                - row [ref=f49e730]:
                  - cell [ref=f49e731]
                  - cell [ref=f49e733]
                  - cell [ref=f49e735]
                  - cell [ref=f49e737]
                  - cell [ref=f49e739]
                  - cell [ref=f49e741]
  - button "Open MedBrains assistant (drag to reposition)" [ref=f49e743]
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
      |                                                             ^ Error: doctor: problems a user would meet
  121 |   });
  122 | }
  123 | 
```