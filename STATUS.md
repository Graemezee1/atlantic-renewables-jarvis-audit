# Project Status — Atlantic Renewables / Jarvis

**Last updated:** 19 June 2026

> One place to understand where the project stands right now.

---

## Current Phase

Architecture and CRM strategy confirmed. Jarvis is built and running with 8,912 imported leads. Twenty CRM selected as the CRM layer alongside Jarvis. Telephony replacement research complete — cost comparison drafted for Dean. Immediate priority: push the demo to Vercel so Dean can see the system working.

| Milestone | Status |
|---|---|
| Supabase schema | ✅ Complete |
| Next.js scaffold + Google OAuth | ✅ Complete |
| Pipeline tracking | ✅ Complete |
| Google Drive folder automation | ✅ Complete |
| Lead intake automation (Cap 1) | ✅ Built — 62 rules, 33 templates |
| Task management | ✅ Complete |
| Milestone notifications | ✅ Complete |
| Chase sequences | ✅ Complete |
| Production deployment | ✅ Live, OAuth working |
| Post-install checklist | ✅ Confirmed working |
| FreshSales import | ✅ 8,912 leads imported |
| Leads list page | ✅ Live |
| Lead record page + dashboard + pipeline board | ⚠️ Built but not pushed — commit c9fbc8a unpushed |
| Twenty CRM — server provisioned | ⏳ Pending Hetzner account setup by Dean |
| Twenty CRM — installed | ⏳ Pending server |
| Telephony — Twilio integration | ⏳ Pending Dean's decision (Aircall vs Twilio) |

---

## Email Template System

- 13 templates seeded with real content; 10 templates seeded with placeholder content awaiting staff sign-off
- FreshSales template inventory complete: ~85 templates extracted and catalogued (June 2026)
- Jack confirmed: templates cannot be exported from FreshSales; old templates not wanted in new system — many need updating
- Template admin screen live — staff can manage rules and templates without developer involvement

---

## Cap 1 Rules — Status

62 rules built and tested. 49 of 62 are in test/dry-run state pending explicit approval from Dean and Jack. This is a deliberate safety gate — no automation runs live for real customers until Dean approves. The approval review is scheduled after the demo lands.

---

## Twenty CRM — Selected June 2026

Open-source CRM selected to run alongside Jarvis. Key facts:
- Self-hosted on Hetzner CX22 server (5.49 EUR/month) — AR owns the data, no vendor lock-in
- No per-seat pricing — unlimited users
- Jarvis connects via Twenty's native MCP server and REST/GraphQL API
- Single Opportunities record carries the full lead-to-project lifecycle via Stage field changes
- Architecture validated against Twenty's documentation

---

## Telephony Research — Complete

Freshcaller (current): PRO plan, 5 seats, £175/month. Options compared:
- Aircall: £150/month (5 seats yearly) — standalone, no deep integration
- Twilio via Jarvis: £24-44/month — fully integrated, calls auto-log to CRM record, screen pop on inbound call

Awaiting Dean's decision. Both support number porting from Freshcaller.

---

## Active Blockers

| Blocker | Owner | Notes |
|---|---|---|
| Demo not live | OpenCode | Commit c9fbc8a (lead record, dashboard, pipeline board) not pushed. Demo invisible until live. |
| Hetzner account setup | Dean | 10 minutes at hetzner.com/cloud — needed before Twenty can be installed |
| Telephony decision | Dean | Aircall vs Twilio — cost comparison sent |
| Automation rules go-live approval | Dean / Jack | 49 of 62 rules in test mode — needs demo first |
| WhatsApp Business channel | Dean | Blocked on Meta Business Account setup |
| Bubble data migration | Phase 2 | Separate planning phase |
| Staff content sign-off | Dean / Jack | 10 placeholder email templates need real copy |

---

## What's Next (Priority Order)

1. Push commit c9fbc8a — lead record, dashboard, pipeline board go live on Vercel
2. Dean sets up Hetzner account (CX22, hetzner.com/cloud)
3. Install Twenty on Hetzner via Docker Compose
4. Dean decides on telephony (Aircall or Twilio)
5. Demo to Dean — show Jarvis and Twenty working together
6. Dean approves automation rules — 49 rules graduate from test to live
