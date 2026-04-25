# AI SDLC AutoPilot — Ultimate (TH/EN)

**EN:** A file-driven AI SDLC AutoPilot that builds end-to-end software with **Web + Mobile + Desktop**, enforced by **Quality Gates**, with **visible UI previews** and **auditable evidence packs**.

**TH:** ระบบ AI SDLC AutoPilot ที่ขับเคลื่อนด้วยไฟล์ สร้างซอฟต์แวร์แบบ end-to-end รองรับ **Web + Mobile + Desktop** โดยบังคับใช้ **Quality Gates**, มี **UI preview ให้เห็นจริง**, และมี **Evidence Pack** สำหรับตรวจสอบ/อนุมัติ release

> Build: 2026-04-25 09:42:29

---

## TL;DR

### Quick Start (No‑Ask)
1) Edit `requirement.md`
2) Run `prompts/PROMPT-1-sdlc-autopilot.txt`
3) Run `prompts/PROMPT-2-rewrite-loop.txt` until stable
4) Run `prompts/PROMPT-4-one-shot-build.txt`

### When requirements change
Run: `PROMPT-3 → PROMPT-2 → PROMPT-4`

---

## What is this? / นี่คืออะไร?

**EN:** This repository is an SDLC “autopilot” where **files are the only source of truth**. Any AI agent can resume from the latest state by reading `meta/sdlc-state.json`.

**TH:** Repo นี้คือระบบ “AutoPilot” สำหรับ SDLC ที่ยึดหลักว่า **ไฟล์คือความจริงเดียว** AI agent ตัวไหนเข้ามาก็เริ่มต่อจากสถานะล่าสุดได้ โดยอ่าน `meta/sdlc-state.json`

---

## Core Principles / หลักการ

1) **File = Source of Truth** (ไม่พึ่งความจำแชท)
2) **State-machine SDLC** (`meta/sdlc-state.json` บอก phase)
3) **Profiles lock decisions** (project/engineering/design)
4) **Artifact Contract** (`meta/artifact-map.yaml`)
5) **Quality Gates** decide PASS/FAIL (`meta/quality-gates.yaml`)
6) **UI must be visible** (Web: Storybook, Mobile/Desktop: screenshot packs)
7) **Evidence pack required** for releases (`/evidence`)

---

## Repository Map / โครงสร้าง

```
/
  requirement.md
  /meta/...
  /docs/...
  /ui/...
  /compliance/ /security/ /ops/ /evidence/
  /integrations/
  /prompts/
  /src/
```

---

## Start from Latest State (Agent Checklist)

1) Read `meta/sdlc-state.json`
2) Read profiles:
   - `meta/project-profile.yaml`
   - `meta/engineering-profile.yaml`
   - `meta/design-profile.yaml`
3) Read:
   - `meta/quality-gates.yaml`
   - `meta/artifact-map.yaml`
4) Continue by phase:
   - discovery/requirements → generate/repair artifacts (PROMPT‑1/2)
   - build → implement code/tests/previews/evidence (PROMPT‑4)
   - release → evidence approval (PROMPT‑E/PROMPT‑5)

---

## Prompts / คำสั่ง

- **PROMPT‑1** Generate SDLC artifacts
- **PROMPT‑2** Consistency reviewer (minimal rewrite)
- **PROMPT‑3** Impact analysis (rewrite only impacted)
- **PROMPT‑4** One-shot build (code + tests + previews + evidence)
- **PROMPT‑5** Quality gate enforcer (PASS/FAIL)
- **PROMPT‑E** Evidence collector (release approval)
- **PROMPT‑0W** Optional wizard (override defaults)

---

## Change & Bug workflow

- `changes/CR-*.md` for feature changes
- `incidents/BUG-*.md` for bugs (add regression test first)

---

## License
MIT (see `LICENSE`).
