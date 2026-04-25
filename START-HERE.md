# START HERE / เริ่มตรงนี้

## EN

- This repo is an AI SDLC AutoPilot (file-as-truth).
- Read order (MUST follow exactly):
  1. `meta/sdlc-state.json` — current phase/status/mode
  2. `meta/project-profile.yaml` — stack & platform
  3. `meta/engineering-profile.yaml` — architecture, testing, quality
  4. `meta/design-profile.yaml` — UI system, theme, preview
  5. `meta/quality-gates.yaml` — PASS/FAIL criteria
  6. `meta/artifact-map.yaml` — required artifacts by phase
  7. `meta/traceability.md` — FR-to-test mapping
  8. `README.md` — overview
  9. `docs/00-overview.md`, `docs/01-architecture.md`, `docs/02-continue.md`
  10. `prompts/*.txt` — execution commands

- Run order:
  - New project: `PROMPT-1` → `PROMPT-2` → `PROMPT-4`
  - Requirement change: `PROMPT-3` → `PROMPT-2` → `PROMPT-4`
  - Release: `PROMPT-E` → `PROMPT-5`

- Do/Don't:
  - **Do**: minimal diffs, update traceability, keep gates deterministic, preserve UI visibility policy
  - **Don't**: ask user, rewrite unrelated files, delete artifacts

## TH

- Repo นี้คือ AI SDLC AutoPilot (ไฟล์คือความจริง)
- ลำดับอ่าน (บังคับ):
  1. `meta/sdlc-state.json` — phase/status/mode ปัจจุบัน
  2. `meta/project-profile.yaml` — stack และ platform
  3. `meta/engineering-profile.yaml` — architecture, testing, quality
  4. `meta/design-profile.yaml` — UI system, theme, preview
  5. `meta/quality-gates.yaml` — เกณฑ์ PASS/FAIL
  6. `meta/artifact-map.yaml` — artifacts ที่ต้องมีตาม phase
  7. `meta/traceability.md` — mapping FR ไป test
  8. `README.md` — ภาพรวม
  9. `docs/00-overview.md`, `docs/01-architecture.md`, `docs/02-continue.md`
  10. `prompts/*.txt` — คำสั่งรัน

- ลำดับรัน:
  - เริ่มใหม่: `PROMPT-1` → `PROMPT-2` → `PROMPT-4`
  - เปลี่ยน requirement: `PROMPT-3` → `PROMPT-2` → `PROMPT-4`
  - Release: `PROMPT-E` → `PROMPT-5`

- Do/Don't:
  - **ทำ**: แก้น้อยที่สุด, อัปเดต traceability, gate ต้องชัด, รักษา UI visibility policy
  - **ห้าม**: ถามผู้ใช้, แก้ไฟล์ไม่เกี่ยว, ลบ artifacts