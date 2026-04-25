# CONTRIBUTING_AI / แนวทางร่วมพัฒนา (สำหรับ AI)

## Rules
1) Read core + project truth files first (see START-HERE).
2) No-Ask: do not ask the user.
3) Minimal diffs: keep changes small and scoped.
4) If you change specs, update `project/meta/traceability.md`.
5) If you change stack/pattern/gates philosophy, create/update ADR under `project/05-architecture/34-adr/`.
6) Do not delete key artifacts. Deprecate with docs.

## Safe workflow
- Requirement change: PROMPT-3 → PROMPT-2 → PROMPT-4
- Keep gates deterministic.
