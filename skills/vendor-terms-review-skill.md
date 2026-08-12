---
name: vendor-terms-review-skill
description: Review an AI vendor's terms, data processing agreement, or privacy documentation against the six data rights that matter in an AI deal, and identify which are absent, conditional, or stated as policy rather than contract. Use when a vendor sends terms, when comparing bidders on privacy posture, when a proposal answers data questions with a webpage link, or before any AI agreement is signed.
parent: ai-procurement-toolkit
version: 1.0
language: en-CA
---

# Vendor Terms Review Skill

## Purpose

Vendors address two of the six data rights clearly and hope nobody asks about the other four.

The two they answer are the ones customers ask about: whether they train on your data, and who owns the output. The four they tend to leave vague are human review, retention and residency, subprocessors, and the conditions attached to the intellectual property indemnity. Those four are where the exposure sits.

This skill reads a vendor's terms and reports, right by right, what is actually committed, what is merely stated as policy, what is conditional, and what is absent. It produces a gap list and the specific redline asks to send back.

It exists because the gap between "we do not train on enterprise data" as a marketing sentence and the same words as a contractual obligation is the entire job, and that gap is invisible unless someone looks for it deliberately.

## Parent Skill

Part of ai-procurement-toolkit. Runs after ai-buy-routing-diagnostic.md has set the data tier and governance track. Feeds ai-contract-gap-review-skill.md, which covers the wider clause set beyond data rights.

## When to Use

- A vendor has sent terms, a data processing agreement, or privacy documentation
- You are comparing bidders and need a like for like view of privacy posture
- A proposal answers data questions by linking to a webpage
- An existing AI arrangement is up for renewal and the terms have never been reviewed against these six rights
- AI features have been enabled in an application you already licence and you need to know what the existing agreement actually permits

## Do Not Use

- As legal advice or as a substitute for legal review. This prepares a gap list for counsel
- To assess technical security posture. That is a separate review
- To conclude that terms are acceptable. The skill identifies gaps, it does not clear an agreement
- Where no terms have been provided. If a vendor has only made verbal or slide deck claims, the finding is that there are no terms to review

## Required Inputs

1. The vendor's terms, data processing agreement, privacy policy, or trust centre documentation, as text
2. Which of those documents are contractually incorporated, and which are webpages the vendor can change
3. The data tier for this buy, from the routing diagnostic, or a description of what data will be involved
4. Whether personal information or personal health information is in scope
5. The jurisdiction and any residency requirement that applies
6. Whether this is a negotiated agreement or vendor standard terms offered on a take it or leave it basis

## Missing Information Rule

Input 2 decides how much of the review is meaningful. If it is unclear which documents are contractually binding, say so before reporting any finding, because a commitment in a non incorporated webpage is not a commitment.

Where a right is not addressed anywhere in the supplied material, report it as absent rather than inferring a position from surrounding language. Absence is a finding, and it is the most common one.

## Workflow

### Step 1: Establish what is actually binding

Before assessing any right, sort the supplied material:

| Category | Weight |
|---|---|
| Signed agreement, or terms incorporated by reference into one | Binding |
| Data processing agreement executed alongside | Binding |
| Documentation incorporated by an explicit clause naming it | Binding, but check whether the vendor can amend it unilaterally |
| Trust centre page, privacy policy, or FAQ with no incorporation | Not binding. A statement of current practice |
| Statements in a proposal, slide deck, or email | Not binding unless the proposal is incorporated |

Report anything in the bottom two categories as policy rather than commitment, however clearly it is worded.

### Step 2: Assess each of the six rights

For each right, find the governing language, and classify it.

**Right 1. Training on your inputs.** Is there a contractual commitment that customer inputs, including prompts, uploaded documents, and derived data, will not be used to train, fine tune, or improve any model? Does the commitment extend to subprocessors?

**Right 2. Training on your outputs.** Is the model's response to you covered by the same commitment? Many terms cover inputs and stop there.

**Right 3. Human review.** Under what circumstances may vendor personnel or contractors access customer data? What triggers it, how narrow is the trigger, is access logged, and is notice given where lawful?

**Right 4. Retention and residency.** How long is data retained, where is it processed, and where is it retained? Note that these can differ. Is deletion available on demand and on termination, and is it certified?

**Right 5. Output ownership.** Does the customer own outputs? Is that ownership unconditional, or is it made conditional on compliance with an acceptable use policy or other term?

**Right 6. Intellectual property indemnity.** Is there an indemnity for third party claims arising from outputs? What is the cap? What conditions attach, and would normal use of the product breach them?

Classify each right using this scale:

| Rating | Meaning |
|---|---|
| **Committed** | Clear contractual obligation, adequate scope, extends to subprocessors where relevant |
| **Partial** | Addressed but narrower than needed, or silent on subprocessors, or subject to a carve out |
| **Conditional** | Present but dependent on conditions that may not hold in normal use |
| **Policy only** | Stated in non binding material |
| **Absent** | Not addressed in the supplied material |

### Step 3: Test the indemnity conditions against real use

This step is separate because it is the most commonly missed failure.

An output indemnity is frequently conditioned on the customer using default safety settings and not modifying outputs. Almost every real workflow modifies outputs, because a person edits the draft before it is used.

Take the actual described workflow and walk it against each condition. Report plainly whether normal use would void the indemnity. A cap is irrelevant on an indemnity that has been voided on day one.

### Step 4: Check for unilateral amendment

Identify every term the vendor can change without agreement. Pay particular attention to:

- Acceptable use policies incorporated by a link
- Subprocessor lists maintained on a webpage
- Documentation incorporated by reference
- Service descriptions that define what is being purchased
- Any clause permitting changes on notice, with no termination right attached

A unilaterally amendable acceptable use policy is significant because it can make an existing use case a breach after signature.

### Step 5: Apply the data tier

Findings that are tolerable at a low data tier are not tolerable at a high one. Where personal or personal health information is in scope, mark any right rated Partial, Conditional, Policy only, or Absent as requiring resolution before signature rather than as a negotiation preference.

Note also that a vendor policy is not a control for the purposes of privacy legislation. Where lawful authority to disclose information to a processor is required, the control needs to be contractual, with audit and certified deletion.

### Step 6: Produce the review

Use the output format below.

## Output Format

**Executive summary.** Three sentences. How many of the six rights are adequately committed, which single gap creates the most exposure, and whether the agreement is signable at the applicable data tier without changes.

**Binding status of supplied material**

| Document | Binding, or policy only | Vendor may amend unilaterally |
|---|---|---|

**The six rights**

| # | Right | Rating | What the terms actually say | Gap |
|---|---|---|---|---|

Paraphrase the vendor's position. Quote only where the exact wording carries the meaning, and keep any quotation short.

**Indemnity conditions against your workflow**

The Step 3 walk through, stated plainly, with a clear conclusion on whether normal use would void it.

**Unilaterally amendable terms**

The Step 4 list, with the consequence of each.

**Redline asks**

Written so they can be sent as written, ordered by exposure. Separate them into:

- Must have before signature
- Should have, worth pushing for
- Nice to have, trade away if needed

**Questions for the vendor**

Where the terms are ambiguous rather than absent, the specific questions that would resolve them.

**What this review does not cover**

State plainly that this is a data rights review, not a full contract review, not a security assessment, and not legal advice.

## Review Checks

Before the output is used, confirm:

- Every rating traces to specific language in the supplied material, or is reported as absent
- Policy statements have not been recorded as commitments
- Subprocessor scope has been checked on rights 1 and 2, not just the headline commitment
- Retention and processing locations have been assessed separately
- The indemnity conditions have been tested against the described workflow, not assessed in the abstract
- Nothing has been rated Committed on the strength of a trust centre page
- The output does not state that the agreement is acceptable. It states what the gaps are

## Human Review

This skill prepares a gap list. It does not clear an agreement.

Legal owns every clause position and the final assessment. Privacy owns the data tier, the residency determination, and whether the arrangement supports lawful disclosure. Procurement owns the negotiation sequence and which asks are traded.

Where the review finds gaps at a high data tier, the output goes to counsel before it goes to the vendor.

## Guardrails

- A policy is not a contract term. Rate it as policy however clearly it is worded, and say why the distinction matters
- Do not infer a commitment from silence, from a security certification, or from a vendor's reputation
- Attack indemnity conditions before arguing about the cap. An indemnity voided by normal use is not an indemnity
- Never advise that terms are acceptable or that an agreement may be signed. That is not this skill's role
- Where the vendor is offering standard terms with no negotiation, say so, and note that the remaining decision is whether the use case can be adjusted to fit the terms rather than the reverse
- This skill assists a review. It is not legal advice and does not create a solicitor client relationship

## Example User Request

```
Run the vendor terms review skill on this.

We are buying an AI tool that will process case notes for our client
services team. Case notes contain personal information about
identifiable individuals.

The vendor has sent their standard terms of service and pointed us to
their trust centre page for anything about data handling. They have
said in an email that they do not train on customer data.

Their terms say the customer owns outputs, subject to compliance with
their acceptable use policy, which is linked rather than attached.

Their indemnity covers third party intellectual property claims arising
from outputs, capped at fees paid in the preceding twelve months,
provided the customer has not modified the output.

Our caseworkers will edit every output before it goes into a file.

We are in Ontario and need processing to stay in Canada.

[paste the terms here]
```

Expected response: the trust centre page and the email classified as policy rather than commitment, training rights on inputs rated policy only and on outputs likely absent, output ownership rated conditional because it depends on a unilaterally amendable acceptable use policy, the indemnity walked against the caseworker editing step and found to be voided by normal use, residency assessed separately for processing and retention, and the whole review escalated because personal information is in scope.

---

*Part of the ai-procurement-toolkit. Works in any assistant that accepts a structured instruction file. This is a procurement and commercial tool, not legal advice.*
