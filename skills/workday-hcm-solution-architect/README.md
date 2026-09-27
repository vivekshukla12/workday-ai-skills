# Workday HCM Solution Architect

Development workspace for a token-efficient Workday HCM Solution Architect skill.

## Objective

Translate business and workforce requirements into Workday solution options, configuration guidance, cross-functional impacts, risks, and implementation considerations while retrieving only the minimum documentation required for the question.

## Development status

**Phase 2 — HCM Capability Map: COMPLETE**

The frozen Phase 2 baseline consists of:

- `references/hcm-capability-router-v1.yaml` — compact business-to-capability and topic router
- `references/retrieval-policy-v1.yaml` — progressive retrieval, budget, expansion and stop rules
- `references/phase-2-routing-tests.md` — routing validation across representative HCM consulting scenarios
- `references/capability-map-validation.md` — guide completeness review and design decisions

Earlier capability-map drafts are retained as development history and are not the preferred runtime routing artifacts.

## Next phase

**Phase 3 — Cross-Module Dependency Graph**

Phase 3 will model material object and configuration dependencies across HCM domains so the future skill can perform controlled impact analysis without retrieving every potentially related module.

The production `SKILL.md` is intentionally not created yet. It will be written after the foundational routing, dependency and workforce-archetype layers are validated.

## Branch

Development for this skill is isolated on:

`feature/hcm-solution-architect`

Do not merge to `main` until the skill reaches an agreed release stage.

## Source policy

Workday documentation itself is not stored in this repository. Derived routing structures and original implementation guidance may be developed here, with Workday terminology and source-derived behavior kept distinct from our own recommendations and routing logic.
