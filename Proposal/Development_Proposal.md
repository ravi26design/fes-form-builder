![FES — Foundation for Ecological Security](fes_logo.png)

# Development Proposal
## FES "Form Builder" — Field Data Collection System

*Prepared by:*

![Pseudocode](pseudocode_logo.png)

---

## 1. Executive Summary

FES requires a production-grade, multi-tenant **form-builder and field data-collection platform** that lets organizations design custom data-collection forms (with rich conditional logic), assign them to programs and field teams, collect data **offline in the field**, and monitor results through role-based dashboards and analytics.

The provided Figma prototype defines a complete **Phase 1 product**: **4 user roles, 8 functional modules, and 44+ screens**, including a drag-and-drop **Form Builder with unlimited-depth conditional follow-up questions** and an **offline-first mobile field app with sync**.

This proposal covers **engineering (development) only** — UI/UX design is excluded (FES provides the Figma design; we implement to it). It is scoped as an **accelerated 12-week delivery** by a lean team at **India small-company rates**.

| Item | Detail |
|---|---|
| Timeline | **~12 weeks (≈3 months)** |
| Core team | ~6 people (lean, blended) |
| Effort | ~301 person-days |
| Professional fees (ex-GST) | **₹15,29,000** |
| GST @ 18% | ₹2,75,220 |
| **Total payable (incl. GST)** | **₹18,04,220** |

> The 12-week plan is an accelerated, lean-team delivery. It assumes tight scope prioritization, prompt FES sign-offs, and design delivered per module at sprint start. Detailed cost breakdown in Section 8.

---

## 2. Understanding of Requirements

The prototype is a **mid-fidelity wireframe system** (no backend, mocked auth, non-persisted data). It clearly specifies *what* to build. Our job is to build the real, secure product behind it — implementing the front-end from the design FES provides.

### 2.1 User Roles (4)
1. **FES Super Admin** – full platform control: organization CRUD, org approvals, platform-wide user administration, monitoring.
2. **Organization Admin** – programs, form builder, indicators, org hierarchy, org users, onboarding wizard.
3. **Program Manager** – program oversight, form requests, submission review.
4. **Field User** – mobile-first, offline data collection and sync.

### 2.2 Functional Modules (7)
1. **Authentication & Access** – email/mobile login, OTP verification, session handling, permission control, first-time onboarding.
2. **Organization Management** – list, approve/reject, add/edit, detail, **hierarchy tree** (Org → Division → Department → Team).
3. **Program Management** – programs CRUD, indicator mapping, assign forms to programs.
4. **Form Management (Form Builder)** – *the core*: drag-and-drop editor, 11+ field types, field property panel, **unlimited-depth conditional follow-up questions**, preview, draft/publish.
5. **User & Role Management** – invite flow, user lists, role assignment, RBAC.
6. **Indicator Management** – indicator library, CRUD, categorization, mapping to programs.
7. **Help, Onboarding & Support** – setup wizard, contextual help, help center/FAQs.

Plus supporting areas: **dashboards & analytics**, **submissions review**, **template gallery**, **settings**, and **error/empty states**.

### 2.3 The Two Hardest Pieces (drive most of the estimate)
- **Form Builder with unlimited nesting** — a recursive, path-based schema where any answer can trigger follow-up questions to any depth, each with its own field types and validation. Requires a robust schema model, versioning, and a performant recursive editor UI.
- **Offline-first field app + sync** — local storage of form definitions and responses, photo/GPS capture, background sync, and conflict resolution when connectivity returns.

---

## 3. Proposed Technical Solution

The prototype is already React + TypeScript. We carry that forward and build a matching backend.

- **Frontend (Web admin):** React 18 + TypeScript, Vite, Tailwind, Radix/shadcn UI, React Router, Recharts (reuses the prototype's stack), implemented from FES-provided Figma design.
- **Backend / API:** Node.js (NestJS) **or** Python (Django REST) — REST/JSON, JWT auth, role-based authorization, multi-tenant data isolation.
- **Database:** PostgreSQL (relational core + JSONB for flexible form schemas & responses).
- **File/Media storage:** S3-compatible object storage (photos, uploads, signatures).
- **Infra/DevOps:** Dockerized services, CI/CD pipeline, staging + production environments, monitoring & backups.

**Key engineering components:** multi-tenant data model with RBAC; **form-schema engine** (nested/recursive definitions with versioning & publish); **submission engine** (validation, media, audit); **sync engine** (change-log, reconciliation, conflict resolution); OTP/notification services.

---

## 4. Delivery Approach

- **Methodology:** Agile / Scrum, **2-week sprints** (6 sprints over 12 weeks), sprint demos to FES.
- **Environments:** Dev → Staging (for FES review/UAT) → Production.
- **Quality:** automated tests on critical logic (form schema, sync), continuous manual QA, and a final hardening/UAT week before launch.
- **Communication:** weekly status, sprint demo every 2 weeks, single point of contact.

---

## 5. Timeline & Phase Plan (12 Weeks)

Delivered in 6 two-week sprints. Backend and frontend run in parallel; QA is continuous.

| Sprint | Weeks | Focus / Deliverables |
|---|---|---|
| **Sprint 1 – Foundation** | Weeks 1–2 | Discovery & data model, project/CI-CD setup, environments, **Auth + OTP + RBAC**, app shell & navigation |
| **Sprint 2 – Admin & Programs** | Weeks 3–4 | FES Admin (orgs CRUD, approvals, hierarchy tree), Org Admin dashboards, programs, indicators, user management |
| **Sprint 3 – Form Builder** | Weeks 5–7* | Drag-and-drop editor, all field types, **unlimited nested conditional logic**, field properties, preview, draft/publish |
| **Sprint 4 – Field App** | Weeks 8–9 | Mobile-first PWA, form renderer with conditional logic, offline capture (photo/GPS), drafts, **sync + conflict resolution** |
| **Sprint 5 – Analytics & Rest** | Weeks 10–11 | Dashboards/charts, submissions review, onboarding wizard, settings, help center, notifications |
| **Sprint 6 – QA & Launch** | Week 12 | End-to-end testing, security & performance checks, UAT support, bug-fixing, deployment, handover/training |

*\*Sprint 3 spans ~3 weeks as the Form Builder is the largest component; other sprints are 2 weeks.*

---

## 6. Resources Required (Team)

Lean small-company team for a 12-week delivery. Some roles are part-time.

| Role | Count | Allocation | Responsibility |
|---|---|---|---|
| Frontend Developers (React/PWA) | 2 | Full 12 weeks | Web admin + field PWA + form builder UI |
| Backend Developers (Node/Django + PG) | 2 | Full 12 weeks | APIs, schema engine, sync, auth, multi-tenancy |
| QA Engineer | 1 | ~8 weeks (part-time) | Test plans, manual + automated testing, UAT |
| Project Manager / Business Analyst | 1 | Part-time | Delivery, backlog, FES liaison, requirements |
| Tech Lead / Architect | 1 | Part-time (oversight) | Architecture, code review, technical governance |
| DevOps | 0.5 | Part-time | CI/CD, environments, deployment, monitoring |
| **Total** | **~6 people** | | (several shared/part-time) |

**Client-side (FES) involvement needed:** a product owner for fast sign-offs, **the final UI design (Figma) and assets**, subject-matter input on forms/indicators, UAT testers, and access to third-party services (SMS/email/OTP provider, domains, cloud account).

---

## 7. Effort Estimate (indicative, person-days — development only)

| Work area | Frontend | Backend | QA | Total |
|---|---:|---:|---:|---:|
| Setup, infra, CI/CD, Auth + OTP + RBAC | 12 | 18 | 4 | 34 |
| Org, program, indicator & user management (admin) | 22 | 20 | 6 | 48 |
| **Form Builder (drag-drop + unlimited nesting)** | 34 | 16 | 8 | 58 |
| **Field app: renderer + offline + sync** | 24 | 22 | 8 | 54 |
| Dashboards, analytics & submissions | 12 | 10 | 5 | 27 |
| Onboarding, settings, help, notifications, templates | 8 | 7 | 3 | 18 |
| Error states, polish, integration, hardening, UAT | 3 | 2 | 4 | 9 |
| **Subtotal (person-days)** | **115** | **95** | **38** | **248** |
| PM / Tech Lead / DevOps (28 + 14 + 11) | | | | **53** |
| **Grand total** | | | | **~301 person-days** |

**Fit within 12 weeks:** Over ~12 weeks (≈60 working days per person), the team provides roughly 2 × 60 = 120 frontend and 120 backend person-days, plus part-time QA (~40 PD), PM, Tech Lead and DevOps capacity. The ~301 person-days above fit within this capacity and are delivered across the 6 sprints in Section 5.

| Discipline | Required (PD) | Available over 12 wks (PD) | Team |
|---|---:|---:|---|
| Frontend | 115 | ~120 | 2 devs × 12 wks |
| Backend | 95 | ~120 | 2 devs × 12 wks |
| QA | 38 | ~40 | 1 × ~8 wks (part-time) |
| PM / Tech Lead / DevOps | 53 | ~55 | shared, part-time |

---

## 8. Budget

Development only (UI/UX design excluded). All amounts in INR at **India small-company day-rates**. Costs are built up from effort (person-days) × discipline day-rate. **GST @ 18%** is applied on professional fees.

| # | Cost Component | Effort (person-days) | Rate (₹/day) | Amount (₹) |
|---|---|---:|---:|---:|
| 1 | Frontend Development (web admin + field PWA + form builder UI) | 115 | 5,000 | 5,75,000 |
| 2 | Backend Development (APIs, schema engine, sync, auth, multi-tenancy) | 95 | 5,500 | 5,22,500 |
| 3 | QA & Testing (test plans, manual + automated, UAT) | 38 | 3,500 | 1,33,000 |
| 4 | Project Management / Business Analysis | 28 | 5,000 | 1,40,000 |
| 5 | Solution Architecture / Tech Lead | 14 | 7,000 | 98,000 |
| 6 | DevOps & Infrastructure (CI/CD, environments, deployment) | 11 | 5,500 | 60,500 |
| | **Subtotal — Professional Fees** | **301** | | **15,29,000** |
| | **GST @ 18%** | | | **2,75,220** |
| | **Total Payable (incl. GST)** | | | **18,04,220** |

*Rates are indicative India small-company day-rates and may be adjusted based on the final team seniority mix and engagement model.*

### Recurring / operational costs (not included above)
| Item | Indicative |
|---|---|
| Cloud infrastructure (staging + prod, storage, DB, backups) | ₹20,000–45,000 / month (scales with usage) |
| SMS/OTP + email provider | Usage-based (₹0.15–0.25 per SMS typical) |
| Post-launch support & maintenance (bug fixes, minor changes, updates) | AMC at ~15–18% of build cost / year |

*Third-party costs (cloud, SMS, email, domains, app-store fees) are billed at actuals or paid directly by FES. Recurring costs are exclusive of GST.*

### Suggested payment milestones
| Milestone | % | Trigger |
|---|---:|---|
| Mobilization | 20% | Contract signing / kickoff |
| Auth + Admin modules | 20% | Sprints 1–2 accepted (end Week 4) |
| Form Builder | 25% | Sprint 3 accepted (end Week 7) |
| Field App (offline + sync) | 20% | Sprint 4 accepted (end Week 9) |
| Analytics & remaining modules | 10% | Sprint 5 accepted (end Week 11) |
| Go-live & handover | 5% | UAT sign-off & production launch (Week 12) |

*Each milestone percentage is applied to the total contract value; GST @ 18% is added to every invoice.*

---

## 9. Assumptions

- The **12-week timeline is aggressive** and assumes tight scope prioritization, prompt FES sign-offs (within 1–2 business days), and no major mid-sprint scope changes; lower-priority items may be phased if needed to protect the launch date.
- The Figma prototype is the agreed functional scope; material additions are handled via change requests.
- Field app is delivered as an **installable PWA**; native iOS/Android apps are an optional add-on.
- One environment set (dev/staging/prod) on a cloud account provided/approved by FES.
- English-language UI initially; multi-language/localization can be added (estimate on request).

## 10. Key Risks & Mitigation
| Risk | Mitigation |
|---|---|
| Aggressive 12-week timeline | Strict sprint scope, parallel FE/BE tracks, lower-priority items phased; weekly burn-down tracking |
| Design delivered late/incomplete by FES | Back-end/API work proceeds in parallel; design needed per module at sprint start |
| Form-builder nesting complexity | Prototyped in Sprint 3 first; schema model validated in Sprint 1 |
| Offline sync edge cases / conflicts | Clear conflict-resolution strategy defined up front; dedicated test pass |
| Scope creep | Change-request process; backlog locked per sprint |

## 11. Deliverables
- Production web application (all admin roles) + field PWA, implemented from FES design.
- Backend APIs, database, and infrastructure (CI/CD).
- Source code, technical documentation, and API docs.
- Test artifacts and UAT support.
- Deployment to production + admin/user handover training.

## 12. Next Steps
1. Confirm scope and approve this proposal.
2. Short kickoff to lock data model, sprint plan, and design-handoff schedule.
3. Sign engagement and mobilize the team.

---

*This is an indicative, development-only proposal (UI/UX design excluded) based on the Phase 1 prototype, scoped for an accelerated 12-week delivery at India small-company rates. Final scope and pricing are confirmed at kickoff.*
