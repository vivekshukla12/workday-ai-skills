# HCM Capability Map Validation

**Phase:** 2F — Validate completeness against the HCM guide  
**Branch:** `feature/hcm-solution-architect`  
**Status:** Complete  
**Validated artifact:** `references/hcm-capability-map.yaml` v0.1

## Objective

Validate that the capability map covers the major HCM functional areas in the supplied Workday HCM administration guide without turning the map into a copy of the documentation. The map must remain a compact routing layer that helps an AI determine which capabilities and documentation topics are materially relevant to a consulting question.

## Validation method

The validation used the guide table of contents plus targeted review of setup-consideration, touchpoint, security, reporting, integration, and cross-product sections. Particular attention was given to areas that are easy to miss when routing by module name alone, including staffing subdomains, worker experience, onboarding, workforce metrics, HCM hubs, and Innovation Services.

## Result

The v0.1 taxonomy covers the major HCM guide areas and does not require a new top-level functional capability solely for every documentation chapter. The current broad routing model remains appropriate, but several subdomains and routing rules need to be added before the map is frozen.

## Required amendments

### 1. Expand STAFFING rather than create additional primary nodes

Add these documented subdomains under `STAFFING`:

- International and Domestic Assignments
- Flexible Work Arrangements
- HCM Headcount Plans
- HR Partner Hub
- Ad Hoc Worker Communications
- Retirees

Add corresponding routing cues and narrow retrieval topics. HCM Headcount Plans should remain under Staffing for routing purposes; advanced enterprise planning requirements can later route to Adaptive Planning documentation when appropriate.

### 2. Expand ONBOARDING to cover both onboarding experiences

The guide contains onboarding content in both Recruiting and Staffing contexts. Add:

- Staffing onboarding
- Onboarding Dashboard and Landing Page
- Form I-9
- Background Checks

The router should distinguish onboarding experience/content questions from onboarding compliance and staffing-lifecycle questions.

### 3. Expand TALENT and REPORTING coverage

Add these areas to the Talent routing domain:

- Mentors and Connections
- Talent Matrix Reports
- Workforce Metrics
- Talent Insight Apps
- Professional Profiles

`Workforce Metrics` should also activate the cross-cutting `REPORTING_ANALYTICS` capability when analytics design or reporting architecture is material.

### 4. Treat HCM hubs and conversational channels as an experience layer

`SELF_SERVICE` and `HR_SERVICE` should not behave like ordinary functional modules. They should form an experience/channel layer used only when the question involves user interaction, hubs, mobile access, collaboration tools, HR service delivery, or case/knowledge management.

Recommended logical layers:

- Functional capabilities: Worker Data, Localization, Recruiting, Staffing, Onboarding, Compensation, Benefits, Talent, Skills, Learning, Scheduling, Absence, Time Tracking, Safety
- Experience channels: Self-Service/Hubs, Assistant/Everywhere/Help
- Cross-cutting architecture: Security, Business Process, Reporting & Analytics, Integrations, Payroll

This prevents the router from retrieving hub or Assistant documentation simply because those experiences can expose an underlying HCM function.

### 5. Expand WORKER_DATA worker-experience coverage

Add worker-profile topics that appear in the Worker Information section:

- Skills and Experience
- Competencies
- Certifications
- Job History
- Talent Statements

These should create touchpoints to Skills, Talent, and Learning rather than duplicate their detailed configuration knowledge.

### 6. Expand BENEFITS long-tail routing without creating extra modules

Add routing coverage for:

- Dependents and Beneficiaries
- Wellness
- Regulatory benefit topics such as ACA and COBRA

These remain within `BENEFITS`; country-specific or statutory questions may also activate Localization and Payroll.

### 7. Expand LEARNING for external learning populations and integrations

Add:

- Extended Enterprise Learning
- Cloud Connect for Learning

This enables direct routing for external learners and learning-provider integration questions without widening every Learning request into an Integrations search.

### 8. Strengthen source-authority routing

Cross-cutting capabilities should explicitly prefer their dedicated guides where available:

- Payroll → Payroll Admin Guide
- Integrations → Integrations Admin Guide
- Reporting & Analytics → Reporting and Analytics Admin Guide

The HCM guide remains a secondary source for functional touchpoints and HCM-specific implications.

## Decisions: no new primary capability

The following were reviewed but should **not** become independent top-level routing capabilities in this phase:

- HCM Headcount Plans — route through Staffing; escalate to Adaptive Planning only when required.
- HR Partner Hub — experience surface backed primarily by Staffing data.
- Professional Profiles — route through Talent/Skills/Worker Data depending on the question.
- Workforce Metrics — route through Talent plus Reporting & Analytics when analytics is material.
- Workday Assistant / Workday Everywhere — experience channels, not functional HCM modules.

This keeps the capability map compact and avoids unnecessary retrieval fan-out.

## Phase 2F conclusion

**2F is complete.** The v0.1 taxonomy is structurally sound, with the amendments above required for v0.2. No production `SKILL.md` should be created yet.

## Next step

**Phase 2G — Token-efficiency optimization.**

Apply the validated amendments and define retrieval budgets, routing thresholds, second-hop dependency rules, stop conditions, and narrow-query patterns. Then run scenario tests before freezing Phase 2 v1.
