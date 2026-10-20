# Hotel Pricing System - Iteration 4

Executed 2026-10-18 after iteration 3. Refined container topology, query sequence, authorization and versioned pagination.

## Iteration Goal
Protect query availability and tenfold volume while enforcing current hotel permissions.

## Drivers to Address
HPS-1/3/6; QA-3/4/5; CON-2/6.

## ADD Process Steps

### Step 2: Select drivers and goal
Address primary availability/scalability/security without weakening immediate committed price visibility.

### Step 3: Choose elements to refine
Refine deployment, primary-store query, authorization, sessions, resource pools and cursor lifecycle. Preserve atomic publication and separate CMS processing.

### Step 4: Choose design concepts

| Concept | Pros | Cons | Discarded alternatives |
|---|---|---|---|
| Multi-zone API and synchronous standby | Handles node failure | Cost and failover interruption | Single zone; active-active before RTO/RPO known |
| Primary indexed queries | Immediate consistency | Database bottleneck | Stale replica/cache without contract |
| Query resource reservations | Limits workload interference | Tuning and explicit overload rejection | Unlimited pools |
| Per-request entitlements | Explicit revocation boundary | Database work | Long-lived stale permission claims |
| Durable version snapshot manifest | Stable pagination across replicas | Storage/retention cost | Mutable offset pagination |

### Step 5: Instantiate and define interfaces

| Decision | Rationale |
|---|---|
| Two-zone API and standby with bounded retries | Availability tactics without zero-downtime claim |
| Reserve query pools; background tasks yield | Shared DB must not be exhausted by polling/recalculation |
| Current grants for human and machine subjects | External API must follow hotel restrictions |
| Snapshot manifest with retained referenced versions and expiry | Cursor survives replicas and cannot mix pages |
| Measure both mean latency and errors/achieved throughput | QA-4 cannot pass by dropping traffic |
| Allocate publication sequence under hotel lock | Delivery order follows commit order |

Architecture 5 and 7.5 precede query-port refinement in section 8. 116 queries/s is a sizing hypothesis, not an approved traffic ceiling.

### Step 6: Record decisions

| Driver | Decision | Rationale | Discarded alternative |
|---|---|---|---|
| QA-3/4, CON-2/6 | D8 | Fault isolation and reserved query resources | Single-zone production |
| HPS-1/6, QA-5 | D2 refinement | Current entitlements and audited grants | UI checks/stale claims |
| HPS-3, QA-4 | D5 refinement | Indexed bounded snapshot queries | Inconsistent live pagination |

### Step 7: Analyze achievement

| Driver | Analysis result |
|---|---|
| HPS-1/3/6 | Satisfied at design level under access/snapshot assumptions; tests pending |
| QA-3 | Partially satisfied: SLI policy, RTO/RPO and fault evidence pending |
| QA-4 | Partially satisfied: requirement direction resolved; workload/capacity evidence pending |
| QA-5 | Satisfied at design level under A7 in-flight boundary; provider/negative tests pending |
| CON-2/6 | Satisfied at design level: managed cloud and provider identity |

Primary-driver tactics are explicit. Quantitative targets remain unproven. Proceed to implementation/evidence governance, not ATAM.
