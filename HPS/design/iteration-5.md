# Hotel Pricing System - Iteration 5

Executed 2026-10-18 after iteration 4. Completed architecture 7.6-7.8, D9/D10/D12 and validation-plan.md.

## Iteration Goal
Make architecture extensible, independently testable and promotable, with safe cutover and honest final coverage.

## Drivers to Address
QA-6/7/9; CON-3/4/5; CRN-2/3/4/5; final review of all HPS, QA, CON and CRN drivers.

## ADD Process Steps

### Step 2: Select drivers and goal
Preserve price/receipt consistency while adding implementation controls. Completion means explicit design responses and residual decisions, not measured quality compliance.

### Step 3: Choose elements to refine
Refine adapters, composition root, test harnesses, runtime configuration, pipeline and migration. Revisit irreversible activation effects and all-driver closure.

### Step 4: Choose design concepts

| Concept | Pros | Cons | Discarded alternatives |
|---|---|---|---|
| Protocol-neutral core | New transport avoids business rewrite | Mapping/contract work | Business logic repeated per endpoint |
| Disposable DB and external doubles | Repeatable isolated tests | Mock drift requires staging contracts | All tests depend on live partners |
| Same digest plus runtime config | Repeatable promotion | Config schema/secrets management | Per-environment rebuild |
| Expand/contract schema | Overlap and application rollback | Delayed cleanup | Breaking schema rollout |
| Reconciled snapshot and authority switch | Detects loss/conflicting edits | Freeze and reverse-reconciliation agreements | Uncoordinated dual writes |

### Step 5: Instantiate and define interfaces

| Decision | Rationale |
|---|---|
| Future adapter in component diagram and protocol sequence | Demonstrate extension boundary |
| Independent inventory including activation/infrastructure | QA-9 applies to all elements |
| Existing Git and same backend/UI digests | Preserve CON-3 and QA-7 |
| Migration sequence with delivery watermark transfer | Legacy backlog cannot be silently lost |
| Unrecoverable activation remains explicit A12 | No invented repair can alter immutable target without business decision |
| Full driver-by-driver final table | Preserve HPS-4/5 partial status rather than hide it in QA summary |

### Step 6: Record decisions

| Driver | Decision | Rationale | Discarded alternative |
|---|---|---|---|
| QA-6/9, CON-5 | D9 | Stable core and isolated dependencies | Transport SDK in domain |
| QA-7, CON-3, CRN-5 | D10 | Reproducible promotion | Rebuild per environment |
| HPS-2, QA-2, CRN-4 | D12 | Single authority and reconciled delivery | Dual writes |
| CON-4, CRN-2/3/4 | D11 refinement | Relative milestones and real evidence | Unstaffed date guarantees |

### Step 7: Analyze achievement

| Driver | Analysis result |
|---|---|
| QA-6/7/9 | Satisfied at design level: ports, digests and test inventory; implementation demonstrations pending |
| CON-3/5, CRN-2/5 | Satisfied at design level: existing Git, REST, known stack and pipeline |
| CON-4, CRN-3/4 | Partially satisfied: staffing, ownership and sustained enforcement pending |
| HPS-1/3/6, QA-5 | Satisfied at design level under stated authorization assumptions; negative tests pending |
| HPS-2/4/5 | Partially satisfied: CMS, monetary policy and exceptional activation handling await agreement |
| QA-1/2/3/4/8 | Partially satisfied: mechanisms exist, acceptance decisions/evidence remain |

All five planned ADD design iterations are complete. validation-plan.md individually covers all 26 drivers, open assumptions and experiments. No runtime tests, deployment or ATAM were executed. Future failed experiments or rejected assumptions must reopen affected ADD decisions.
