# HPS ATAM Participation Record

Fresh rerun: 2026-10-23 through 2026-10-24, Asia/Seoul. This record replaces the current participation record; the previous run remains in [history](history/2026-10-20/participation.md). All participants are simulated agents. This is not actual stakeholder approval, acceptance of proposed targets, or executed test evidence. Only ATAM artifacts were revised; ADD and requirements remain frozen.

## Participants and preparation

| Participant | Role and work in this rerun |
|---|---|
| Root facilitator | Coordinated reviews, published concerns, recorded ballots and verified aggregation; no vote |
| Architecture designer | Rechecked the unchanged ADD baseline and challenged causal quality classifications; no vote |
| Architecture evaluator | Prepared Steps 1-3, identified approaches, scored initial scenarios, analyzed every scenario and consolidated findings; no vote |
| SH1 Revenue/pricing product owner | Pricing correctness and exceptional policy activation recovery |
| SH2 CMS/integration owner | Receipt ambiguity, receiver contract and legacy authority fencing |
| SH3 SRE/operations | Shared database capacity, query continuity and storage/recovery pressure |
| SH4 Security/identity owner | Current hotel authorization, key trust and safe recovery authority |
| SH5 Engineering/QA delivery lead | Protocol extension, faithful independent tests and feasible release/rollback |

The five stakeholder roles satisfy the user limit of five. Facilitator, designer and evaluator are evaluation roles and do not cast stakeholder votes. Sessions used existing role agents, with bounded simultaneous work.

On 2026-10-23 the designer reviewed D1-D14 and residual assumptions. The evaluator prepared the method and baseline in [preparation.md](preparation.md). Each stakeholder reread the baseline, reviewed the changed method and retained two candidates with clarified primary attributes. On 2026-10-24 all five reviewed the consolidated ten-candidate pool and Phase 1 analysis before casting fresh ballots. Stable scenario IDs preserve provenance, but historical ballots were not reused.

## Preparation and Phase 1 review

The designer distinguished functional price integrity from a named quality attribute, ordered-delivery head-of-line delay from a separate quality tradeoff, and administrative activation blockage from query unavailability. Ports improving both modifiability and testability are not opposing effects. Shared database resource competition alone does not establish a cross-attribute tradeoff. Current grant caching alone does not preserve queries when the same primary database is unavailable.

The evaluator therefore retained three formal tradeoffs: synchronous replication (QA-2 versus QA-1), durable unsampled publication evidence (QA-8 versus QA-1), and bounded known-key trust (QA-3 versus QA-5). Both key-trust options reject unknown keys and preserve token/session expiry. Four non-risks are bounded architectural responsibilities, not claims that implementation passed tests. All five stakeholder ballot reviews accepted these classifications and requested no initial score changes.

Initial I/D scores confirmed in this run: QA-1 100/90; QA-2 100/100; QA-3 100/80; QA-4 90/80; QA-5 100/70; QA-6 60/50; QA-7 60/50; QA-8 80/90; QA-9 70/60. These remain evaluator judgments, not measured outcomes or actual business priorities approved by humans.

## Phase 2 recap and consolidation

The Phase 2 recap reused Steps 1-6: method, drivers, architecture, approaches, initial utility tree and findings. [Scenario pool](scenario-pool.md) contains the ten newly reviewed use-case, growth and exploratory candidates with stimulus, environment, response and measures. Each has one primary attribute; related effects use existing QA IDs and are not extra utility-tree branches.

No exact duplicates were found, and all five roles confirmed retaining ten candidates. S-01 routine stale-preview/replay behavior differs from S-02 exceptional blocked activation. S-03 CMS receipt ambiguity differs from S-06 combined storage/telemetry/failover stress. S-04 receiver authority generations differ from S-10 artifact/schema and business rollback feasibility. New workload and recovery numbers remain hypothetical test proposals.

## Public fresh ballots - 2026-10-24

Each role cast five distinct votes, at most one per candidate. Blank influence from evaluator/designer is not counted. Ranking uses descending totals, then ascending numeric scenario ID.

| Candidate | SH1 | SH2 | SH3 | SH4 | SH5 | Total |
|---|---:|---:|---:|---:|---:|---:|
| S-01 | 0 | 0 | 0 | 0 | 0 | 0 |
| S-02 | 1 | 1 | 1 | 1 | 0 | 4 |
| S-03 | 1 | 1 | 1 | 0 | 1 | 4 |
| S-04 | 1 | 1 | 0 | 1 | 1 | 4 |
| S-05 | 1 | 1 | 1 | 0 | 1 | 4 |
| S-06 | 1 | 1 | 1 | 0 | 0 | 3 |
| S-07 | 0 | 0 | 0 | 1 | 0 | 1 |
| S-08 | 0 | 0 | 1 | 1 | 0 | 2 |
| S-09 | 0 | 0 | 0 | 1 | 1 | 2 |
| S-10 | 0 | 0 | 0 | 0 | 1 | 1 |
| Total | 5 | 5 | 5 | 5 | 5 | 25 |

Public ranking: S-02, S-03, S-04, S-05, S-06, S-08, S-09, S-07, S-10, S-01. The first five become new leaves; the initial nine remain, making fourteen final leaves. All ten candidates are analyzed regardless of votes, including zero-vote S-01.

### Ballot rationale and exchanges

| Role | Fresh choices | Rationale and response to other roles |
|---|---|---|
| SH1 | S-02, S-03, S-04, S-05, S-06 | Exceptional policy recovery and end-to-end/legacy integrity remain critical. Broad storage/failover impact moves S-06 ahead of routine S-01 compared with the archived ballot. Supports SH3 storage concern; retention/admission must be agreed with SH2 without deleting pending CMS evidence or live history |
| SH2 | S-02, S-03, S-04, S-05, S-06 | Receiver ambiguity and authority fencing require explicit contracts. Shared capacity and CMS drain move S-05 ahead of S-07 compared with the archived ballot. Query protection must not starve delivery; S-07 still needs analysis despite not receiving this role's vote |
| SH3 | S-02, S-03, S-05, S-06, S-08 | Permanent blockage, CMS backlog, hotel skew and compound storage failure create operational risk. Supports SH1/SH2 capacity concerns but independently retains S-08 because IdP/key failure can interrupt queries even when the DB is healthy; S-04 remains a cutover gate |
| SH4 | S-02, S-04, S-07, S-08, S-09 | Recovery authority, obsolete producers, revoked scopes, trust-window policy and protocol security parity matter. Supports SH3's independent IdP path and SH1/SH2 integrity concerns while retaining role-specific S-07/09. Current replay authorization is already required; uncertainty is policy/implementation evidence, not an intended bypass |
| SH5 | S-03, S-04, S-05, S-09, S-10 | Faithful CMS fixtures, delayed legacy traffic, mixed-load experiments, unchanged-core protocol extension and separate binary/business rollback expose feasibility. Supports SH3's S-08 concern even without a vote; tests must distinguish cached-key trust from token expiry and preserve authorization |

SH2's worker-concurrency concern can become a QA-2/QA-4 tradeoff only with explicit saturation and recovery assumptions. It is not added to the formal register without that causal evidence. SH3 likewise declined to label query/worker throughput allocation a formal cross-quality tradeoff. No role requested a new unnamed quality branch.

## Step 8 and closing presentation

The evaluator analyzes all nine initial scenarios and all ten candidate scenarios, with one architectural decision table and Trade-Off Map per scenario, and explicitly revalidates the initial nine against Phase 2 challenges. [Result](result.md) contains the ranked vote table, final fourteen-leaf tree, evidence limits, twelve risks, ten sensitivity entries, three formal tradeoffs and four scoped non-risks. The evaluation assesses quality suitability as conditional and buildability as undetermined until policies, contracts, resource estimates and planned experiments are resolved.

All five closing reviews and the designer consistency review were received on 2026-10-24. They acknowledge presentation and preservation of concerns; they do not approve the architecture for implementation or production.


| Closing reviewer | Confirmation and remaining boundary |
|---|---|
| SH1 | Fresh S-02..06 ballot and changed S-06 priority accurately preserved; pricing recovery and unselected S-01 retained. No material correction |
| SH2 | CMS contract, authority fencing, replay retention and delivery starvation concerns preserved; worker competition remains conditional. No material correction |
| SH3 | Shared DB, hotel locks, storage recovery, CMS backlog and unselected IdP failure path retained. Proposed operational numbers remain unapproved. No material correction |
| SH4 | Fresh S-02/04/07/08/09 ballot accurate; unselected security scenarios retained; current replay authorization distinguished from unresolved trust policy. Unknown keys rejected and token/session expiry unchanged. No material correction |
| SH5 | Fresh S-03/04/05/09/10 ballot accurate; unselected protocol/release scenarios retain parity, test fidelity, schema/business rollback and capacity gates. No material correction |
| Architecture designer | All nineteen analyses/maps and fourteen primary-matched leaves consistent with unchanged ADD. Three opposing-QA tradeoffs and four bounded non-risks supported. Durable evidence does not resolve exact timing. No material correction |

The facilitator checked arithmetic, per-role vote limits, tie ordering, primary-attribute consistency, local links and code fences. The evaluator and facilitator checked the ten requirement/ADD baseline hashes. No runtime quality tests were performed. The earlier method hash was discovered to differ from the current skill during final verification; the final preparation record identifies the current method version after rechecking its requirements. The previous evaluation remains separately archived.
