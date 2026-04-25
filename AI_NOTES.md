# AI_NOTES.md

## EN

### What this repo is
This is an AI SDLC AutoPilot repository - a file-driven SDLC pipeline that generates complete software development lifecycle artifacts (requirements, architecture, tests, UI previews, evidence) from a single requirement file. It enforces deterministic quality gates and supports Web + Mobile + Desktop platforms with enterprise compliance (GDPR/PDPA).

### Current State
- **phase**: `discovery`
- **status**: `draft`
- **mode**: `no-ask`
- **compliance_profile**: `enterprise-global`
- **last_updated**: `2026-04-25T09:42:29`

### Source-of-Truth Set
| File | Purpose |
|------|---------|
| `meta/sdlc-state.json` | Current phase/status/mode |
| `meta/project-profile.yaml` | Stack, platform, deployment |
| `meta/engineering-profile.yaml` | Architecture, testing, quality |
| `meta/design-profile.yaml` | UI system, theme, preview |
| `meta/quality-gates.yaml` | PASS/FAIL criteria |
| `meta/artifact-map.yaml` | Required artifacts by phase |
| `meta/traceability.md` | FR-to-test mapping |

### What Works Well
- Complete meta/ profiles covering project, engineering, design
- Quality gates defined with clear PASS/FAIL criteria
- Artifact map specifies required documents per phase
- Enterprise compliance folders exist (compliance/, security/, ops/, evidence/)
- UI visibility policy documented (Storybook for web, screenshots for mobile/desktop)
- Prompts folder has all 7 prompt files (PROMPT-0W to PROMPT-E)
- Evidence folder has index and 6 report templates
- Documentation structure in place (docs/00-02)
- Integration templates exist (LINE OA, payments, logistics, sure-sure)

### Top 10 Issues/Risks

1. **Empty traceability matrix** - `meta/traceability.md` has no FR mappings filled in
2. **Empty requirements artifacts** - `03-requirements/11-SRS.md`, `12-NFR.md`, `14-acceptance-criteria.md` are all templates with no actual content
3. **Empty vision** - `01-discovery/00-vision.md` is a blank template
4. **No actual FRs defined** - `requirement.md` has no specific requirements, only template placeholders
5. **Empty UI specs** - `ui/IA.md`, `ui/user-flows.md`, `ui/component-inventory.md` are all templates
6. **No state machines filled** - `04-domain/23-state-machines.md` has placeholder content only
7. **Empty API contracts** - `05-architecture/32-api-contracts.md` is a template
8. **No test implementation** - `08-testing/70-test-strategy.md` is a template
9. **Release checklist incomplete** - `09-release/80-release-checklist.md` has no specific items
10. **Missing actual code** - No `src/` directory with actual implementation exists

### Improvement Plan (Phased)

**Phase 1: Fill Core Artifacts (Priority)**
- Update `requirement.md` with specific FRs (or note this is a template repo)
- Complete `01-discovery/00-vision.md`
- Complete `03-requirements/11-SRS.md`, `12-NFR.md`, `14-acceptance-criteria.md`
- Update `meta/traceability.md` with actual mappings

**Phase 2: Complete UI Specs**
- Fill `ui/IA.md` with sitemap
- Fill `ui/user-flows.md` with flows
- Fill `ui/component-inventory.md` with components

**Phase 3: Architecture & Domain**
- Complete `04-domain/23-state-machines.md`
- Complete `05-architecture/32-api-contracts.md`
- Add more ADRs if needed

**Phase 4: Testing & Release**
- Complete `08-testing/70-test-strategy.md`
- Complete `09-release/80-release-checklist.md`

### Unconfirmed / Needs Human Decision
- Whether this repo is meant to be a **template** (blank) or should have **actual project requirements** filled in
- The actual project name (currently `<auto-from-requirement>` in project-profile.yaml)
- Target users and core problem being solved (not defined in any artifact)
- Specific FRs to implement (none currently defined)

---

## TH

### Repo นี้คืออะไร
Repo นี้คือ AI SDLC AutoPilot - pipeline SDLC ที่ขับเคลื่อนด้วยไฟล์ สร้าง artifacts SDLC ครบ (requirements, architecture, tests, UI previews, evidence) จากไฟล์ requirement เดียว บังคับ deterministic quality gates และรองรับ Web + Mobile + Desktop พร้อม enterprise compliance (GDPR/PDPA)

### สถานะปัจจุบัน
- **phase**: `discovery`
- **status**: `draft`
- **mode**: `no-ask`
- **compliance_profile**: `enterprise-global`
- **last_updated**: `2026-04-25T09:42:29`

### ชุดไฟล์ความจริง
| ไฟล์ | หน้าที่ |
|------|---------|
| `meta/sdlc-state.json` | phase/status/mode ปัจจุบัน |
| `meta/project-profile.yaml` | Stack, platform, deployment |
| `meta/engineering-profile.yaml` | Architecture, testing, quality |
| `meta/design-profile.yaml` | UI system, theme, preview |
| `meta/quality-gates.yaml` | เกณฑ์ PASS/FAIL |
| `meta/artifact-map.yaml` | Artifacts ที่ต้องมีตาม phase |
| `meta/traceability.md` | Mapping FR ไป test |

### จุดที่ทำได้ดี
- Meta/ profiles ครบ covering project, engineering, design
- Quality gates มีเกณฑ์ PASS/FAIL ชัดเจน
- Artifact map ระบุเอกสารที่ต้องมีตาม phase
- Enterprise compliance folders มีครบ (compliance/, security/, ops/, evidence/)
- UI visibility policy มี (Storybook สำหรับ web, screenshots สำหรับ mobile/desktop)
- Prompts ครบ 7 ไฟล์ (PROMPT-0W ถึง PROMPT-E)
- Evidence folder มี index และ 6 report templates
- เอกสาร structure พร้อม (docs/00-02)
- Integration templates มี (LINE OA, payments, logistics, sure-sure)

### Top 10 จุดบอด/ความเสี่ยง

1. **Traceability matrix ว่าง** - `meta/traceability.md` ไม่มี FR mappings
2. **Requirements artifacts ว่าง** - `03-requirements/11-SRS.md`, `12-NFR.md`, `14-acceptance-criteria.md` เป็นแค่ template
3. **Vision ว่าง** - `01-discovery/00-vision.md` เป็น template ว่าง
4. **ไม่มี FR จริง** - `requirement.md` ไม่มี requirements เฉพาะ มีแค่ template placeholders
5. **UI specs ว่าง** - `ui/IA.md`, `ui/user-flows.md`, `ui/component-inventory.md` เป็น template
6. **State machines ไม่มี** - `04-domain/23-state-machines.md` มีแค่ placeholder
7. **API contracts ว่าง** - `05-architecture/32-api-contracts.md` เป็น template
8. **ไม่มี test implementation** - `08-testing/70-test-strategy.md` เป็น template
9. **Release checklist ไม่สมบูรณ์** - `09-release/80-release-checklist.md` ไม่มีรายละเอียด
10. **ไม่มี code จริง** - ไม่มี `src/` directory กับ implementation

### แผนปรับปรุง (เป็นขั้น)

**ขั้น 1: เติม Core Artifacts (เร่งด่วน)**
- อัปเดต `requirement.md` ด้วย FRs เฉพาะ (หรือบันทึกว่าเป็น template repo)
- กรอก `01-discovery/00-vision.md`
- กรอก `03-requirements/11-SRS.md`, `12-NFR.md`, `14-acceptance-criteria.md`
- อัปเดต `meta/traceability.md` ด้วย mappings จริง

**ขั้น 2: กรอก UI Specs**
- กรอก `ui/IA.md` ด้วย sitemap
- กรอก `ui/user-flows.md` ด้วย flows
- กรอก `ui/component-inventory.md` ด้วย components

**ขั้น 3: Architecture & Domain**
- กรอก `04-domain/23-state-machines.md`
- กรอก `05-architecture/32-api-contracts.md`
- เพิ่ม ADRs ถ้าต้องการ

**ขั้น 4: Testing & Release**
- กรอก `08-testing/70-test-strategy.md`
- กรอก `09-release/80-release-checklist.md`

### เรื่องที่ยืนยันไม่ได้จากไฟล์
- Repo นี้เป็น **template** (ว่าง) หรือควรมี **project requirements** จริง
- ชื่อ project จริง (ตอนนี้คือ `<auto-from-requirement>` ใน project-profile.yaml)
- Target users และ core problem ที่จะแก้ (ไม่มีใน artifact ไหน)
- FRs เฉพาะที่จะ implement (ตอนนี้ไม่มี)