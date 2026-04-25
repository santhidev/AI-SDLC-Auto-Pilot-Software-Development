# AI CONTEXT / บริบทสำหรับ AI

## EN

### Mission
This AI SDLC AutoPilot optimizes for **speed + quality + auditability**. The system generates complete SDLC artifacts (requirements, architecture, tests, evidence) from a single requirement file, with deterministic quality gates that enforce PASS/FAIL criteria.

### Core Philosophy
- **File-as-truth**: All state, decisions, and artifacts are stored in files. No chat memory.
- **Gates**: Quality gates (traceability, UI visibility, security scans, evidence) determine completion.
- **Previews**: Web requires Storybook; Mobile/Desktop require screenshot packs.
- **Evidence**: Release requires collected evidence pack under `/evidence`.

### Default Stack Choices (from meta/*)
| Component | Default |
|-----------|---------|
| Backend | .NET 9 + YARP + SignalR + Minimal APIs + PostgreSQL + Redis Pub/Sub + Seq |
| Web | Blazor WebAssembly (PWA) + Tailwind CSS + Fluxor |
| Mobile | .NET MAUI + CommunityToolkit.Mvvm + Material 3 |
| Desktop | Avalonia UI + ReactiveUI + Fluent Theme (Skia) |
| CI/CD | GitHub Actions |
| Deployment | VPS + Docker Compose |
| Design System | Design Tokens (JSON-driven) + Platform-specific themes |
| Testing | TDD (xUnit + NSubstitute, unit high, integration medium, e2e critical-only) |

### Glossary
- **AutoPilot**: The SDLC pipeline driven by prompts (PROMPT-1/2/3/4/5/E)
- **Gates**: Quality gates in `meta/quality-gates.yaml` that enforce PASS/FAIL
- **Artifacts**: SDLC documents generated per phase (see `meta/artifact-map.yaml`)
- **Evidence**: Release artifacts collected in `/evidence` for audit/approval
- **Traceability**: FR → Acceptance → Design → Code → Test mapping in `meta/traceability.md`
- **ADR**: Architecture Decision Records in `05-architecture/34-adr/`
- **Design Tokens**: JSON-driven design system (color, typography, spacing, radius) auto-generated to each platform

---

## TH

### ภารกิจ
AI SDLC AutoPilot นี้ optimize เพื่อ **ความเร็ว + คุณภาพ + ตรวจสอบได้** ระบบสร้าง artifacts SDLC ครบ (requirements, architecture, tests, evidence) จากไฟล์ requirement เดียว มี quality gates ที่ deterministic บังคับเกณฑ์ PASS/FAIL

### ปรัชญาหลัก
- **ไฟล์คือจริง**: ทุก state, การตัดสินใจ, และ artifacts เก็บในไฟล์ ไม่พึ่งความจำแชท
- **Gates**: Quality gates (traceability, UI visibility, security scans, evidence) ตัดสินเสร็จหรือไม่
- **Previews**: Web ต้องมี Storybook; Mobile/Desktop ต้องมี screenshot packs
- **Evidence**: Release ต้องมี evidence pack เก็บใน `/evidence`

### ค่า Default Stack (จาก meta/*)
| ส่วน | Default |
|------|---------|
| Backend | .NET 9 + YARP + SignalR + Minimal APIs + PostgreSQL + Redis Pub/Sub + Seq |
| Web | Blazor WebAssembly (PWA) + Tailwind CSS + Fluxor |
| Mobile | .NET MAUI + CommunityToolkit.Mvvm + Material 3 |
| Desktop | Avalonia UI + ReactiveUI + Fluent Theme (Skia) |
| CI/CD | GitHub Actions |
| Deployment | VPS + Docker Compose |
| Design System | Design Tokens (JSON-driven) + Platform-specific themes |
| Testing | TDD (xUnit + NSubstitute, unit high, integration medium, e2e critical-only) |

### คำศัพท์สำคัญ
- **AutoPilot**: SDLC pipeline ที่ขับเคลื่อนด้วย prompts (PROMPT-1/2/3/4/5/E)
- **Gates**: Quality gates ใน `meta/quality-gates.yaml` ที่บังคับ PASS/FAIL
- **Artifacts**: เอกสาร SDLC ที่ generate ตาม phase (ดู `meta/artifact-map.yaml`)
- **Evidence**: Artifacts release ที่เก็บใน `/evidence` สำหรับตรวจสอบ/อนุมัติ
- **Traceability**: Mapping FR → Acceptance → Design → Code → Test ใน `meta/traceability.md`
- **ADR**: Architecture Decision Records ใน `05-architecture/34-adr/`
- **Design Tokens**: Design system ที่ขับเดินด้วย JSON (สี, ฟอนต์, ระยะห่าง, มุม) auto-generate ให้แต่ละ platform