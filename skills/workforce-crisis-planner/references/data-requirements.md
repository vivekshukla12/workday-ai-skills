# Data requirements for the simplified workbook

Use [workbook-field-definitions.md](workbook-field-definitions.md) as the field-level authority. Request only the sheets and fields needed for the selected scope. This reference explains collection, not a second mandatory catalogue.

## Minimum first submission

Start with Start Here and aggregate WD Workforce. Add Service Requirements to evaluate service staffing gaps. Recommend independent headcount and FTE controls in Control Totals. Missing optional domains limit the corresponding conclusions; they do not block unrelated analysis.

| Workbook sheet | Source and use |
| --- | --- |
| Start Here | Neutral assessment ID, version, as-of date, horizon, units and approval statuses. |
| WD Workforce | Workday aggregates by period, entity where relevant, location, role and Worker Type. Headcount and filled FTE; leave and vacancies only when reliable and relevant. Base pay is optional sensitive. |
| Service Requirements | Customer-defined service minima, verified skill requirements and Dedicated/Shared/Backup bands. Off-site capacity is customer input, optionally from a verified custom Workday calculation. |
| WD Skills & Credentials | Conditional aggregate verified critical skills and mandatory credentials. No self-assessment, worker identities or personnel notes. |
| Financial Performance | Conditional finance-system inputs, kept separate from workforce extracts even when sourced from Workday Financial Management. Exact financial amounts are optional sensitive. |
| Liquidity | Only for in-scope liquidity analysis with appropriate approvals. Exact values are optional sensitive. |
| Operational Capacity | Conditional matching-period capacity, demand and output in declared units. |
| Critical Dependencies | Conditional neutral dependency codes, impact bands, alternatives and switch times. Exact exposure is optional sensitive. |
| Requested Scenarios | Optional plain-language customer requests, including relocation. Most proposals should come from the agent. |
| Scenario Assumptions | Shared assumptions with original and editable current values, provenance and explicit approval for use. |
| Control Totals | Selected independent source totals at matching scope, date, unit and version. Exact finance totals remain optional sensitive. |

AI Scenario Register, Validation Results, Simulation Runs and the four Plan Library sections are managed by the agent, with explicit customer decisions. Do not ask customers to fill technical validation outputs.

## Source contract without extra customer columns

The agent records a compact private submission note containing each supplied dataset's version, date basis, units, population, role/location mappings, counting rule, source owner role and limitations. Reference this note in Simulation Runs or the private run snapshot. Do not repeat metadata in every row or invent a Data Catalogue or Sources tab.

Confirm:
- FTE means filled capacity; vacancy is separate. Establish whether reported leave is included in FTE.
- Point-in-time snapshots are not monthly averages. Do not sum headcount or FTE across snapshot dates.
- Headcount counting rules address multiple assignments. Do not claim distinct people by adding overlapping populations.
- Role and location crosswalks use neutral stable codes. No unmatched mapping may silently become zero.
- Financial quantities have currency, period and amount/rate/index/band basis. Base pay has a known pay frequency if used.
- Percent inputs use the template's stated convention; absent a statement, confirm whether 30 means 30% or whether 0.30 means 30%. Normalize once and record the convention.

## Privacy and conditional collection

Use aggregate non-identifying data by default. Keep small-group suppression and controls against re-identification through comparisons consistent across inputs and outputs. Confirm the customer's threshold; a generic threshold is not proof of anonymity. Suppressed values remain unknown.

Do not request worker keys, leave reasons, individual dates, protected characteristics, salary records, performance ratings, customer/supplier names, contracts, tenant URLs or access details for the portable pilot.

If the scope needs more than the approved fields, first explain the missing decision evidence and seek an aggregate or assumption-based alternative. Any additional sensitive collection needs an explicit purpose and authorization. Declining optional sensitive data is allowed; mark the affected metric unavailable or indicative instead of inventing an amount.

## Validation

Test aggregate-key uniqueness, required-field completeness within scope, date and unit validity, approved mappings, source versions and reconciliation. Keep unknown, zero and not applicable distinct. Record evidence and outcome in Validation Results; record unexecuted checks as Not Tested. Read [analysis-method.md](analysis-method.md) for metric-specific prerequisites and scoped failure handling.
