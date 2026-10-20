# Hotel Pricing System - Iteration 2

Executed 2026-10-18 after iteration 1. Updated architecture 7.2/7.3 before recording their interfaces and decisions.

## Iteration Goal
Make simulation deterministic, accepted prices atomically visible and configuration activation recoverable.

## Drivers to Address
HPS-2/3/4/5; QA-1/2; CRN-4.

## ADD Process Steps

### Step 2: Select drivers and goal
QA-1 local readiness and QA-2 durability jointly define the transaction boundary. Business semantics cannot be invented to fill pricing-policy gaps.

### Step 3: Choose elements to refine
Refine pricing/calculator, configuration activation, PriceSet, transaction port and query consistency. Keep identity and CMS outside the local commit.

### Step 4: Choose design concepts

| Concept | Pros | Cons | Discarded alternatives |
|---|---|---|---|
| Pure versioned calculator | Preview parity and testability | Business rules still need approval | Arbitrary code or remote calculator |
| Atomic price/publication/task/receipt | No local dual-write loss | Transaction size and contention | Separate network write inside commit |
| Exclusive hotel lock | Simple sequence/policy invariants | Different dates in a hot hotel serialize | Fine-grained locks without ordering proof |
| Durable activation date tasks | Resumable and bounded | Different dates may temporarily use different policies | Unbounded transaction or in-memory jobs |
| Primary-store snapshots | Immediate consistent query | Primary capacity dependency | Async projection without freshness contract |

### Step 5: Instantiate and define interfaces

| Decision | Rationale |
|---|---|
| Version-check preview and recalculate at commit | Stale UI cannot overwrite changed inputs |
| Replay committed idempotency receipt before checking stale versions | Lost response does not become a false conflict |
| One exclusive hotel lock for all mutations | Explicit contention consequence, no ambiguous lock mode |
| 75 ms work allocation plus 15 ms contingency | 90 ms internal ceiling leaves headroom below 100 ms |
| Activation pointer and tasks commit together | Crash cannot lose recalculation obligations |
| Per-date recalculation reads latest base/fixed values | Avoid stale activation overwrite of user changes |
| Keep last complete set and expose transition status | No mixed rules inside a date; cross-date policy needs agreement |

Architecture 7.2/7.3 define sequences, section 8 defines contracts. Architecture 4's ConfigurationActivation is now given a durable lifecycle. Task storage remains within the existing worker/database containers.

### Step 6: Record decisions

| Driver | Decision | Rationale | Discarded alternative |
|---|---|---|---|
| HPS-2/4/5, QA-1 | D3 | Bounded deterministic work | Unbounded rules |
| QA-1/2 | D4 | Atomic acceptance and recoverable work | Dual writes |
| HPS-3 | D5 | Immediate complete query | Undefined stale reads |
| HPS-2/4/5, QA-1/2 | D13/D14 | Explicit serialization and activation recovery | Hidden lock scope/fire-and-forget tasks |

### Step 7: Analyze achievement

| Driver | Analysis result |
|---|---|
| HPS-2 | Partially satisfied: local preview/change complete; CMS next |
| HPS-3 | Satisfied at design level: complete snapshot contract |
| HPS-4/5 | Partially satisfied: lifecycle complete; policy and cross-date acceptance require domain confirmation |
| QA-1 | Partially satisfied: 90 ms engineering ceiling, no benchmark and A1 pending |
| QA-2 | Partially satisfied: local atomicity; receiver/recovery agreement pending |
| CRN-4 | Partially satisfied: explicit invariants; implementation enforcement required |

Transaction and activation design achieved. Carry receiver and measurement work to iteration 3; hot-hotel contention remains a required experiment.
