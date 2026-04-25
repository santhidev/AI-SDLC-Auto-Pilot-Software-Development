# ADR-000: AutoPilot Default Stack

## Context
This project is managed by AutoPilot. Decisions are locked via project profiles.

## Decisions
- Multi-platform: web + mobile + desktop
- Web: Next.js + MUI
- Backend: NestJS + Postgres (custom) or SaaS (optional)
- Mobile: Flutter
- Desktop: Tauri
- UI preview policy: Storybook (web) + screenshot packs (mobile/desktop)

## Consequences
- Pros: consistent, scalable baseline
- Cons: can be overkill for tiny projects; tune profiles
