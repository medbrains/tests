# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: scenarios/ui-patient-registration.spec.ts >> Patient Registration — UI >> receptionist fills and submits registration form; UHID appears in patient list
- Location: e2e/scenarios/ui-patient-registration.spec.ts:32:3

# Error details

```
Error: Test timeout of 30000ms exceeded
```

# Page snapshot

```yaml
- generic [ref=f2e3]:
  - banner [ref=f2e4]:
    - generic [ref=f2e5]:
      - paragraph [ref=f2e9] [cursor=pointer]: MedBrains HMS
      - generic [ref=f2e10]:
        - separator [ref=f2e11]
        - button "Search... ⌘K" [ref=f2e12] [cursor=pointer]:
          - generic [ref=f2e13]:
            - paragraph [ref=f2e18]: Search...
            - generic [ref=f2e19]: ⌘K
        - button "Help" [ref=f2e20] [cursor=pointer]
        - button "Notes" [ref=f2e25] [cursor=pointer]
        - button "Notifications" [ref=f2e31] [cursor=pointer]
        - generic [ref=f2e36] [cursor=pointer]:
          - checkbox "Switch to light mode" [checked]
        - button "Language" [ref=f2e47] [cursor=pointer]
        - separator [ref=f2e55]
        - generic [ref=f2e56] [cursor=pointer]:
          - generic [ref=f2e57]: E
          - generic [ref=f2e59]:
            - paragraph [ref=f2e60]: E2E Receptionist mwkk2j4n
            - paragraph [ref=f2e61]: receptionist
  - navigation [ref=f2e62]:
    - generic [ref=f2e65]:
      - generic [ref=f2e66]:
        - paragraph [ref=f2e67]: Core
        - link [ref=f2e68] [cursor=pointer]:
          - /url: /dashboard
          - generic [aria-hidden] [ref=f2e71]: DB
          - generic [ref=f2e72]: Dashboard
          - button "Pin to favorites" [ref=f2e74]
        - link [ref=f2e78] [cursor=pointer]:
          - /url: /approvals
          - generic [ref=f2e84]: Approvals
          - button "Pin to favorites" [ref=f2e86]
        - link [ref=f2e90] [cursor=pointer]:
          - /url: /health-pulse
          - generic [aria-hidden] [ref=f2e93]: HP
          - generic [ref=f2e94]: Health Pulse
          - button "Pin to favorites" [ref=f2e96]
        - link [ref=f2e100] [cursor=pointer]:
          - /url: /token-board
          - generic [aria-hidden] [ref=f2e103]: TB
          - generic [ref=f2e104]: Token Board
          - button "Pin to favorites" [ref=f2e106]
        - link [ref=f2e110] [cursor=pointer]:
          - /url: /token-console
          - generic [aria-hidden] [ref=f2e113]: TC
          - generic [ref=f2e114]: Token Console
          - button "Pin to favorites" [ref=f2e116]
      - generic [ref=f2e120]:
        - separator [ref=f2e121]
        - paragraph [ref=f2e122]: Clinical
        - link [ref=f2e123] [cursor=pointer]:
          - /url: /patients
          - generic [aria-hidden] [ref=f2e126]: Pt
          - generic [ref=f2e127]: Patients
          - button "Pin to favorites" [ref=f2e129]
        - link [ref=f2e133] [cursor=pointer]:
          - /url: /opd
          - generic [aria-hidden] [ref=f2e136]: OPD
          - generic [ref=f2e137]: OPD Queue
          - button "Pin to favorites" [ref=f2e139]
        - link [ref=f2e143] [cursor=pointer]:
          - /url: /opd/appointments
          - generic [aria-hidden] [ref=f2e146]: Apt
          - generic [ref=f2e147]: Appointments
          - button "Pin to favorites" [ref=f2e149]
        - link [ref=f2e153] [cursor=pointer]:
          - /url: /telemedicine
          - generic [aria-hidden] [ref=f2e156]: Tel
          - generic [ref=f2e157]: Telemedicine
          - button "Pin to favorites" [ref=f2e159]
        - link [ref=f2e163] [cursor=pointer]:
          - /url: /emergency
          - generic [aria-hidden] [ref=f2e166]: ER
          - generic [ref=f2e167]: Emergency
          - button "Pin to favorites" [ref=f2e169]
      - generic [ref=f2e173]:
        - separator [ref=f2e174]
        - paragraph [ref=f2e175]: Finance
        - link [ref=f2e176] [cursor=pointer]:
          - /url: /billing
          - generic [aria-hidden] [ref=f2e179]: Bil
          - generic [ref=f2e180]: Billing
          - button "Pin to favorites" [ref=f2e182]
        - link [ref=f2e186] [cursor=pointer]:
          - /url: /insurance
          - generic [aria-hidden] [ref=f2e189]: Ins
          - generic [ref=f2e190]: Insurance & TPA
          - button "Pin to favorites" [ref=f2e192]
      - generic [ref=f2e196]:
        - separator [ref=f2e197]
        - paragraph [ref=f2e198]: Operations
        - link [ref=f2e199] [cursor=pointer]:
          - /url: /front-office
          - generic [aria-hidden] [ref=f2e202]: FO
          - generic [ref=f2e203]: Front Office
          - button "Pin to favorites" [ref=f2e205]
        - link [ref=f2e209] [cursor=pointer]:
          - /url: /camp
          - generic [aria-hidden] [ref=f2e212]: Cmp
          - generic [ref=f2e213]: Camp Management
          - button "Pin to favorites" [ref=f2e215]
        - link [ref=f2e219] [cursor=pointer]:
          - /url: /lms
          - generic [aria-hidden] [ref=f2e222]: LMS
          - generic [ref=f2e223]: Learning (LMS)
          - button "Pin to favorites" [ref=f2e225]
      - generic [ref=f2e229]:
        - separator [ref=f2e230]
        - paragraph [ref=f2e231]: Network
        - link [ref=f2e232] [cursor=pointer]:
          - /url: /uhi-requests
          - generic [ref=f2e238]: UHI requests
          - button "Pin to favorites" [ref=f2e240]
      - generic [ref=f2e244]:
        - separator [ref=f2e245]
        - paragraph [ref=f2e246]: Marketing & Web
        - link [ref=f2e247] [cursor=pointer]:
          - /url: /marketing
          - generic [ref=f2e254]: Marketing
          - button "Pin to favorites" [ref=f2e256]
        - link [ref=f2e260] [cursor=pointer]:
          - /url: /health-packages
          - generic [ref=f2e267]: Health packages
          - button "Pin to favorites" [ref=f2e269]
        - link [ref=f2e273] [cursor=pointer]:
          - /url: /testimonials
          - generic [ref=f2e278]: Testimonials
          - button "Pin to favorites" [ref=f2e280]
        - link [ref=f2e284] [cursor=pointer]:
          - /url: /microsite-settings
          - generic [ref=f2e290]: Micro-site settings
          - button "Pin to favorites" [ref=f2e292]
      - generic [ref=f2e296]:
        - separator [ref=f2e297]
        - paragraph [ref=f2e298]: Administration
        - button "Admin" [ref=f2e300] [cursor=pointer]:
          - generic [aria-hidden] [ref=f2e303]: Usr
    - generic [ref=f2e308]:
      - separator
      - button "Collapse" [ref=f2e310] [cursor=pointer]:
        - paragraph [ref=f2e315]: Collapse
      - paragraph [ref=f2e317]: v3.33.2 · b266fbb · Nov 17, 2026
  - main [ref=f2e318]:
    - alert "Verify your email" [ref=f2e319]:
      - generic [ref=f2e324]:
        - generic [ref=f2e325]: Verify your email
        - generic [ref=f2e328]:
          - paragraph [ref=f2e329]: Confirm e2e_receptionist_mwkk2j4n@e2e.medbrains.localhost to secure your account — check your inbox for the link.
          - button "Resend" [ref=f2e330] [cursor=pointer]
    - navigation "Breadcrumb" [ref=f2e334]:
      - list [ref=f2e335]:
        - listitem [ref=f2e336]:
          - link "Patients" [ref=f2e337] [cursor=pointer]:
            - /url: /patients
          - generic [aria-hidden] [ref=f2e338]: /
        - listitem [ref=f2e339]:
          - generic [ref=f2e340]: Register Patient
    - generic [ref=f2e342]:
      - generic [ref=f2e344]:
        - generic [ref=f2e345]:
          - generic [aria-hidden] [ref=f2e346]: Pt
          - generic [ref=f2e347]:
            - heading "Register Patient" [level=1] [ref=f2e348]
            - paragraph [ref=f2e349]: Create a patient record and link the first OPD workflow when required.
        - button "Back to Patients" [ref=f2e351] [cursor=pointer]
      - generic [ref=f2e358]:
        - button "Show checklist 3" [ref=f2e360] [cursor=pointer]:
          - generic [ref=f2e361]:
            - generic [ref=f2e367]: Show checklist
            - generic [ref=f2e368]: "3"
        - generic [ref=f2e375]:
          - generic [ref=f2e376]:
            - generic [ref=f2e377]:
              - heading [level=3] [ref=f2e378]:
                - text: Patient registration
                - emphasis [ref=f2e379]: — OPD
              - generic [ref=f2e380]: New patient intake
            - generic [ref=f2e381]:
              - generic [ref=f2e382]:
                - generic [ref=f2e383]: "07"
                - generic [ref=f2e384]: Safety flags
              - generic [ref=f2e385]:
                - generic [ref=f2e386]: Safety flags
                - generic [ref=f2e389]:
                  - generic [ref=f2e392]:
                    - checkbox "Medico-legal case" [ref=f2e394] [cursor=pointer]
                    - generic [ref=f2e395] [cursor=pointer]: Medico-legal case
                  - textbox "MLC number" [ref=f2e400]
                  - generic [ref=f2e403]:
                    - checkbox "VIP patient" [ref=f2e405] [cursor=pointer]
                    - generic [ref=f2e406] [cursor=pointer]: VIP patient
            - generic [ref=f2e408]:
              - generic [ref=f2e409]:
                - generic [ref=f2e410]: "09"
                - generic [ref=f2e411]: Family & background
              - generic [ref=f2e412]:
                - generic [ref=f2e413]: Father's name
                - textbox [ref=f2e417]
              - generic [ref=f2e418]:
                - generic [ref=f2e419]: Guardian
                - generic [ref=f2e422]:
                  - textbox "Name" [ref=f2e426]
                  - textbox "Relation" [ref=f2e430]
              - generic [ref=f2e431]:
                - generic [ref=f2e432]: Marital · religion · occupation
                - generic [ref=f2e435]:
                  - combobox "Marital" [ref=f2e439] [cursor=pointer]
                  - textbox "Religion" [ref=f2e443]
                  - textbox "Occupation" [ref=f2e447]
            - generic [ref=f2e448]:
              - generic [ref=f2e449]:
                - generic [ref=f2e450]: "10"
                - generic [ref=f2e451]: Address
              - generic [ref=f2e452]:
                - generic [ref=f2e453]: Address line 1
                - textbox "House / building / street" [ref=f2e457]
              - generic [ref=f2e458]:
                - generic [ref=f2e459]: Address line 2
                - textbox "Locality / area (optional)" [ref=f2e463]
              - generic [ref=f2e464]:
                - generic [ref=f2e465]: Landmark
                - textbox "Near temple / opposite school / etc." [ref=f2e469]
              - generic [ref=f2e470]:
                - generic [ref=f2e471]: City · district · state · pin
                - generic [ref=f2e474]:
                  - textbox "City / village" [ref=f2e478]
                  - textbox "District / Taluka" [ref=f2e482]
                  - textbox "State" [ref=f2e486]
                  - textbox "Pin" [ref=f2e490]
                  - textbox [ref=f2e494]: India
            - generic [ref=f2e495]:
              - generic [ref=f2e496]:
                - generic [ref=f2e497]: "11"
                - generic [ref=f2e498]: Next of kin & emergency contact
              - generic [ref=f2e499]:
                - generic [ref=f2e500]: Next of kin
                - generic [ref=f2e503]:
                  - textbox "Full name" [ref=f2e507]
                  - textbox "Relation" [ref=f2e511]
                  - textbox "Phone" [ref=f2e515]
              - generic [ref=f2e516]:
                - generic [ref=f2e517]: Emergency contact (different person if needed)
                - generic [ref=f2e520]:
                  - textbox "Full name" [ref=f2e524]
                  - textbox "Relation" [ref=f2e528]
                  - textbox "Phone" [ref=f2e532]
            - generic [ref=f2e533]:
              - generic [ref=f2e534]: Save now creates a minimum-fields patient; Register complete saves the full record.
              - generic [ref=f2e535]:
                - button "Back" [ref=f2e536] [cursor=pointer]
                - button "Save now" [ref=f2e539] [cursor=pointer]
                - button "Next" [active] [ref=f2e542] [cursor=pointer]
          - generic [ref=f2e547]:
            - button "Intake" [ref=f2e548] [cursor=pointer]
            - button "Contact & identity" [ref=f2e557] [cursor=pointer]
            - button "3 Family · address · safety" [ref=f2e566]:
              - generic [ref=f2e567]: "3"
              - generic [ref=f2e570]: Family · address · safety
            - button "4 Prefs & billing" [ref=f2e573]:
              - generic [ref=f2e574]: "4"
              - generic [ref=f2e577]: Prefs & billing
            - button "5 Review" [ref=f2e580]:
              - generic [ref=f2e581]: "5"
              - generic [ref=f2e584]: Review
  - button "Open MedBrains assistant (drag to reposition)" [ref=f2e586]
```

# Test source

```ts
  1  | /**
  2  |  * Accessibility and reachability checks every journey runs on the screens it
  3  |  * visits (WCAG 2.2 AA — medbrains/docs/WCAG-2.2-RULES.md).
  4  |  */
  5  | import { expect, type Locator, type Page } from "@playwright/test";
  6  | import axe from "axe-core";
  7  | 
  8  | const AA_TAGS = ["wcag2a", "wcag2aa", "wcag21a", "wcag21aa", "wcag22aa"];
  9  | 
  10 | /**
  11 |  * Violations already present on a screen before this work, by axe rule id.
  12 |  * A journey fails on anything new; an entry here is debt with a name, to be
  13 |  * removed when fixed — never a place to hide a new finding.
  14 |  */
  15 | const KNOWN: Record<string, readonly string[]> = {};
  16 | 
  17 | /** axe WCAG 2.2 AA on the page's main region; fails on any unrecorded violation. */
  18 | export async function expectScreenAccessible(page: Page, screen: string): Promise<void> {
  19 |   await waitForSettledScreen(page);
  20 |   await page.addScriptTag({ content: axe.source });
  21 |   const violations = await page.evaluate(async (tags) => {
  22 |     const root = document.querySelector("main") ?? document;
  23 |     const result = await (window as unknown as { axe: typeof axe }).axe.run(root, {
  24 |       runOnly: { type: "tag", values: tags },
  25 |       resultTypes: ["violations"],
  26 |     });
  27 |     return result.violations.map((v) => ({
  28 |       id: v.id,
  29 |       impact: v.impact,
  30 |       help: v.help,
  31 |       nodes: v.nodes.slice(0, 3).map((n) => ({
  32 |         target: n.target.join(" "),
  33 |         html: n.html.slice(0, 160),
  34 |         why: n.failureSummary?.split("\n").slice(1, 2).join(" ").trim(),
  35 |       })),
  36 |     }));
  37 |   }, AA_TAGS);
  38 |   const known = new Set(KNOWN[screen] ?? []);
  39 |   const fresh = violations.filter((v) => !known.has(v.id));
  40 |   expect(fresh, `${screen}: WCAG 2.2 AA violations\n${JSON.stringify(fresh, null, 2)}`).toEqual([]);
  41 | }
  42 | 
  43 | /**
  44 |  * The control is there, enabled, reachable by keyboard, and nothing covers it:
  45 |  * a trial click fails when another element (a floating launcher, an overlay)
  46 |  * would receive the click instead.
  47 |  */
  48 | export async function expectUsable(control: Locator, name: string): Promise<void> {
  49 |   await expect(control, `${name} is visible`).toBeVisible();
  50 |   await expect(control, `${name} is enabled`).toBeEnabled();
  51 |   // A live list re-renders its rows on every poll, which can steal focus
  52 |   // between focus() and the check; retry until focus holds.
  53 |   await expect(async () => {
  54 |     await control.focus();
  55 |     await expect(control, `${name} is keyboard focusable`).toBeFocused({ timeout: 1_000 });
> 56 |   }).toPass({ timeout: 10_000 });
     |      ^ Error: Test timeout of 30000ms exceeded
  57 |   await control.click({ trial: true, timeout: 5_000 });
  58 | }
  59 | 
  60 | /**
  61 |  * The screen has settled: the loading skeleton is gone and every finite
  62 |  * animation (page fade-in, drawer slide) has finished. Scanning earlier caught
  63 |  * text half-way through a fade and reported contrast the user never sees.
  64 |  * Infinite decorative loops are ignored. No fixed sleeps.
  65 |  */
  66 | export async function waitForSettledScreen(page: Page): Promise<void> {
  67 |   await expect(page.getByRole("status", { name: "Loading page" })).toHaveCount(0, {
  68 |     timeout: 20_000,
  69 |   });
  70 |   await page.waitForFunction(
  71 |     () =>
  72 |       document
  73 |         .getAnimations()
  74 |         .every(
  75 |           (a) =>
  76 |             a.playState !== "running" ||
  77 |             a.effect?.getComputedTiming().iterations === Number.POSITIVE_INFINITY,
  78 |         ),
  79 |     undefined,
  80 |     { timeout: 10_000 },
  81 |   );
  82 | }
  83 | 
```