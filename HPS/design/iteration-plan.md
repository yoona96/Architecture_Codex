# Hotel Pricing System - Iteration Plan

Prepared 2026-10-18. This is a design sequence, not an implementation staffing commitment. Each iteration updates architecture.md and records decisions and coverage separately.

## Iteration Plan Overview

| Iteration | Goal | Drivers |
|---|---|---|
| 1 | Establish whole-system structure and authorized hotel-to-price workflow | HPS-1/2/3/4; QA-5; CON-1/2/4/6; CRN-1/2/3/4 |
| 2 | Deterministic pricing, atomic publication and recoverable configuration activation | HPS-2/3/4/5; QA-1/2; CRN-4 |
| 3 | Recoverable REST delivery and complete publication accounting | HPS-2; QA-2/8; CON-5; CRN-4 |
| 4 | Query availability, scalability and complete authorization | HPS-1/3/6; QA-3/4/5; CON-2/6 |
| 5 | Protocol extension, isolated testing, promotion and cutover | QA-6/7/9; CON-3/4/5; CRN-2/3/4/5; all-driver final review |

## Detailed Iteration Goals

### Iteration 1: Initial structure
Refine the whole HPS. Address HPS-1/2/3/4, QA-5, CON-1/2/4/6 and CRN-1/2/3/4 through context, containers, module boundaries and ownership.

### Iteration 2: Pricing transaction
Refine calculator, configuration and persistence for HPS-2/3/4/5, QA-1/2 and CRN-4. Specify lock scope, a budget below 100 ms, simulation/commit parity and durable activation progress. Business policy remains conditional.

### Iteration 3: Delivery and measurement
Refine worker, receipt and measurement contracts for HPS-2, QA-2/8, CON-5 and CRN-4. Expose CMS contract dependencies and recovery limits.

### Iteration 4: Resilience and access
Refine deployment, queries and entitlements for HPS-1/3/6, QA-3/4/5 and CON-2/6. Define workload experiments and failure boundaries without claiming capacity.

### Iteration 5: Delivery readiness
Refine ports, tests, CI/CD and migration for QA-6/7/9, CON-3/4/5 and CRN-2/3/4/5. Reassess every driver and record remaining qualification.

## Implementation Timeline

| Relative period | Work | Evidence required |
|---|---|---|
| Weeks 1-2 | Cloud/Git skeleton, hotel configuration, login | Iteration 1; authorization and deployment smoke checks |
| Weeks 3-6 | Preview/change/query, basic rate and permission administration | Iteration 2; golden examples and early latency measurements |
| Weeks 7-8, within month 2 | Staging CMS flow and MVP demo | Iterations 3 and early 4; authorized end-to-end workflow and recovery |
| Months 3-4 | Operational resilience, full administration and tuning | Iteration 4; load and fault evidence |
| Months 5-6 | Contract verification, migration rehearsal and release | Iteration 5; validation-plan gates |

Basic HPS-1 through HPS-6 support the primary workflows in the proposed MVP. Rich administration and additional protocols may follow. No fixed completion date is asserted without staffing, scope, kickoff and external access agreement. Design iterations are not sprints.

## Alignment with Development Team

| Responsibility | Needed expertise | Coordination |
|---|---|---|
| Browser | Angular, accessibility and browser testing | Application contracts |
| Pricing/configuration | Java, domain rules and transactional SQL | Domain owner approval of golden cases |
| Integration | Java, REST, retries and reconciliation | CMS contract owner |
| Platform/quality | Cloud, CI/CD, performance and fault testing | Release evidence and operations |

These are responsibility areas, not four assumed teams. Named owners and capacity await the roster; individuals may cover multiple areas. Contract changes require consumer review.
