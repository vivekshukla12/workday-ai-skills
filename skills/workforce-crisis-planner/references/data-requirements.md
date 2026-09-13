# Data requirements

Tailor this catalogue to the company's industry, operating model, jurisdictions, configured Workday products, and lawful purpose. Do not claim that a field exists in a tenant until verified.

## Workforce data

| Domain | Typical items | Primary use |
| --- | --- | --- |
| Organization and assignment | Pseudonymous worker key, worker type, active status, company, supervisory organization, cost center, location, country, time zone, job profile, position, management level, FTE, scheduled hours, start and expected end dates | Scope, capacity, location, and cost allocation |
| Criticality and demand | Critical role, critical service or process, minimum staffing, demand units, coverage hours, shift, on-call need, service priority, recovery objective | Required capacity and service continuity |
| Skills and credentials | Skill, proficiency, certification or licence, expiry, language, lawful clearance, successor or backup role | Skill coverage, expiry risk, and single points of failure |
| Compensation and labor cost | Base pay, pay frequency, plan, allowances, bonus target, employer taxes and benefits, overtime rules, currency, costing allocation | Baseline labor cost and option cost |
| Time, absence, and availability | Schedule, actual hours where permitted, overtime, leave category, absence dates and duration, return status, work arrangement, remote eligibility | Deployable capacity and absence sensitivity |
| Talent flow | Open positions, requisition status, vacancy age, candidate stage, time to fill, hire, transfer, exit, and retirement dates | Replacement and redeployment lead time |
| Succession and continuity | Aggregated talent categories where lawful, successor coverage, readiness, backup coverage | Continuity options; never automated individual decisions |
| Contractual constraints | Work authorization expiry, contractual hours, collective agreement, notice period, mobility preference, accommodation category only where lawful and necessary | Feasible scheduling, transfer, and consultation actions |
| History | Periodic headcount, FTE, hires, exits, absence, overtime, vacancies, payroll cost, and organization history | Baselines, seasonality, and assumption calibration |

## Financial, operational, and external data

| Domain | Typical items | Primary use |
| --- | --- | --- |
| Profit and loss | Revenue, gross margin, operating expense, labor and contractor cost, overtime, restructuring cost, insurance recovery | Affordability and profit impact |
| Cash and liquidity | Opening cash, operating cash flow, committed facilities, covenant headroom, payroll dates, payment terms, receivables aging, expected collections | Runway and response timing |
| Balance sheet | Working capital, inventory, debt, leases, provisions, assets, and currency exposure | Resilience and asset exposure |
| Budget and forecast | Approved budget, latest forecast, workforce plan, revenue drivers, volume, price, productivity, scenario version | Plan-versus-actual and alternative cases |
| Customers and commitments | Customer or segment, contract, service obligation, backlog, recurring revenue, concentration, penalty, renewal, geography | Revenue at risk and service priority |
| Suppliers and third parties | Supplier or category, spend, critical service, substitute, lead time, geography, financial health, contract and service level | Interruption and substitution time |
| Operations and capacity | Site, process, product or service, capacity, throughput, utilization, downtime, inventory days, recovery objective, quality metric | Translate workforce gaps into service effects |
| External indicators | Inflation, rates, FX, unemployment, health alerts, weather, energy, sanctions, transport, cyber indicators | Scenario triggers and calibration |

## Required catalogue metadata

For every data item record: ID, domain, business definition, source system, source object or report, grain, effective-date rule, required status, owner, refresh frequency, stable join key, permitted use, sensitivity, retention rule, quality control, status, source version, and notes.

Use shared governed dimensions for Period, Legal Entity, Business Unit, Cost Center, Location, Service, Job Profile or Role, Worker Type, Currency, Scenario, and Version. Maintain crosswalks between Workday and external codes.

## Minimum controls

- **Completeness:** profile missing required fields by business unit and location.
- **Uniqueness:** test the declared grain and flag duplicate worker-period, position-period, ledger-period, and scenario IDs.
- **Validity:** validate dates, currency, hours, FTE, pay frequency, status, and controlled categories.
- **Reconciliation:** tie headcount and FTE to approved Workday controls; tie payroll and financial amounts to ledger or forecast controls.
- **Timeliness:** compare refresh age with decision frequency and visibly mark stale data.
- **Privacy and access:** enforce minimum necessity, role-based access, retention, pseudonymization, lawful basis, and human review.
- **Versioning:** timestamp or version extracts, assumptions, analyses, recommendations, decisions, and approvals.
