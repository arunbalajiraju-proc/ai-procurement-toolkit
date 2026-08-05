---
name: model-routing-skill
description: Classify AI workloads to the cheapest model tier that can do the job, size the cost difference, and produce a routing position to take into a vendor conversation. Use before negotiating an AI deal, when reviewing a vendor's model recommendation, when an AI bill is higher than forecast, or when a business case assumes a flagship model throughout.
parent: ai-procurement-toolkit
version: 1.0
language: en-CA
---

# Model Routing Skill

## Purpose

Vendors quote flagship models. Most enterprise work does not need one.

The gap between the top and bottom of a vendor's model ladder is twenty five to fifty times. The gap between two vendors' flagship models is around twenty percent. Procurement teams routinely spend their energy on the second number and never touch the first.

This skill takes a set of workloads, classifies each one to the cheapest tier that can actually do the job, estimates the cost difference, and produces a routing position you can put in front of a vendor or an internal technical team.

It exists because the largest cost lever in an AI deal is not a discount. It is an architecture decision, and it is usually made without procurement in the room.

## Parent Skill

Part of ai-procurement-toolkit. Runs after the buy has been routed by ai-buy-routing-diagnostic.md. Feeds the token-cost-calculator.xlsx, which turns the routing decision into a monthly number.

## When to Use

- Before any commercial conversation about an AI purchase
- When a vendor has recommended a model and you want to test the recommendation
- When an AI bill has come in higher than forecast
- When a business case assumes one model for every task
- When you are writing evaluation criteria and need to require tier justification from bidders

## Do Not Use

- To select a vendor. This routes workloads to tiers, not to brands
- To make the final technical decision. The output is a challenge to put to a technical team, not a replacement for them
- To assess whether a model is accurate enough for a task. That needs evaluation on real data
- Where the model choice is not yours to make, such as AI embedded in an application you already licence

## Required Inputs

1. A description of each workload, in plain language, saying what the task actually is
2. Estimated volume for each workload, as transactions per month
3. The vendor's recommended model and tier, if one has been given
4. The vendor's published rate card, or at least the rates for the tiers being considered
5. Whether outputs are reviewed by a person before use, and how thoroughly
6. Any latency requirement, meaning whether a user is waiting in real time

## Missing Information Rule

Do not guess. If volume, rates, or the review posture are unavailable, state which are missing and produce the routing with the cost sizing marked as indicative. Never produce a dollar figure from an assumed rate. If the review posture in input 5 is unknown, route conservatively, because an unreviewed output carries more risk from a weaker model.

## Workflow

### Step 1: Break the request into distinct workloads

Most AI requests are several tasks presented as one product. Separate them. A contract review assistant is usually extraction, then classification, then summarization, then drafting. Those are four workloads with four different tier answers.

List each workload separately before going further. If the request cannot be broken down, say so and route the whole thing at the highest tier any part of it requires.

### Step 2: Classify each workload by task type

| Type | What it involves | Typical tier |
|---|---|---|
| **Extraction** | Pulling named values out of a document. Dates, amounts, parties, clause presence | High volume |
| **Classification** | Sorting into categories. Routing, tagging, triage, flagging | High volume |
| **Search and retrieval** | Finding the relevant passage and returning it | High volume |
| **Summarization** | Condensing known content without adding judgment | Production |
| **Structured drafting** | Producing text to a known template or format | Production |
| **Comparison** | Setting two or more things side by side against defined criteria | Production |
| **Analysis with judgment** | Weighing factors, identifying what matters, reasoning about consequence | Flagship |
| **Novel reasoning** | Multi step problems with no established method, or genuinely ambiguous material | Frontier |

The test for the top two tiers is whether the task requires the model to decide what matters, rather than to apply a rule about what matters. Most tasks described as complex are actually applying a known rule to unfamiliar material, and that is production tier work.

### Step 3: Apply the risk adjustments

Move a workload up one tier if any of these is true:

- The output is used without human review
- The output feeds a decision about an identifiable person
- An error is expensive, difficult to detect, or difficult to reverse
- The source material is adversarial, meaning someone benefits from the model being wrong
- The task requires the model to say when it does not know, which weaker models do poorly

Move a workload down one tier if all of these are true:

- A person reviews every output before it is used
- The task has a verifiable right answer that a reviewer can check quickly
- Errors are cheap and visible
- Volume is high enough that cost matters more than polish

Never move a workload down more than one tier below its task type. Never move it below high volume tier if the output is unreviewed.

### Step 4: Test the vendor recommendation

If the vendor has recommended a tier, compare it to your Step 3 result. Where the vendor's recommendation is higher, ask directly:

- What specifically about this task requires that tier?
- Have you evaluated the tier below on this task? Show the results
- What is the measured accuracy difference on our material, not on a public benchmark?
- What does the cost difference look like across our full volume?

A vendor who cannot answer the second question has not tested the recommendation. They have defaulted upward.

### Step 5: Size the difference

For each workload, calculate the monthly cost at the vendor recommended tier and at your routed tier. Use the actual rate card. Show input and output separately, because output dominates.

Then produce the total across all workloads, and the difference as both a dollar figure and a percentage.

If token counts per transaction are unknown, state that the sizing is indicative and give the ratio between tiers instead of a dollar figure. A ratio is still useful and does not pretend to precision you do not have.

### Step 6: Identify the mixed routing design

Most workloads are not one tier. They are a cheap tier handling the majority of cases and an expensive tier handling the difficult minority.

Where this applies, describe it plainly. State what share of volume goes to each tier, what triggers escalation to the higher tier, and what the blended cost looks like against a single tier approach.

This is usually the single largest saving available, and it is almost never in a vendor's proposal.

### Step 7: Produce the routing position

Use the output format below.

## Output Format

**Executive summary.** Three sentences. How many workloads, where the vendor recommendation differs from the routed position, and the size of the difference.

**Workload routing**

| Workload | Task type | Vendor tier | Routed tier | Adjustment applied | Monthly volume |
|---|---|---|---|---|---|

**Cost comparison**

| Workload | Cost at vendor tier | Cost at routed tier | Difference |
|---|---|---|---|

State clearly whether figures are calculated from a real rate card or are indicative.

**Mixed routing opportunities**

For each workload where a split makes sense: the split, the escalation trigger, and the blended cost against single tier.

**Questions for the vendor**

The specific challenges from Step 4, written so they can be sent as written. Ordered by how much the answer would change your position.

**Questions for your technical team**

What procurement cannot answer alone. Cache hit rate, whether escalation logic is feasible, what evaluation has been run.

**What this does not tell you**

State plainly that tier routing is a cost position, not an accuracy judgment, and that the routed tier needs evaluation on real material before it is adopted.

## Review Checks

Before the output is used, confirm:

- Every workload has been separated properly, and a composite task has not been routed as one thing
- No workload has been routed down more than one tier below its task type
- No unreviewed output has been routed to the bottom tier
- Every dollar figure traces to a real rate card, with its date
- Where sizing is indicative, it says so in the output rather than only in the working
- The output does not claim an accuracy finding. It claims a cost position

## Human Review

This skill produces a challenge, not a decision.

A technical lead confirms whether the routed tier can actually do the task, which requires evaluation on real material. Procurement owns the cost position and the vendor questions. The business owner confirms the review posture in input 5, because routing depends on it and procurement cannot assert it on their behalf.

Do not adopt a routed tier in production on the strength of this output alone. Use it to require the evaluation that should have happened anyway.

## Guardrails

- Cost per token is the wrong metric. Cost per successful outcome is the right one. A cheaper model that needs more retries or more human correction is not cheaper. Say this in the output whenever a downward routing is recommended
- Do not route down where the output is unreviewed and affects a person. The saving is not worth the exposure
- Tokenizers differ between models. Two models at the same headline rate can produce different token counts for the same text. Where a routing crosses model families, note that the cost comparison needs re-checking against a real sample
- Rates change quickly. Any figure carries its date
- This skill assists a commercial position. It is not a technical evaluation and it is not legal advice

## Example User Request

```
Run the model routing skill on this.

A vendor has proposed an AI assistant for our contract team. They have
quoted their flagship model for everything.

The assistant does four things. It pulls key dates and values out of
incoming contracts. It flags which of our standard clauses are missing.
It produces a plain language summary of each contract for the business
owner. And it drafts a first pass negotiation position.

Volumes are roughly 800 contracts a month for the first three, and
about 150 a month for the drafting.

Every output is reviewed by a contract manager before it goes anywhere.

Their rate card: flagship is 5 dollars input and 25 output per million
tokens. Their production tier is 3 and 15. Their high volume tier is
1 and 5.
```

Expected response: four workloads separated, extraction and clause flagging routed to high volume tier, summarization to production, drafting to production with a note on the review posture, a cost comparison against the flagship quote across all four, at least one mixed routing opportunity on the drafting workload, and the specific questions to put back to the vendor about why flagship was quoted throughout.

---

*Part of the ai-procurement-toolkit. Works in any assistant that accepts a structured instruction file. This is a procurement and commercial tool, not legal advice.*
