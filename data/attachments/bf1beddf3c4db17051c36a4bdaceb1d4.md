# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: mock/module-smoke.spec.ts >> Module Screen Smoke (mock) >> telemedicine screen renders basic module surface
- Location: e2e/mock/module-smoke.spec.ts:45:5

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByRole('heading').first()
Expected: visible
Timeout: 15000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" getByRole('heading').first() with timeout 15000ms
  - waiting for getByRole('heading').first()

```

```yaml
- banner:
  - img
  - paragraph: MedBrains HMS
  - paragraph: powered by MedBrains
  - separator
  - button "Search... ⌘K":
    - paragraph: Search...
    - text: ⌘K
  - button "Help":
    - img
  - button "Notes":
    - img
  - button "Notifications":
    - img
  - checkbox "Switch to light mode" [checked]
  - button "Language"
  - separator
  - text: M
  - paragraph: Mock Super Admin
  - paragraph: super admin
- navigation:
  - paragraph: Core
  - link "Dashboard Pin to favorites":
    - /url: /dashboard
    - text: Dashboard
    - button "Pin to favorites":
      - img
  - link "Approvals Pin to favorites":
    - /url: /approvals
    - img
    - text: Approvals
    - button "Pin to favorites":
      - img
  - link "My Earnings Pin to favorites":
    - /url: /my-earnings
    - text: My Earnings
    - button "Pin to favorites":
      - img
  - link "Health Pulse Pin to favorites":
    - /url: /health-pulse
    - text: Health Pulse
    - button "Pin to favorites":
      - img
  - link "Health intelligence Pin to favorites":
    - /url: /health-intel
    - text: Health intelligence
    - button "Pin to favorites":
      - img
  - link "Token Board Pin to favorites":
    - /url: /token-board
    - text: Token Board
    - button "Pin to favorites":
      - img
  - link "Token Console Pin to favorites":
    - /url: /token-console
    - text: Token Console
    - button "Pin to favorites":
      - img
  - separator
  - paragraph: Clinical
  - link "Patients Pin to favorites":
    - /url: /patients
    - text: Patients
    - button "Pin to favorites":
      - img
  - link "Immunisation clinic Pin to favorites":
    - /url: /immunization-clinic
    - text: Immunisation clinic
    - button "Pin to favorites":
      - img
  - link "OPD Queue Pin to favorites":
    - /url: /opd
    - text: OPD Queue
    - button "Pin to favorites":
      - img
  - link "Appointments Pin to favorites":
    - /url: /opd/appointments
    - text: Appointments
    - button "Pin to favorites":
      - img
  - link "Telemedicine Pin to favorites":
    - /url: /telemedicine
    - text: Telemedicine
    - button "Pin to favorites":
      - img
  - link "Doctor Sign-offs Pin to favorites":
    - /url: /doctor/signoffs
    - text: Doctor Sign-offs
    - button "Pin to favorites":
      - img
  - link "Emergency Pin to favorites":
    - /url: /emergency
    - text: Emergency
    - button "Pin to favorites":
      - img
  - link "Order Sets Pin to favorites":
    - /url: /order-sets
    - text: Order Sets
    - button "Pin to favorites":
      - img
  - link "Chronic Care Pin to favorites":
    - /url: /chronic-care
    - text: Chronic Care
    - button "Pin to favorites":
      - img
  - link "Home healthcare Pin to favorites":
    - /url: /home-healthcare
    - img
    - text: Home healthcare
    - button "Pin to favorites":
      - img
  - link "Home visits Pin to favorites":
    - /url: /home-visits
    - img
    - text: Home visits
    - button "Pin to favorites":
      - img
  - separator
  - paragraph: Diagnostics
  - link "Lab Pin to favorites":
    - /url: /lab
    - text: Lab
    - button "Pin to favorites":
      - img
  - link "Radiology Pin to favorites":
    - /url: /radiology
    - text: Radiology
    - button "Pin to favorites":
      - img
  - link "Ward Stock Pin to favorites":
    - /url: /ward-stock
    - img
    - text: Ward Stock
    - button "Pin to favorites":
      - img
  - link "Pharmacy Pin to favorites":
    - /url: /pharmacy
    - text: Pharmacy
    - button "Pin to favorites":
      - img
  - link "Pharmacy Finance Pin to favorites":
    - /url: /pharmacy/finance
    - text: Pharmacy Finance
    - button "Pin to favorites":
      - img
  - link "Fulfilment Queue Pin to favorites":
    - /url: /pharmacy/fulfilment
    - text: Fulfilment Queue
    - button "Pin to favorites":
      - img
  - link "Home Deliveries Pin to favorites":
    - /url: /pharmacy/deliveries
    - text: Home Deliveries
    - button "Pin to favorites":
      - img
  - link "Online orders Pin to favorites":
    - /url: /pharmacy/online-orders
    - text: Online orders
    - button "Pin to favorites":
      - img
  - link "H1 register Pin to favorites":
    - /url: /pharmacy/h1-register
    - text: H1 register
    - button "Pin to favorites":
      - img
  - link "Returns quarantine Pin to favorites":
    - /url: /pharmacy/quarantine
    - text: Returns quarantine
    - button "Pin to favorites":
      - img
  - link "NPPA ceilings Pin to favorites":
    - /url: /pharmacy/nppa-ceilings
    - text: NPPA ceilings
    - button "Pin to favorites":
      - img
  - link "Collection Counter Pin to favorites":
    - /url: /pharmacy/dispatch
    - text: Collection Counter
    - button "Pin to favorites":
      - img
  - link "Blood Bank Pin to favorites":
    - /url: /blood-bank
    - text: Blood Bank
    - button "Pin to favorites":
      - img
  - separator
  - paragraph: Inpatient
  - link "IPD Pin to favorites":
    - /url: /ipd
    - text: IPD
    - button "Pin to favorites":
      - img
  - link "Care View Pin to favorites":
    - /url: /care-view
    - text: Care View
    - button "Pin to favorites":
      - img
  - link "Case sheet review Pin to favorites":
    - /url: /case-sheet-review
    - img
    - text: Case sheet review
    - button "Pin to favorites":
      - img
  - link "ICU Pin to favorites":
    - /url: /icu
    - text: ICU
    - button "Pin to favorites":
      - img
  - link "Nurse Activities Pin to favorites":
    - /url: /nurse
    - text: Nurse Activities
    - button "Pin to favorites":
      - img
  - link "Operation Theatre Pin to favorites":
    - /url: /ot
    - text: Operation Theatre
    - button "Pin to favorites":
      - img
  - link "Diet & Kitchen Pin to favorites":
    - /url: /diet-kitchen
    - text: Diet & Kitchen
    - button "Pin to favorites":
      - img
  - link "Bedside Portal Pin to favorites":
    - /url: /bedside-portal
    - text: Bedside Portal
    - button "Pin to favorites":
      - img
  - separator
  - paragraph: Finance
  - link "Billing Pin to favorites":
    - /url: /billing
    - text: Billing
    - button "Pin to favorites":
      - img
  - link "Doctor Payouts Pin to favorites":
    - /url: /billing/doctor-payouts
    - text: Doctor Payouts
    - button "Pin to favorites":
      - img
  - link "Insurance & TPA Pin to favorites":
    - /url: /insurance
    - text: Insurance & TPA
    - button "Pin to favorites":
      - img
  - link "Procurement Pin to favorites":
    - /url: /procurement
    - text: Procurement
    - button "Pin to favorites":
      - img
  - link "Indent & Store Pin to favorites":
    - /url: /indent
    - text: Indent & Store
    - button "Pin to favorites":
      - img
  - link "Materials Pin to favorites":
    - /url: /materials
    - text: Materials
    - button "Pin to favorites":
      - img
  - link "Payroll Pin to favorites":
    - /url: /hr/payroll
    - img
    - text: Payroll
    - button "Pin to favorites":
      - img
  - separator
  - paragraph: Operations
  - link "Front Office Pin to favorites":
    - /url: /front-office
    - text: Front Office
    - button "Pin to favorites":
      - img
  - link "Smart Scheduling Pin to favorites":
    - /url: /scheduling
    - text: Smart Scheduling
    - button "Pin to favorites":
      - img
  - link "Command Center Pin to favorites":
    - /url: /command-center
    - text: Command Center
    - button "Pin to favorites":
      - img
  - link "MedBrains Flow Pin to favorites":
    - /url: /flow
    - text: MedBrains Flow
    - button "Pin to favorites":
      - img
  - link "Communications Pin to favorites":
    - /url: /communications
    - text: Communications
    - button "Pin to favorites":
      - img
  - link "Camp Management Pin to favorites":
    - /url: /camp
    - text: Camp Management
    - button "Pin to favorites":
      - img
  - link "Ambulance Pin to favorites":
    - /url: /ambulance
    - text: Ambulance
    - button "Pin to favorites":
      - img
  - link "Housekeeping Pin to favorites":
    - /url: /housekeeping
    - text: Housekeeping
    - button "Pin to favorites":
      - img
  - link "CSSD Pin to favorites":
    - /url: /cssd
    - text: CSSD
    - button "Pin to favorites":
      - img
  - link "Facilities Management Pin to favorites":
    - /url: /facilities
    - text: Facilities Management
    - button "Pin to favorites":
      - img
  - link "Biomedical Engineering Pin to favorites":
    - /url: /bme
    - text: Biomedical Engineering
    - button "Pin to favorites":
      - img
  - link "Security Pin to favorites":
    - /url: /security
    - text: Security
    - button "Pin to favorites":
      - img
  - link "Security intelligence Pin to favorites":
    - /url: /security/intelligence
    - img
    - text: Security intelligence
    - button "Pin to favorites":
      - img
  - link "MedBrains access Pin to favorites":
    - /url: /security/medbrains-access
    - img
    - text: MedBrains access
    - button "Pin to favorites":
      - img
  - link "HR & Staffing Pin to favorites":
    - /url: /hr
    - text: HR & Staffing
    - button "Pin to favorites":
      - img
  - link "Learning (LMS) Pin to favorites":
    - /url: /lms
    - text: Learning (LMS)
    - button "Pin to favorites":
      - img
  - link "Medical Records Pin to favorites":
    - /url: /mrd
    - text: Medical Records
    - button "Pin to favorites":
      - img
  - link "Clinical Knowledge Pin to favorites":
    - /url: /clinical-kb
    - text: Clinical Knowledge
    - button "Pin to favorites":
      - img
  - separator
  - paragraph: Network
  - link "Directory Pin to favorites":
    - /url: /directory
    - img
    - text: Directory
    - button "Pin to favorites":
      - img
  - link "Hospital groups Pin to favorites":
    - /url: /hospital-groups
    - img
    - text: Hospital groups
    - button "Pin to favorites":
      - img
  - link "Inter-hospital transfers Pin to favorites":
    - /url: /inter-hospital-transfers
    - img
    - text: Inter-hospital transfers
    - button "Pin to favorites":
      - img
  - link "Inter-hospital stock Pin to favorites":
    - /url: /inter-hospital-stock
    - img
    - text: Inter-hospital stock
    - button "Pin to favorites":
      - img
  - link "UHI requests Pin to favorites":
    - /url: /uhi-requests
    - img
    - text: UHI requests
    - button "Pin to favorites":
      - img
  - separator
  - paragraph: Marketing & Web
  - link "Marketing Pin to favorites":
    - /url: /marketing
    - img
    - text: Marketing
    - button "Pin to favorites":
      - img
  - link "Health packages Pin to favorites":
    - /url: /health-packages
    - img
    - text: Health packages
    - button "Pin to favorites":
      - img
  - link "Testimonials Pin to favorites":
    - /url: /testimonials
    - img
    - text: Testimonials
    - button "Pin to favorites":
      - img
  - link "Micro-site settings Pin to favorites":
    - /url: /microsite-settings
    - img
    - text: Micro-site settings
    - button "Pin to favorites":
      - img
  - separator
  - paragraph: Compliance
  - link "Quality Pin to favorites":
    - /url: /quality
    - text: Quality
    - button "Pin to favorites":
      - img
  - link "Infection Control Pin to favorites":
    - /url: /infection-control
    - text: Infection Control
    - button "Pin to favorites":
      - img
  - link "Consent Management Pin to favorites":
    - /url: /consent
    - text: Consent Management
    - button "Pin to favorites":
      - img
  - link "Regulatory Compliance Pin to favorites":
    - /url: /regulatory
    - text: Regulatory Compliance
    - button "Pin to favorites":
      - img
  - link "Privacy & CERT-In Pin to favorites":
    - /url: /privacy-compliance
    - text: Privacy & CERT-In
    - button "Pin to favorites":
      - img
  - link "ABDM dashboard Pin to favorites":
    - /url: /abdm/dashboard
    - img
    - text: ABDM dashboard
    - button "Pin to favorites":
      - img
  - link "Analytics & Dashboards Pin to favorites":
    - /url: /analytics
    - text: Analytics & Dashboards
    - button "Pin to favorites":
      - img
  - link "Paperless meter Pin to favorites":
    - /url: /analytics/paperless
    - text: Paperless meter
    - button "Pin to favorites":
      - img
  - link "Reports Center Pin to favorites":
    - /url: /reports
    - text: Reports Center
    - button "Pin to favorites":
      - img
  - link "Audit Trail Pin to favorites":
    - /url: /audit
    - text: Audit Trail
    - button "Pin to favorites":
      - img
  - link "SNOMED CT Pin to favorites":
    - /url: /terminology/snomed
    - img
    - text: SNOMED CT
    - button "Pin to favorites":
      - img
  - link "Utilization Review Pin to favorites":
    - /url: /utilization-review
    - text: Utilization Review
    - button "Pin to favorites":
      - img
  - link "Case Management Pin to favorites":
    - /url: /case-management
    - text: Case Management
    - button "Pin to favorites":
      - img
  - separator
  - paragraph: Specialty
  - link "Ophthalmology Pin to favorites":
    - /url: /specialty/ophthalmology
    - text: Ophthalmology
    - button "Pin to favorites":
      - img
  - link "Dental Pin to favorites":
    - /url: /specialty/dental
    - text: Dental
    - button "Pin to favorites":
      - img
  - link "Cath Lab Pin to favorites":
    - /url: /specialty/cath-lab
    - text: Cath Lab
    - button "Pin to favorites":
      - img
  - link "Endoscopy Pin to favorites":
    - /url: /specialty/endoscopy
    - text: Endoscopy
    - button "Pin to favorites":
      - img
  - link "Psychiatry Pin to favorites":
    - /url: /specialty/psychiatry
    - text: Psychiatry
    - button "Pin to favorites":
      - img
  - link "Physical Medicine Pin to favorites":
    - /url: /specialty/pmr
    - text: Physical Medicine
    - button "Pin to favorites":
      - img
  - link "Palliative Care Pin to favorites":
    - /url: /specialty/palliative
    - text: Palliative Care
    - button "Pin to favorites":
      - img
  - link "Maternity Pin to favorites":
    - /url: /specialty/maternity
    - text: Maternity
    - button "Pin to favorites":
      - img
  - link "Other Specialties Pin to favorites":
    - /url: /specialty/other
    - text: Other Specialties
    - button "Pin to favorites":
      - img
  - link "Cancer registry Pin to favorites":
    - /url: /specialty/cancer-registry
    - text: Cancer registry
    - button "Pin to favorites":
      - img
  - link "Clinical trials Pin to favorites":
    - /url: /clinical-trials
    - img
    - text: Clinical trials
    - button "Pin to favorites":
      - img
  - link "Long-term care Pin to favorites":
    - /url: /long-term-care
    - img
    - text: Long-term care
    - button "Pin to favorites":
      - img
  - link "Occupational Health Pin to favorites":
    - /url: /occupational-health
    - text: Occupational Health
    - button "Pin to favorites":
      - img
  - separator
  - paragraph: Administration
  - button "Admin":
    - text: Admin
    - img
  - separator
  - button "Collapse":
    - paragraph: Collapse
  - paragraph: v3.33.2 · bd8151a · Nov 27, 2026
- main:
  - alert "Verify your email":
    - img
    - text: Verify your email
    - paragraph: Confirm mock.admin@medbrains.local to secure your account — check your inbox for the link.
    - button "Resend"
  - navigation "Breadcrumb":
    - list:
      - listitem: Telemedicine
  - img
  - paragraph: Telemedicine
  - paragraph: Video consultations — Jitsi, an external link, or a connected provider (Zoom).
  - button "Research"
  - button "Video provider settings":
    - img
  - button "New consultation":
    - img
    - text: New consultation
  - img
  - paragraph: No tele-consultations yet.
- button "Open MedBrains assistant (drag to reposition)"
- alert: Couldn't check for critical alerts Live alerts are not reaching this screen. Check the lab worklist directly until this clears.
```

# Test source

```ts
  1  | import { expect, test } from "@playwright/test";
  2  | import { NAV_GROUPS } from "@/config/navigation";
  3  | import { installMockApi, seedMockSession } from "./mockApi";
  4  | 
  5  | interface ModuleTarget {
  6  |   label: string;
  7  |   path: string;
  8  | }
  9  | 
  10 | function flattenModuleTargets(): ModuleTarget[] {
  11 |   const targets: ModuleTarget[] = [];
  12 | 
  13 |   for (const group of NAV_GROUPS) {
  14 |     for (const item of group.items) {
  15 |       if (item.children?.length) {
  16 |         for (const child of item.children) {
  17 |           targets.push({ label: child.i18nKey, path: child.path });
  18 |         }
  19 |         continue;
  20 |       }
  21 | 
  22 |       targets.push({ label: item.i18nKey, path: item.path });
  23 |     }
  24 |   }
  25 | 
  26 |   const seen = new Set<string>();
  27 |   return targets.filter((target) => {
  28 |     if (seen.has(target.path)) {
  29 |       return false;
  30 |     }
  31 |     seen.add(target.path);
  32 |     return true;
  33 |   });
  34 | }
  35 | 
  36 | const moduleTargets = flattenModuleTargets();
  37 | 
  38 | test.describe("Module Screen Smoke (mock)", () => {
  39 |   test.beforeEach(async ({ page }) => {
  40 |     await installMockApi(page);
  41 |     await seedMockSession(page);
  42 |   });
  43 | 
  44 |   for (const moduleTarget of moduleTargets) {
  45 |     test(`${moduleTarget.label} screen renders basic module surface`, async ({ page }) => {
  46 |       const pageErrors: string[] = [];
  47 |       page.on("pageerror", (error) => pageErrors.push(error.message));
  48 | 
  49 |       await page.goto(moduleTarget.path);
  50 |       await expect(page).not.toHaveURL(/\/login$/);
  51 | 
  52 |       const heading = page.getByRole("heading").first();
> 53 |       await expect(heading).toBeVisible({ timeout: 15_000 });
     |                             ^ Error: expect(locator).toBeVisible() failed
  54 | 
  55 |       const moduleSurface = page.locator(
  56 |         [
  57 |           "button:visible",
  58 |           "[role='button']:visible",
  59 |           "table:visible",
  60 |           "[role='table']:visible",
  61 |           "input:visible",
  62 |           "[role='textbox']:visible",
  63 |           "[role='combobox']:visible",
  64 |           "[role='tab']:visible",
  65 |           "[role='grid']:visible",
  66 |           "[role='searchbox']:visible",
  67 |         ].join(", "),
  68 |       ).first();
  69 | 
  70 |       await expect(moduleSurface).toBeVisible({ timeout: 15_000 });
  71 |       expect(pageErrors, `page errors for ${moduleTarget.path}`).toEqual([]);
  72 |     });
  73 |   }
  74 | });
  75 | 
```