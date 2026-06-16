# Project Status — Atlantic Renewables / Jarvis

**Last updated:** 16 June 2026

> One place to understand where the project stands right now.

---

## Current Phase

FreshSales import complete (8,912 leads imported, all flagged `imported_from_freshsales = true` for safety). Leads list page live. Public intake endpoint working. Patrick can see imported leads in Jarvis.

| Milestone | Status |
|---|---|
| Supabase schema | ✅ Complete |
| Next.js scaffold + Google OAuth | ✅ Complete |
| Pipeline tracking | ✅ Complete |
| Google Drive folder automation | ✅ Complete |
| Lead intake automation (Cap 1) | ✅ Built — 61 rules, 33 templates (see note below) |
| Task management | ✅ Complete |
| Milestone notifications | ✅ Complete |
| Chase sequences | ✅ Complete |
| Production deployment | ✅ Live, OAuth working |
| Post-install checklist | ✅ Confirmed working by Patrick |
| Referral scheme | Deprioritised — low usage, confirmed by Dean |
| FreshSales import | ✅ 8,912 leads imported, zero lost |
| Leads list page | ✅ Live |

---

## Email Template System

- Two-layer architecture: developer-built email shell + plain-text content file editable by non-technical staff
- 13 templates seeded with real content; 10 templates seeded with placeholder content awaiting staff sign-off
- Template admin screen live — staff can manage rules and templates without developer involvement
- Outstanding: staff content sign-off on placeholder templates before go-live

---

## Cap 1 Rules Reconciliation Audit — 16 June 2026

A full audit compared the 62 live automation rules against the documented FreshSales workflow behaviour to check nothing was lost or guessed incorrectly in the rebuild.

**Result:** No contamination from incomplete data — all rules correctly avoid logic that depended on fields not yet in the schema. Three real gaps found and fixed:
1. Battery-only leads weren't being automatically converted to a project (FreshSales did this automatically) — fixed
2. Payment milestone automation was too generic — one rule fired for any payment, rather than distinct actions per payment stage — fixed, now models each payment as a timestamped event
3. The "Earn Scheme" referral email was missing from the final-payment workflow — fixed

**Outstanding:** Most automation rules (49 of 62) are in a test/dry-run state pending explicit approval from Dean and Jack before they run live for real customers. This is a deliberate safety gate, not an oversight — but it means most automation isn't yet live.

---

## Active Blockers

| Blocker | Owner | Notes |
|---|---|---|
| Automation rules awaiting go-live approval | Dean / Jack | 49 of 62 rules built and tested but not yet switched on |
| WhatsApp Business channel | Dean | Blocked on Meta Business Account setup |
| Bubble data migration | Patrick | ~1,500–1,600 active projects to migrate; export method confirmed (CSV, Bubble API, or third-party backup service) |
| Staff content sign-off | Dean / Jack | 10 placeholder email templates need real copy before go-live |

---

## What's Next

1. Dean/Jack review and approve automation rules for go-live
2. Staff content sign-off on placeholder templates
3. Patrick to export full FreshSales template library — cross-reference against what's been rebuilt, catch any gaps
4. Bubble data migration planning
5. WhatsApp channel build (blocked on Meta Business Account)
