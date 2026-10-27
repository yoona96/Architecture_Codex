# HPS ATAM Preparation

Fresh ATAM rerun started 2026-10-23 and finalized 2026-10-24, Asia/Seoul. Earlier evaluation is preserved under history/2026-10-20 and is not current participation evidence. This document records ATAM Steps 1-3 using the completed five-iteration ADD baseline. It is a document-based, agent-simulated evaluation, not a workshop with actual employees, approval by AD&D Hotels, implementation testing, or a production certification. Requirements and ADD files remain unchanged. Their statements that ATAM is subsequent describe the historical baseline; this evaluation is the subsequent record.

## Step 1: Present ATAM and evaluation rules

Method reference: [SEI ATAM collection](https://www.sei.cmu.edu/library/architecture-tradeoff-analysis-method-collection/), checked by the facilitator. Numeric 0..100 scoring, analyzing every scenario, adding the five vote winners and simulated agent participation are this workspace's explicit adaptation, not claims about mandatory standard ATAM rules.

The evaluator examines whether architectural decisions plausibly support required quality and whether the system is buildable with available resources. Phase 1 identifies approaches, builds the QA-1..9 utility tree and analyzes every initial scenario. Phase 2 reviews the baseline, collects use-case, growth and exploratory scenarios from five independent stakeholder roles, merges equivalent concerns, records public ballots, analyzes every candidate and presents risks, nonrisks, sensitivities and tradeoffs. The top five voted new scenarios are added to the utility tree. Analysis is not restricted to the winners.

Importance and difficulty use integers 0..100 in increments of 10. Importance anchors: 0 no material business impact; 50 meaningful supporting capability; 100 critical price integrity, revenue, access or continuity impact. Difficulty anchors: 0 trivial verified fit; 50 bounded conventional work with manageable dependencies; 100 unresolved cross-system or stringent feasibility constraint. Intermediate scores express evaluator judgement, not measured probability. Original High/Medium priorities are preserved as context; numeric scores refine them. Sum means Importance + Difficulty; it does not override the stakeholder vote ranking.

Each stakeholder may cast up to five votes, at most one per candidate, after viewing the merged pool and other roles' concerns. Rank by votes descending, then numeric scenario ID ascending. The evaluator and designer do not vote. Duplicate candidates merge only when stimulus, response and concern are equivalent; overlapping scenarios may remain separate. Proposed numeric targets in stakeholder scenarios remain proposals until business owners agree; original QA targets are not silently amended.

Risk means a decision or absence of one may cause a quality attribute to go unmet. A non-risk is a sound, well-justified decision requiring no architectural change in its explicitly bounded scope; it is not a passed test. A sensitivity point is a decision with high leverage over one named quality attribute. A tradeoff point is the same decision sensitive for at least two named quality attributes with opposite directional effects. All runtime evidence is absent. Existing validation-plan experiments are planned work, not executed results.

## Step 2: Present business drivers and participants

Replace the unreliable legacy pricing system for approximately 300 hotels, prevent financial loss, make prices quickly queryable and reliably delivered to CMS, and decouple failures and deployments. Priorities are HPS-2/3/4 and QA-1..5. Preserve browser access, cloud identity, existing proprietary Git, Java/Angular knowledge, initial REST integration, cloud-native preference, two-month MVP and six-month initial release. Calendar commitments cannot be established without kickoff, staffing, budget and agreed scope.

| Role | Evaluation responsibility and concern |
|---|---|
| Root facilitator | Orchestrates independent participation and records public exchanges; no stakeholder vote |
| Architecture evaluator | Authors preparation/result, analyzes decisions, assigns explicit provisional scores; no vote |
| Architecture designer | Presents D1..D14, explains baseline assumptions and answers challenges; no vote |
| SH1 Revenue/pricing product owner | Correct prices, usable configuration activation and rapid pricing changes |
| SH2 CMS/integration owner | Durable receipt, ordering, contract compatibility and legacy transition |
| SH3 SRE/operations | Query continuity, recovery, resource isolation, backlog and observability |
| SH4 Security/identity owner | Hotel scope, revocation, administrator control and safe recovery access |
| SH5 Engineering/QA delivery lead | Independent evidence, release/rollback and feasibility within delivery limits |

These are five simulated stakeholder agents selected by the facilitator, not named real people. Role sessions are scheduled sequentially as necessary under the four-active-agent limit; written scenarios and ballots preserve each role's contribution. Evidence of brainstorming, exchange and voting is recorded with the final result.

## Step 3: Present and freeze architecture baseline

Angular browser; modular Java API across zones; separately bounded worker pools; HPS-owned relational primary with synchronous standby; provider identity; transactional price/publication/task/receipt; REST CMS delivery and ports for future protocols. The same exclusive hotel mutation lock orders configuration, prices and publication sequences. Authoritative reads use complete primary-store snapshots. Activation is durable per-date work with temporary cross-date policy differences. Outbox, receiver deduplication/sequence/receipt, telemetry ledger, immutable promotions and controlled migration are key approaches. The designer is asked to review this mapping and residual assumptions before Phase 1 findings are closed.

Reviewed inputs: [drivers](../architectural-drivers.md), [architecture](../design/architecture.md), [preparation](../design/preparation.md), [iteration plan](../design/iteration-plan.md), all five iteration records and [validation plan](../design/validation-plan.md). Current normative requirement tables take precedence over older preparation comments embedded in drivers. All 26 drivers are in scope; QA-1..9 structure initial analysis, and functional/buildability concerns remain in findings.

| Baseline file relative to HPS | SHA-256 |
|---|---|
| architectural-drivers.md | E9417D698CE8A246D7D38526ADC90413CA3733227CCFAF81049ED00248303894 |
| design/architecture.md | 0894806A3B829D11F286767F6BF5EFB69EDD96635AD7524A4A0235B891A2D9CF |
| design/iteration-1.md | 90562BB6C46B21B8BBD94004EC262AD14499ED7DE4ABE1CB887F0CDC37034FF2 |
| design/iteration-2.md | 430D5469862DC16D543BD96AC455E4AE3E9E2C77000125CB5C53994608401D42 |
| design/iteration-3.md | 9BF83045CBE4E152A96D923ECC9017D962A48512446029F1C4C81A938DA97DE1 |
| design/iteration-4.md | 1EC1A291DD0587F1FCE2A44C0679C7D99B5CAC826B3C5DD241BE9415D946A72A |
| design/iteration-5.md | DAC0EA72D5B6C8CC215F64DC1094405B6287527D07FF2DE94705D90247842E14 |
| design/iteration-plan.md | FD6D37DB288DEC26908E8DF21DC908328B450FE61181F0A106B45EBD2AFBF133 |
| design/preparation.md | F2B34F86E46A8D14945024D92087C0C88FCE84E07DBACA3B9D3A9CD425CAE537 |
| design/validation-plan.md | 3B0980F7BD19B3F3D5F87E13876CAC1226E3991229D28A89206E88C015BB360F |

### Open decisions carried into evaluation

A1 timing/load/dimensions; A2 accepted change/outage/delivery deadline; A3 CMS receipt/deduplication/order; A4 SLA accounting/RTO/RPO; A5 query mix/peaks; A6 monetary/rule policy; A7 identity scopes/revocation; A8 telemetry scope/exact timing/retention; A9 resources/MVP; A10 legacy transfer/rollback; A11 test fidelity; A12 activation consistency and unrecoverable target; A13 cursor/replay retention. These are not approvals. No new procurement, infrastructure or implementation activity is undertaken by this evaluation.


## Current method baseline and classifications

Final verified evaluation skill SHA-256: `C03C18BC12F0D5AC013D8134723B83538544AD1769B021A097A80ED4583B10D7`; template: `7C627C231D3FD4F845C9ED1BFB55CD7D3036FC865566FBEF17FE41D3941EF960`. Initial and final utility trees include Sum. Every scenario receives Architectural Approach Analysis and a Trade-Off Map. Primary Attribute exactly matches its tree branch; Related quality effects reference the existing QA IDs; functional invariants and delivery constraints are separately labeled. No unnamed quality attribute is added.

A sensitivity is a decision with high leverage over one named quality attribute. A formal tradeoff is a shared decision sensitive for at least two named quality attributes with opposite directional effects. A cost, effort, simplicity or invariant concern alone is not a formal tradeoff in this evaluation. A non-risk is a sound justified decision needing no architectural change within its stated scope, not a blanket claim for every untested tactic. Structural causal evidence supports classifications; no effect size or target compliance is measured. A/B options explain consequences and do not authorize replacing the baseline or weakening requirements.

Fresh stakeholder proposals, review and public votes must be collected in this run; archived votes are not reused as current ballots. The current designer review and fresh stakeholder classification review are recorded in participation.md. The three formal tradeoffs are bounded by structural evidence; all five roles accepted the current primary classifications and scores on 2026-10-24.

## Current execution record

Steps 1-3 reused the frozen ADD documents; Step 4 recorded ten architectural approaches and reproduced the exact ADD container diagram. Steps 5-6 analyzed all nine initial scenarios with Sum and revised classifications. Five independent roles freshly reviewed ten candidates and cast 25 new public votes; Step 7 selected S-02/03/04/05/06 by the prescribed ranking. Step 8 analyzed all ten candidates, including unselected cases, and revalidated the nine initial scenarios. Step 9 presents risks, scoped non-risks, sensitivities, three formal tradeoffs, owner/evidence gates and conditional suitability/buildability conclusions in result.md. The facilitator records closing presentation in participation.md. Previous evaluation remains archived; no historical vote is presented as current.

### Final method-file recheck

The evaluator reread the complete current SKILL.md after final verification found a hash difference. Earlier read provenance was `362554731E83B2E70B5F18000E3DB31424822A9D036564634B989CF93FD60B8C`; the final verified current hash is `C03C18BC12F0D5AC013D8134723B83538544AD1769B021A097A80ED4583B10D7`. The current Trade-Off Map example names conflicting attributes rather than the earlier simplicity/cost examples. The report already uses named opposing quality attributes with direction and reason, and marks unestablished cases explicitly. All current requirements were checked: separate reviewed preparation; approach inventory; initial/final trees with Sum and 0..100-by-ten scores; all scenarios analyzed with per-scenario decision tables and maps; fresh public ballots, numeric tie order and five new leaves; structural evidence; and final presentation of risks, non-risks, sensitivities and tradeoffs. No analytical change was required. Template hash is unchanged. All five stakeholder closing reviews and the designer review accepted the report without material correction, as recorded by the facilitator.
