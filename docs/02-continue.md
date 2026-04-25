# Continue / ทำงานต่อโดยไม่เริ่มใหม่

## EN

### What Changed (2026-04-25)
- Added AI onboarding pack: START-HERE.md, AI_CONTEXT.md, REPO_MANIFEST.yaml, CONTRIBUTING_AI.md, CHANGELOG_AUTOPILOT.md
- Created AI_NOTES.md with current state analysis
- Created AUTOPILOT_IMPROVEMENT_PLAN.md with improvement roadmap

### How to Continue
1. Read `meta/sdlc-state.json` to get current phase/status
2. Read onboarding files first:
   - START-HERE.md (read order + run order)
   - AI_CONTEXT.md (mission, philosophy, stack)
   - REPO_MANIFEST.yaml (file structure)
   - CONTRIBUTING_AI.md (rules)
3. Check AI_NOTES.md for current issues and improvement plan
4. Continue by phase:
   - New project: PROMPT-1 → PROMPT-2 → PROMPT-4
   - Requirement change: PROMPT-3 → PROMPT-2 → PROMPT-4
   - Release: PROMPT-E → PROMPT-5
5. If you change specs: update traceability in `meta/traceability.md`
6. Each batch: update CHANGELOG_AUTOPILOT.md

### Basic Workflow
- If you change requirements: run PROMPT-3 → PROMPT-2 → PROMPT-4
- If you fix a bug: add regression test first, then patch code

---

## TH

### มีอะไรเปลี่ยน (2026-04-25)
- เพิ่ม AI onboarding pack: START-HERE.md, AI_CONTEXT.md, REPO_MANIFEST.yaml, CONTRIBUTING_AI.md, CHANGELOG_AUTOPILOT.md
- สร้าง AI_NOTES.md วิเคราะห์สถานะปัจจุบัน
- สร้าง AUTOPILOT_IMPROVEMENT_PLAN.md วางแผนปรับปรุง

### วิธีทำต่อ
1. อ่าน `meta/sdlc-state.json` เช็ค phase/status ปัจจุบัน
2. อ่าน onboarding files ก่อน:
   - START-HERE.md (ลำดับอ่าน + ลำดับรัน)
   - AI_CONTEXT.md (ภารกิจ, ปรัชญา, stack)
   - REPO_MANIFEST.yaml (โครงสร้างไฟล์)
   - CONTRIBUTING_AI.md (กติกา)
3. ดู AI_NOTES.md สำหรับปัญหาปัจจุบันและแผนปรับปรุง
4. ทำต่อตาม phase:
   - เริ่มใหม่: PROMPT-1 → PROMPT-2 → PROMPT-4
   - เปลี่ยน requirement: PROMPT-3 → PROMPT-2 → PROMPT-4
   - Release: PROMPT-E → PROMPT-5
5. ถ้าเปลี่ยนสเปค: อัปเดต traceability ใน `meta/traceability.md`
6. ทุก batch: อัปเดต CHANGELOG_AUTOPILOT.md

### Workflow พื้นฐาน
- ถ้า requirement เปลี่ยน: รัน PROMPT-3 → PROMPT-2 → PROMPT-4
- ถ้าแก้บั๊ก: เพิ่ม regression test ก่อน แล้วค่อยแก้โค้ด