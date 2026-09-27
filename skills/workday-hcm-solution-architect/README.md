# Workday HCM Solution Architect

Development workspace for a token-efficient Workday HCM Solution Architect skill.

## Objective

Translate business and workforce requirements into Workday solution options, configuration guidance, cross-functional impacts, risks, and implementation considerations while retrieving only the minimum documentation required for the question.

## Current development phase

**Phase 2 — HCM Capability Map**

Current work covers:

- HCM capability taxonomy
- business-to-capability routing
- cross-cutting domains such as Security, Business Process, Reporting, Integrations, and Payroll
- targeted documentation retrieval topics
- token-efficiency rules
- validation against realistic HCM consulting scenarios

The production `SKILL.md` has intentionally not been created yet. It will be designed after the capability map and routing model are validated.

## Branch

Development for this skill is isolated on:

`feature/hcm-solution-architect`

Do not merge to `main` until the skill reaches an agreed release stage.

## Source policy

Workday documentation itself is not stored in this repository. Derived routing structures and original implementation guidance may be developed here, with Workday terminology and source-derived behavior kept distinct from our own recommendations and routing logic.
