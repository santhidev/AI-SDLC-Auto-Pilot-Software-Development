# AutoPilot MANUAL (Single File) — คู่มือรวม (ไฟล์เดียวจบ)

> **Build:** 2026-04-25 17:24:23  
> **Repo layout:** `autopilot-core/` (engine) + `project/` (single project)

---

## 1) What is this? / นี่คืออะไร?

**EN:** This repository is an **AI SDLC AutoPilot**. It enforces a deterministic SDLC using files as the only source of truth. Agents can resume from the latest state without chat history.

**TH:** Repo นี้คือ **AI SDLC AutoPilot** ที่ทำ SDLC แบบ deterministic โดยยึดไฟล์เป็นความจริงเดียว Agent ใดๆ สามารถเริ่มต่อจากสถานะล่าสุดได้โดยไม่ต้องอ่านแชท

---

## 2) Core Principles / หลักการสำคัญ

1) **File-as-Truth**: Files are the only truth.
2) **No-Ask default**: Agents do not ask the user.
3) **Minimal diffs**: Change the smallest possible set of files.
4) **State-driven**: `project/meta/sdlc-state.json` defines phase/status.
5) **Contracts**: `autopilot-core/meta/*` defines required artifacts and gates.
6) **Stack Catalog**: stacks are files; selection is a pointer.
7) **Traceability**: FR → Acceptance → Code/Tests → Evidence.

---

## 3) Repository Layout / โครงสร้าง Repo

### 3.1 Minimal file set (keep it minimal)

- Root
  - `README.md` (short landing)
  - `PROJECT_ROOT.txt`
  - `LICENSE`

- Core engine
  - `autopilot-core/START-HERE.md` (short)
  - `autopilot-core/MANUAL.md` (this file)
  - `autopilot-core/meta/` (contracts)
  - `autopilot-core/prompts/` (prompt files)
  - `autopilot-core/stacks/` (stack catalog)

- Project workspace
  - `project/requirement.md`
  - `project/meta/` (state + selected stack + materialized profiles)
  - `project/*` artifacts and code

---

## 4) Source of Truth & Read Order / ไฟล์จริงและลำดับอ่าน

### 4.1 Source of truth (Core)
- `autopilot-core/meta/quality-gates.yaml`
- `autopilot-core/meta/artifact-map.yaml`
- `autopilot-core/stacks/default.stackref`
- `autopilot-core/stacks/*.yaml`
- `autopilot-core/prompts/*`

### 4.2 Source of truth (Project)
- `project/meta/sdlc-state.json`
- `project/meta/stack.selected.stackref` (optional)
- `project/meta/stack.overrides.yaml` (optional)
- `project/meta/project-profile.yaml` (materialized)
- `project/meta/engineering-profile.yaml` (materialized)
- `project/meta/design-profile.yaml` (materialized)
- `project/meta/traceability.md`

### 4.3 Mandatory read order (for any AI)
1) This `autopilot-core/MANUAL.md`
2) Core contracts: `autopilot-core/meta/*`
3) Stack catalog: `autopilot-core/stacks/*`
4) Project state: `project/meta/sdlc-state.json`
5) Project profiles: `project/meta/*-profile.yaml`
6) Requirement/spec artifacts: `project/requirement.md`, `project/03-requirements/*`
7) Decisions: `project/05-architecture/34-adr/*`
8) UI/Enterprise packs if enabled

---

## 5) Stack Catalog System (NEW) / ระบบ Stack Catalog (ใหม่)

### 5.1 Why stack catalog?
**EN:** Wizard should not hardcode stacks. A stack is a file that includes **3 profiles**. The project selects a stack via a pointer file.

**TH:** Wizard ไม่ควร hardcode stack อีกต่อไป ให้ stack เป็นไฟล์ (ไฟล์ละ stack) และต้องมี **3 profiles** ครบ โปรเจกต์เลือก stack ด้วยไฟล์ pointer

### 5.2 Files involved
- Default stack pointer: `autopilot-core/stacks/default.stackref`
- Stack files: `autopilot-core/stacks/<stack_id>.yaml`
- Project selected stack pointer: `project/meta/stack.selected.stackref` (optional)
- Overrides: `project/meta/stack.overrides.yaml` (optional)

### 5.3 Resolution rules (deterministic)
1) If `project/meta/stack.selected.stackref` exists and contains an ID → use it.
2) Else use `autopilot-core/stacks/default.stackref`.
3) Load the stack file `autopilot-core/stacks/<id>.yaml`.
4) Materialize `project/meta/*-profile.yaml` from `stack.profiles`.
5) Apply overrides: deep-merge override wins.

### 5.4 Stack file schema (required)
A stack file MUST contain:
- `id`, `name`, `version`, `updated`, `tags`
- `profiles.project_profile`
- `profiles.engineering_profile`
- `profiles.design_profile`
- optional: `files[]` to write extra files into `project/`
- optional: `constraints` (runtime requirements)

### 5.5 Overrides deep-merge rules
- Only keys in overrides replace corresponding keys in the final profile.
- Unspecified keys remain from the selected stack.
- Keep overrides small.

### 5.6 Stack-provided files (`files[]`)
If stack defines:
```yaml
files:
  - to: "project/stack/.meteor-packages.txt"
    content: |
      ...
```
The system MUST write that content to that file.

---

## 6) Wizard (PROMPT-0W) — Updated Usage / วิธีใช้ Wizard (อัปเดตแล้ว)

### 6.1 Wizard purpose
**EN:** Wizard now lists stacks from catalog and lets you select by ID. It then materializes profiles and writes pointers.

**TH:** Wizard เปลี่ยนเป็นโหมด “เลือก stack จาก catalog” แล้วค่อย materialize profiles และเขียน pointer

### 6.2 Wizard commands
- `/wizard start`
- `/wizard list stacks`
- `/wizard select stack <stack_id>`
- `/wizard set override <path> <value>` (optional)
- `/wizard review`
- `/wizard finish`

### 6.3 Example: list & select
```text
/wizard start
/wizard list stacks
/wizard select stack meteorjs-3.4-baccarat
/wizard review
/wizard finish
```

### 6.4 Example: override preview (small change)
```text
/wizard start
/wizard select stack omni-global-nestjs
/wizard set override design.preview.web storybook
/wizard finish
```

### 6.5 What Wizard MUST write/update
- `project/meta/stack.selected.stackref`
- `project/meta/stack.overrides.yaml` (if override used)
- `project/meta/project-profile.yaml`
- `project/meta/engineering-profile.yaml`
- `project/meta/design-profile.yaml`
- `project/05-architecture/34-adr/ADR-000-tech-stack.md` (update decision)
- `project/meta/sdlc-state.json.mode = "no-ask"`

---

## 7) Prompts (PROMPT-1..5/E) — What they do / แต่ละ Prompt ทำอะไร

### PROMPT-1 — SDLC Autopilot
- Resolve stack selection
- Materialize profiles if missing
- Generate missing SDLC artifacts under `project/`
- Set phase to `requirements`

### PROMPT-2 — Consistency Reviewer
- Minimal rewrite until stable
- Ensure traceability, state machines, API contracts, UI checklist
- Set status to `stable`

### PROMPT-3 — Impact Analysis
- Use traceability to rewrite only impacted files after requirement change
- Set status to `draft`

### PROMPT-4 — One-shot Build
- Build code/tests
- Produce UI previews
- Produce evidence reports
- Stop when gates PASS and phase becomes `release`

### PROMPT-5 — Quality Gate
- Validate contracts and report PASS/FAIL into evidence

### PROMPT-E — Evidence Collector
- Update evidence index and summaries

---

## 8) Run Flows / Flow การใช้งาน

### 8.1 New start
1) (optional) PROMPT-0W (choose stack)
2) PROMPT-1
3) PROMPT-2
4) PROMPT-4

### 8.2 Requirement changed
1) Edit `project/requirement.md`
2) PROMPT-3
3) PROMPT-2
4) PROMPT-4

### 8.3 Switch stack
1) PROMPT-0W
2) PROMPT-2 (stabilize)
3) PROMPT-4 (rebuild)

---

## 9) Contracts / กติกา (Artifact Map + Quality Gates)

- `autopilot-core/meta/artifact-map.yaml` defines required files per phase.
- `autopilot-core/meta/quality-gates.yaml` defines PASS/FAIL criteria.

If you add a new required file, update artifact-map.
If you change PASS/FAIL logic, update quality-gates and document in changelog/ADR.

---

## 10) Traceability & ADR Rules / กติกา Traceability และ ADR

### 10.1 Traceability
- If spec changes, update `project/meta/traceability.md`.
- Ensure FR maps to acceptance and tests.

### 10.2 ADR
- Major decision changes must be recorded under `project/05-architecture/34-adr/`.
- Keep ADR-000 updated with chosen stack.

---

## 11) How to add a new stack file / วิธีเพิ่ม Stack ใหม่

1) Copy an existing stack file as a template.
2) Ensure it contains 3 profiles.
3) Add optional `files[]` for necessary stack-specific files.
4) Add to `autopilot-core/stacks/`.
5) Optionally change default by editing `default.stackref`.

---

## 12) Troubleshooting / แก้ปัญหา

- If profiles look wrong: check `stack.selected.stackref` + `stack.overrides.yaml`.
- If Wizard shows no stacks: ensure `autopilot-core/stacks/*.yaml` exists.
- If build fails due to runtime: check stack `constraints.requires`.

---

## Appendix: Minimal expectations / สรุปสิ่งที่ต้องมี

- Keep docs minimal: README short, START-HERE short, MANUAL single detailed file.
- Keep system deterministic: pointers + catalog + contracts.

END.
