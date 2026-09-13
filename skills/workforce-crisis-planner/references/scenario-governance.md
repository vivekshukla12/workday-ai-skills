# Scenario library and approval governance

## Relational records

Use stable IDs and versioned records. Relationships are `Scenario -> Gap -> Mitigation -> Decision -> Milestone`.

One scenario can have several gaps; one gap several mitigation options; one mitigation several review decisions over time; and one approved mitigation several milestones. Do not duplicate the scenario narrative in downstream tables.

## Scenario record

Record identity and version; title and category; status and owner; confidentiality; event and causal chain; scope and exclusions; horizon, onset, duration, and recovery pattern; evidence, observation date, rationale, confidence, and last review; workforce, productivity, demand, price, cost, cash, FX, supplier, facility, and technology assumptions; leading indicators, thresholds, source, frequency, trigger owner, and activation level; affected services, roles, skills, locations, customers, suppliers, legal duties, statements, and cash; decision authority, consultation requirements, approval state, conditions, expiry, next review, and evidence links.

Starter categories: people and health; economic and market; operational; technology and cyber; supply chain; climate and natural hazard; legal and regulatory; security and geopolitical; reputation and conduct; combined crisis.

## Mitigation record

Classify options as Prevent, Prepare, Detect, Respond, Recover, or Adapt. Link each option to a scenario and gap. Record protected service, affected workforce, expected benefit, cost and cash timing, lead time, dependencies, legal or consultation review, people impact, reversibility, residual risk, proposed owner, evidence, and proposal status.

## Decision discussion

Review one scenario at a time:

1. Confirm definition, evidence, assumptions, horizon, and trigger.
2. Review baseline controls, missing data, and confidence.
3. Validate services, minimum levels, role and skill gaps, people risks, and financial exposure.
4. Compare options, dependencies, lead times, cash needs, legal constraints, and residual risk.
5. Ask the user or named authority for an explicit decision for each option.
6. Record Approved, Approved with conditions, Rejected, Deferred, or More analysis required, plus rationale, dissent, authority, required reviews, effective date, expiry, review date, cost, evidence, and record owner.

Never infer approval from silence, positive sentiment, workshop attendance, or selection for further analysis.

## Timeline

Use relative time first: before trigger, detection, immediate response, stabilization, continuity, recovery, and adaptation. Add calendar dates only from the user's trigger or approved target dates. Record milestone ID, scenario ID, mitigation ID, phase, milestone, owner, predecessor, relative start and finish, planned start and finish, status, percent complete, deliverable or evidence, blocker, next update, and last-updated date.

Every scheduled milestone must trace to an approved or conditionally approved mitigation. Conditions that block execution must remain visible.
