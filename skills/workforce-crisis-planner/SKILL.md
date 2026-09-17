---
name: workforce-crisis-planner
description: Analyze workforce, financial, operational, and external-indicator data to identify crisis exposure; develop scenario-specific mitigations; record accountable approvals; and create implementation timelines. Use for workforce resilience, business-continuity workforce planning, crisis workforce gap analysis, or maintaining a structured crisis-plan register. Do not use for automated individual employment decisions.
---

# Workforce Crisis Planner

Build an evidence-based workforce resilience assessment that links workforce supply, critical service demand, financial capacity, crisis assumptions, approved mitigations, and implementation milestones.

## Non-negotiable controls

- Treat recommendations as decision support. Never make or recommend fully automated hiring, termination, promotion, absence, health, disciplinary, or other individual employment decisions.
- Analyze roles, skills, services, locations, and aggregated populations before individuals. Use pseudonymous worker keys only when authorized linkage is necessary.
- Never place credentials, tokens, tenant names or URLs, customer identifiers, employee names, contact details, raw health data, protected characteristics, free-text personnel notes, or confidential source extracts in this skill or a public repository.
- Before exporting or publishing any reusable artifact, scan file names, metadata, formulas, links, comments, notes, sample rows, and embedded objects for sensitive or tenant-specific content. Stop and ask the user if safe sanitization would remove information needed for the requested result.
- Separate source facts, assumptions, calculations, recommendations, decisions, and milestones. Preserve source observations and version history.
- Treat legal, privacy, employee relations, works council, health and safety, regulatory, and finance reviews as approval gates where applicable.
- Do not label a mitigation approved until the user or named decision authority explicitly approves it. Record the authority, date, conditions, required reviews, review date, and evidence link.
- State uncertainty and data limitations. Do not fabricate missing figures, Workday objects, report fields, crisis probabilities, thresholds, costs, or dates.

## Operating workflow

Maintain a visible phase status and resume from the last completed phase.

1. **Scope.** Confirm company or planning-unit scope, legal entities, regions, critical services, planning horizon, reporting date, base currency, workforce populations, decision owners, output location, and confidentiality level. Ask only for items that materially change the analysis.
2. **Define workforce data.** Read [data-requirements.md](references/data-requirements.md). Produce a field-level catalogue with business definition, grain, effective-date rule, source, join key, refresh frequency, owner, sensitivity, permitted use, retention, and quality control. Distinguish required, conditional, and optional items.
3. **Define financial and operational data.** Use the same reference. Include the minimum financial and operational evidence needed to translate workforce gaps into service, margin, cost, and cash exposure. Reconcile Workday and external-system dimensions through governed mapping tables; never join on display labels when stable IDs exist.
4. **Acquire and validate.** Request only approved extracts. Record source version and as-of date. Test completeness, uniqueness, validity, reconciliation, timeliness, privacy, and referential integrity before analysis. Do not infer a healthy baseline from incomplete data.
5. **Analyze gaps.** Read [analysis-method.md](references/analysis-method.md). Establish the baseline at the lowest reliable planning grain, normally period by entity, service, location, and role or skill. Calculate scenario-adjusted capacity and financial exposure, identify single points of failure and missing evidence, and keep data confidence separate from risk severity.
6. **Build the scenario library.** Read [scenario-governance.md](references/scenario-governance.md). Copy [workforce-crisis-planning-template.xlsx](assets/workforce-crisis-planning-template.xlsx) for a new engagement; do not edit the master asset. Register company-relevant scenarios with stable IDs, versions, evidence, assumptions, triggers, impacts, owners, confidentiality, and review dates. Include combined scenarios when dependencies can cascade.
7. **Develop mitigation options.** For each material gap, generate prevention, preparation, detection, response, recovery, and adaptation options as relevant. Record protected service, affected workforce, expected benefit, one-time and recurring cost, cash timing, lead time, dependencies, people impact, consultation needs, reversibility, residual risk, owner, and evidence.
8. **Discuss and decide.** Review one scenario at a time with the user. Confirm the definition, assumptions, baseline controls, gaps, options, costs, dependencies, workforce impact, and residual risk. Record each option as Approved, Approved with conditions, Rejected, Deferred, or More analysis required. Preserve dissent and conditions; never silently convert a proposal into a decision.
9. **Build the timeline.** Create milestones only for approved or conditionally approved mitigations. Start with time relative to trigger `T`, then assign calendar dates from user inputs after activation or approval. Each milestone requires an owner, predecessor review, deliverable, status, evidence, blocker, and next update.
10. **Learn and refresh.** Compare exercises or events with assumptions, capture lessons, expire stale approvals, version changed records rather than deleting them, and agree refresh cadence.

## Workbook rules

- Read [workbook-field-definitions.md](references/workbook-field-definitions.md) when creating, explaining, or revising the customer intake workbook. Treat its approved sheet and field decisions as the default schema, and record later walkthrough decisions there before changing the template.
- Use the supplied template as the default structured library. Preserve its stable Scenario, Gap, Mitigation, Decision, and Milestone IDs and linked table structure.
- Populate the Data Catalogue before loading observations. Keep Actual, Budget, Forecast, and Scenario versions distinct.
- Use formulas for transparent derived metrics and preserve editable assumptions as inputs. Reconcile headcount, FTE, labor cost, revenue, and cash to named controls.
- Keep example rows visibly marked and never present them as company findings.
- When creating or editing `.xlsx`, use the available spreadsheet-authoring workflow and visually verify every changed sheet.
- If the user chooses a different system of record, preserve the logical schema from [scenario-governance.md](references/scenario-governance.md).

## Source discipline

Read [source-basis.md](references/source-basis.md) when selecting sources or explaining why a field, control, or workflow is included. Prefer current company-controlled Workday documentation, company policies, continuity standards, and authoritative public guidance. Cite sources beside hardcoded inputs or in the workbook Sources sheet. Treat documentation as a capability reference, not proof that a tenant has enabled or populated a feature.

## Prism architecture references

For a proposed Prism data layer supporting crisis simulation, use these downloadable design references:

- [Prism architecture workbook](assets/prism-crisis-simulation-architecture.xlsx): logical datasets, approved workbook mappings, run metadata, controls, and implementation checklist.
- [Prism architecture guide](references/prism-crisis-simulation-architecture.docx): platform responsibilities, data preparation, assumptions and reruns, security, reporting, and implementation guidance.

These references describe a proposed architecture, not a deployed integration or executable simulation. Validate tenant capabilities and security before implementation. The approved workbook field definitions remain authoritative for customer intake; preserve their privacy and optional-sensitive-data rules. Keep customer-filled copies outside the public repository.

## Completion standard

A phase is complete only when its required evidence, owner, version, and limitations are recorded. The overall plan is complete when material scenarios link to validated gaps, each proposed mitigation has an accountable decision, approved actions have an owned dependency-aware timeline, and unresolved data or governance blockers remain visible.
