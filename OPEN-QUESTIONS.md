# Open Questions — Atlantic Renewables / Jarvis

> Questions that need an answer before something can be built or decided. Resolved questions are kept below, not deleted — the resolution is part of the record.

This log excludes internal software development tooling questions — it covers business and data questions relevant to anyone supporting or reviewing the project from outside the development team.

---

## Open

### Schema Migration — Unified Customer Record
**Raised:** 10 June 2026 — Patrick confirmed the approach is safe.
**Question:** Should leads, contacts, and projects be collapsed into a single record that grows with the customer relationship, rather than three separate tables?
**Status:** Direction approved by Patrick. Awaiting Jack/Dean confirmation. No functional blocker — proceeding on the approved direction.

### Daryl's Bubble Sync — Exact Fields Needed
**Raised:** 10 June 2026
**Question:** When a project's stage changes in the new system, it needs to mirror to the existing Bubble app for Daryl. Which specific stage changes need mirroring, and which Bubble fields do they map to?
**Status:** Patrick to clarify with Daryl directly.

### Multi-Technology Lead Intake
**Raised:** 28 April 2026 — Dean confirmed FreshSales behaviour: if a customer selects multiple services on the website form (e.g. solar + re-roofing), both relevant follow-up emails currently fire.
**Question:** Does the new system correctly handle a customer selecting more than one service at once?
**Status:** Needs verification before go-live.

### Bubble Data Export — Skills Matrix and Quoting Constants
**Question:** What are the current staff skill categories and rating scale used in the existing Bubble app? What are the current scaffold cost calculation constants (cost per storey, handrail cost, etc.)?
**Status:** Awaiting Patrick's Bubble data export.

### FreshSales Field Duplication
**Question:** Several fields appear twice in the FreshSales export with slightly different names (Customer Type, Roof Material, Surname/Last Name). Which version is the canonical one in each case?
**Status:** Awaiting Patrick's guidance during data migration planning.

### Cap 7 — Referral Scheme Webhook
**Question:** What does the existing referral webhook integration do, and is it still needed?
**Status:** Resolved 15 June 2026 — see below.

### Google Calendar Structure
**Question:** Is the business's existing Google Calendar set up as one calendar per staff member, or shared calendars by job type? This affects how the diary feature creates events.
**Status:** To confirm with Dean.

---

## Resolved

### ✅ Referral Webhook — Resolved 15 June 2026
**Answer (Patrick):** The webhook is not Zapier — it's Make (formerly Integromat). The referral scheme has low usage and is currently out of scope for the rebuild. No replication needed at this stage; native logic will be built if/when the referral scheme is prioritised.

### ✅ Bubble App Link Structure — Resolved 15 June 2026
**Answer (Patrick):** Confirmed the URL pattern used by the existing Bubble app for individual project records, including how the record identifier is structured. This allows old "view in app" links found in historical email templates to be correctly replaced with equivalent links in the new system.

### ✅ Bubble Data Migration Scale and Method — Resolved 15 June 2026
**Answer (Patrick):** Approximately 1,500–1,600 active projects exist in the Bubble app. Export is possible via per-table CSV export, the official Bubble Data API, or a third-party backup service. Very few (if any) records are expected to exist in Bubble that aren't already captured in the FreshSales export.

### ✅ Domestic Solar Payment Stage Names — Resolved 15 June 2026
**Answer (Jack):** Confirmed the exact stage names used for tracking payment milestones, and confirmed that — in the new system — these should trigger automated actions at the moment each is marked paid, rather than being checked periodically.

### ✅ Contractor-Type Leads — Resolved 15 June 2026
**Answer (Jack):** No automated workflow currently exists in FreshSales for this customer type — historically handled manually, if at all. The new system will create a manual follow-up task for this case rather than building an automated email that was never actually used.

### ✅ Customer Type and Technology Interest Fields — Identified 15 June 2026
**Found by:** Patrick, reviewing the rebuild
**Issue:** The website enquiry form captures customer type (homeowner/commercial/contractor) and technology interest (solar, battery, roofing, etc.), but neither field existed yet in the new system's database or intake process — meaning a key piece of routing logic was at risk of being lost in the rebuild.
**Resolution:** Both fields are being added to the schema and intake process, with routing rules updated to use them directly instead of approximations.

### ✅ What Does the Quoting Engine Need to Calculate?
**Resolved:** 6 March 2026 (Patrick)
**Answer:** Per-template profit rates, electrical work estimated separately, catalogue markup applied per item. Tile multipliers and labour data tables are the key inputs from the existing system.

### ✅ What Was the Original FreshSales Data Structure?
**Resolved:** 12 March 2026
**Answer:** Four linked areas — Leads, Contacts, Accounts, Deals — with Deals as the critical bridge between a lead and an active job.

### ✅ Email Template Sender/Reply-To Configuration
**Resolved:** 5 May 2026
**Answer:** Default sender is the main company address for all automated emails. Staff with appropriate permissions can change both the "from" and "reply-to" address independently per send — maximum flexibility, confirmed as the preferred approach.

### ✅ Are the Rebuilt Email Templates Real Content or Placeholder?
**Resolved:** 16 May 2026
**Answer:** Mixed by design. Three templates (commercial solar, roofing, battery) use real content from actual past company emails. Ten templates use placeholder content pending staff review before go-live.
