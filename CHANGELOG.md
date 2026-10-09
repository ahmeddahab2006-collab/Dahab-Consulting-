# ELECWORKS PRO — CHANGELOG

## PHASE 1 — Premium UI/UX (2026-10-08) — ADDITIVE ONLY, ZERO FUNCTIONAL CHANGES
### Added
- Light/Dark theme (`data-theme` token layer; sidebar/top stay dark-navy in light mode) + 🌙 toggle, persisted `ui_theme`
- Command Palette: Ctrl+K, searches 26 modules + projects + 6 actions, AR/EN, keyboard nav
- Alerts Center 🔔: live-computed from project data (overdue tasks, open RFIs, failed tests, checklist findings, low health, trial ending) — read-only computed, no schema change
- Breadcrumbs bar (#crumbBar): Home › current module · project · Ctrl+K hint; login-aware
- Global search = palette; project switcher accessible from palette
### Compatibility preserved (verified)
- render() logic unchanged (2 additive hook lines only); all 241 functions & 40+ inline handlers intact
- All localStorage/sessionStorage keys untouched; no schema change
- GD guard order preserved; print pipeline intact; PWA untouched
### Regression gate — 9/9 PASSED (6 roles × 26 views, AR/EN, golden calc vectors, save/load, BOQ, print, admin, mobile CSS, PWA)

## PHASE 2 — Storage Adapters · Migration · Error Boundary · XSS Shield · IndexedDB (2026-10-08)
### Added
- storage.js facade (get/set/update/delete/sync) + LocalStorageProvider (default) + CloudDatabaseProvider (lazy stub for PHASE 3+)
- Schema migration v3: `schemaVersion` on projects DB + `createdAt` stamps + users meta (`users_meta_v1`) — NON-destructive, pre-migration auto-backups (`*_backup_pre_m3`)
- Global Error Boundary: render() wrapped (window + lexical bindings) + window.onerror → friendly AR/EN error card, logged to audit trail — NO blank pages
- XSS shield: `esc()` helper applied to 14 user-input sinks (tasks/minutes/RFIs/risks/photos/captions/BOQ/checklist remarks/reports/SCC)
- IndexedDB PhotoStore (photos no longer quota-limited to ~5MB; cross-tab persistence; sessionStorage fallback intact)
- Sync status pill (🟢 online / 🔴 offline · local-first)
### Compatibility (verified — 20/20 gate)
- All storage keys preserved; existing localStorage call-sites untouched; USERS stays an array
- 6 roles × 26 views · golden calc vectors · AR/EN · migration idempotent
### File: ElecWorks_Pro_v2.1.html (new name per convention)

## PHASES 3-6 — Backend · Secure AI Gateway · Vision · Email Center (2026-10-08)
### Added
- **PHASE 3 Backend** (/backend): Express server · JWT auth + RBAC middleware (bcrypt password hashing, legacy-hash tool) · sync push/pull routes · security headers · Supabase schema (7 tables + audit_trail) · .env.example · DEPLOY.md
- **PHASE 4 Secure AI Gateway**: /api/ai/chat + /vision + /email-assist with provider adapters (OpenAI/Kimi/Claude/Gemini) — keys server-side only · frontend AIClient routes through gateway; legacy client-key path kept as fallback · local smartReport engine = offline fallback · every AI output labeled "ملاحظة أولية — تتطلب مراجعة مهندس"
- **PHASE 5 Photos + AI Vision**: 🔍 analyze per photo (gateway vision OR local heuristic fallback — always labeled) · Before/After comparison UI · IndexedDB persistence intact
- **PHASE 6 Email Center**: Inbox/Drafts/Compose · per-email AI (summarize/classify/draft) · mandatory "مراجعة وإرسال" confirm · demo mode when backend offline (drafts queue locally) · backend email routes (Graph/Gmail OAuth URLs + SMTP + mock)
### Frontend additions
- API client (timeout/abort/offline taxonomy) · Admin ☁️ Server tab (save/test/disconnect) · sync pill integration · mail nav item (non-demo roles) · mailSend demo-guarded
### Gate — 12/12 PASSED (gateway chat/vision/report via mock fetch, local fallbacks, 4 roles × 27 views, golden calc, site AI UI)
### Files: ElecWorks_Pro_v3.0.html (NEW NAME) · ElecWorks_Backend_v3.zip · CHANGELOG.md

## PHASES 7-10 — WhatsApp · Comms Hub · Documents · AI Copilot (2026-10-08)
- **PHASE 7 WhatsApp Center**: project conversations · mock/demo mode offline (real Meta Cloud API routes already in backend) · AI chat summary/action extraction · mandatory send confirmation · demo-guarded
- **PHASE 8 Comms Hub**: unified Email+WhatsApp+RFI feed · type filters · daily communication summary (local counts; full AI summary via backend)
- **PHASE 9 Document Center**: 17-category revisioned register · edit bumps Rev and PRESERVES full history (never overwrites) · revision history viewer · printable register (EL-DOC-REG) · seed register included
- **PHASE 10 AI Copilot**: floating 🤖 panel across the whole app · quick prompts (summary/RFI/tests/loads/BOQ) · local deterministic answer engine from live project data · cloud copilot via secure gateway when backend connected · every answer labeled "Engineer Verification Required"
### Gate — 15/15 PASSED (wa/hub/docs/copilot flows, revision-history integrity, 4 roles × 30 views, golden calc, AR/EN)
### File: ElecWorks_Pro_v3.1.html (NEW NAME)

## PHASES 11-14 — Analytics · Workflow · Notifications · Security+Deploy (2026-10-08)
- **PHASE 11**: Analytics view (6 KPI cards + phase progress bars) · printable registers: RFI / Test / Risk / **Snag auto-extracted from failed checklist items** · CSV export of all registers
- **PHASE 12**: Task workflow engine — 8 statuses (Open→Assigned→InProgress→Pending Consultant/Contractor/Client→Closed/Rejected) · SLA indicators (⛔ overdue / ⏳ due≤2d) · fully backward-compatible with legacy s field
- **PHASE 13**: Persistent notification engine (localStorage, read/unread, deep-link to module) merged with live alerts in the bell · auto-scan on load (overdue tasks, open RFIs, failed tests) · mark-all-read
- **PHASE 14**: v3.2 · Report-Only CSP meta (non-breaking hardening) · README runbook · backups lineage
### Final gate — 20/20 PASSED (6 roles × 31 views, golden calc, AR/EN, all register/workflow/notification flows)
### File: ElecWorks_Pro_v3.2.html

## PHASES 15-16 — Grouped Navigation · Task Hierarchy (2026-10-08) — FINAL v3.3
- **PHASE 15**: Sidebar restructured into 7 collapsible main sections (Main · Project Mgmt · Engineering & Design · Cost & Tender · Quality & Site · Reports & Analytics · System) with icons, per-section permission filtering, persisted collapse state
- **PHASE 16**: Task hierarchy engine — stable task IDs (non-destructive migration) · main tasks expandable to subtasks (indented, counter badge, inline add-subtask inheriting owner/due+3d) · auto progress = % closed subtasks · workflow statuses + SLA apply to subtasks · legacy tasks unaffected (no parent = main)
### Gate — 15/15 PASSED (grouped nav render/collapse/perm-filter, hierarchy progress 50%→100%, 6 roles × 31 views, golden calc + SCC physics, AR/EN)
### File: ElecWorks_Pro_v3.3.html (FINAL — synced)

## PHASES A-C — Panel Simulator · What-If Engine · Site Walk (2026-10-08) — v3.4
- **Virtual Panel Simulator**: interactive panel face (big 42px breaker icons), Web Audio sounds (ON clack 1400Hz / OFF thunk 320Hz / warn / overload alarm, persisted mute), live L1/L2/L3 loading bars, all-on/all-off, overload blink
- **What-If Scenario Engine**: load ×1.0/1.2/1.5/0.8 + length ×1.0/1.3/1.6 — instant old-vs-new comparison (In, cable size with growth arrow, ΔV), cable cost delta in EGP, compliance counter — original data untouched
- **Site Walk Mode**: 8 walk points, huge 130×130px thumb buttons (✅/❌) with sounds, counter+progress+color-coded point grid, back button, PDF walk report (EL-WALK-*) with signature
### Gate — 23/23 PASSED (physics: exact 45kW pump spread, 79.14kW total, no false overload; what-if both directions; walk flow; 4 roles × 34 views; golden calc; AR/EN)
### File: ElecWorks_Pro_v3.4.html (FINAL)

## PHASES D-G — VE Engine · Maintenance Log · Presentation Mode · Project Templates (2026-10-08) — v3.5
- **Value Engineering**: Cu→Al alternative per circuit (size ×1.6, CAPEX −55%/OPEX +losses), honest payback table + tariff/hours inputs — small sizes correctly flagged as NOT cheaper (market reality)
- **Maintenance Log**: 7 seeded equipment (gen/trafo/UPS/panels/FA/pumps) with big icons, run-hours tracking, service intervals, 3-state auto status (OK/Due soon/SERVICE DUE) with alarm sound, service history
- **Presentation Mode**: 8 fullscreen auto-generated client slides (title/scope/design/progress/photos/financial/team/closing) with keyboard nav, progress dots, sounds, phone number closing
- **Project Templates**: 4 templates (residential tower/admin/healthcare/villas) — one-click project with activated phase, 4 tailored dated tasks, realistic high risk, instant notification
- **Review fixes**: presentation slide-index clamping; VE honesty for small conductors
### Gate — 24/24 PASSED (VE physics & payback, maintenance status transitions incl. alarm boundary, presentation nav/clamp, template creation flow, 6 roles × 38 views, golden calc + SCC, AR/EN)
### File: ElecWorks_Pro_v3.5.html (FINAL)

## HOTFIX v3.6 — Expired-trial lockout resolved (2026-10-09)
- Trial-ended screen now includes: **direct admin login** (email+password fields + sign-in), **🔄 Start new trial** button (owner reset), back-to-signin kept
- doLogin reads credentials from either field set (login screen or expired screen)
- Plus the 7 features from this session: WhatsApp invite (contact search + branded message), email-or-phone register/login, luxury report CSS, cross-module BOQ sync banner, per-module guides (11), contracting-standard role matrix + reset, live showcase project (Nile Tower)
### Gate — 9/9 PASSED (admin login despite expiry, reset flow, fresh-trial re-grant, renders)
### File: ElecWorks_Pro_v3.6.html
