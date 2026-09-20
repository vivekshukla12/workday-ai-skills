# Workforce and financial gap analysis

These are calculation rules for the portable skill, not claims that the workbook contains a simulation engine. Use reproducible arithmetic in available calculation tools and retain formulas, inputs and units with the private run. Do not claim a check ran without execution evidence.

## Establish the baseline

Read the approved field definitions. State scope, time basis, units and source versions. Workforce starts at period/entity/location/role/Worker Type grain; service requirements are a separate customer source. Do not assume service-level allocation exists in Workday.

Aggregate only disjoint populations at compatible grain. Validate join cardinality and unmatched codes before calculations. A workforce total repeated across several services is not additive. Repeated service/role staffing minima on skill rows count once when identical; conflicting minima require resolution.

## Capacity

Let F be filled FTE and L be FTE on Leave included in F, for the same population and date.
- Baseline available FTE B = F - L.
- If F already excludes leave, B = F; do not subtract leave again. Explain the source basis and leave-field treatment.
- If leave is missing and material, B is unknown unless an explicit assumption is approved for the intended run. Missing leave is not automatically zero.
- Vacant FTE is a separate unfilled-capacity measure. Never subtract it from filled FTE.
- Subtract any other known unavailability only once and only when its population is included in B.

For an additional availability shock with approved loss fraction s, scenario available FTE A = B × (1 - s), where 0 <= s <= 1. The loss is incremental to the baseline and must not reapply leave or a loss already counted. Apply sequential/combined shocks only with an explicit overlap rule; otherwise show separate cases.

For complete site unavailability, let O be confirmed deployable off-site FTE within B. Then A = O, with 0 <= O <= B. O is not added to B. A percentage requires an explicit denominator and timing; convert it before applying this rule. Capability must be usable for the relevant service, duration and dependencies. Missing O yields an unresolved capacity result or an authorized sensitivity range, not zero.

Dedicated/Shared/Backup bands do not quantify service allocations. For shared pools, report pool-level exposure and conditional service exposure; do not claim simultaneous service coverage without a feasible allocation. Additional staffing requires known availability and lead time and must not be taken from another service without recording its loss there.

## Requirements and gaps

Use approved minimum staffing for the role/service/scope and its sustainable duration. Minimum staffing is a continuity floor, not necessarily staffing required for full expected demand.
- Signed capacity gap = A - R, where R is the compatible approved requirement.
- Shortfall = max(R - A, 0).
- Surplus = max(A - R, 0).
- Coverage = A / R only when R > 0. For zero requirement, report coverage as Not applicable and keep the absolute comparison.
- Shortfall percentage = shortfall / R only when R > 0.

Show signed-gap convention and unit explicitly. Preserve fractional FTE. Do not translate FTE into people without a justified conversion.

Required capacity may alternatively be demand / validated output per FTE for compatible periods, output mix and allocation. Historical productivity is an assumption for future output, not proof of a linear relationship. Without operations evidence, report workforce gaps only; do not infer production or revenue loss directly from FTE loss.

## Qualifications and dependencies

Qualified-headcount coverage = available, valid qualified heads / required qualified heads when the denominator is positive. If only qualification counts exist, report qualification coverage and mark availability unresolved. Do not scale skill counts by a workforce loss rate unless explicitly approved as an assumption. Do not add skill counts as distinct people or infer joint-credential coverage, distinct backups or shift coverage from independent totals.

Location concentration uses a consistent disjoint population and denominator. Dependency impact bands remain qualitative. If mapping percentages to the approved bands, interpret boundaries continuously: Low <20%, Moderate 20% to <50%, High 50% to <80%, Critical 80% to 100% or service cannot operate. Never replace a band by its midpoint or add overlapping dependency exposures.

## Financial effects only when supported

Use matching currencies, periods and version bases. Obtain an approved conversion rate and date if conversion is necessary. Never combine indices or bands with exact amounts.

- Scenario labor cost = baseline finance-defined labor cost + incremental costs - evidenced avoidable savings. Ensure components do not overlap. Base pay alone is not total labor cost, and unavailable FTE does not automatically reduce payroll.
- Revenue at risk = unserved volume × revenue per unit, only when sales linkage and timing are supported.
- Contribution at risk = unserved volume × contribution per unit, with an explicit margin definition. A margin rate first needs a revenue basis. Revenue and contribution losses are alternative views, not additive losses.
- Keep penalties, transition costs and cash timing separate. Do not double-count labor within contribution loss.
- Simple cash runway = usable liquidity above the approved minimum buffer / positive net cash outflow per period, only under an explicitly stated constant-outflow assumption. Include committed facilities only if accessible in the relevant horizon and exclude restrictions/double counting. If already below the buffer, report the breach; zero or negative outflow does not imply infinite safety. Missing outflow means runway unavailable. Use a period cash schedule for variable flows.

Affordability conclusions require financial evidence; workforce-only scenarios can proceed without them.

## Evidence and run gates

| Condition | Treatment |
| --- | --- |
| Missing optional finance or dependency data outside scope | Omit that metric; disclose limitation; continue unrelated workforce analysis. |
| Missing independent control | Mark reconciliation Not Tested; explain scope of uncertainty. Do not invent Pass. |
| Proposed assumption authorized as Indicative Only | Use only in a clearly labelled indicative run. |
| Required value missing or suppressed | Ask for evidence or propose an explicit assumption/range; no silent zero. |
| Impossible values, conflicting duplicate keys or incompatible units | Block affected calculations until corrected; approval cannot make invalid arithmetic valid. |
| Required scenario or assumption approval absent | Block final conclusions; an indicative run also requires explicit authorization. |
| Unresolved shared allocation | Report pool-level results; withhold unsupported per-service totals. |

Missing data cannot be worked around by excluding a required input and presenting the result as complete. Classify readiness per scenario and affected metric; unrelated valid scope may continue. User-approved tolerance or modelling assumptions must remain explicit and cannot override privacy or required authorization.

## Results and uncertainty

Record each gap with Scenario ID and Run ID in Plan Library. Keep confidence separate from severity. Do not invent crisis probabilities or universal risk weights. Disclose AI-origin assumptions, indicative-only assumptions, excluded assumptions and unavailable metrics. If a key estimate is uncertain, compare approved lower/upper cases and explain what changes. Define model version as skill version plus any run-specific calculation overrides.

Read [scenario-governance.md](scenario-governance.md) before reruns, approvals or timelines.
