# Hotel Pricing System - Iteration 1

Executed 2026-10-18 after preparation. Architecture sections 5-7 and 9 were instantiated in this iteration.

## Iteration Goal
Establish whole-system structure for an authorized hotel-to-price vertical slice.

## Drivers to Address
HPS-1/2/3/4; QA-5; CON-1/2/4/6; CRN-1/2/3/4.

## ADD Process Steps

### Step 2: Select drivers and goal
Follow iteration-plan iteration 1. Establish primary business workflow ownership and login before exposing hotel data.

### Step 3: Choose elements to refine
Refine the whole HPS into browser, application, durable storage and worker. Identity and enterprise systems remain external contracts.

### Step 4: Choose design concepts

| Concept | Pros | Cons | Discarded alternatives |
|---|---|---|---|
| Modular Java and Angular | Familiar stack, local transactions | Shared release and resource contention | Microservice per domain adds coordination before demand is known |
| Ports and adapters | Isolates protocols and test doubles | Mapping/interface overhead | Embedded HTTP/SDK logic in domain |
| Managed cloud storage/runtime | Less platform operations | Vendor limits and recurring cost need sizing | Self-managed orchestration without justification |
| Provider login/server scopes | SSO and no duplicate password ownership | Provider dependency | Custom identity or UI-only protection |

### Step 5: Instantiate and define interfaces

| Decision | Rationale |
|---|---|
| Context, container and application/browser component diagrams | Make boundaries and ownership explicit |
| Login sequence before session/configuration/permission contracts | Define trust and actor responsibilities |
| Separate worker execution from requests | CMS failure must not occupy browser request processing |
| Responsibility areas rather than assumed headcounts | Team roster unknown |

Pricing internals remain for iteration 2; external receipt for iteration 3. Architecture 7.1 and 8 define the initial security contracts.

### Step 6: Record decisions

| Driver | Decision | Rationale | Discarded alternative |
|---|---|---|---|
| CRN-1/2, CON-1/4/6 | D1 | Familiar modular foundation | Premature microservices |
| HPS-1, QA-5, CON-2 | D2 | Provider identity and server scopes | Local passwords |
| CRN-3/4, CON-4 | D11 | Explicit responsibility and gates | Unstaffed commitments |

### Step 7: Analyze achievement

| Driver | Analysis result |
|---|---|
| CRN-1/2 | Satisfied at design level: structure and familiar stack |
| CRN-3/4 | Partially satisfied: actual owners and sustained enforcement pending |
| HPS-1, QA-5 | Partially satisfied: login foundation; revocation/external access in iteration 4 |
| HPS-2/3 | Partially satisfied: responsibilities exist; transaction/query semantics next |
| HPS-4 | Partially satisfied: scoped configuration; activation semantics next |
| CON-1/2/6 | Satisfied at design level, provider/browser verification pending |
| CON-4 | Partially satisfied: small initial surface, capacity/scope unknown |

Whole-system structuring achieved. No runtime evidence claimed. Proceed to pricing and activation refinement.
