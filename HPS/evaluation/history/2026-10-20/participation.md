# HPS ATAM Participation and Ballot Record

Sessions began 2026-10-18, resumed 2026-10-19, and completed closing review on 2026-10-20, Asia/Seoul. This is an agent-simulated evaluation. No actual hotel employee, CMS supplier or authority approved a requirement, score, design or release. The facilitator, evaluator and designer do not vote. Five distinct stakeholder agents independently proposed two scenarios each, then reviewed the same [candidate pool](scenario-pool.md), [preparation](preparation.md) and Phase 1 [analysis](result.md) before voting. Work was scheduled within the four-active-agent limit; written exchanges preserve role independence.

## Participants and baseline review

| ID | Role / agent | Main responsibility |
|---|---|---|
| SH1 | Revenue/pricing product owner / stakeholder_revenue | Price correctness, financial continuity and recoverable policy changes |
| SH2 | CMS/integration owner / stakeholder_integration | Durable receipts, ordering, partner contracts and legacy authority transition |
| SH3 | SRE/operations lead / stakeholder_operations | Availability, capacity, storage, backlog and recovery |
| SH4 | Security/identity lead / stakeholder_security | Hotel authorization, revocation, key trust and recovery privileges |
| SH5 | Engineering/QA delivery lead / stakeholder_engineering | Protocol boundaries, credible tests, release safety and buildability |

The designer confirmed the preparation presentation and D1-D14/A1-A13 mapping on 2026-10-19. Clarifications: (1) hotel lock queueing invalidates any inference that a 90 ms allocation guarantees the target; (2) sender-only logic cannot prove CMS receipt; (3) immutable activation can remain Blocked without A12 resolution; (4) durable IDs do not prove exact commit timing; (5) primary failover and shared CPU/I/O/WAL/storage remain availability/capacity dependencies. Current authorization is required before returning an idempotency receipt; receipt precedence only overrides stale version checks. Maximum cached-key trust/emergency revocation, late legacy producer fencing and post-retention command replay semantics remain unspecified.

## Consolidation and cross-role exchanges

All five roles reviewed and accepted the ten-candidate pool without merging. They distinguished S-04 receiver authority fencing from S-10 artifact/schema/business rollback and schedule feasibility. SH3 distinguished S-05 growth contention from S-06 storage/failover recovery. SH4 distinguished S-07 local grants, S-08 external identity trust and S-09 new-entry-point parity.

| Role | Response to another stakeholder |
|---|---|
| SH1 | Supports SH2's receiver fencing: routing/sender locks cannot retract old network requests. Supports SH3 query protection but rejects indefinite starvation of recalculation/CMS convergence. |
| SH2 | Supports SH5's distinction between binary and authority rollback; adds late legacy request fencing. Supports SH3 retaining pending CMS records under storage pressure, with jointly agreed admission/drain limits. |
| SH3 | Recognizes SH1 correctness priority but selects storage/identity compound failures over routine S-01; nonselected cutover/release risks still require analysis. |
| SH4 | Supports SH2 replay-scope concern while accepting designer clarification that authorization is already required. Supports SH1 recovery but requires bounded privileged compensation and audit. |
| SH5 | Supports SH2 receipt evidence as part of QA-2. Raising QA-8 importance concerns broader measurement completeness and does not prove delivery or double-count the same risk. |

## Public ballots

Each entry represents one vote. Every role used five distinct choices, within the up-to-five limit. IDs in each row are sorted for readability; there is no within-ballot preference weight.

| Stakeholder | S-01 | S-02 | S-03 | S-04 | S-05 | S-06 | S-07 | S-08 | S-09 | S-10 | Total |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| SH1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 5 |
| SH2 | 0 | 1 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 5 |
| SH3 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 1 | 0 | 0 | 5 |
| SH4 | 0 | 1 | 0 | 1 | 0 | 0 | 1 | 1 | 1 | 0 | 5 |
| SH5 | 0 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 1 | 1 | 5 |
| Total | 1 | 4 | 4 | 4 | 3 | 2 | 2 | 2 | 2 | 1 | 25 |

| Role | Reasons for its choices |
|---|---|
| SH1 | S-01 confirmed versus sold price; S-02 unblock revenue policy; S-03 correct channel prices; S-04 protect launch-time price authority; S-05 preserve peak revenue opportunity. |
| SH2 | S-03 durable receiver guarantees; S-04 legacy fencing; S-02 converge already-delivered partial policy; S-06 preserve receipt/replay evidence; S-07 protect replay disclosure. |
| SH3 | S-05 actual shared resource limits; S-06 avoid repeated outage during recovery; S-02 restore blocked hotel operations; S-03 drain backlog faster than arrivals; S-08 bound identity retry cascades. |
| SH4 | S-07 comprehensive revocation paths; S-08 missing trust/compromise policy; S-09 secure new adapter parity; S-02 privileged compensation scope; S-04 receiver authority validation. |
| SH5 | S-09 unchanged core/test fidelity; S-10 release/rollback/capacity; S-04 distinguish binary rollback from authority; S-03 realistic failure fixtures; S-05 expose redesign before schedule commitments. |

Computed rank is S-02, S-03, S-04, S-05, S-06, S-07, S-08, S-09, S-01, S-10. The first five are promoted as new utility-tree leaves. S-06 wins the four-way two-vote tie by numeric ID, not by inferred severity. All ten remain analyzed. Low votes do not accept a risk, remove a requirement or prove a design.

## Score review record

Phase 1 scores were shared before voting: QA-1 100/90, QA-2 100/100, QA-3 100/80, QA-4 90/80, QA-5 100/60, QA-6 60/50, QA-7 60/50, QA-8 70/90, QA-9 70/60 (Importance/Difficulty).

| Proposal | Role positions | Evaluator response |
|---|---|---|
| QA-8 Importance 70 -> 80 | SH1 proposed for revenue reconciliation; SH3, SH4 and SH5 supported for incident/recovery evidence. SH2 accepted original70 provided receipt evidence remains core QA-2. | Accepted for final prioritization, Difficulty90 retained; original score/history preserved. No requirement scope change or receipt guarantee inferred. |
| QA-5 Difficulty 60 -> 70 | SH4 proposed because emergency key/session trust and in-flight policy are unresolved; other roles did not propose a change. | Accepted for final prioritization; Importance100 retained. This is evaluator judgement informed by role feedback, not a vote result or measured effort. |

All stakeholders explicitly retained hypothetical numeric stress/recovery proposals as unapproved. Initial high-level driver priorities remain unchanged. Importance/difficulty sum does not determine the top-five selection.

## Presentation of results

The final report, ranked pool and ballot record were returned to all five roles for closing review on 2026-10-20. Every role confirmed its votes and concerns were represented and requested no material correction. These responses confirm faithful documentation only; they do not constitute actual business approval, a new vote or runtime evidence.

| Role | Closing response |
|---|---|
| SH1 | Confirmed S-01..05 ballot and QA-8 score proposal; pricing correctness, activation compensation, CMS convergence and legacy fencing remain. Nonselected S-01 retains analysis; T10 preserves the concern about worker starvation. |
| SH2 | Confirmed S-02/03/04/06/07 and tie rules; receiver guarantees, producer epochs and replay expiry remain in S-03/S-04/RT2. Receipt evidence remains QA-2 even after QA-8 score change. Actual contracts/rehearsals still needed. |
| SH3 | Confirmed S-02/03/05/06/08, shared resource/storage/failover findings and QA-8 score change. S-06 selection by ID does not imply greater severity than S-08; operational targets remain unapproved until service selection/testing. |
| SH4 | Confirmed S-02/04/07/08/09, QA-5 Difficulty70 and QA-8 Importance80. Nonselected security/protocol scenarios retain analysis; replay authorization is existing policy, while key trust, in-flight boundaries and limited recovery privileges remain open. |
| SH5 | Confirmed S-03/04/05/09/10 and distinction between ballot ranking and analytical scores. Nonselected protocol/release cases retain gates for test fidelity, binary versus authority rollback and staffing. Buildability remains undetermined. |

## Documentation verification

The facilitator independently recalculated all 25 votes and the numeric-ID tie order; checked 14 final utility-tree leaves and their score increments/sums; confirmed analyses for all nine original and ten new scenarios; checked local Markdown links and balanced fenced blocks; and matched all ten frozen baseline hashes. No requirement or ADD artifact was changed. These are documentation checks, not implementation tests.
