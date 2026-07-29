---
name: ai-buy-routing-diagnostic
description: Route an AI purchase to the correct commercial path, clause set, and governance track before any sourcing work begins. Use at intake, when a business unit asks to buy an AI tool, when an existing vendor enables AI features, or when a request has been logged as ordinary software and may not be.
parent: ai-procurement-toolkit
version: 1.0
language: en-CA
---

# AI Buy Routing Diagnostic

## Purpose

Most AI purchases arrive at procurement mislabelled. They come in as software, they get routed to a software process, and they inherit a software contract that does not cover training rights, output ownership, model deprecation, or who carries the risk when a model is confidently wrong.

This diagnostic sorts an AI request into one of five routes before any sourcing effort is spent. It tells you which commercial path applies, which clauses are load bearing, which governance steps are triggered, and what the next three actions are.

It takes about ten minutes and it is designed to be run at intake, not after a business case has already been written.

## Parent Skill

Part of ai-procurement-toolkit. This is the intake and routing layer. It hands off to the pricing, negotiation, and contract review tools in the same toolkit once a route is established.

## When to Use

- A business unit has asked to buy an AI tool or an AI enabled service
- An existing application vendor has announced or enabled AI features
- A request has been logged as ordinary software and you suspect it is not
- You are deciding whether a competitive process is warranted
- You need to know which governance assessments are triggered before committing effort

## Do Not Use

- To evaluate model quality or technical fit. This routes a buy, it does not select a product
- To replace a privacy impact assessment or an AI risk assessment. It tells you when those are triggered
- To produce a final contract position. It identifies which clause set applies
- As a substitute for legal review on any purchase it flags as elevated or high

## Required Inputs

1. What the business unit says they want to buy, in their own words
2. The vendor name and product, if known
3. What data will go into the tool
4. What the output will be used for, and whether it affects a decision about a person
5. Whether the organization has an existing cloud commitment or enterprise agreement
6. Whether the vendor is already under contract for something else

## Missing Information Rule

If any required input is unavailable, do not guess. State clearly which input is missing, route on what is known, and mark the routing as provisional. Missing input 4, the decision impact, always forces the highest governance track until answered, because that is the input that determines regulatory exposure.

## Workflow

### Step 1: Classify the buy

Ask what is actually being purchased. Select one.

| Code | The buy | Signal |
|---|---|---|
| A | Raw model access | The team wants to call a model through an interface programming interface and build something |
| B | Model access through a cloud platform | Same as A, but routed through an existing cloud provider |
| C | An AI enabled application | A product whose value is the AI, sold as a subscription |
| D | AI features inside an application already in use | Arrived through a terms update, a release note, or a renewal |
| E | AI professional services | People building or implementing something, not a product |

If more than one applies, run the diagnostic separately for each. A vendor selling an application with an implementation package is two buys, and they carry different risk.

### Step 2: Classify the data exposure

Select the highest tier that applies.

| Tier | Data going in |
|---|---|
| 1 | Public or non sensitive organizational information only |
| 2 | Internal commercial information, including vendor, pricing, or negotiation material |
| 3 | Personal information |
| 4 | Personal health information, or information about identifiable individuals in a vulnerable relationship with the organization |

### Step 3: Classify the decision impact

Select one.

| Level | The output |
|---|---|
| I | Informs internal work only. A human produces the actual work product |
| II | Informs a decision about a supplier, a process, or an organizational matter |
| III | Informs or influences a decision about an identifiable person |
| IV | Determines or substantially determines a decision about an identifiable person |

### Step 4: Test commercial control

Answer yes or no to each.

1. Can we see the consumption meter, whatever the unit is?
2. Can we choose or change the underlying model?
3. Can we get the vendor to commit to no training on our data, in the contract?
4. Do we know what it costs to leave, and what we get back?
5. Does this spend draw down an existing commitment we have already made?

Count the number of no answers. Three or more means low commercial control, and the leverage discussion moves to renewal.

### Step 5: Route

Read the route from the Step 1 code.

| Route | Applies to | Commercial path | The clauses that carry the risk |
|---|---|---|---|
| **A. Direct model access** | Code A | Usually not a competitive process on its own. Vendor paper, negotiated | Training rights, output ownership, rate protection, deprecation notice, indemnity conditions |
| **B. Platform access** | Code B | Existing cloud vehicle or a marketplace private offer | Same as A, plus reserved capacity terms, residency, and drawdown treatment |
| **C. AI enabled application** | Code C | Full competitive process. Treat as software procurement with an AI clause set layered on | The full six data rights, model substitution, explainability, exit |
| **D. Embedded AI** | Code D | No sourcing event exists. Leverage is at renewal only | Model substitution notice, unilateral terms amendment, subprocessors, the right to disable |
| **E. AI services** | Code E | Existing consulting vehicle with an AI specific statement of work | Ownership of what is built, ownership of prompts and configurations, whose model, whose data, exit and handover |

### Step 6: Set the governance track

Cross the data tier from Step 2 with the decision level from Step 3.

| | Level I | Level II | Level III | Level IV |
|---|---|---|---|---|
| **Tier 1** | Standard | Standard | Elevated | Elevated |
| **Tier 2** | Standard | Standard | Elevated | High |
| **Tier 3** | Elevated | Elevated | High | High |
| **Tier 4** | Elevated | High | High | High |

**Standard.** Normal software governance plus the AI clause set. Confirm training rights and output ownership in writing before signature.

**Elevated.** Everything in Standard, plus a privacy impact assessment, a documented AI risk assessment, named human review in the process design, and legal review of the indemnity conditions rather than only the cap.

**High.** Everything in Elevated, plus explainability sufficient to answer an affected person or a regulator, documented bias and fairness testing from the vendor, a named accountable owner, a challenge and correction mechanism, and disclosure or registration as required by the applicable directive. Do not proceed on vendor standard terms.

### Step 7: Produce the output

Use the format below. Keep it to one page.

## Output Format

**Executive summary.** Three sentences. What is being bought, which route it belongs to, and the single thing that most needs attention before this goes further.

**Routing result**

| Field | Result |
|---|---|
| Buy classification | |
| Data tier | |
| Decision level | |
| Route | |
| Governance track | |
| Commercial control | High, moderate, or low, with the count of no answers |
| Routing confidence | Firm, or provisional with the missing input named |

**Clause priorities for this buy**

List the clauses from the route table, ordered by what carries the most risk in this specific case, with one line each on why.

**Governance triggers**

List only the assessments and approvals actually triggered. Do not list everything that exists.

**What to do next**

Exactly three actions, each with an owner and a date. Not five, not ten. Three.

**Open questions**

Anything that could change the route if answered differently.

## Review Checks

Before the output leaves your hands, confirm:

- The buy classification matches what the vendor is actually selling, not what the business unit called it
- The data tier reflects the data that will realistically end up in the tool, including what users will paste in without being told to
- The decision level was set on the output's actual influence, not its intended influence
- Any code D routing has a named renewal date, because that is the only leverage point
- Nothing has been marked Standard that involves personal information and a decision about a person
- Every figure or vendor claim is sourced, not assumed

## Human Review

This diagnostic routes. It does not approve, clear, or assess.

A procurement professional confirms the classification. Privacy confirms the data tier. Legal owns the clause positions on anything routed Elevated or High. The accountable business owner confirms the decision level, in writing, because that is the input a regulator will ask about and it is not procurement's to assert.

Any output of this diagnostic that reaches a decision maker should carry the reviewer's name.

## Guardrails

- A route is not an approval. Nothing here clears a purchase
- Do not soften a data tier or a decision level to reach a faster track. The classification exists to be honest, and understating it moves the risk rather than removing it
- Code D is the most commonly missed route. AI features that arrive through a terms update are still an AI system the organization now operates, with governance obligations that attach whether or not a purchase order exists
- Where the applicable public sector AI directive and this diagnostic disagree, the directive wins
- This tool assists judgment. It does not replace legal, privacy, or accessibility advice

## Example User Request

```
Run the AI buy routing diagnostic on this.

Our HR team wants to buy a resume screening tool. The vendor says it
uses AI to rank applicants against the job posting. It would take in
applications submitted through our careers page, including everything
candidates upload. HR wants to use the ranking to decide who goes to
first interview.

We have an existing cloud commitment with one major provider but this
vendor is new to us.
```

Expected response: buy classification C, data tier 3, decision level IV, Route C, governance track High, commercial control assessed against the five questions, clause priorities led by the six data rights and explainability, governance triggers naming the privacy impact assessment and the AI risk assessment, and three next actions.

---

*Part of the ai-procurement-toolkit. Works in any assistant that accepts a structured instruction file. This is a procurement and commercial tool, not legal advice.*
