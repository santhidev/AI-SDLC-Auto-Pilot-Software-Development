# START HERE / เริ่มตรงนี้ (AutoPilot Core)

## EN — What is this repo?
This repository is an **AI SDLC AutoPilot** that uses **files as the only source of truth**.
It is split into:
- `autopilot-core/`: the engine (prompts, gates, templates)
- `project/`: the single project workspace (requirements, artifacts, code)

## TH — Repo นี้คืออะไร?
Repo นี้คือ **AI SDLC AutoPilot** ที่ยึดหลักว่า **ไฟล์คือความจริงเดียว**
และแยกส่วนชัดเจน:
- `autopilot-core/`: เครื่องยนต์ (prompts, gates, templates)
- `project/`: โปรเจกต์เดียว (requirements, artifacts, code)

---

## Mandatory Read Order / ลำดับอ่าน (บังคับ)

### Core (understand the engine)
1) `autopilot-core/AI_CONTEXT.md`
2) `autopilot-core/meta/quality-gates.yaml`
3) `autopilot-core/meta/artifact-map.yaml`
4) `autopilot-core/prompts/*`

### Project (understand current state)
5) `project/meta/sdlc-state.json`
6) `project/meta/*-profile.yaml`
7) `project/requirement.md` + `project/03-requirements/*`
8) `project/meta/traceability.md` + `project/05-architecture/34-adr/*`
9) `project/ui/*` (if UI)
10) `project/compliance|security|ops|evidence|integrations/*` (if enterprise)

---

## Run Order / ลำดับรัน
- New / เริ่มใหม่: **PROMPT-1 → PROMPT-2 → PROMPT-4**
- Requirement change / เปลี่ยน requirement: **PROMPT-3 → PROMPT-2 → PROMPT-4**

---

## Non-negotiable rules / กติกาห้ามฝ่าฝืน
- Files are the only source of truth (ไม่พึ่งแชท)
- No-Ask default (ห้ามถามผู้ใช้)
- Minimal diffs (แก้น้อยที่สุด)
- Update traceability when specs change (แก้สเปคต้องอัปเดต traceability)
- UI must be visible if UI exists (ต้องมี preview/screenshot)
