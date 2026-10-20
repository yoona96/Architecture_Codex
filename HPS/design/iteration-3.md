# Hotel Pricing System - Iteration 3

Executed 2026-10-18 after iteration 2. Added worker components, delivery sequence, contracts and D6/D7.

## Iteration Goal
Recover CMS delivery and publication accounting without coupling queries to CMS health.

## Drivers to Address
HPS-2; QA-2/8; CON-5; CRN-4.

## ADD Process Steps

### Step 2: Select drivers and goal
Distinguish local publication from downstream receipt. Prioritize no silent discard and explicit unknown outcomes.

### Step 3: Choose elements to refine
Refine claimant, delivery coordinator, CMS adapter, attempt ledger, reconciler and exporter. Connect the activation coordinator to the already defined pricing transaction port.

### Step 4: Choose design concepts

| Concept | Pros | Cons | Discarded alternatives |
|---|---|---|---|
| Database transactional queue | Reuses atomic task creation | Polling and retention load | Mandatory broker without measured demand |
| At-least-once plus receiver deduplication | Recovers ambiguous responses | Requires receiver agreement | Exactly-once HTTP promise |
| Ordered leases/fencing | Crash recovery and local stale-worker exclusion | Head-of-line blocking; old network traffic still needs receiver checks | Unordered overwrites |
| Durable unsampled ledger | Reconstructs accounting | Storage and exact timing uncertainty | Sampled telemetry only |

### Step 5: Instantiate and define interfaces

| Decision | Rationale |
|---|---|
| Pending/Leased/RetryDue/Blocked/Acknowledged | Avoid treating timeouts as confirmed failure or success |
| Persist intent before network send | Ambiguous crash remains discoverable |
| Immutable publication ID and sequence on retries | Prevent duplicate or stale logical updates |
| Receipt lookup and 202 polling | Distinguish request acceptance from durable receipt |
| ID-set export reconciliation and retention watermark | Detect missing records after monitoring outage |
| Backlog alarms and admission before exhaustion | Finite storage cannot cover permanent outage |

Architecture 6 and 7.4 precede section 8's negotiated CMS/measurement contracts.

### Step 6: Record decisions

| Driver | Decision | Rationale | Discarded alternative |
|---|---|---|---|
| QA-2, CON-5 | D6 | Durable REST recovery | Synchronous remote dependency |
| QA-8 | D7 | Unsampled durable accounting | Volatile counters only |
| HPS-2, CRN-4 | Preserve D4 | Retry exact accepted payload | Re-read newer mutable prices for old event |

### Step 7: Analyze achievement

| Driver | Analysis result |
|---|---|
| HPS-2 | Partially satisfied overall: internal flow designed, CMS agreement pending |
| QA-2 | Partially satisfied: receiver semantics and finite recovery window unresolved |
| QA-8 | Partially satisfied: exact crash-window timing, pre-persistence scope and retention unresolved |
| CON-5 | Satisfied at design level: initial REST contracts isolated |
| CRN-4 | Partially satisfied: state/repair explicit, operational ownership pending |

Recovery design achieved conditionally. No delivery or monitoring experiments have run. Continue to query resilience and access refinement.
