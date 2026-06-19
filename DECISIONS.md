# Architectural & Business Decisions — Atlantic Renewables / Jarvis

> Every significant decision affecting the system or the business, when it was made, and why. Decisions are never deleted — if a decision is revisited, a new entry is added below the old one.

This log excludes internal AI development-tooling configuration (agent model selection, prompt architecture) — those are implementation details of how the system is built, not decisions about what the system does or why.

---

### Payment Stages Modelled as Events, Not a Status Field
**Date:** 16 June 2026
**Decision:** Payment milestones (first payment, interim payment, install-ready payment, final invoice paid) are recorded as timestamped event records, not as a single "current stage" field on a project.
**Why:** The business need is to trigger different actions (tasks, emails) at the moment each payment milestone is reached, and to retain a timestamp history of when each was reached — not just the current state. A single status field would lose this history and couldn't represent revisiting a stage.

---

### Google Ecosystem — Jarvis Retrieves Data, Gemini Writes Content
**Date:** 1 June 2026
**Decision:** Jarvis is the data layer — it retrieves accurate, verified information from Google services (Drive, Calendar, Gmail, and in future YouTube, Search Console, Analytics) using a service account. Gemini is the language layer — it receives that verified data and produces copy and drafts from it. Neither layer does the other's job.
**Why:** An AI writing content without accurate data inputs produces plausible-looking but incorrect output (invented IDs, fabricated figures). Supplying verified facts first means the language layer only has to get the wording right, not the facts.

---

### Template Content Lives in Google Drive, Not a Custom Editor
**Date:** 28 April 2026
**Decision:** Email template content (body text, images, video links, PDF attachments) is stored and edited in Google Drive/Docs — tools staff already use — rather than a bespoke editor inside Jarvis. Jarvis holds a reference to the file and merges customer data at send time.
**Why:** Building a custom rich content editor (handling images, video, attachments, version history) would be significant extra scope for no benefit over what Drive already does natively.

---

### Template Admin Screen — Required Before Go-Live
**Date:** 28 April 2026
**Decision:** Dean and Jack must be able to add and amend email/SMS/WhatsApp templates and automation rules themselves, without developer involvement, before FreshSales is switched off.
**Why:** Without this, every template change requires a developer — unacceptable for day-to-day operations.

---

### All Correspondence Written for Dean, Not Patrick
**Date:** 28 April 2026
**Decision:** All written communication — including messages addressed to Patrick — is written as if Dean is the primary reader. Dean is non-technical and reads developer language literally.
**Why:** Phrases like "this will break" or "this is a blocker" cause unnecessary alarm about live business risk when the actual intent was a technical planning question between developers. Patrick is part-time and slow to respond; when he doesn't reply Dean sometimes steps in, which adds confusion if the original question was purely technical.

---

### Soft Transition — FreshSales Runs in Parallel Until Jarvis is Proven
**Date:** 28 April 2026
**Decision:** FreshSales stays live and continues handling enquiries and automations throughout the Jarvis trial period. The two systems run side by side. FreshSales is only switched off once Jarvis is tested and confirmed reliable — there is no fixed cutover date.
**Why:** Any disruption to lead intake while testing a new system would directly harm the business. The transition must be proven safe first, not scheduled first.

---

### Property-First Data Model
**Date:** Phase 1 analysis
**Decision:** The core entity in the system is the Property, not the Customer. A property can have multiple projects over time and persistent assets (e.g. roofs) that carry across them.
**Why:** Commercial solar customers in particular often have multiple projects on the same site over time. Modelling Property as the anchor reflects the real relationship.

---

### Quote Snapshot System
**Date:** Phase 1 analysis
**Decision:** Pricing is locked at the moment a quote is created. Historical quotes never change retroactively, even if catalogue prices or labour rates change later.
**Why:** Both a legal requirement and a trust issue — a customer's quote must remain accurate to what they were actually offered.

---

### Diary Is a Google Calendar Front-End, Not a Custom Calendar
**Date:** Phase 1 analysis
**Decision:** The diary feature reads and writes directly to Google Calendar rather than maintaining its own calendar data.
**Why:** The business already runs on Google Calendar and staff already see jobs on their phones via it. A parallel calendar system would create ongoing sync work for no benefit.

---

### Staff Sign In With Google Workspace Accounts
**Date:** Phase 1 analysis
**Decision:** No separate username/password system — staff authenticate with their existing Google Workspace login.
**Why:** The business is already on Google Workspace, and this immediately grants the scoped access needed for Calendar, Drive, and Gmail integration.

---

### FreshSales Is Being Fully Replaced
**Date:** March 2026
**Decision:** A bespoke CRM is being built as core infrastructure, replacing FreshSales entirely. The FreshSales subscription will be cancelled once the new system is proven (see Soft Transition decision above).
**Why:** FreshSales and the existing Bubble app are not connected at the database level, requiring duplicate manual data entry. A unified replacement removes this duplication and the ongoing subscription cost.
**Constraint while in progress:** The existing FreshSales ↔ Bubble integration must not be broken while the Bubble app is still in active use.

---

### Two Legacy Cloud Services Retired, Replaced Natively
**Date:** 18 March 2026
**Decision:** Two small backend services (a staff scheduling algorithm and a scaffold cost calculator) that previously ran on Google Cloud Run are being retired and rebuilt as simple functions inside the new system.
**Why:** Both were small, fully understood pieces of logic. Keeping them as separate cloud services created an ongoing infrastructure dependency for no benefit.

---

### Manual Override Pattern
**Date:** Phase 1 analysis
**Decision:** Every field that gets an automatic suggested value must remain manually editable by staff, with the original suggestion retained for reference.
**Why:** Staff need to be able to correct automated suggestions without losing the system's original reasoning as a reference point.

---

### White-Label-Ready Design System
**Date:** Phase 1 design
**Decision:** Visual styling (colours, spacing, branding) is fully separated from the underlying components, so the same system could in future be re-skinned for a different business without changing code.
**Why:** Keeps the option open for future use beyond Atlantic Renewables without committing to it now. As a side benefit, the colour conventions already familiar to staff from the existing Bubble app (e.g. pink for "install") are preserved.

---

### Jarvis Control Centre — Staff Self-Service for Templates and Rules
**Date:** 7 May 2026
**Decision:** Dean and Jack have direct, no-developer-needed access to view, edit, and create communication templates and to enable/disable automation rules. Technical configuration (raw rule logic) is always shown to them as plain English, never as raw code.
**Why:** Day-to-day template and rule management must not depend on developer availability.

---

### Drive Content Editing Built Natively Into the Control Centre
**Date:** 16 May 2026
**Decision:** After the originally planned third-party editing tool (StackEdit) turned out to be permanently broken, a simple content editor was built directly into the Jarvis Control Centre instead, reading and writing the same Google Drive files.
**Why:** Avoids dependency on an external tool that doesn't work reliably. Staff edit in one place, with no change to where the actual content lives.

---

### Email System Launches With Two Content Tiers
**Date:** 16 May 2026
**Decision:** The email system launches with some templates containing real, ready-to-use content (drawn from actual past Atlantic Renewables emails) and others containing placeholder content that Dean/Jack will need to review and finalise before go-live.
**Why:** Real content existed for some customer journeys already; others need staff input on wording before they're customer-ready. This was scoped explicitly rather than blocking the whole system on full content completion.

---

### Single Google Cloud Account for All Jarvis Infrastructure
**Date:** 11 April 2026
**Decision:** All Google Cloud resources (API credentials, sign-in configuration) for Jarvis are managed under one designated Google account, not spread across personal or ad-hoc accounts.
**Why:** Keeps billing, credentials, and account ownership in one auditable place, removing the risk of access being lost if a personal account becomes inaccessible.

---

### Twenty CRM Selected as CRM Layer Alongside Jarvis
**Date:** 19 June 2026
**Decision:** Twenty (open-source CRM) selected to run alongside Jarvis as the system of record for contacts, pipeline, and communication history. Self-hosted on a Hetzner CX22 server owned by Atlantic Renewables.
**Why:** No per-seat pricing (unlimited users at a flat server cost of ~£4.60/month vs £175+/month for equivalent SaaS). AR owns the data — no vendor lock-in, no subscription that can be changed or cancelled by a third party. Open-source means any developer can work with it in future, not just a specific individual.

---

### Twenty Integration — MCP and API Only, No Direct Database Access
**Date:** 19 June 2026
**Decision:** All integration between Jarvis and Twenty routes through Twenty's native MCP server, REST/GraphQL API, and webhooks. Direct database access is not used, even though it is technically possible on a self-hosted deployment.
**Why:** Direct database writes bypass all of Twenty's application logic — no workflow triggers fire, no webhooks send, no permissions are enforced, and no audit trail is created. The MCP/API path is the only route that keeps governance, logging, and trigger visibility intact.

---

### Single Opportunities Object for the Full Lead-to-Project Lifecycle
**Date:** 19 June 2026
**Decision:** The entire customer journey — from first enquiry through to completed project — is carried on a single Opportunities record in Twenty, with the Stage field driving automation at each transition. No separate Lead object, no forced conversion step creating a new record.
**Why:** Twenty does not have a separate Lead object by design — this is the recommended default path. It matches the existing Jarvis model (one record per person, status changes drive automation). Avoids the data duplication and sync complexity that arises when lead and project are separate records.

---

### Telephony — Freshcaller Replacement Under Evaluation
**Date:** 19 June 2026
**Decision:** Freshcaller (Freshdesk PRO, 5 seats, £175/month) will be replaced. Two options evaluated: Aircall (£150/month, standalone) and Twilio via Jarvis (£24-44/month, fully integrated). Decision pending Dean's approval.
**Why the change is happening:** Freshcaller is embedded in FreshSales. Moving away from FreshSales means moving away from Freshcaller. Both replacement options support number porting — the existing Manchester numbers are preserved. The Twilio option is significantly cheaper and integrates calls directly into the CRM record, but requires a short build sprint. Aircall requires no build work but remains a standalone subscription.
