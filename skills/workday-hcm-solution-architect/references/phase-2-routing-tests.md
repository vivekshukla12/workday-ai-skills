# Phase 2 Routing Validation

Status: **PASS — Phase 2 routing baseline accepted**

This validation checks whether the capability router selects the smallest useful set of HCM capabilities and documentation topics before detailed retrieval. It is a routing test, not a claim that every scenario can be fully designed without tenant-specific discovery.

## Acceptance criteria

A scenario passes when the router:

1. identifies the correct primary functional capability or capabilities;
2. avoids unrelated modules in the first retrieval pass;
3. activates experience channels only when user interaction matters;
4. activates Payroll, Integrations, Reporting, Security, or Business Process only when material;
5. points to specific documentation topics rather than broad guide sections; and
6. marks architecture-changing unknowns as assumptions or tenant validation instead of inventing facts.

## Test results

| # | Scenario | Mode | Expected first route | Key evidence topics | Result |
|---|---|---|---|---|---|
| 1 | Large blue-collar / factory population | Solution architecture | Staffing, Time Tracking, Scheduling, Compensation | Staffing touchpoints; Time Tracking eligibility; Scheduling; hourly compensation | PASS |
| 2 | High-volume seasonal hiring | Solution architecture | Recruiting + Staffing | Evergreen Requisitions; Autocomplete Staffing Events; Job Requisition for Multiple Existing Positions | PASS |
| 3 | Position Management vs Job Management | Design decision | Staffing | Staffing Model Comparisons; Staffing Models; Hiring Restrictions | PASS |
| 4 | Factory overtime and shift premiums | Solution architecture | Time Tracking + Compensation + Scheduling | Time Calculations; Standard Overtime; Shift Differential Calculations; Schedule settings | PASS |
| 5 | Multiple jobs affecting time, absence, benefits and payroll | Impact analysis | Staffing + Time Tracking + Absence | Impacts of Primary Position Designation; Impacts of Enabling Multiple Jobs | PASS |
| 6 | Germany population covered by collective agreements | Solution architecture | Staffing + Compensation + Absence; Localization conditional | Setup Considerations: Collective Agreements | PASS |
| 7 | Onboarding with mandatory training | Solution architecture | Onboarding + Learning | Onboarding Plans; Required Learning for You; Pre-Hire Access to Learning Content | PASS |
| 8 | Worker location change impact | Impact analysis | Staffing; expand selectively to Compensation, Time, Absence and Payroll | Setup Considerations: Job Changes; Staffing Connections and Touchpoints | PASS |
| 9 | External time clock feeding Workday | Architecture / integration boundary | Time Tracking + Integrations | Importing Time Clock Events; Time Clock Events | PASS |
| 10 | Workday calculated time sent to third-party payroll | Architecture / integration boundary | Time Tracking + Integrations + Payroll | Exporting Time Blocks; Get Calculated Time Blocks; Time/Payroll touchpoints | PASS |
| 11 | Frontline workers without regular desktop access | Solution architecture | Time Tracking + Self-Service; Scheduling conditional | Time Kiosk; mobile check-in; geofencing | PASS |
| 12 | Basic HCM headcount planning | Capability / architecture | Staffing + Reporting & Analytics | Headcount Plans; Headcount Plan Dimensions for HCM | PASS |

## Evidence-based observations used during testing

- Workday documents evergreen requisitions as supporting seasonal, high-volume, and hard-to-fill positions. Staffing autocomplete also explicitly identifies high-volume, retail, and seasonal hiring as use cases.
- The multiple-jobs material documents primary-position impacts across Absence, Time Tracking, Staffing, Talent, Compensation, Benefits, Payroll, and Reporting. This validates selective second-hop expansion rather than treating Multiple Jobs as a Staffing-only question.
- Collective Agreements can affect notice/probation periods, allowance and benefit eligibility, time-off and absence eligibility, weekly working hours, and minimum base pay. Country/location restrictions and eligibility rules are documented design considerations. The router therefore activates Localization only when the user's country context materially changes the question; it must not invent German legal rules.
- Required Learning can be surfaced in onboarding plans, and Learning documentation identifies required learning campaigns as an Onboarding touchpoint. This validates a two-capability route rather than retrieving the full Talent domain.
- Change Job covers location changes and supports related subprocesses. Staffing documentation also identifies downstream impacts on Compensation, Payroll, Absence, Recruiting, and Time Tracking. For an impact-analysis question, these become second-hop candidates rather than automatic first-pass retrieval.
- Workday Time Tracking supports third-party time collection through time clock event web services and can export calculated time blocks to third-party scheduling or payroll vendors. The router should start in Time Tracking and activate Integrations/Payroll only because an external-system boundary is explicit.
- For frontline access, Workday documents mobile check-in, geofencing, and Time Kiosk on shared tablets. This validates activating the Self-Service/experience layer only when access method is part of the business problem.

## Tuning performed after tests

The Phase 2 router was adjusted in these areas:

- added explicit Multiple Jobs impact retrieval topics;
- added Job Changes as the preferred entry point for location-change impact analysis;
- added third-party clock and third-party payroll retrieval topics under Time Tracking;
- added mobile / kiosk routing for frontline populations;
- added explicit collective-agreement routing without encoding country-specific legal assumptions;
- added headcount planning, HR Partner Hub, flexible work arrangements, worker communications, and retiree coverage under Staffing;
- separated functional capabilities from experience channels and cross-cutting domains;
- added specialist-source handoff rules for Payroll, Integrations, and Reporting & Analytics.

## Token-efficiency result

All scenarios can be routed with no documentation retrieval at classification time. Under the retrieval policy, narrow questions start with one capability and approximately 1–2 topics; design questions typically start with 1–2 capabilities; broad solution-architecture questions are capped at four primary capabilities before selective dependency expansion.

The test set did not reveal a case requiring unrestricted whole-guide retrieval.

## Phase 2 conclusion

The capability taxonomy, source-routing rules, retrieval budgets, and scenario routes are sufficient to proceed to the cross-module dependency graph. Future Phase 3 findings may refine individual touchpoints, but they do not block the Phase 2 baseline.
