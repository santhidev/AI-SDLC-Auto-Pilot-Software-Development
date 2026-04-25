# START-HERE (AutoPilot Core) — Read This First

## EN (60 seconds)
- **Files are the only source of truth.** No chat memory.
- **No-Ask** by default. Do not ask the user.
- **Minimal diffs** only.

**Read order:**
1) `autopilot-core/MANUAL.md`
2) `autopilot-core/meta/quality-gates.yaml` + `autopilot-core/meta/artifact-map.yaml`
3) `autopilot-core/stacks/default.stackref` + `autopilot-core/stacks/*.yaml`
4) `project/meta/sdlc-state.json` + `project/meta/*.yaml`

**Run order:**
- New: `PROMPT-1 → PROMPT-2 → PROMPT-4`
- Req change: `PROMPT-3 → PROMPT-2 → PROMPT-4`
- Stack change: `PROMPT-0W → PROMPT-1 → PROMPT-2 → PROMPT-4`

## TH (60 วินาที)
- **ไฟล์คือความจริงเดียว** ไม่พึ่งแชท
- **No-Ask** เป็นค่าเริ่มต้น ห้ามถามผู้ใช้
- **แก้น้อยที่สุด** (minimal diffs)

**ลำดับอ่าน:**
1) `autopilot-core/MANUAL.md`
2) `autopilot-core/meta/quality-gates.yaml` + `autopilot-core/meta/artifact-map.yaml`
3) `autopilot-core/stacks/default.stackref` + `autopilot-core/stacks/*.yaml`
4) `project/meta/sdlc-state.json` + `project/meta/*.yaml`

**ลำดับรัน:**
- เริ่มใหม่: `PROMPT-1 → PROMPT-2 → PROMPT-4`
- แก้ requirement: `PROMPT-3 → PROMPT-2 → PROMPT-4`
- เปลี่ยน stack: `PROMPT-0W → PROMPT-1 → PROMPT-2 → PROMPT-4`
