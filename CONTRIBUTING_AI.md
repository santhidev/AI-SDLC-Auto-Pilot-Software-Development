# CONTRIBUTING (AI)

## EN

### For AI Agents
- Read core files first: `meta/sdlc-state.json`, `meta/*-profile.yaml`, `meta/quality-gates.yaml`
- No-Ask: Do not ask the user. If ambiguous, choose repo defaults and document.
- Minimal diffs: Change <=10 files per batch. Never rewrite unrelated files.
- Update traceability if spec changes (FR → Acceptance → Test mapping in `meta/traceability.md`)
- ADR required for major decisions (stack, pattern, gates philosophy)
- Preserve UI visibility policy: Web → Storybook, Mobile/Desktop → screenshot packs
- Never delete artifacts; deprecate with docs instead
- Update `CHANGELOG_AUTOPILOT.md` for each batch

### Workflow
- New project: PROMPT-1 → PROMPT-2 → PROMPT-4
- Requirement change: PROMPT-3 → PROMPT-2 → PROMPT-4
- Release: PROMPT-E → PROMPT-5

---

## TH

### สำหรับ AI Agents
- อ่านไฟล์ core ก่อน: `meta/sdlc-state.json`, `meta/*-profile.yaml`, `meta/quality-gates.yaml`
- ห้ามถาม: ถ้าคลุมเครือ ใช้ default ของ repo แล้วบันทึก
- แก้น้อยที่สุด: เปลี่ยน <=10 ไฟล์ต่อ batch ห้ามแก้ไฟล์ไม่เกี่ยว
- อัปเดต traceability ถ้าสเปคเปลี่ยน (FR → Acceptance → Test ใน `meta/traceability.md`)
- ต้องมี ADR สำหรับการตัดสินใจใหญ่ (stack, pattern, gates philosophy)
- รักษา UI visibility policy: Web → Storybook, Mobile/Desktop → screenshot packs
- ห้ามลบ artifacts; ใช้ deprecate แทนพร้อม docs
- อัปเดต `CHANGELOG_AUTOPILOT.md` ทุก batch

### Workflow
- เริ่มใหม่: PROMPT-1 → PROMPT-2 → PROMPT-4
- เปลี่ยน requirement: PROMPT-3 → PROMPT-2 → PROMPT-4
- Release: PROMPT-E → PROMPT-5