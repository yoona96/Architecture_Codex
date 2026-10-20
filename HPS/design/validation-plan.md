# Hotel Pricing System - Validation Plan

Prepared 2026-10-18 after ADD iteration 5. This is a future implementation evidence plan. No HPS implementation, load, security, failover or integration test was executed. Documentation checks do not prove quantitative targets. ATAM is a subsequent separately requested process.

## Acceptance decisions

| ID | Decision needed | Working basis | Responsible role / gate |
|---|---|---|---|
| A1 | QA-1 timing, dimensions, normal load and statistical rule | Ingress-to-commit <100 ms; 90 ms internal engineering ceiling, no assumed percentile exemption | Product/performance leads before benchmark acceptance |
| A2 | Accepted changes, outage/recovery and delivery delay | Accepted means committed; eventual receipt after recoverable outage | Product/CMS owners before QA-2 sign-off |
| A3 | CMS deduplication, ordering and durable receipt lookup | Publication ID and hotel sequence; 202 polled unless durable by contract | Integration/CMS owners before integration completion |
| A4 | Availability period, exclusions, RTO/RPO and backups | Proposed 30-day time SLI plus request-success diagnostic | Operations/product before production readiness |
| A5 | QA-4 workload, peak, baseline and errors | Mean increase <=20% is explicit; provisional 10x-average peak, same query mix | Performance/product before load sign-off |
| A6 | Currency, rounding, tax, rule precedence/effective dates | Decimal/pinned policy; no invented conversion | Domain owner before calculator acceptance |
| A7 | Human/machine/admin scope and revocation | Current grants per request; in-flight authorized requests may finish | Security/product before access sign-off |
| A8 | Measurement scope, retention and exact timing | Durable accepted ledger; unknown commit-crash latency and separate ingress failures | Operations/product before QA-8 sign-off |
| A9 | Team, budget, provider, kickoff and MVP | Responsibility areas, relative two/six months | Engineering/product before date/cost commitment |
| A10 | Export, freeze, legacy backlog and rollback | Single writer, reconciliation and delivery watermark transfer | Migration/system owners before cutover |
| A11 | Full independent-test fidelity | All inventory elements without live external business systems | Quality lead before QA-9 sign-off |
| A12 | Activation cross-date consistency and unrecoverable target | Last complete per-date prices remain visible; blocked immutable target needs exceptional compensating policy | Domain/product before activation implementation acceptance |
| A13 | Cursor/replay retention and bounded storage | Durable snapshot manifest retains references until explicit expiry; receipt retention covers replay | Operations/product before query/recovery acceptance |

These are open decisions, not approvals. A12 can require redesign if temporary cross-date policy differences are unacceptable; do not substitute an unbounded atomic hotel recalculation without rechecking QA-1/3.

## Scenario experiments

| Driver | Experiment | Pass evidence |
|---|---|---|
| HPS-1/6, QA-5 | Invalid issuer/audience, expired tokens, unknown keys, forged scopes and over-grant; revoke during in-flight request | No unauthorized disclosure; 401/403; audited revision and agreed revocation boundary |
| HPS-2 | Preview/commit with changed inputs, lost responses and duplicate keys | Preview has no side effects; stale versions conflict; replay original durable result |
| HPS-3 | Commit then query; paginate during changes and replica restart | Complete snapshot, current scope each page, explicit expiry; retained versions not pruned early |
| HPS-4/5 | Invalid graphs, retire referenced rates, activate and crash before/after each transaction | Pointer/tasks atomic, progress durable, no stale base overwrite; Blocked state visible and approved repair semantics |
| QA-1 | Maximum approved dimensions under mixed normal load, same-hotel different-date contention and activation background work | Strict <100 ms under agreed A1; all durations/locks/errors retained; rejection cannot fake a pass |
| QA-2 | Crash around commit/send/receipt; delayed old sends, 202, duplicates, outage and restore | Every accepted ID queryable and eventually receipt-matched within A2; no stale overwrite, silent discard or duplicate logical CMS update |
| QA-3 | Kill API, interrupt zone/primary, fail identity/CMS, overload and restore backup | Approved uptime/RTO/RPO; exclusions explicit and failover/dependency failures counted |
| QA-4 | 100k/day and 1m/day-equivalent stable loads plus agreed peaks, same data/query skew | Mean high latency <=1.2 baseline; achieved throughput and errors reported alongside p95/p99 and DB saturation |
| QA-6 | Add thin alternative-protocol adapter | Core source unchanged; same validation/security/result semantics |
| QA-7 | Promote backend/UI digests integration->staging | Identical artifacts, only validated runtime config differs |
| QA-8 | Disable exporter, crash at commit/timing window and after attempt intent, recover backlog | Reconcile publication/attempt/receipt/export ID sets; unknown timing labeled; completeness not asserted without evidence |
| QA-9 | Run every inventory harness without live identity/CMS/other business systems | All elements testable with real storage where semantics matter |

Use monotonic elapsed time at the application boundary. A pre-commit timestamp cannot prove completion latency. If exact crash-window reconstruction is impossible, keep QA-8 partial and report unknown/bounded results. Compare accepted publication IDs, price versions, outstanding tasks, confirmed CMS IDs and exported IDs. Check sustained backlog drain exceeds arrival rate within the agreed recovery window. Synchronous standby/failover durability depends on selected service guarantees and must be fault-tested; disaster-loss assumptions cannot be hidden behind local transaction claims.

## Independent integration-test inventory

| Element | Harness and substitute | Key checks |
|---|---|---|
| Browser shell/client | Browser runner, API/identity redirect double | Cookie/CSRF, errors and no token leakage |
| Hotel/access/pricing/query views | Versioned API simulator | Scoped views, preview/commit distinction and cursor expiry |
| REST and future protocol adapters | Application harness and identity double | Bounds, errors and protocol parity |
| Identity/authorization | Provider/JWKS simulator and real entitlement repository | Rotation, invalid identity, revocation and grants |
| Configuration/permissions | Disposable real database | Versions, valid graphs, audit and scope |
| Calculator/pricing | Golden domain examples and real repositories | Decimal rules, fixed independence, parity and atomicity |
| Transaction/relational adapters | Production-equivalent database version | Rollback, unique keys, hotel locks and sequence ordering |
| Query/read port | Representative indexed database | Immediate visibility, snapshot manifests and retention |
| Task claimant/leases | Concurrent workers and real database | Expiry, fencing and bounded pools |
| Activation coordinator | Crash injection and real pricing transaction | Exactly one durable date completion; current base values and Blocked recovery |
| Delivery coordinator/CMS adapter | Programmable HTTP simulator | Timeout, 202/429/5xx, duplicate and late sequence |
| Ledger/reconciler/exporter | Real store, failing CMS/telemetry doubles | Unknown outcomes, resumable ID reconciliation |
| Ingress/runtime/secrets | Ephemeral cloud test environment, synthetic clients | Health routing, drain, config validation and secrets isolation |
| CI/migration | Disposable integration environment, old/new binaries and legacy export fixture | Same digest, compatible schema, full reconciliation and rollback |

Pure calculator unit/property tests supplement integration evidence. Staging against all actual external test systems detects double drift; independent testing does not eliminate partner verification.

## Release gates

| Gate | Evidence | Owner |
|---|---|---|
| MVP within month 2 | Basic HPS-1..6 workflow with staging CMS; early latency/recovery | Product/engineering |
| Architecture boundary | No transport/provider SDK in core; versioned contracts | Module owners |
| Business/security | Approved A6/A7/A12 and golden/negative tests | Domain/security |
| Quality | A1-A5 agreed, performance/fault results, A8 measurement accounting | Quality/performance/operations |
| Deployment | Same-digest promotion, compatible migrations and alerts | Platform |
| Cutover/release within month 6 | A9/A10 feasibility, rehearsal and no unresolved high-priority acceptance blocker | Product/engineering/operations |

If evidence fails or an assumption is rejected, reopen its ADD decision. Do not improve latency by weakening visibility, reliability by discarding tasks, or availability by excluding unplanned outages.

## Final driver coverage

Satisfied means sufficient design decisions under stated assumptions, not passed implementation tests. Partial means required decisions or acceptance evidence still constrain the claim.

| Driver | Final design status | Decisions / evidence | Remaining qualification |
|---|---|---|---|
| HPS-1 | Satisfied | D2; architecture 7.1/7.5 | Provider capabilities and security tests |
| HPS-2 | Partial | D3/4/6/12/13; 7.3/7.4/7.8 | A2/A3/A6, CMS and cutover proof |
| HPS-3 | Satisfied | D5/8; 7.5 | Snapshot implementation, A13 and query tests |
| HPS-4 | Partial | D3/13/14; 7.2 | A6/A12 activation and monetary policies |
| HPS-5 | Partial | D3/14; 7.2 | Rule semantics and unrecoverable target policy |
| HPS-6 | Satisfied | D2; 7.1/7.5 | A7 and negative authorization tests |
| QA-1 | Partial | D3/4/13; 7.3 | A1 and hot-hotel benchmark |
| QA-2 | Partial | D4/6/12/14; 7.3/7.4/7.8 | A2/A3/A10, recovery and receipt evidence |
| QA-3 | Partial | D8/10; 5/7.5 | A4, failure/restore measurements |
| QA-4 | Partial | D5/8/13; 7.5 | A5, primary capacity and errors |
| QA-5 | Satisfied | D2; 7.1/7.5 | A7 in-flight assumption and security verification |
| QA-6 | Satisfied | D9; 6/7.6 | Alternate adapter with unchanged core |
| QA-7 | Satisfied | D10; 7.7 | Same-digest demonstration |
| QA-8 | Partial | D7; 7.4 | A8 exact timing, pre-persistence scope and retention |
| QA-9 | Satisfied | D9; 7.6 and inventory above | A11 full harness execution |
| CON-1 | Satisfied | D1; 5/6 | Browser/device matrix |
| CON-2 | Satisfied | D1/2/8; 5 | Cloud/identity capability agreement |
| CON-3 | Satisfied | D10; 7.7 | Existing Git runner integration |
| CON-4 | Partial | D1/11; iteration-plan | A9 staffing/scope and external access |
| CON-5 | Satisfied | D6/9; 7.4/8 | Negotiated initial REST contracts |
| CON-6 | Satisfied | D1/8; 5 | Managed capabilities and cost sizing |
| CRN-1 | Satisfied | D1; 2/5/6 | Implement documented boundaries |
| CRN-2 | Satisfied | D1/11; iteration-plan | Confirm available Java/Angular capacity |
| CRN-3 | Partial | D11; iteration-plan | Assign actual people |
| CRN-4 | Partial | D3/4/9/10/12/13/14 | Ongoing checks, unresolved business gates |
| CRN-5 | Satisfied | D10; 7.7 | Pipeline implementation and release evidence |

## Residual risks

Primary database and hotel serialization are bottlenecks; node scaling cannot remove them. Strict CMS ordering causes head-of-line blocking. Large rule graphs may violate latency. Identity outage affects login. Exact commit timing can be unknown after crashes. Activation temporarily exposes different policy versions across dates and an unrecoverable target needs approved exceptional handling. Cloud cost, staffing and external readiness remain unproven. These are explicit inputs for later evaluation, not claims resolved by documentation.
