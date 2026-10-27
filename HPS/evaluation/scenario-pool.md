# HPS ATAM Stakeholder Scenario Pool

Freshly reviewed and revised on 2026-10-23, Asia/Seoul, under the changed evaluation skill. All five independent simulated stakeholder agents reread the ADD baseline and retained their two historical candidates with explicit quality classifications. Stable IDs permit comparison; this does not reuse historical votes. This run's ballots are recorded separately in participation.md. These are not interviews with actual employees or approved new requirements. New time/load values below are hypothetical test proposals pending owner agreement.

## Consolidation and voting rules

No exact duplicates were found. S-04 and S-10 both cover cutover but remain separate: S-04 tests receiver fencing of delayed legacy requests across authority generations; S-10 tests artifact/schema rollback and delivery feasibility. S-01 and S-02 distinguish routine stale-preview correctness from permanently blocked activation recovery. S-03 and S-06 distinguish CMS receipt recovery from storage/telemetry/failover interaction. All five stakeholder roles confirmed this consolidation before their fresh 2026-10-24 ballots; see [participation](participation.md).

Each SH1-SH5 casts up to five distinct votes, one per scenario. Rank by total votes descending, then numeric ID ascending. Top five become new utility-tree leaves; all candidates are analyzed. Numeric importance/difficulty sums do not override votes. Initial QA-1..9 remain in the tree. Facilitator, designer and evaluator do not vote.

| ID | Origin | Type | Title | Primary attribute | Related quality effects, not additional primary branches |
|---|---|---|---|---|---|
| S-01 | SH1-U | Use case | Confirm pricing after policy changes and replay a lost response | Reliability, QA-2 | QA-1 publication timing; monetary correctness is HPS-2/4/5 |
| S-02 | SH1-E | Exploratory/growth | Recover an irreparable policy activation at portfolio scale | Reliability, QA-2 | QA-8 progress; QA-3 only if price queries are interrupted |
| S-03 | SH2-S1 | Use case | Recover lost CMS receipts with duplicate and late requests | Reliability, QA-2 | QA-8 receipt evidence; order/deduplication are response invariants |
| S-04 | SH2-S2 | Exploratory | Fence delayed legacy requests during cutover and rollback | Reliability, QA-2 | QA-8 reconciliation; QA-3 only for actual query interruption |
| S-05 | SH3-1 | Growth | Sustain query growth with concentrated hotel mutations | Scalability, QA-4 | QA-1 normal publication timing; QA-3 query success; QA-8 observations |
| S-06 | SH3-2 | Exploratory | Recover database failure during telemetry/storage pressure | Availability, QA-3 | QA-2 committed records; QA-8 measurement accounting |
| S-07 | SH4-1 | Use case | Enforce revoked hotel scope across cursors and replays | Security, QA-5 | QA-1 grant lookup overhead; audit supports evidence, not expanded QA-8 |
| S-08 | SH4-2 | Exploratory | Handle identity key rotation during provider outage | Security, QA-5 | QA-3 authorized query availability under key-cache policy |
| S-09 | SH5-1 | Growth | Extend query protocol with trustworthy independent tests | Modifiability, QA-6 | QA-9 independent testing; QA-5 security parity |
| S-10 | SH5-2 | Exploratory | Deliver and roll back a release after accepted writes | Deployability, QA-7 | QA-2 publication preservation; QA-9 rehearsal fidelity; CON-4 is a constraint |

These primary labels are the required utility-tree and Step 6/8 Attribute(s) labels. Correctness, complete PriceSets, single-writer authority and monetary policy are functional invariants, not silently introduced quality branches. A blocked management operation or write freeze does not by itself violate QA-3, which measures price-query uptime. Additional failure/recovery criteria refine this evaluation's scenarios and remain proposals where not present in the original requirements.

## Fresh role review of the stricter tradeoff definition

SH1 identified atomic price/task/receipt writes as reliability protection with potential publication latency cost. SH2 cautioned that ordered delivery versus head-of-line delay is not automatically two different attributes; increasing worker resources may affect QA-2 recovery and QA-4 query latency only under explicit saturation/recovery assumptions. SH3 separated competing performance workloads from formal cross-attribute tradeoffs and identified synchronous replication and durable telemetry write costs. SH4 defined a bounded known-key trust-window comparison: shorter trust favors QA-5 compromise response but can reduce QA-3 during IdP outage; unknown keys and expired tokens remain rejected under either option. SH5 found no opposing-QA tradeoff merely from ports, test maintenance, schema complexity or deadlines. The evaluator determines formal classification from the actual baseline and states unsupported cases as None or conditional candidates.

## S-01: Confirm pricing after policy changes and replay a lost response

- Source/stimulus: a revenue user previews base-price edits; an administrator activates tax/derived-rate changes before confirmation. The user submits stale expected versions, refreshes, commits and retries after losing the response.
- Environment/artifact: normal load with overlapping configuration activation; calculator, version checks, PriceSet, receipt and delivery.
- Response: reject a stale new command; present the new policy for a fresh preview; publish one complete policy-consistent set atomically; replay the original durable result for the same committed request after current authorization.
- Measure: zero stale new commits, zero incomplete sets, one logical publication per key, exact A6-approved golden amounts and no unintended fixed-rate changes. Existing QA-1 <100 ms applies only under agreed normal A1 conditions. CMS deadline remains A2/A3.
- Evidence/concern: HPS-2/3/4/5; D3/4/6/13/14; A1/2/3/6/12. Monetary semantics, cross-date transition visibility and lock contention are unresolved. Financial correctness and the user's confirmed price are the business concern.

## S-02: Recover an irreparable policy activation at portfolio scale

- Source/stimulus: headquarters applies seasonal policy, discovers an irreparable target after some dates publish, and needs to correct policy while sales continue.
- Environment/artifact: proposed 300 hotels x 365 future dates with concurrent queries/changes; ConfigurationActivation, tasks, pointer, PriceSets, blocked recovery and CMS.
- Response: expose affected dates/versions and local versus CMS progress; never claim incomplete work complete; preserve latest base/fixed edits; use an approved compensating/replacement transition to converge to correct prices.
- Measure: zero false completion, invalid sets or overwritten latest edits; all affected dates traceable. Proposed alarm <=60 seconds and full local/CMS convergence <=30 minutes after compensation approval are hypothetical, not accepted requirements.
- Evidence/concern: HPS-2/3/4/5; primary QA-2, related QA-8; D3/4/6/13/14; A2/3/6/8/12. Current immutable target can remain Blocked indefinitely and prevents another activation. This is not itself a QA-3 query outage. A12 has no approved exceptional recovery path. Unbounded atomic recalculation could create performance/availability risks and requires separate evidence.

## S-03: Recover lost CMS receipts with duplicate and late requests

- Source/stimulus: CMS durably receives publication N but its reply is lost; a lease expires, retry starts, N+1 waits and an old worker's request arrives late.
- Environment/artifact: continuing pricing during a recoverable CMS outage; REST adapter, leases, immutable publication, ledger and CMS receiver.
- Response: query receipt or retry the same ID; receiver deduplicates and rejects stale sequence effects; acknowledge only durable receipt; unrelated hotels progress.
- Measure: every accepted test publication logically matches a receipt; zero lost changes, duplicate logical updates or stale overwrites. Proposed backlog drain <=5 minutes after recovery depends on agreed workload/A2/A3 and is hypothetical.
- Evidence/concern: HPS-2; QA-2/8; D4/6/7/13; A2/3/8. Local fencing cannot cancel network traffic already sent. CMS capability agreement is necessary for price integrity across sales channels.

## S-04: Fence delayed legacy requests during cutover and rollback

- Source/stimulus: after legacy freeze and HPS writes, an unconfirmed legacy CMS request arrives late while an operator requests rollback.
- Environment/artifact: cutover rehearsal with different ID/sequence namespaces and ambiguous legacy receipts; import, authority gate, backlog, CMS mapping and rollback procedure.
- Response: reconcile outstanding legacy IDs and receipts, establish shared watermarks/mapping and receiver rejection of obsolete authority; block cutover if unresolved. After HPS writes, require reverse reconciliation before returning authority.
- Measure: zero unowned/unmapped accepted changes or outstanding deliveries, zero stale overwrites, zero simultaneous authoritative writers, zero gate passes with unresolved differences. Freeze and rollback duration remain A10, no new time target.
- Evidence/concern: HPS-2/3; QA-2/3/8; D6/7/12; A3/A10. Routing alone cannot fence in-flight legacy traffic; authority epoch or equivalent receiver mechanism is not yet concretely specified.

## S-05: Sustain query growth with concentrated hotel mutations

- Source/stimulus: reservation queries grow from 100k/day to 1m/day equivalents while one popular hotel attracts price changes and activation work.
- Environment/artifact: same baseline data/query mix; API, primary DB, query reservations, hotel lock and activation worker. Ten-times-average peak for 30 minutes and 50% of mutations to one hotel are hypothetical stress conditions.
- Response: protect query resources, bound background work, publish complete sets and expose queueing, errors and starvation.
- Measure: original QA-4 mean <=1.2 baseline; QA-1 <100 ms only for agreed A1 normal load. Proposed >=99.9% valid-query success and no continuously growing queue during the 30-minute peak are test hypotheses, not approved SLA changes. Report offered/completed throughput and all rejects/timeouts.
- Evidence/concern: HPS-2/3/4; QA-1/3/4/8; D5/8/13/14; A1/4/5. API scaling cannot remove a hotel lock or shared DB bottleneck. Resource reservations trade query continuity against background drain speed.

## S-06: Recover database failure during telemetry/storage pressure

- Source/stimulus: telemetry export stops while retained records/versions accumulate; the primary DB zone fails.
- Environment/artifact: continued reads/writes; primary/standby, prices/tasks/receipts/ledger, export checkpoint, snapshot retention. Proposed 24-hour export outage, 70% initial storage use and one DB failure are hypothetical.
- Response: recover queries/tasks, retain committed records, resume/reconcile exports; do not delete pending CMS records or live snapshot references to reclaim space.
- Measure: proposed query recovery <=60 seconds, committed-record RPO=0, alert within one minute of 80% storage, export drain <=4 hours after recovery. All are proposed, service capability-dependent values. Reconcile all accepted/exported IDs, zero premature reference deletion, label unrecoverable exact timing unknown rather than claiming QA-8 compliance.
- Evidence/concern: HPS-2/3; QA-2/3/8; D5/7/8; A4/8/13. Durability, complete telemetry and retained snapshots compete for storage/I/O and commit latency; capacity and service guarantees are not measured.

## S-07: Enforce revoked hotel scope across cursors and replays

- Source/stimulus: revoked human or machine account reuses session, token, cursor, publication ID and idempotency key and substitutes another hotel ID after revocation commits.
- Environment/artifact: multiple API replicas, some requests authorized before revocation; entitlement store, query/pricing ports, replay and pagination.
- Response: every authorization after revocation uses current grants; deny forbidden scope without replay disclosure. Already-authorized in-flight requests follow A7 and remain auditable by authorization revision.
- Measure: zero unauthorized exposure/change after a post-revocation check; zero bypass paths; atomic entitlement revision/audit. This run does not prescribe a new attempt-count threshold.
- Evidence/concern: HPS-1/2/3/6; primary QA-5; D2/5; A7. Audit is supporting evidence, not a new QA-8 obligation. Replaying a receipt before version checks must not bypass authorization. A stricter no-commit-after-revocation policy would require changed design.

## S-08: Handle identity key rotation during provider outage

- Source/stimulus: IdP/JWKS is unavailable during signing-key rotation; calls use both cached valid keys and unknown key IDs.
- Environment/artifact: normal queries with a hypothetical 15-minute outage; identity adapter, key cache, sessions, query pools and auth telemetry.
- Response: fail closed for unverified identity; process valid existing sessions/tokens only within approved trust/expiry and current grants; bound refresh/retries to protect query resources; count actual query failures in availability.
- Measure: zero unverified access, zero expiry bypass. Maximum key/session trust and emergency invalidation remain open. This run does not prescribe a new alert/recovery time; 15-minute outage remains a hypothetical test environment.
- Evidence/concern: HPS-1/3; primary QA-5, related QA-3; CON-2; D2/8/9; A4/7. Longer trust in previously verified keys can aid query availability but prolong compromised-key exposure. Both shorter and longer bounded policies reject unknown keys and never extend token expiry. Monitoring/testing are supporting means, not additional primary attributes.

## S-09: Extend query protocol with trustworthy independent tests

- Source/stimulus: integration developer adds a non-REST price-query endpoint such as gRPC.
- Environment/artifact: integration without live CMS/identity and with production-equivalent real storage; protocol adapters, query port, entitlements, snapshot semantics and full harness inventory.
- Response: adapter/composition-only changes preserve authorization, amounts, versions, pagination and errors; programmable external doubles and real storage validate behavior, with partner comparison in staging.
- Measure: zero core source changes (QA-6); all elements independently testable (QA-9); parity includes revocation, expiry, amounts and errors. No new duration target.
- Evidence/concern: HPS-3/6; QA-5/6/9; CON-5; CRN-2/4; D9; A7/11/13. Ports alone do not prove independence; doubles may drift and in-memory storage cannot prove locking/snapshots.

## S-10: Deliver and roll back a release after accepted writes

- Source/stimulus: release lead promotes compatible schema changes and transfers legacy authority; a defect appears after HPS accepts writes and some CMS publications.
- Environment/artifact: staging rehearsal with old/new binaries, legacy fixture and programmable CMS; CI, immutable artifacts, migrations, authority switch and receipt reconciliation; two/six-month delivery constraints.
- Response: same digests/runtime configuration, verified schema overlap and one writer; distinguish binary rollback from legacy authority rollback. Reconcile business state and external receipts before authority rollback; block unsafe gates and prepare forward recovery. Confirm actual owners, scope and dependencies before dates.
- Measure: no environment code changes (QA-7), identical digests, zero overlapping writers and all accepted changes accounted for (QA-2); MVP/release within two/six months from agreed kickoff (CON-4). Staffing, rollback duration and RTO remain open.
- Evidence/concern: HPS-2/3; QA-2/7/9; CON-3/4; CRN-3/4/5; D10/11/12; A2/3/9/10/11. Expand/contract does not reverse business state/CMS effects; a schedule without capacity is not evidence of buildability.
