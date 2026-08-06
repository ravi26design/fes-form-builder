![FES — Foundation for Ecological Security](fes_logo.png)

# Development Proposal
## FES "Form Builder" — Field Data Collection System

*Prepared by:*

![Pseudocode](pseudocode_logo.png)

---

## 1. Executive Summary

FES requires a production-grade, multi-tenant **form-builder and field data-collection platform** that lets organizations design custom data-collection forms (with rich conditional logic), assign them to programs and field teams, collect data **offline in the field**, and monitor results through role-based dashboards and analytics.

The provided Figma prototype defines a complete **Phase 1 product**: **4 user roles, 8 functional modules, and 44+ screens**, including a drag-and-drop **Form Builder with unlimited-depth conditional follow-up questions** and a **mobile app (React Native / Angular)** for offline field data collection with sync.

This proposal covers the **web platform build plus a native mobile app (UI/UX design + development)**. It is scoped as an **accelerated 12-week delivery** by a lean team at **India small-company rates**.

| Item | Detail |
|---|---|
| Timeline | **~12 weeks (≈3 months)** |
| Core team | ~6–7 people (lean, blended) |
| Effort | ~302 person-days |
| Professional fees (ex-GST) | **₹15,29,000** |
| GST @ 18% | ₹2,75,220 |
| **Total payable (incl. GST)** | **₹18,04,220** |

> The 12-week plan is an accelerated, lean-team delivery. It assumes tight scope prioritization, prompt FES sign-offs, and web design (Figma) delivered per module at sprint start. Detailed cost breakdown in Section 8.

---

## 2. Understanding of Requirements

The prototype is a **mid-fidelity wireframe system** (no backend, mocked auth, non-persisted data). It clearly specifies *what* to build. Our job is to build the real, secure product behind it — the web platform (implemented from FES's Figma design) and a native mobile app for field users.

### 2.1 User Roles (4)
1. **FES Super Admin** – full platform control: organization CRUD, org approvals, platform-wide user administration, monitoring.
2. **Organization Admin** – programs, form builder, indicators, org hierarchy, org users, onboarding wizard.
3. **Program Manager** – program oversight, form requests, submission review.
4. **Field User** – mobile app, offline data collection and sync.

### 2.2 Functional Modules (8)
1. **Authentication & Access** – email/mobile login, OTP verification, session handling, permission control, first-time onboarding.
2. **Organization Management** – list, approve/reject, add/edit, detail, **hierarchy tree** (Org → Division → Department → Team).
3. **Program Management** – programs CRUD, indicator mapping, assign forms to programs.
4. **Form Management (Form Builder)** – *the core*: drag-and-drop editor, 11+ field types, field property panel, **unlimited-depth conditional follow-up questions**, preview, draft/publish.
5. **User & Role Management** – invite flow, user lists, role assignment, RBAC.
6. **Indicator Management** – indicator library, CRUD, categorization, mapping to programs.
7. **Help, Onboarding & Support** – setup wizard, contextual help, help center/FAQs.
8. **Mobile App (React Native / Angular)** – mobile form filling for field users, **offline capture** (photo/GPS), drafts, submission, **sync + conflict resolution**.

Plus supporting areas: **dashboards & analytics**, **submissions review**, **template gallery**, **settings**, and **error/empty states**.

### 2.3 The Two Hardest Pieces (drive most of the estimate)
- **Form Builder with unlimited nesting** — a recursive, path-based schema where any answer can trigger follow-up questions to any depth, each with its own field types and validation. Requires a robust schema model, versioning, and a performant recursive editor UI.
- **Offline-first mobile app + sync** — local storage of form definitions and responses, photo/GPS capture, background sync, and conflict resolution when connectivity returns.

---

## 3. Proposed Technical Solution

The prototype is already React + TypeScript. We carry that forward, build a matching backend, and deliver a native mobile app.

- **Frontend (Web admin):** React 18 + TypeScript, Vite, Tailwind, Radix/shadcn UI, React Router, Recharts (reuses the prototype's stack), implemented from FES-provided Figma design.
- **Mobile App:** **React Native (or Angular / Ionic)** with offline storage (SQLite/IndexedDB) and background sync — for field data collection on Android/iOS.
- **Backend / API:** Node.js (NestJS) **or** Python (Django REST) — REST/JSON, JWT auth, role-based authorization, multi-tenant data isolation, plus **dedicated mobile APIs** (auth, offline sync, submissions).
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

Delivered in 6 two-week sprints. Web, backend and mobile tracks run in parallel; QA is continuous.

| Sprint / Track | Weeks | Focus / Deliverables |
|---|---|---|
| **Sprint 1 – Foundation** | Weeks 1–2 | Discovery & data model, project/CI-CD setup, environments, **Auth + OTP + RBAC**, app shell & navigation, mobile app scaffold |
| **Sprint 2 – Admin & Programs** | Weeks 3–4 | FES Admin (orgs CRUD, approvals, hierarchy tree), Org Admin dashboards, programs, indicators, user management |
| **Sprint 3 – Form Builder** | Weeks 5–7* | Drag-and-drop editor, all field types, **unlimited nested conditional logic**, field properties, preview, draft/publish |
| **Sprint 4 – Mobile Integration & Sync** | Weeks 8–9 | Integrate the mobile app end-to-end, finalize **sync + conflict resolution**, field-user testing |
| **Sprint 5 – Analytics & Rest** | Weeks 10–11 | Dashboards/charts, submissions review, onboarding wizard, settings, help center, notifications |
| **Sprint 6 – QA & Launch** | Week 12 | End-to-end testing, security & performance checks, UAT support, bug-fixing, deployment, handover/training |
| **Mobile App UI/UX Design** *(parallel track)* | Weeks 3–5 (~3 weeks) | Mobile screens, flows, states & assets; runs parallel to web sprints and hands off before development |
| **Mobile App Development (React Native / Angular)** *(parallel track)* | Weeks 7–9 (~3 weeks) | Build the mobile app: form rendering with conditional logic, offline capture (photo/GPS), drafts, sync |

*\*Sprint 3 spans ~3 weeks as the Form Builder is the largest component; other sprints are 2 weeks. The mobile app runs as a parallel track — ~3 weeks of UI/UX design (Weeks 3–5) followed by ~3 weeks of development (Weeks 7–9) — converging into Sprint 4 for integration and sync.*

---

## 6. Resources Required (Team)

Lean small-company team for a 12-week delivery. Some roles are part-time.

| Role | Count | Allocation | Responsibility |
|---|---|---|---|
| Frontend Developer (React) | 1 | Full 12 weeks | Web admin + form builder UI |
| Backend Developer (Node/Django + PG) | 1 | Full 12 weeks | APIs, schema engine, sync, auth, multi-tenancy |
| Mobile App Developer (React Native / Angular) | 1–2 | Full 4 weeks | Mobile app build, offline + sync |
| Mobile UI/UX Designer | 1 | ~4 weeks (part-time) | Mobile app design |
| QA Engineer | 1 | ~6 weeks (part-time) | Test plans, manual + automated testing, UAT |
| PM/BA · Tech Lead · DevOps | shared | Part-time | Delivery, architecture, CI/CD, infra |
| **Total** | **~6–7 people** | | (several shared/part-time) |

**Client-side (FES) involvement needed:** a product owner for fast sign-offs, **the web UI design (Figma) and assets**, subject-matter input on forms/indicators, UAT testers, and access to third-party services (SMS/email/OTP provider, domains, cloud account, app-store accounts).

---

## 7. Effort Estimate (indicative, person-days)

| Work area | Frontend | Backend | QA | Total |
|---|---:|---:|---:|---:|
| Setup, infra, CI/CD, Auth + OTP + RBAC | 8 | 8 | 3 | 19 |
| Org, program, indicator & user management (admin) | 16 | 8 | 5 | 29 |
| **Form Builder (drag-drop + unlimited nesting)** | 32 | 10 | 8 | 50 |
| Dashboards, analytics & submissions | 12 | 4 | 5 | 21 |
| Onboarding, settings, help, notifications, templates | 6 | 2 | 3 | 11 |
| Error states, polish, integration, hardening, UAT | 2 | 2 | 2 | 6 |
| **Web subtotal (person-days)** | **76** | **34** | **26** | **136** |
| **Mobile App — UI/UX Design** | | | | **30** |
| **Mobile App — Development (React Native / Angular)** | 52 | 10 | 8 | **70** |
| **Mobile App — API Development (auth, sync, submissions)** | | 20 | | **20** |
| PM / Tech Lead / DevOps (20 + 12 + 14) | | | | 46 |
| **Grand total** | | | | **~302 person-days** |

*Mobile App Development columns denote mobile client development (Frontend), client-side integration (Backend), and testing (QA); Mobile App API Development is server-side backend work (auth, offline sync, submissions). UI/UX Design is a design-only effort (shown in Total).*

**Fit within 12 weeks:** Over ~12 weeks (≈60 working days per person), the required ~302 person-days are covered by the team below and delivered across the 6 sprints in Section 5.

| Discipline | Required (PD) | Available over 12 wks (PD) | Team |
|---|---:|---:|---|
| Web Frontend | 76 | ~90 | 1–2 devs |
| Backend | 54 | ~60 | 1 dev × 12 wks |
| Mobile App (design + dev) | 100 | ~110 | 1 designer (part) + 1–2 mobile devs |
| QA | 26 | ~40 | 1 × part-time |
| PM / Tech Lead / DevOps | 46 | ~50 | shared, part-time |

---

## 8. Budget

All amounts in INR at **India small-company day-rates**. Costs are built up from effort (person-days) × discipline day-rate. **GST @ 18%** is applied on professional fees.

| # | Cost Component | Effort (person-days) | Rate (₹/day) | Amount (₹) |
|---|---|---:|---:|---:|
| 1 | Frontend Development (web admin + form builder UI) | 76 | 5,000 | 3,80,000 |
| 2 | Backend Development — web platform (schema engine, auth, multi-tenancy) | 34 | 5,500 | 1,87,000 |
| 3 | QA & Testing (test plans, manual + automated, UAT) | 26 | 3,500 | 91,000 |
| 4 | Project Management / Business Analysis | 20 | 5,000 | 1,00,000 |
| 5 | Solution Architecture / Tech Lead | 12 | 7,000 | 84,000 |
| 6 | DevOps & Infrastructure (CI/CD, environments, deployment) | 14 | 5,500 | 77,000 |
| 7 | **Mobile App UI/UX Design** | 30 | 5,000 | **1,50,000** |
| 8 | **Mobile App Development (React Native / Angular)** | 70 | 5,000 | **3,50,000** |
| 9 | **Mobile App API Development (auth, offline sync, submissions)** | 20 | 5,500 | **1,10,000** |
| | **Subtotal — Professional Fees** | **302** | | **15,29,000** |
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
| Mobile App (offline + sync) | 20% | Sprint 4 accepted (end Week 9) |
| Analytics & remaining modules | 10% | Sprint 5 accepted (end Week 11) |
| Go-live & handover | 5% | UAT sign-off & production launch (Week 12) |

*Each milestone percentage is applied to the total contract value; GST @ 18% is added to every invoice.*

---

## 9. Assumptions

- The **12-week timeline is aggressive** and assumes tight scope prioritization, prompt FES sign-offs (within 1–2 business days), and no major mid-sprint scope changes; lower-priority items may be phased if needed to protect the launch date.
- **Web UI design is provided by FES** (Figma); **mobile app UI/UX design is included** in this proposal.
- The Figma prototype is the agreed functional scope; material additions are handled via change requests.
- Mobile app is built with **React Native (or Angular / Ionic)** for Android/iOS; app-store publishing/accounts are handled by FES (support included).
- One environment set (dev/staging/prod) on a cloud account provided/approved by FES.
- English-language UI initially; multi-language/localization can be added (estimate on request).

## 10. Key Risks & Mitigation
| Risk | Mitigation |
|---|---|
| Aggressive 12-week timeline | Strict sprint scope, parallel web/backend/mobile tracks, lower-priority items phased; weekly burn-down tracking |
| Web design delivered late/incomplete by FES | Back-end/API work proceeds in parallel; design needed per module at sprint start |
| Form-builder nesting complexity | Prototyped in Sprint 3 first; schema model validated in Sprint 1 |
| Offline sync edge cases / conflicts | Clear conflict-resolution strategy defined up front; dedicated test pass |
| Scope creep | Change-request process; backlog locked per sprint |

## 11. Deliverables
- Production web application (all admin roles), implemented from FES design.
- **Mobile app (React Native / Angular)** for field users — including its UI/UX design.
- Backend APIs (web + mobile: auth, offline sync, submissions), database, and infrastructure (CI/CD).
- Source code, technical documentation, and API docs.
- Test artifacts and UAT support.
- Deployment to production + admin/user handover training.

## 12. Next Steps
1. Confirm scope and approve this proposal.
2. Short kickoff to lock data model, sprint plan, and design-handoff schedule.
3. Sign engagement and mobilize the team.

---

*This is an indicative proposal (web build + mobile app design & development) based on the Phase 1 prototype, scoped for an accelerated 12-week delivery at India small-company rates. Final scope and pricing are confirmed at kickoff.*
