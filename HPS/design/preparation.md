# Hotel Pricing System - ADD Preparation

Prepared 2026-10-18. Reviewed the current drivers, use-case figure, AGENTS.md, preparatory-steps, add-process and iteration skills and templates. HPS/design was empty at execution time. The earlier reviewed design is background knowledge, not an existing artifact or proof of completed work. This execution creates the design anew; it does not run ATAM or implementation tests.

## Preparation step 1: Review inputs

The normative requirements contain HPS-1 through HPS-6, QA-1 through QA-9, CON-1 through CON-6 and CRN-1 through CRN-5. HPS-2/3/4 and QA-1/2/3/4/5 have priority. The figure confirms administrator inheritance of commercial capabilities. Current source explicitly says nine scenarios and limits QA-4 latency increase to 20%; older source preparation comments are historical and do not override these requirements. Current skill paths resolve correctly.

| Input | Working basis | Unresolved decision |
|---|---|---|
| QA-1 | Complete hotel/date prices queryable strictly below 100 ms; proposed clock is ingress-to-commit | Normal workload, maximum dimensions, timing start and statistical acceptance |
| QA-2 | Every durably accepted edit produces prices and eventual CMS receipt under recoverable failure | Acceptance, receipt semantics, duplicate/sequence support, maximum outage and delivery delay |
| QA-3 | 99.9% query availability outside maintenance | Accounting period, exclusions, RTO/RPO and dependency treatment |
| QA-4 | High-volume mean latency at most 1.2 times baseline | Query mix, peaks, baseline and error accounting |
| QA-5 | Provider authentication; server-enforced hotel and operation authorization | Machine identities, admin scope and in-flight revocation |
| QA-8/9 | Durable publication measurement and inventory of independently testable elements | Retention, pre-persistence failures, exact crash-window timing and test fidelity |
| Pricing | Decimal money, versioned rules/tax policy, fixed-rate independence and acyclic derived rates | Currency, rounding, precedence, effective dates and shared rate definitions |
| Configuration activation | Durable bounded recalculation; old price versions remain explainable | Whether temporary different policy versions across dates are acceptable |
| Delivery constraints | Relative two-month MVP and six-month release | Team, budget, vendor, kickoff, external test access and MVP agreement |
| Replacement system | Controlled import and single authoritative writer | Export contract, freeze duration and rollback reconciliation |

These are explicit design assumptions, not approved requirement amendments. They permit conditional design progress. The source and root/.codex files are unchanged; decisions are tracked in validation-plan.md.

## Preparation step 2: Create domain model

Architecture section 4 contains the class diagram and responsibilities. PriceSet is introduced to express complete hotel/date visibility. Publication and Delivery distinguish local acceptance from external receipt. ConfigurationActivation makes affected-date recalculation and its progress explicit. These are concepts, not one-service-per-class instructions.

## Preparation step 3: Create iteration plan

The plan sequences whole-system structure, pricing correctness, delivery, resilience/security and delivery readiness. Each iteration executes ADD steps 2-7. Shared input review is the preparatory step, not omitted work.
