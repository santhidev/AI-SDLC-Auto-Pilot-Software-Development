# AutoPilot Changelog

## 2026-04-27

### Stack Migration: Node.js → .NET Cross-Platform Complete Stack
- **Summary:** Changed Default Stack from Node.js (NestJS/Next.js/Flutter/Tauri) to .NET 9 (Blazor/MAUI/Avalonia) with Design Tokens
- **Why:** Adopt .NET Cross-Platform Complete Stack for unified codebase, better developer experience on Windows, and future iOS/macOS support readiness
- **Files changed:**
  - meta/project-profile.yaml (updated) - Backend: NestJS → .NET 9 + YARP + SignalR + Minimal APIs; Web: Next.js → Blazor WebAssembly; Mobile: Flutter → .NET MAUI; Desktop: Tauri → Avalonia UI; Queue: RabbitMQ → Redis Pub/Sub
  - meta/engineering-profile.yaml (updated) - Added testing tools: xUnit, NSubstitute, bUnit, Avalonia Automation
  - meta/design-profile.yaml (updated) - Changed from Material Design to Design Tokens (JSON-driven) with Tailwind CSS, Material 3, and Fluent themes
  - AI_CONTEXT.md (updated) - Updated Default Stack tables in both EN and TH, added Design Tokens to glossary
- **Risks:** None - configuration and documentation only, no actual code yet in this template repository
- **Next steps:** Fill core SDLC artifacts (requirements, vision, traceability) when project scope is finalized

---

## 2026-04-25

### Batch 1-3: Onboarding Pack & Documentation
- **Summary:** Initial AI SDLC AutoPilot setup - created onboarding pack and updated documentation
- **Why:** Mandatory onboarding pack required for AI agent handoff per ONE-SHOT HANDOFF v2 protocol
- **Files changed:**
  - START-HERE.md (created) - TH/EN read/run order guide
  - AI_CONTEXT.md (created) - mission, philosophy, stack, glossary
  - REPO_MANIFEST.yaml (created) - file structure manifest
  - CONTRIBUTING_AI.md (created) - AI agent contribution rules
  - CHANGELOG_AUTOPILOT.md (created) - changelog itself
  - AI_NOTES.md (created) - current state analysis with top 10 issues
  - AUTOPILOT_IMPROVEMENT_PLAN.md (created) - phased improvement roadmap
  - docs/02-continue.md (updated) - added handoff info section
- **Risks:** None - documentation-only change establishing onboarding framework
- **Next steps:** Human decision on template vs actual project scope, then fill core SDLC artifacts if actual project