# AI_CONTEXT / บริบทสำหรับ AI

## EN
### Mission
Make software delivery **faster** while remaining **traceable**, **testable**, and **auditable**.

### Philosophy
- **File-as-Truth**: the repo files are the only truth.
- **State-driven**: `project/meta/sdlc-state.json` decides the next action.
- **Profiles lock decisions**: stack/engineering/design are configured and not guessed.
- **Gates decide done**: completion is PASS/FAIL based on objective criteria.
- **UI visibility**: previews are mandatory.
- **Evidence**: releases require evidence reports.

### Glossary
- **Artifact**: a deliverable file (SRS, NFR, acceptance, ADR, state machine, API contract, etc.)
- **Gate**: objective PASS/FAIL rule
- **Traceability**: mapping FR → acceptance → code/tests → evidence
- **ADR**: Architecture Decision Record

## TH
### ภารกิจ
ทำให้การส่งมอบซอฟต์แวร์ **เร็วขึ้น** แต่ยัง **ตรวจสอบได้**, **ทดสอบได้**, และ **ออดิตได้**

### หลักคิด
- **File-as-Truth**: ไฟล์ใน repo คือความจริงเดียว
- **State-driven**: ใช้ `project/meta/sdlc-state.json` ตัดสินใจขั้นถัดไป
- **Profiles**: ล็อกการตัดสินใจเรื่อง stack/engineering/design
- **Gates**: เสร็จหรือไม่เสร็จตัดสินด้วย PASS/FAIL
- **UI visibility**: ต้องมี preview/screenshot
- **Evidence**: การปล่อยงานต้องมีหลักฐาน

### Glossary (คำศัพท์)
- **Artifact**: ไฟล์ส่งมอบ (SRS/NFR/AC/ADR/State Machine/API Contracts ฯลฯ)
- **Gate**: กฎ PASS/FAIL แบบวัดได้
- **Traceability**: การโยง FR → AC → code/tests → evidence
- **ADR**: เอกสารตัดสินใจด้านสถาปัตยกรรม
