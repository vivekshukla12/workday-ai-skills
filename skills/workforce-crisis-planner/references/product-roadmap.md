# Workforce Crisis Planner — enhancement roadmap

Status: Proposed enhancements recorded for future prioritization; not blanket approval to change the approved intake.
Reviewed baseline: workbook-field-definitions.md blob 8e15b90dc97f1c06291243389f5e1741eed3d662.
Scope: reusable framework only. Never store filled customer workbooks, run snapshots, approvals, or logs in this public repository.

## Delivery policy
Rebuild the current intake from approved definitions. Keep this backlog distinct from implemented features. If a calculation is unsafe or underspecified, disclose the limitation and leave its result agent-managed or unavailable instead of inventing a formula. No dates, owners, or implementation commitments are assigned by this roadmap.

## Priority and release sequence
- P0 / Before customer simulation: reconcile conflicting references, capacity arithmetic, assumption provenance, units and approvals.
- P1 / Controlled pilot: complete mapping, scenario-specific validation, financial and operational semantics, reproducible outputs.
- P2 / Application workflow: authenticated edit history, controlled integrations, repeatable refresh and production hardening.
All items below are Proposed. Acceptance evidence is required before marking Done.

| ID | Priority | Area | Enhancement | Acceptance evidence |
| --- | --- | --- | --- | --- |
| R01 | P0 | Skill routing | Make approved aggregate intake authoritative over the broad legacy catalogue; include strategic workforce transformations explicitly. | All references use the same default collection boundary. |
| R02 | P0 | Data minimization | Move worker-level fields, talent data, detailed absence, and individual dates to approved extensions, not default requests. | No standard intake field requires an individual record. |
| R03 | P1 | Source evidence | Add primary references and field-level extraction specifications with tenant verification. | Each source-backed mapping identifies its evidence and custom/standard status. |
| R04 | P0 | Privacy | Separate necessity from sensitivity and explain what cannot be calculated when optional sensitive values are omitted. | Each conditional/sensitive field has use condition and omission consequence. |
| R05 | P1 | Privacy | Assess small groups, rare combinations, totals, and differencing; five workers is not an anonymity guarantee. | Synthetic tests show suppression does not reveal hidden groups. |
| R06 | P1 | Privacy | Permit approved concentration flags where exact small counts are suppressed. | Suppression does not imply no risk or zero capacity. |
| R07 | P0 | Storage | Separate generic public skill content from controlled customer submissions and execution records. | Publication scan and runtime destination controls exclude customer data. |
| R08 | P1 | Start Here | Separate schema version, submission version, per-dataset as-of date and historical coverage. | Stale datasets are identifiable independently. |
| R09 | P1 | Start Here | Add scenario scope, exclusions, external research permission and indicative-run authorization; assess readiness per scenario. | Missing finance blocks only dependent outputs. |
| R10 | P0 | Workforce | Define filled FTE, snapshot versus period average and multiple-assignment counting. | Reconciled synthetic headcount/FTE with no duplicate assignments. |
| R11 | P0 | Capacity arithmetic | Do not subtract vacant FTE from filled-worker FTE; avoid overlapping loss deductions. | A filled population with vacancies retains correct available supply. |
| R12 | P1 | Workforce | Define leave snapshot versus period capacity loss; support vacancy-only groups and unknown types. | Leave and vacancies have consistent population/date rules. |
| R13 | P1 | Compensation | Specify annualized versus period pay, currency, and aggregation; do not multiply already aggregated pay by FTE. | Consistent cost comparisons across frequency and currency. |
| R14 | P1 | Stable IDs | Persist generated IDs across sorting and refresh. | Sort and reload do not change identity. |
| R15 | P1 | Service requirements | Define normal/reduced/emergency minimum service level and sustainable duration. | Minimum FTE has a declared service level and effective period. |
| R16 | P0 | Service requirements | Separate staffing and skill requirement tables or otherwise prevent repeated skill rows multiplying Minimum FTE. | Three credential requirements do not triple staffing demand. |
| R17 | P0 | Shared capacity | Keep Dedicated/Shared/Backup bands; ask targeted allocation/priority questions or show ranges when exact quantities are needed. | No arbitrary percentage conversion or duplicated shared capacity. |
| R18 | P1 | Off-site capacity | Define denominator, activation delay and enabling dependencies; do not add off-site capability as extra workforce. | Site disruption conserves total workforce capacity. |
| R19 | P0 | Skills | Distinguish qualified from available and unique people from overlapping skill counts. | Counts are not summed as unique workforce. |
| R20 | P1 | Skills | Support approved aggregate counts meeting combined credential requirements and expiry buckets when needed. | Intersections and time-dependent coverage are not fabricated. |
| R21 | P1 | Skills | Confirm backup designation source and count of credentials versus workers affected. | Data dictionary defines the counted object. |
| R22 | P0 | Finance | Define amount versus percentage, exact versus index/band, cost inclusion, currency and financial-unit mapping. | Incompatible measurement bases cannot be combined. |
| R23 | P1 | Finance | Separate transition costs from recurring cost and avoid artificial direct revenue attribution to support functions. | Relocation costing shows both cost types without duplicates. |
| R24 | P0 | Liquidity | Add approved net cash-flow inputs/assumptions or accept customer runway bands; cash balance alone is insufficient. | No runway without outflow evidence; balances are not summed over time. |
| R25 | P1 | Liquidity | Account for cash restrictions, transferability, drawability and minimum liquidity floor. | Entity liquidity is not assumed freely interchangeable. |
| R26 | P0 | Operations | Define labor/equipment/material constraints and aligned productivity denominator; do not assume proportional output loss. | Shared roles or machinery bottlenecks trigger explicit assumptions. |
| R27 | P1 | Dependencies | Define continuous impact bands, service-stopping flag, Unknown alternative, restored capacity and exposure type/currency/period. | Dependency estimates have clear semantics. |
| R28 | P0 | Dependencies | Prevent overlapping interrupted output or financial exposure from being added twice. | Combined disruption test avoids duplicate losses. |
| R29 | P1 | Requests | Allow minimal plain-language entry, linked Request IDs, explicit duration units, target baseline and future locations. | Relocation request works without fabricated current-site records. |
| R30 | P1 | Scenario generation | Prioritize evidence-based shortlist; distinguish observation/event/assumption/impact and prevention versus impact reduction. | No invented event probabilities; sensitive inputs requested only for selected scenarios. |
| R31 | P0 | Assumptions | Detect submission changes against accepted snapshot; a value difference cannot authenticate editor identity. | Changed or unchanged-confirmed assumptions retain accurate provenance. |
| R32 | P0 | Assumptions | Snapshot complete value, unit, scope, dates, source and approval per run; invalidate approval after material change. | Editing 20 days to 20 weeks triggers review despite same number. |
| R33 | P0 | Assumptions | Separate proposer from evidence source; treat approved scenario overrides distinctly from baseline facts. | Baseline 100 FTE and scenario 70 FTE coexist correctly. |
| R34 | P1 | Controls | Add scope type, version, unit/currency, time basis and tolerance type; reconcile suppressed data at safe level. | Controls compare like-for-like values without exposing suppressed rows. |
| R35 | P0 | Validation | Separate test result, severity and execution permission; Not Tested has scenario-dependent consequence. | Unrelated scenarios can proceed while unsupported outputs remain blocked. |
| R36 | P0 | Uploaded data | Treat cell text as untrusted data; flag suspicious instructions without executing or echoing sensitive content. | Injection-style synthetic notes cannot change workflow or exfiltrate data. |
| R37 | P1 | Outputs | Harmonize run, gap, mitigation, decision, milestone and comparison schemas with revised inputs. | Every result traces to run inputs and each timeline action to a decision. |
| R38 | P0 | Approvals | Separate simulation approval from implementation authority; require traceable role-based decisions. | Agent never approves its own mitigation or treats simulation as execution approval. |
| R39 | P1 | Timelines | Support backwards planning from transformation target dates plus forward crisis-trigger planning. | Dependencies and blocking conditions determine feasible dates. |
| R40 | P2 | Application | Add authenticated edit logs, version storage, access controls, source refresh and automated revalidation. | Real platform controls replace spreadsheet-only audit claims. |

## Verification plan
Use synthetic data only. Cover multiple entities/locations, vacancies, leave, shared and backup roles, overlapping credentials, combined disruptions, privacy suppression, absent financial values, incompatible units, relocation, assumption edits, reverted edits, and rejected assumptions. Verify formula results, dropdowns, field help, safe defaults, protected metadata, exports, and run reproducibility.

## Current deliverable boundary
The approved-schema workbook is an intake and planning interface, not a self-contained simulation engine. Agent-assessed outputs, stable IDs, validation, timestamps, provenance and run snapshots need an executing agent or application. Sheet protection is an accidental-edit guard only. This roadmap does not claim those application features are implemented.
