---
name: finetune-vs-rag-skill
description: Test whether a proposed fine tune is justified against a retrieval baseline, and size the full multi year cost of hosting a custom model. Use when a vendor proposes fine tuning, when a business case treats model training as a one time cost, when an AI proposal promises a model trained on your data, or before approving any spend on a custom model.
parent: ai-procurement-toolkit
version: 1.0
language: en-CA
---

# Fine Tune vs RAG Decision Skill

## Purpose

A vendor offers to train a model on your organization's documents. The training run costs a few hundred dollars. It sounds like a bargain.

What was not said is that a custom model is yours alone, so it needs its own capacity to sit on, and that capacity is billed by the hour whether or not anybody uses it. When the base model is deprecated, and current deprecation cycles run six to twelve months, you retrain at your cost. The one time project cost is a multi year obligation.

This skill does two things. It tests whether fine tuning is justified at all, against a retrieval baseline that is usually cheaper, more current, and more auditable. Then, where fine tuning is genuinely warranted, it sizes the full cost over the life of the arrangement rather than the training run alone.

It exists because fine tuning is the most commonly over sold item in an AI proposal, and because the cost that matters is almost never the one being quoted.

## Parent Skill

Part of ai-procurement-toolkit. Runs after ai-buy-routing-diagnostic.md has established the route. The cost outputs feed token-cost-calculator.xlsx for the inference side of the picture.

## When to Use

- A vendor has proposed fine tuning, or a model trained on your data
- A business case treats model training as a one time cost
- A proposal promises the model will learn your terminology, templates, or way of working
- You are comparing proposals where one includes a custom model and others do not
- An existing custom model is up for renewal and nobody has priced the alternative

## Do Not Use

- To assess whether a fine tuned model performs better. That requires evaluation on real material
- To design the technical solution. This tests a commercial proposition
- Where the model is embedded in an application and the training approach is not yours to choose
- As the only input to a decision. It produces a challenge and a cost picture for a technical team to answer

## Required Inputs

1. What the vendor says fine tuning will achieve, in their words
2. The quoted training cost, and what it covers
3. Whether the quote includes hosting the resulting model, and at what rate
4. The intended use case, described as a task rather than a product
5. How often the underlying knowledge changes, meaning the documents, policies, or data the model is meant to know
6. Expected volume, as transactions per month
7. Whether outputs need to be explainable, meaning whether anyone will have to say why the system produced a particular answer

## Missing Information Rule

Input 3 is the one that decides the answer, and it is the one most commonly absent from a proposal. If hosting cost is not stated, do not estimate it. Say plainly that the proposal is unpriced, and that no decision should be taken until the vendor states the hourly or monthly hosting rate and the minimum commitment.

If input 5 is unknown, treat the knowledge as changing, because that is the common case and it is the assumption that favours retrieval.

## Workflow

### Step 1: Establish what the fine tune is actually for

Fine tuning changes how a model behaves. Retrieval changes what a model knows. These are different problems and they are constantly conflated in proposals.

Classify the stated purpose:

| Stated purpose | What it actually needs |
|---|---|
| The model should know our policies, contracts, or documents | Retrieval. This is a knowledge problem |
| The model should use our terminology | Usually instructions, sometimes retrieval. Rarely fine tuning |
| The model should follow our template or output format | Instructions first. Fine tuning only if instructions have demonstrably failed |
| The model should match our house style or tone | This is a genuine fine tuning case, if the style cannot be described in instructions |
| The model should perform a specialized task no general model does well | A genuine fine tuning case, subject to evaluation |
| The model should be more accurate on our domain | Ambiguous. Requires evaluation to determine which approach helps |

If the purpose falls into the first three rows, the proposal is likely proposing the wrong technique. Say so directly and move to Step 5.

### Step 2: Run the retrieval baseline test

Answer each. Every yes strengthens the case for retrieval over fine tuning.

1. Does the model mainly need access to information rather than a change in behaviour?
2. Does that information change, whether monthly, quarterly, or on any cycle?
3. Would it matter if the system cited which document an answer came from?
4. Will anyone have to explain why the system produced a particular answer?
5. Is the body of knowledge large, meaning larger than could sit in a single prompt?
6. Would different teams need different subsets of the knowledge?
7. Is there a compliance or records requirement attached to the underlying documents?

Four or more yes answers means retrieval should be the baseline and the fine tune must justify itself against it.

### Step 3: Compare the two approaches

| | Fine tuning | Retrieval |
|---|---|---|
| What it changes | How the model behaves | What the model can see |
| Upfront cost | Training run | Building the retrieval layer |
| Ongoing cost | Dedicated hosting, billed whether used or not, plus inference | Inference only, and the repeated context is usually cacheable |
| Updating the knowledge | Retrain | Update a document |
| When the base model changes | Retrain from scratch | Change a setting |
| Explainability | The model knows it, and cannot show you where from | The source document can be cited |
| Access control | Baked in. Everyone gets the same model | Can be applied per user or per team at retrieval time |
| Lock in | High. The model is vendor specific | Low. The documents remain yours |
| Removing information | Requires retraining | Delete the document |

The explainability and removal rows matter disproportionately for public sector buyers. If an individual asks why a decision was reached, or exercises a right relating to their information, a fine tuned model is a difficult place to have put that information.

### Step 4: Size the full cost

Never compare a training run to a retrieval build. Compare total cost over the intended life, which should be at least thirty six months.

**Fine tuning total:**

1. Training run, as quoted
2. Hosting, at the stated rate, multiplied by the full period. If billed hourly, multiply by 730 hours per month
3. Inference cost on top of hosting, since hosting buys capacity, not usage
4. Retraining, at least once, on the assumption the base model is deprecated within the period. Use the vendor's stated deprecation notice if available, and note it if they will not state one
5. Engineering time for each retraining cycle
6. Evaluation after each retrain, because a retrained model is not the model you validated

**Retrieval total:**

1. Building the retrieval layer, as a one time cost
2. Vector storage and retrieval infrastructure, ongoing
3. Inference cost, with the repeated context largely cacheable
4. Maintenance of the document set, which is a real but modest ongoing effort

State both totals, and state the break even point if one exists.

### Step 5: Identify what was left out of the proposal

List every cost present in Step 4 that does not appear in the vendor's quote. This list is usually the most useful output of the whole exercise.

Flag in particular:

- Hosting cost, if absent or vague
- Minimum commitment or minimum term on the hosting
- What happens to the custom model at contract end. Can it be exported, and in what form
- Deprecation notice period for the base model
- Who pays for retraining
- Whether the custom model can be moved to another provider, and the honest answer is usually not

### Step 6: Produce the position

Use the output format below.

## Output Format

**Executive summary.** Three sentences. Whether fine tuning is justified, what the full cost is against the quoted cost, and the single most important thing missing from the proposal.

**Purpose classification**

What the vendor says the fine tune achieves, what that purpose actually requires, and whether they match.

**Retrieval baseline result**

The seven questions with answers, the count, and the conclusion.

**Approach comparison**

The relevant rows from Step 3 for this specific case, not the whole table.

**Full cost over thirty six months**

| Line | Fine tuning | Retrieval |
|---|---|---|

Show the quoted cost separately from the total, so the gap is visible.

**What the proposal does not price**

The Step 5 list. State plainly where a figure is unavailable rather than estimating it.

**Questions for the vendor**

Written so they can be sent as written. Lead with the hosting rate and the deprecation notice.

**Recommendation**

One of: retrieval baseline first, fine tuning justified subject to evaluation, or insufficient information to decide. Say which, and say what would change the answer.

## Review Checks

Before the output is used, confirm:

- The comparison is total cost over the full period, not training run against build cost
- Hosting has been included, or its absence has been flagged as unpriced
- At least one retraining cycle is in the fine tuning total, or the omission is justified and stated
- No cost has been estimated where the vendor has not stated it. Missing is reported as missing
- The recommendation does not claim a performance finding. Performance requires evaluation
- The explainability point has been raised where the use case involves decisions about people

## Human Review

This skill tests a commercial proposition. It does not test a model.

A technical lead confirms whether retrieval can actually meet the requirement, which needs evaluation rather than reasoning. Procurement owns the cost comparison and the vendor questions. Where explainability or information rights are engaged, privacy and legal own that assessment.

A recommendation of retrieval first should be taken as a requirement to evaluate both, not as a technical conclusion reached without testing.

## Guardrails

- Do not treat a fine tune as an accuracy improvement without evidence. It is a behaviour change, and whether it helps is an empirical question
- Do not compare a training run to anything. The training run is the smallest number in the arrangement
- A custom model that nobody calls still bills. Say this explicitly whenever hosting is priced hourly
- Where a vendor will not state a deprecation notice period, treat retraining within twelve months as the planning assumption and say why
- Fine tuning on personal information carries obligations that survive the model. Information placed in a model is difficult to locate, correct, or remove. Flag this whenever input data includes personal information
- This skill assists a commercial decision. It is not a technical evaluation and it is not legal advice

## Example User Request

```
Run the fine tune versus RAG skill on this proposal.

A vendor wants to fine tune a model on our procurement policies,
standard templates, and about eight years of past tender documents.
They say it will understand our way of working and reduce the time
our team spends drafting.

Training is quoted at 400 dollars. The proposal does not mention
hosting.

The use case is drafting first pass tender documents and answering
staff questions about our procurement rules.

Our policies get updated a few times a year. Templates change less
often.

We would run maybe 300 drafting requests and 2000 policy questions
a month.

Staff need to be able to point to the rule an answer came from.
```

Expected response: purpose classified as a knowledge problem rather than a behaviour problem, retrieval baseline test returning a high count, the proposal identified as unpriced because hosting is absent, a thirty six month comparison with the hosting line marked unavailable, the explainability requirement flagged as decisive given the citation need, and the hosting rate and deprecation notice as the first two questions back to the vendor.

---

*Part of the ai-procurement-toolkit. Works in any assistant that accepts a structured instruction file. This is a procurement and commercial tool, not legal advice.*
