# AI / ML Procurement Playbook
### Commercial constructs, market map, negotiation levers, and contract review
**Version 1.0 | July 2026 | Buyer-side | Ontario public sector lens**

---

## How to use this playbook

| If you are... | Go to |
|---|---|
| Trying to understand what you are actually buying | Part 1 |
| Building a sourcing strategy or business case | Part 2, Part 3 |
| Writing an RFP or VOR requirement | Part 6, Appendix A |
| Sitting across the table | Part 7 |
| Reviewing a contract or MSA | Part 8, Appendix B |
| Doing a fast sanity check | Part 9 (red flags) |

---

# PART 1: WHAT YOU ARE ACTUALLY BUYING

There are five distinct commercial constructs. Vendors will blur them. Do not let them.

## 1.1 Token pricing

A **token** is roughly 4 characters of English text, or about 0.75 of a word. It is the vendor's invented billing unit. Everything is metered against it.

You are billed on two meters, at different rates:

| Meter | What it is | Rate posture |
|---|---|---|
| **Input tokens** | Everything you send: the prompt, the system instructions, conversation history, attached documents, tool definitions | Cheaper |
| **Output tokens** | Everything the model generates back | 5x to 6x the input rate across almost every vendor |

**Why this matters commercially:** a read-heavy workload (summarize this contract, answer questions about this policy) is far cheaper than a generation-heavy workload (draft this document, write this code) at the same total token count. Two use cases with identical "volume" can differ 4x in cost. Any vendor forecast that quotes you "tokens per month" without splitting input and output is either careless or managing you.

**The modifiers that change the real price (all of these are levers):**

| Modifier | Typical effect | Buyer note |
|---|---|---|
| **Prompt caching** | Repeated prompt prefixes bill at roughly 10% of the input rate. Cache writes cost slightly more than standard input (typically 1.25x) | Largest single cost lever for production workloads. Requires engineering discipline, not negotiation |
| **Batch / asynchronous processing** | Flat 50% off input and output, across every major vendor, for jobs that can wait up to 24 hours | Free money for non-urgent workloads. Stacks with caching |
| **Long context surcharge** | Some vendors double input price above a 200K token prompt. Others include the full window at flat rate | This is a genuine differentiator. Check per model, not per vendor |
| **Data residency / regional endpoints** | Roughly a 10% uplift for keeping inference in a named geography | Directly relevant to Ontario data residency requirements. Price it in from day one |
| **Reasoning / "thinking" tokens** | The model generates internal reasoning before answering. Billed at the **output** rate | This is the sleeper cost. Can be a large share of a request on hard tasks. Ask for it broken out |
| **Fast / priority modes** | Premium tier for lower latency, at a multiple of standard | Only buy if you have an SLA that requires it |
| **Server-side tools** | Web search, code execution, etc., billed separately (e.g. per 1,000 searches) | Separate meters. Get them all listed |

## 1.2 Inference vs training costs

These are two completely different cost structures and should never sit in one line item.

| | **Inference** | **Training / fine-tuning** |
|---|---|---|
| **What it is** | Running the model to get an answer | Adapting a model on your data |
| **Cost shape** | Ongoing, variable, scales with usage forever | One-time or periodic, capital-like |
| **Meter** | Per token | Per training token, plus hosting the resulting model |
| **The trap** | Volume creep. Nobody owns the meter | The **hosting fee**. A custom model often must sit on dedicated capacity, billed hourly whether you call it or not |
| **Who bears it** | Almost always you | Almost always you |
| **Procurement question** | What is our cost per transaction, per successful outcome? | What is the total cost to keep this model alive for five years, including retraining when the base model is deprecated? |

**The single most under-priced item in AI deals is the ongoing hosting cost of a fine-tuned model.** A vendor will happily quote you the training run. Ask what it costs to keep that model deployed and reachable for 36 months, and what happens to it when the base model is retired. Very often the answer is: you retrain, at your cost.

**Also note:** fine-tuning is frequently the wrong answer. Retrieval (RAG), prompt engineering, and caching solve most enterprise use cases at a fraction of the cost with none of the lock-in. If a vendor proposes fine-tuning early, ask them to justify it against a RAG baseline. This is a legitimate technical challenge you can put in an RFP.

## 1.3 Model licensing

Three archetypes. Know which one you are in.

| Archetype | What you get | Commercial character | Lock-in |
|---|---|---|---|
| **Proprietary API** (Claude, GPT, Gemini) | A right to call an endpoint. No model, no weights | Pure service. Terms of service govern | Moderate. Prompts are somewhat portable, tooling is not |
| **Open-weight** (Llama, Mistral, DeepSeek, Gemma, Qwen) | The weights themselves, under a licence | Software licence plus your own compute bill | Low on vendor, high on your own infrastructure |
| **Embedded in SaaS** (Copilot, Einstein, Joule, an AI feature in an EMR or CRM) | A feature, priced per seat or per credit | Looks like a normal SaaS deal, is not | Highest. You cannot see or change the meter |

**On open-weight licences: "open" is a marketing word, not a legal one.** Read the actual licence. Common restrictions that catch buyers out:
- Monthly active user thresholds above which you must negotiate a separate commercial licence
- Acceptable use policies incorporated by reference and unilaterally amendable
- Restrictions on using outputs to train competing models
- Naming and attribution obligations
- Field-of-use limits

Treat an open-weight licence review exactly like you would treat an OSS licence review. It is the same discipline.

**On embedded AI: this is where most public sector AI spend will actually land, and it is the hardest to govern.** When your ERP, CRM, or EMR vendor adds AI features, you inherit their model choices, their subprocessors, their data flows, and their pricing, usually via a unilateral terms update. You have no meter visibility. Your leverage is at renewal and nowhere else.

## 1.4 Data usage rights

This is the clause set that separates a competent AI buyer from an incompetent one. There are **six** distinct rights in play, and vendors routinely address two of them and hope you do not notice the rest.

| # | The right | The question to ask | Default you should demand |
|---|---|---|---|
| 1 | **Training on your inputs** | Will our prompts and uploaded data be used to train or improve your models? | No, contractually, for all data, with no opt-out required by us |
| 2 | **Training on your outputs** | Will the model's responses to us be used for training? | No |
| 3 | **Human review** | Will your staff or contractors read our data? Under what trigger? | Only on documented security or abuse trigger, with notice where lawful |
| 4 | **Retention** | How long is our data held, where, and by whom? | Zero-day or defined short retention, named region, deletion on demand and on termination, certified |
| 5 | **Output ownership** | Who owns what the model produces for us? | We do, unconditionally, including for derivative and downstream use |
| 6 | **Provenance and indemnity** | What was the base model trained on, and will you stand behind it? | IP indemnity for third-party claims arising from outputs, uncapped or at a high multiple, with defence obligations |

**The asymmetry to name out loud:** vendors want a broad IP indemnity from you and a narrow one to you. And note that most output indemnities are conditioned on you using their safety filters and not modifying outputs. Read the conditions. An indemnity you have voided by normal use is not an indemnity.

**Ontario-specific:** under FIPPA and PHIPA, you cannot lawfully hand personal or personal health information to a processor without authority and controls. "The vendor says they do not train on it" is not a control. You need it in the contract, with audit and deletion certification, plus a Privacy Impact Assessment on file. The IPC-OHRC *Principles for the Responsible Use of Artificial Intelligence* (January 2026) and the OPS *Responsible Use of Artificial Intelligence Directive* (effective December 2024) are the frameworks a regulator will assess you against. Build your requirements to map to those principles: valid and reliable, safe, privacy-protective, human rights affirming, transparent, accountable. That mapping is also a clean evaluation criteria structure.

## 1.5 Hyperscaler AI services

The three routes to the same models, and why the wrapper matters more than the token rate.

| | **AWS (Bedrock)** | **Microsoft (Azure / Foundry)** | **Google (Vertex)** |
|---|---|---|---|
| **Models** | Multi-vendor marketplace (Anthropic, Meta, Mistral, Amazon's own) | OpenAI models plus a growing multi-model catalogue including Anthropic | Gemini first-party, plus Anthropic and others |
| **Commercial wrapper** | AWS agreement, marketplace private offers, Savings Plans on underlying compute | EA / MCA, and consumption counts toward MACC | Google Cloud agreement, Committed Use Discounts |
| **Reserved capacity construct** | Provisioned Throughput, reserved model units, shorter commitment windows available | Provisioned Throughput Units (PTUs), 1-month or 1-year reservations | Provisioned Throughput, committed use discounts on underlying compute |
| **Key characteristic** | Model choice and flexible commitment terms | Governance and compliance stack, tenant boundary, ties into existing enterprise agreements | Owns the full stack, aggressive on caching and context pricing |
| **The real reason to choose it** | You are already on AWS and want model optionality | You are already on an EA and want the AI spend to draw down an existing commitment | You are already on GCP and have long-context or multimodal workloads |

**Three things every buyer needs to internalize about the hyperscaler route:**

1. **You are usually not buying cheaper tokens.** On several platforms the token rate matches the model vendor's direct rate. What you are buying is the commercial wrapper: existing paper, existing security review, existing procurement vehicle, and drawdown against a commitment you have already made. That is genuinely valuable. Just be honest that that is what you are paying for, and do not let a vendor sell it as a discount.

2. **Regional and data-residency endpoints carry a premium**, commonly around 10%. If Ontario data residency is mandatory for the use case, that is not optional spend and it belongs in the base case.

3. **Provisioned throughput is where the money gets wasted.** Reserved capacity is billed whether or not you use it. Industry break-even sits roughly around sustained high throughput for 8 or more hours a day, and benchmarking work consistently finds buyers who commit early run at 20% to 40% utilization. The correct sequence is almost always: consumption pricing first, measure 60 to 90 days of real production traffic, then convert only the proven steady-state load to reserved capacity, at renewal, when it also becomes a negotiation asset.

**The hidden costs on every hyperscaler bill that are not on the model price list:**
- Data egress (a RAG pipeline pulling from storage in a different cloud will bleed here)
- Vector database and retrieval infrastructure
- Monitoring, logging, observability
- Guardrails and content filtering, often a separate meter
- Networking and private connectivity
- Support tier uplift
- Idle fine-tuned model hosting

Teams that budget only for tokens typically land 15% to 40% over plan. Put a named contingency in the business case and say why.

---

# PART 2: MARKET MAP (as at July 2026)

**Standing warning:** this table has a half-life of about 90 days. Model families, prices, and tiers have moved repeatedly through 2026. Verify against the vendor's own pricing page before you put a number in a business case. Prices are USD per million tokens (MTok), standard rates before caching or batch discounts.

## 2.1 Frontier and flagship tier

| Model | Input | Output | Notes |
|---|---|---|---|
| Claude Fable 5 (Anthropic) | $10 | $50 | Top of Anthropic's lineup |
| GPT-5.5 Pro (OpenAI) | $30 | $180 | Extended-reasoning tier |
| GPT-5.6 Sol (OpenAI) | $5 | $30 | Current flagship tier |
| GPT-5.5 (OpenAI) | $5 | $30 | |
| Claude Opus 4.8 (Anthropic) | $5 | $25 | 1M context at flat rate |
| Gemini 3.1 Pro (Google) | $2 | $12 | Doubles above 200K input tokens ($4 / $18) |

## 2.2 Production / mid tier (where most enterprise workloads should live)

| Model | Input | Output | Notes |
|---|---|---|---|
| Claude Sonnet 5 (Anthropic) | $2 / $10 through 31 Aug 2026, then $3 / $15 | | Introductory pricing. Model your base case at the standard rate, not the intro rate |
| GPT-5.6 Terra (OpenAI) | $2.50 | $15 | |
| GPT-5.4 (OpenAI) | $2.50 | $15 | |
| Claude Sonnet 4.6 (Anthropic) | $3 | $15 | |
| Gemini 3.5 Flash (Google) | $1.50 | $9 | |

## 2.3 High-volume / low-cost tier

| Model | Input | Output |
|---|---|---|
| Claude Haiku 4.5 (Anthropic) | $1 | $5 |
| GPT-5.6 Luna (OpenAI) | $1 | $6 |
| GPT-5.4 nano (OpenAI) | $0.20 | $1.25 |
| Gemini 3.1 Flash-Lite (Google) | $0.25 | $1.50 |
| Gemini 2.5 Flash-Lite (Google) | $0.10 | $0.40 |

## 2.4 Open-weight

Llama (Meta), Mistral, DeepSeek, Qwen, Gemma. No per-token vendor fee. You pay for compute, engineering, and operations, and you carry the licence review. Economically attractive at very high sustained volume or where data cannot leave your estate. Economically poor at low volume, because you are paying for idle GPUs.

## 2.5 What the market map tells a procurement manager

1. **The frontier tier has converged.** Flagship input pricing across the majors clusters around $5. Output is where they differ. If your workload is generation-heavy, the output rate is your real price, and the spread there is meaningful.

2. **Tier choice beats vendor choice.** The gap between a flagship and a high-volume model is 5x to 25x. The gap between two vendors' flagships is maybe 20%. Any sourcing strategy that optimizes vendor selection before optimizing model routing is optimizing the wrong variable.

3. **Introductory pricing is a trap for a business case.** Model the standard rate. Note the intro rate as a timing benefit only.

4. **Tokenizers are not equal.** Some newer models produce roughly 30% more tokens for the same text than their predecessors. Two models at the same headline rate can have materially different effective costs. Ask vendors to benchmark on **your** representative text and quote cost per completed task, not cost per token.

5. **Cost per token is the wrong metric.** The right metric is **cost per successful outcome**. A model that costs 20% more per token but needs 40% fewer retries is cheaper. Make bidders prove this on your data.

---

# PART 3: SOURCING STRATEGY, THE FOUR ROUTES

| Route | When it wins | When it loses | Primary risk |
|---|---|---|---|
| **Direct from model vendor** | Earliest model access, simplest commercial structure, best rate transparency | No existing paper, new security review, another supplier to manage | Vendor concentration, no drawdown against existing commitments |
| **Via hyperscaler** | You have an EA / MACC / cloud commitment, need the governance stack, need residency controls | You pay for the wrapper and often do not get cheaper tokens | Over-committing to provisioned capacity too early |
| **Embedded in a SaaS product** | The AI is a feature of a system you already run, and the use case is narrow | You want meter visibility, model choice, or price leverage | Unilateral terms changes, zero cost transparency, deep lock-in |
| **Self-hosted open-weight** | Very high sustained volume, or data legally cannot leave the estate | You do not have the MLOps capability. Most organizations do not | You have quietly become an AI infrastructure operator |

**Recommended default for most enterprise and public sector buyers:** route through the hyperscaler you are already committed to, on consumption pricing, with a multi-model architecture, and defer any reserved capacity decision until you have 60 to 90 days of production telemetry.

---

# PART 4: BUILDING THE BUSINESS CASE

## 4.1 The cost model, in the order you should build it

1. **Define the transaction.** Not "AI for HR." Rather: "one benefits enquiry, resolved." That is your unit.
2. **Measure the token shape of one transaction.** Input tokens (prompt + system instructions + retrieved context + history), output tokens, thinking tokens. Get this from a pilot, not from a vendor's brochure.
3. **Multiply by volume.** Transactions per month, with a peak factor.
4. **Apply the modifiers.** Cache hit rate, batch-eligible share, residency uplift, model tier.
5. **Add the infrastructure layer.** Vector DB, retrieval, egress, monitoring, guardrails, support.
6. **Add the human layer.** Prompt maintenance, evaluation, review of outputs, incident handling. This is real FTE cost and it never appears in a vendor quote.
7. **Add contingency.** 15% to 40% is the observed gap between token-only budgets and actual bills. Name a number and defend it.
8. **Sensitivity test.** What happens at 3x volume? At half the assumed cache rate? If the model is deprecated in 12 months?

## 4.2 The questions the business case must answer

| Question | Why it matters |
|---|---|
| What is the cost per successful transaction? | The only number leadership should care about |
| What is the fully loaded cost if adoption is 3x the forecast? | AI adoption curves are steep and volume is elastic |
| What is our exit cost? | If prompts, tooling, and fine-tunes are vendor-specific, exit is a rebuild |
| What is the cost of the model being deprecated? | Model lifecycles are running 6 to 12 months. This is a recurring cost, not an edge case |
| What is our cost if we do nothing? | The honest baseline. Sometimes it is the right answer |

---

# PART 5: DUE DILIGENCE CHECKLIST

## 5.1 Commercial

- [ ] Full rate card, every meter, in writing, including server-side tools
- [ ] Price protection: what can change, with how much notice
- [ ] Discount structure: is it a rate discount, a volume tier, or a marketplace private offer
- [ ] Whether spend draws down against an existing cloud commitment
- [ ] Minimum commitments, and what happens to unused commitment
- [ ] Overage treatment and rate
- [ ] Currency and FX exposure (rates are quoted in USD)
- [ ] Billing granularity: can you attribute spend to a business unit, an application, a use case

## 5.2 Technical and operational

- [ ] Rate limits at your tier and how they scale
- [ ] Uptime SLA, and whether it has teeth or is a service credit fig leaf
- [ ] Latency commitments, if the use case needs them
- [ ] Model deprecation policy and notice period
- [ ] Version pinning: can you stay on a version you have validated
- [ ] Regions available and residency guarantees
- [ ] Benchmark results on **your** data, not a public leaderboard

## 5.3 Legal, privacy, and security

- [ ] All six data usage rights from Part 1.4, answered in writing
- [ ] Subprocessor list, and change-notification rights
- [ ] Security certifications (SOC 2 Type II, ISO 27001, ISO 42001)
- [ ] Sector-specific: HIPAA BAA, PHIPA agreement, as applicable
- [ ] IP indemnity scope, conditions, and cap
- [ ] Acceptable use policy, and whether it is unilaterally amendable
- [ ] Model card / system card and documented evaluations
- [ ] Bias and fairness testing evidence
- [ ] Alignment to OPS AI Directive and IPC-OHRC principles

## 5.4 Governance (public sector)

- [ ] AI risk assessment completed per the applicable directive
- [ ] Privacy Impact Assessment
- [ ] Use case registered / disclosed as required
- [ ] Human-in-the-loop design documented for any decision affecting a person
- [ ] Explainability: can you tell an affected person how the decision was reached
- [ ] Whistleblowing and challenge mechanism in place

---

# PART 6: RUNNING THE PROCUREMENT

## 6.1 Choose the instrument

| Situation | Instrument |
|---|---|
| Buying model access as raw capacity | Existing cloud vehicle or a marketplace private offer. Rarely worth a standalone competitive process |
| Buying an AI-enabled application | Full competitive process. This is a software procurement with AI-specific clauses layered on |
| Buying AI professional services | Existing consulting VOR arrangement, with AI-specific SOW terms |
| Enterprise-wide AI capability | A VOR arrangement, structured by category. This is where the leverage is |

**On VOR arrangements specifically:** an AI VOR is attractive because it lets you standardize the clause set once and reuse it across many second-stage calls. That is the real prize, more than the price. But structure it deliberately:
- Separate categories for model access, AI-enabled applications, and AI implementation services. They have nothing in common commercially.
- Bake the data usage rights, IP indemnity, model deprecation, and human-oversight terms into the **arrangement level** so that second-stage users cannot negotiate them away.
- Build in a rate-card refresh mechanism. A 3-year AI VOR on fixed 2026 rates will be embarrassing by 2027. Use a most-favoured-pricing or published-rate-card-tracking mechanism instead of fixed prices.
- Make model substitution a controlled change, not a unilateral vendor right.
- Explicitly reference the VOR arrangement in every second-stage document so that the arrangement terms clearly prevail over vendor standard terms.

## 6.2 Evaluation criteria that actually work

Do not score AI on features. Score it on the things that drive cost and risk.

| Criterion | Weight (indicative) | How to evaluate |
|---|---|---|
| Task performance on our data | 25% | Blind evaluation on a representative sample set that you build, not their demo |
| Cost per successful outcome | 20% | Their benchmark run, priced at their rates, on your sample. Not cost per token |
| Data usage rights and privacy posture | 20% | Against the six rights in Part 1.4. Pass or fail on the critical ones |
| Governance and transparency | 15% | Model card, evaluations, bias testing, explainability, alignment to the applicable directive |
| Operational maturity | 10% | SLA, deprecation policy, version pinning, support model |
| Exit and portability | 10% | What we get back, in what format, and what it costs to leave |

**Make the benchmark mandatory and make it blind.** Give every bidder the same 100 representative tasks with a defined output format and a defined scoring rubric. This single move does more for an AI evaluation than any amount of written response scoring, and it destroys the vendor's ability to sell you a benchmark leaderboard.

## 6.3 The price schedule

Never accept a single blended rate. Require this structure:

| Line | Unit |
|---|---|
| Input tokens, per model tier | $ / MTok |
| Output tokens, per model tier | $ / MTok |
| Cached input read | $ / MTok |
| Cache write | $ / MTok |
| Batch input / output | $ / MTok |
| Long context input / output (above threshold) | $ / MTok |
| Regional / residency uplift | % multiplier |
| Reserved capacity unit | $ / unit / hour |
| Reserved capacity, committed term | $ / unit / hour at 1-month and 1-year |
| Fine-tuning, training | $ / MTok |
| Fine-tuned model hosting | $ / hour or $ / month |
| Each server-side tool | Own unit |
| Support tier | $ or % |
| Professional services | $ / day by role |

Then require a **worked example**: total cost for a defined reference workload, showing every line. This is how you compare bids that use incompatible billing schemas. It is also how you catch the vendor who has quoted you a great token rate and buried the margin in hosting.

---

# PART 7: NEGOTIATION PLAYBOOK

## 7.1 Understand your actual leverage

Be honest with yourself. At the frontier model layer, your leverage is **low** if you are a small spender, because demand exceeds supply and the vendor has no reason to move. Your leverage rises sharply in three situations:

1. **Volume.** Meaningful annual committed spend gets you into private-offer territory. Benchmark work suggests committed buyers above roughly $250K annual spend see 15% to 30% off published rates.
2. **Commitment.** Not spend, but term and predictability. A vendor will pay for forecastability.
3. **Bundle position.** If the AI spend draws down an existing cloud commitment, you are negotiating your cloud agreement, not your AI agreement. That is a much stronger table. Routing through an existing commitment has been observed to unlock 10% to 25% more discount than a standalone deal.

**Reference value is real leverage in the public sector.** A named public sector logo, a case study, or a first-in-province reference has value to a vendor's go-to-market. Price it. Do not give it away for free in a "partnership."

## 7.2 The negotiation levers, ranked by value

| Rank | Lever | Realistic ask | Why it works |
|---|---|---|---|
| 1 | **Architecture, not price** | Route 70% of volume to a lower tier model | Worth 3x to 5x. No vendor can match this with a discount |
| 2 | **Caching and batch** | Engineer for them from day one | 50% to 90% on eligible volume. Free. Not a negotiation |
| 3 | **Draw down an existing commitment** | Route the spend through the EA / MACC / cloud agreement | Converts an AI negotiation into a leverage-rich cloud negotiation |
| 4 | **Rate discount on committed spend** | 15% to 30% at meaningful volume, via private offer | Standard practice above the threshold |
| 5 | **Defer reserved capacity** | Consumption first, convert at renewal | Avoids the single biggest observed source of AI waste |
| 6 | **Price protection** | Rates fixed or capped for the term; automatic benefit of any list price decrease | Prices have been falling. Make sure you get the downside |
| 7 | **Data usage rights** | The full six from Part 1.4 | Costs the vendor nothing on a paid enterprise tier. Ask for all of it |
| 8 | **IP indemnity** | Uncapped or high multiple, defence obligation, few conditions | Vendors have competed on this. Use that |
| 9 | **Model deprecation protection** | 12-month minimum notice, version pinning, migration support at vendor cost | Rarely offered. Ask anyway. Deprecation cycles are short |
| 10 | **Credits and pilot funding** | Proof of concept credits, migration credits, co-funded implementation | Widely available, rarely asked for |
| 11 | **Reference and logo rights** | Paid for, not given | Public sector logos have go-to-market value |
| 12 | **Benchmarking rights** | Right to publish or share evaluation results | Vendors often prohibit this. Push back. You cannot govern what you cannot measure |

## 7.3 Vendor plays and your counters

| Vendor play | What they are doing | Your counter |
|---|---|---|
| "Everyone is on the flagship model" | Anchoring you on the most expensive tier | Ask for the benchmark on the mid tier. Make them prove the flagship is necessary for your tasks |
| "Lock in PTUs now, capacity is scarce" | Manufacturing urgency to sell you idle capacity | Consumption first. Show me the telemetry. Convert at renewal |
| "Our rate is the same as buying direct" | True, and framed as a favour | Correct, so the wrapper is what I am buying. What else comes with it? |
| "We do not train on enterprise data" | A policy statement, not a contract term | Then you will have no difficulty putting it in the agreement, with all six rights covered |
| "Standard terms, take it or leave it" | Testing whether you know AI terms differ from SaaS terms | Cite the specific clause gaps. Vendors negotiate when you demonstrate you know what is missing |
| Discount tied to a 3-year commitment | Buying your optionality in a market where prices fall annually | Shorter term, or a benchmark / price-decrease clause. Prices are falling. A 3-year lock is a bet against the market |
| "Introductory pricing, act now" | Base-casing you on a rate that expires | Model the standard rate. The intro rate is a timing benefit, not a price |
| Bundling AI into an unrelated renewal | Using your renewal pressure on an unrelated buy | Separate the negotiations. Or accept the bundle and take a real price for it |
| Impressive public benchmark scores | Selling a leaderboard | Blind benchmark on our data or the score is not evaluated |
| "We will fine-tune a custom model for you" | Selling lock-in and a hosting annuity | Justify it against a RAG baseline. Then price 36 months of hosting |

## 7.4 The negotiation sequence

1. **Pilot on consumption pricing.** No commitment. Instrument everything.
2. **Measure for 60 to 90 days.** Token shape, cache rate, model tier mix, P95 throughput, cost per outcome.
3. **Do the architecture work before the commercial work.** Model routing and caching. Take the 3x to 5x first.
4. **Then go to the table**, with real numbers, at renewal or at a commitment event, where you have leverage.
5. **Negotiate terms and price together.** Do not settle the clause set and then talk about money. The clause set is worth money.
6. **Commit only the proven steady state.** Leave the peak on consumption.

---

# PART 8: CONTRACT REVIEW

## 8.1 The clause gap analysis

Your standard SaaS or IT clause set does **not** cover these. Every one of them needs to be drafted in.

| Clause | Buyer position | Common vendor position | Fallback |
|---|---|---|---|
| **Training on customer data** | Prohibited for all inputs, outputs, and derived data. Applies to subprocessors | "We do not train on enterprise data" as a policy, or opt-out | Contractual prohibition with audit right. This should be a walk-away item |
| **Human review** | Only on documented security or abuse trigger, notice where lawful, logged | Broad review rights for "service improvement" | Narrow the trigger, require logging, require notice |
| **Data retention** | Zero-day or short defined period. Named region. Deletion on demand and on termination, with certification | 30 days "for abuse monitoring," region unspecified | Define the period, name the region, require certified deletion |
| **Output ownership** | Customer owns all outputs unconditionally | Customer owns, subject to conditions and AUP compliance | Get ownership clean. Accept AUP compliance as a separate covenant, not an ownership condition |
| **IP indemnity** | Vendor indemnifies for third-party IP claims from outputs. Uncapped or high multiple. Defence obligation. Minimal conditions | Capped at fees paid. Conditioned on unmodified use of default safety settings | Push the cap up. Attack the conditions harder than the cap. A conditioned indemnity you void by normal use is worthless |
| **Accuracy / hallucination** | Vendor warrants the service performs materially per documentation. Customer accepts model outputs are probabilistic | Explicit disclaimer of accuracy, "as is" outputs | You will not get an accuracy warranty. Instead get: documented evaluation results, human-in-the-loop design, and clear allocation of who bears the consequence of a wrong output. Then price that risk |
| **Model deprecation** | 12-month minimum notice. Version pinning for validated versions. Migration support at vendor cost | 30 to 90 day notice, or silence | Get the longest notice you can. Get version pinning. Get migration credits |
| **Model substitution** | No substitution of the underlying model without notice and a right to re-validate | Vendor may change models at will | This is critical for embedded AI. A silent model swap can break a validated workflow |
| **Rate changes** | Fixed for the term, or capped. Automatic benefit of any list price decrease | Unilateral change on notice | The downside protection matters as much as the upside. Prices are falling |
| **Subprocessors** | Named list. Notice of change. Right to object | Link to a webpage, unilaterally amendable | Get notice and objection rights at minimum |
| **Acceptable use policy** | Fixed at signature, or changes require notice and give a termination right | Incorporated by reference, unilaterally amendable, on a URL | Do not sign a unilaterally amendable AUP that can retroactively make your use case a breach |
| **Audit** | Right to audit or receive independent assurance on data handling | SOC 2 report and nothing more | Report plus a right to a defined questionnaire process is a workable landing zone |
| **Transparency / explainability** | Vendor provides model card, documented evaluations, and enough information to explain outputs to a regulator or affected person | Trade secret objection | Required if you are a public body making decisions about people. Non-negotiable in that context |
| **Exit** | Full data return in usable format. Deletion certification. Transition assistance at defined rates | Data deleted 30 days after termination, no assistance | Define the format, the timeline, and the rates now, not later |
| **Benchmark publication** | Right to publish or share evaluation results | Prohibited | Push. You cannot govern what you cannot measure, and public bodies have disclosure obligations |
| **Liability cap** | Higher cap or carve-outs for data breach, privacy breach, and IP indemnity | Fees paid in prior 12 months, all-in | Carve-outs matter more than the headline cap on an AI deal, because the fees paid may be small while the exposure is not |

## 8.2 The five clauses to fight hardest for

If you can only win five, win these:

1. **No training on our data**, contractually, covering subprocessors.
2. **Output ownership**, clean and unconditional.
3. **IP indemnity** with the conditions attacked, not just the cap raised.
4. **Model deprecation notice and version pinning.**
5. **Price protection with downside benefit.**

## 8.3 The hallucination problem, stated plainly

No vendor will warrant that the model is correct. This is not vendor obstinacy, it is the nature of the technology. Stop trying to contract for accuracy. Instead:

- Allocate the risk explicitly. Who bears the consequence of a wrong output?
- Require human oversight by design, in the contract, for any decision affecting a person.
- Require documented evaluation results and the right to run your own.
- Require an incident and correction process.
- Price the residual risk and put it in the business case.

A contract that pretends the accuracy risk has been transferred to the vendor is worse than one that names it and manages it.

---

# PART 9: RED FLAGS

Stop and escalate if you see any of these:

| Red flag | Why |
|---|---|
| A single blended token rate with no input/output split | The vendor is either careless or hiding the output multiple |
| No mention of thinking or reasoning tokens in the forecast | Your bill will exceed the forecast |
| A reserved capacity commitment proposed before production traffic exists | The most reliable way to waste AI budget |
| Data usage rights answered by policy or a webpage, not by contract | A policy can change tomorrow |
| An IP indemnity with conditions you will breach through normal use | It is not an indemnity |
| A unilaterally amendable AUP incorporated by URL | Your use case can be made a breach retroactively |
| No model deprecation notice period | You will be forced to migrate at your cost, on their schedule |
| Vendor benchmarks only, on public leaderboards | Meaningless for your workload |
| Fine-tuning proposed before RAG has been tried | Usually selling lock-in and a hosting annuity |
| An AI feature appearing in an existing SaaS product via a terms update | You have just acquired an AI system with no governance |
| Prices quoted in USD with no FX treatment | Real exposure on a multi-year deal |
| The business case has no line for evaluation and human review FTE | The cost is real and it is being hidden |
| A 3-year price lock in a market where prices fall annually | You are betting against the market |

---

# APPENDIX A: RFP REQUIREMENTS LIBRARY

Drop-in mandatory and rated requirements. Adjust to your instrument.

### Mandatory (pass / fail)

1. The Proponent shall confirm that Customer Data, including inputs, outputs, and any derived data, will not be used to train, fine-tune, or improve any model, and shall confirm this obligation extends to all subprocessors.
2. The Proponent shall confirm that the Customer owns all outputs generated on the Customer's behalf.
3. The Proponent shall state all data storage and processing locations, and confirm ability to restrict processing to a named region.
4. The Proponent shall provide its current SOC 2 Type II report and any relevant certifications.
5. The Proponent shall provide a model card or system card for each model offered, including documented evaluations.
6. The Proponent shall confirm its model deprecation notice period and version pinning capability.
7. The Proponent shall provide a complete rate card covering every billable meter.
8. The Proponent shall complete the benchmark task set at Appendix [X] and submit results in the prescribed format.

### Rated

1. Describe your approach to preventing, detecting, and correcting inaccurate outputs, including any human oversight design.
2. Describe how a decision or output can be explained to a regulator or an affected individual.
3. Describe your bias and fairness testing methodology and provide results for the offered models.
4. Provide a worked cost example for the reference workload at Appendix [Y], showing every meter.
5. Describe how the Customer can reduce cost over the term, including caching, batching, and model routing, and what support you provide for this.
6. Describe your model roadmap, deprecation history over the past 24 months, and migration support.
7. Describe your data deletion process and certification.
8. Describe how your solution supports the Customer's obligations under the applicable AI governance framework.

### Vendor questionnaire, the ten questions that reveal the most

1. Split your forecast into input, output, and reasoning tokens for our reference workload.
2. What percentage of our input do you expect to be cacheable, and what is your basis for that?
3. What is the effective cost per successful outcome, on our benchmark set, at each model tier you offer?
4. Which of your models have you deprecated in the past 24 months, and what notice did customers receive?
5. Does the model you are quoting use the same tokenizer as the model we benchmarked?
6. What is billed if we send you a request and receive an error?
7. What is your uptime SLA, what is the remedy, and how many times have you missed it in the past 12 months?
8. Name every subprocessor that will touch our data.
9. Under what circumstances will a human at your organization read our data?
10. What does it cost us to leave, and what do we get back?

---

# APPENDIX B: CONTRACT REVIEW QUICK SHEET

Print this. Use it on every AI contract.

```
COMMERCIAL
[ ] Every meter has a rate                          [ ] Overage rate defined
[ ] Input/output split explicit                     [ ] Currency and FX addressed
[ ] Cache, batch, long-context rates stated         [ ] Price protection: fixed or capped
[ ] Residency uplift stated                         [ ] Downside benefit on list decreases
[ ] Reserved capacity terms and exit                [ ] Draws down existing commitment (Y/N)
[ ] Fine-tune hosting cost, 36 months               [ ] Minimum commitment and unused treatment

DATA RIGHTS  (all six, in the contract, not a policy)
[ ] No training on inputs                           [ ] Retention period and region
[ ] No training on outputs                          [ ] Deletion on demand + certified
[ ] Human review narrowed and logged                [ ] Extends to all subprocessors

IP
[ ] Output ownership, unconditional                 [ ] Indemnity conditions reviewed
[ ] IP indemnity present                            [ ] Indemnity cap acceptable
[ ] Defence obligation                              [ ] Base model provenance addressed

OPERATIONAL
[ ] Deprecation notice >= 12 months                 [ ] Rate limits stated
[ ] Version pinning available                       [ ] Uptime SLA with remedy
[ ] No silent model substitution                    [ ] Migration support and who pays
[ ] Subprocessor list + notice + objection          [ ] AUP fixed or notice + termination right

GOVERNANCE
[ ] Model card / documented evaluations             [ ] Human-in-the-loop designed in
[ ] Explainability sufficient for regulator         [ ] Bias testing evidence
[ ] Audit or assurance right                        [ ] Benchmark publication right
[ ] AI risk assessment complete                     [ ] PIA complete
[ ] Use case registered / disclosed

EXIT
[ ] Data return format and timeline                 [ ] Transition assistance rates
[ ] Deletion certification                          [ ] Exit cost quantified in business case

LIABILITY
[ ] Cap reviewed against actual exposure            [ ] Privacy breach carve-out
[ ] Data breach carve-out                           [ ] IP indemnity carve-out
[ ] Accuracy risk explicitly allocated
```

---

# APPENDIX C: GLOSSARY FOR STAKEHOLDERS

| Term | Plain language |
|---|---|
| **Token** | The billing unit. About 4 characters, or three quarters of a word |
| **Input token** | Text you send to the model. Cheaper |
| **Output token** | Text the model sends back. 5x to 6x the input rate |
| **Reasoning / thinking token** | The model's internal working-out before it answers. Billed as output. The sleeper cost |
| **Context window** | How much text the model can hold at once. Bigger is not free |
| **Prompt caching** | Reusing a repeated chunk of prompt at roughly 10% of the normal input price |
| **Batch API** | Send work now, get answers within 24 hours, pay half |
| **Inference** | Running the model. The ongoing cost |
| **Fine-tuning** | Adapting a model on your data. A one-off cost plus an ongoing hosting cost |
| **RAG** | Retrieval-augmented generation. Feeding the model relevant documents at question time instead of retraining it. Usually the cheaper answer |
| **PTU / provisioned throughput** | Reserved capacity, billed whether you use it or not |
| **Hyperscaler** | AWS, Microsoft Azure, Google Cloud |
| **Open-weight** | The model file is downloadable. Not the same as unrestricted |
| **Hallucination** | The model is confidently wrong. Not a bug you can contract away |
| **Model card** | The vendor's documentation of what a model is, was trained for, and was tested on |
| **Deprecation** | The vendor turns a model off. Currently happening on 6 to 12 month cycles |

---

**Sources and currency:** pricing in Part 2 verified against vendor pricing documentation as at July 2026. Governance references are the Ontario *Responsible Use of Artificial Intelligence Directive* (effective 1 December 2024) and the IPC-OHRC *Principles for the Responsible Use of Artificial Intelligence* (January 2026). Re-verify all pricing before it enters a business case. This playbook is a commercial and procurement guide and is not legal advice.
