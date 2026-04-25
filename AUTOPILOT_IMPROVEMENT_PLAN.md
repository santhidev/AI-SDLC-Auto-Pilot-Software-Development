# AUTOPILOT IMPROVEMENT PLAN

## Goals

1. **Establish complete onboarding pack** - Ensure AI agents can understand and work on this repo without human guidance
2. **Fill core SDLC artifacts** - Complete all template artifacts with actual content or clear documentation
3. **Enable quality gates** - Ensure traceability matrix and acceptance criteria are actionable
4. **Maintain minimal diffs** - Work in small batches with proper changelog entries

## Scope

### In Scope
- Creating/updating onboarding files (START-HERE.md, AI_CONTEXT.md, REPO_MANIFEST.yaml, CONTRIBUTING_AI.md, CHANGELOG_AUTOPILOT.md)
- Writing AI_NOTES.md with current state analysis
- Creating AUTOPILOT_IMPROVEMENT_PLAN.md
- Updating docs/02-continue.md with handoff information
- Filling core SDLC artifacts (requirements, vision, traceability)
- Updating traceability matrix with mappings

### Out Scope
- Writing actual application code (src/ directory)
- Implementing actual tests
- Creating production deployment configs
- Filling all template artifacts completely (focus on core only)

## Batches

### Batch 1: Onboarding Pack (COMPLETED)
**Files (5):**
- START-HERE.md (created)
- AI_CONTEXT.md (created)
- REPO_MANIFEST.yaml (created)
- CONTRIBUTING_AI.md (created)
- CHANGELOG_AUTOPILOT.md (created)

**Status:** ✅ Complete

---

### Batch 2: Analysis & Planning (COMPLETED)
**Files (2):**
- AI_NOTES.md (created)
- AUTOPILOT_IMPROVEMENT_PLAN.md (created)

**Status:** ✅ Complete

---

### Batch 3: Documentation Update
**Files (1-3):**
- docs/02-continue.md (update with handoff info)

**Estimated changes:** Add section about "What changed & how to continue"

---

### Batch 4: Core Artifacts - Requirements
**Files (4):**
- requirement.md (add FRs or document as template repo)
- 01-discovery/00-vision.md (fill or clarify purpose)
- 03-requirements/11-SRS.md (fill with actual requirements)
- 03-requirements/14-acceptance-criteria.md (add acceptance criteria)

**Note:** May need human decision on whether this is template repo or actual project

---

### Batch 5: Traceability
**Files (1-2):**
- meta/traceability.md (update with actual FR→Test mappings)
- evidence/requirements-trace.md (ensure consistency)

---

## Risks + Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| No actual requirements defined | High | Medium | Document as template repo or add placeholder FRs |
| Human decision needed for project scope | Medium | High | Make no-ask choice and document in AI_NOTES.md |
| Incomplete artifacts cause gate failures | Medium | High | Focus on making gates pass with current state |
| Enterprise compliance folders unused | Low | Low | Accept as future-use templates |

## Acceptance Criteria

### For Onboarding Pack
- [x] START-HERE.md exists with TH/EN read/run order
- [x] AI_CONTEXT.md exists with mission, philosophy, stack, glossary
- [x] REPO_MANIFEST.yaml exists with all file categories
- [x] CONTRIBUTING_AI.md exists with AI agent rules
- [x] CHANGELOG_AUTOPILOT.md exists with entry for this session

### For Analysis
- [x] AI_NOTES.md exists with current state, issues, improvement plan
- [x] AUTOPILOT_IMPROVEMENT_PLAN.md exists with goals, scope, batches

### For Documentation
- [ ] docs/02-continue.md updated with handoff info

### For Quality Gates
- [ ] meta/traceability.md has at least one FR mapping (or documented as template)
- [ ] Quality gates can evaluate current state (PASS/FAIL)

## Rollback Notes

If changes cause issues:
1. Onboarding files can be deleted (not critical to SDLC)
2. AI_NOTES.md and AUTOPILOT_IMPROVEMENT_PLAN.md are advisory only
3. Core meta/ files should NOT be modified without ADR
4. If traceability is modified, ensure consistency with evidence/

## Next Steps (After This Session)

1. Human review of onboarding pack completeness
2. Decision: Template repo vs. actual project
3. If actual project: Define specific FRs in requirement.md
4. Continue with Batch 3-5 when ready