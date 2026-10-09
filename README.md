# ELECWORKS PRO v3.2 — AI-Powered Electrical/MEP Engineering Platform
## Quick start (no server needed)
Open `ElecWorks_Pro_v3.2.html` in any modern browser. Works offline. Login: admin `ahmed.dahab2006@gmail.com` / `Dahab@1982`, or any seeded user (01000000001/123456) or "الدخول التجريبي المجاني".
## Architecture
- Single-file SPA (offline-first, PWA) + optional Node.js/Express backend (`/backend`, deploy per backend/DEPLOY.md) + Supabase schema (`/database/schema.sql`)
- Local-first: every feature degrades gracefully without backend
## Phases
0 Analysis · 1 Premium UI (theme/palette/alerts) · 2 Storage adapters+migration+error boundary+XSS+IndexedDB · 3-6 Backend/AI Gateway/Vision/Email · 7-10 WhatsApp/Comms Hub/Documents/Copilot · 11-14 Analytics/Workflow/Notifications/Security+Deploy
## Security notes
- AI keys and OAuth secrets live ONLY in backend .env
- CSP runs Report-Only (inline handlers preserved for backward compatibility; tighten after migration)
- Passwords hashed server-side (bcrypt); legacy local mode is prototype-grade
## Backups
ElecWorks_backup_before_phase*.html — restore by renaming.
