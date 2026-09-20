# Scenario library and approval governance

## Use the approved workbook

Preserve stable Scenario, Assumption, Run, Gap, Mitigation, Decision and Milestone IDs. The links are Scenario -> Run -> Gap -> Mitigation -> Decision -> Milestone. Retain prior runs; new runs do not overwrite historical findings.

Most scenarios are agent proposals derived from validated evidence. Requested Scenarios is optional and accepts plain-language disruptions and strategic changes such as relocation, expansion, consolidation or outsourcing. Proposals are not predictions. Use Workforce Availability rather than People and Health as a category; other categories may cover operations, technology, supply chain, market demand, natural hazards and combined crises.

Record proposals in AI Scenario Register with origin, rationale, neutral scope, confidence, sensitivity and version. Customer review is required before detailed simulation. Approved scenarios may support final analysis; explicitly authorized indicative runs may evaluate proposals with limitations.

## Assumptions and reruns

Use the single Scenario Assumptions sheet. Customers edit Current Value in place. Preserve Original Value and Original Origin. Prefer validated data for the baseline and explicit customer assumptions for hypothetical changes. An assumption changes a scenario, never silently rewrites a source fact.

Current Value Owner reflects confirmed provenance. A difference between values cannot authenticate an editor; confirm edits on resubmission or use available workflow evidence. Customer confirmation of an unchanged AI estimate does not turn it into observed data: retain its AI origin and basis.

For each run, save the submitted workbook and complete assumption snapshot in approved private storage. Record references in Simulation Runs. Snapshot values, units, scope, timing, origin, basis, approval and scenario version, plus dataset versions and calculation/model version. Do not invent storage locations or audit evidence. If durable storage is unavailable, return the snapshot to the user for retention and state the limitation.

Any changed value, unit, scope, timing or material basis invalidates prior approval for that changed assumption until reviewed. Do not overwrite the user's current row or require a replacement row. Retain old run snapshots; increment the scenario version for material approved changes.

Final runs use Approved assumptions only. Indicative Only assumptions require an indicative run. Not Approved assumptions cannot drive calculations. If excluding an assumption removes a necessary input, the affected result is unavailable. Report all AI-origin assumptions actually used, including customer-confirmed estimates, and what evidence would replace them.

## Mitigation and decision discussion

Plan Library has four sections: Workforce Gaps, Mitigation Options, Decisions and Timeline. Use their existing fields. Supporting evidence may be a neutral reference to a private note, not a new mandatory column.

For each scenario, explain the gap, evidence, alternatives, expected benefit, cost limitations, lead time, dependencies, consultation needs, people impact, reversibility and residual risk. Use accountable roles rather than personal identities.

Ask for an explicit decision for each option: Approved, Approved with conditions, Rejected, Deferred or More analysis required. Record authority role, date, rationale, conditions, review date and private evidence reference. Never infer approval from silence or interest.

Scenario approval authorizes simulation only. Mitigation approval records the chosen plan; actual business execution has separate authorization and applicable reviews. Changed inputs or findings require reassessment of affected decisions; keep prior records and mark them stale in the run note until reviewed.

## Timelines

Only approved or conditionally approved options enter an implementation timeline. Keep execution-blocking conditions visible.

Ask only for missing scheduling inputs: trigger/target date, lead times, durations, calendar basis, owner roles and predecessors. Without confirmed dates, use relative timing; without durations, mark them unknown rather than invent commitments. For finish-to-start tasks, earliest start is the later of the agreed trigger/availability date and all predecessor finishes, using the agreed calendar. Flag cycles and impossible target dates. Do not treat elapsed days as working days.

## Exercise mode and private records

At the start, distinguish a demo exercise from live customer planning. Confirm that any supplied tenant data is permitted for this workflow; demo tenant access does not establish export permission. Use aggregates and neutral codes.

Label exercise decisions, plans and output summaries as exercises. Keep all exercise/customer inputs, snapshots, findings and results outside the public skill repository. Running this skill grants no permission to write to GitHub. Do not send tenant details to public search queries or repository issues. Propose generic improvements separately for review, without copying test records.

## Fresh-chat pilot

Read [pilot-workflow.md](pilot-workflow.md) for the first customer-style test and acceptance criteria.
