# AI Procurement Toolkit

An open set of tools for buying AI well: routing an AI purchase, sizing what it will actually cost, and finding the gaps in an AI contract.

Created by **Arun Balaji Raju** as part of the **Procuring AI** series.

## What this project is

Most organizations now have a library of guidance on how to *use* AI. Very few have anything on how to *buy* it.

AI is the first major technology category that does not procure like software. There is no seat count and no licence. You are buying metered compute, priced on a unit the vendor invented, where the same workload can cost several times more or less depending on engineering decisions that appear nowhere in the contract. A standard software agreement does not cover training rights on your data, output ownership, model deprecation, or who carries the risk when a model is confidently wrong.

This repository is a working toolkit for procurement professionals facing that problem. It contains two kinds of tool:

- **Skills.** Structured instruction files you run in an AI assistant. Give one your actual situation and it does the analysis.
- **Calculators.** Working spreadsheets where you enter your own numbers and get your own answer.

Everything here is designed to be used on a real buy, not read once and closed.

This is a companion project to [procurement-ai-assistant](https://github.com/arunbalajiraju-proc/procurement-ai-assistant), which covers using AI for procurement work. This repository covers procuring AI itself.

## Series progress

Tools are released alongside the Procuring AI post series. This table is updated as each one ships.

| # | Topic | Tool | Type | Status |
|---|---|---|---|---|
| 1 | AI does not procure like software | `ai-buy-routing-diagnostic.md` | Skill | Released |
| 2 | The token bill in plain English | `token-cost-calculator.xlsx` | Calculator | Released |
| 3 | Architecture beats the discount | `model-routing-skill.md` | Skill | Released |
| 4 | Inference is a bill, training is an annuity | `finetune-vs-rag-skill.md` | Skill | Released |
| 5 | The six data rights vendors hope you skip | `vendor-terms-review-skill.md` | Skill | Released |
| 6 | Reserved capacity, and where budgets die | `reserved-vs-consumption-calculator.xlsx` | Calculator | Planned |
| 7 | Your software contract has holes | `ai-contract-gap-review-skill.md` | Skill | Planned |

## Start here

If you have an AI purchase in front of you right now, run the routing diagnostic first. It tells you which commercial path applies, which clauses carry the risk, and which governance steps are triggered, before you spend effort on the wrong process.

- [`skills/ai-buy-routing-diagnostic.md`](skills/ai-buy-routing-diagnostic.md)

## How the toolkit works

```
An AI purchase request
   ↓
ai-buy-routing-diagnostic.md
   ↓
Classify the buy, the data, and the decision impact
   ↓
Route to one of five commercial paths
   ↓
Apply the cost, negotiation, and contract tools for that route
   ↓
Human review, legal review, and governance sign-off
   ↓
A decision someone can defend
```

The diagnostic is the entry point. The other tools are independent and can be used on their own once you know which route you are in.

## The five routes

Every AI purchase falls into one of these. They look similar and they are commercially very different.

| Route | What it is | Where the risk sits |
|---|---|---|
| Direct model access | Your team calls a model and builds on it | Rate protection, training rights, deprecation |
| Platform access | The same, through a cloud provider you already buy from | Reserved capacity, residency, drawdown treatment |
| An AI enabled application | A product whose value is the AI, sold as a subscription | The full data rights set, explainability, exit |
| Embedded AI | AI switched on inside something you already run | Unilateral terms changes, model substitution, no meter visibility |
| AI professional services | People building it, not a product | Ownership of what is built, whose model, handover |

The fourth route is the one most organizations miss. It arrives in a terms update rather than a purchase order, and the only leverage point is renewal.

## Quick start

1. Download this repository or the latest release.
2. Read [`guides/GETTING_STARTED.md`](guides/GETTING_STARTED.md).
3. Add the relevant skill file to your AI project or conversation.
4. Give it your actual situation, with sensitive details removed.
5. Review every output before it goes anywhere.

Skills in this repository are model agnostic. They work in Claude, ChatGPT, or any assistant that accepts a structured instruction file.

## Important boundaries

These tools support classification, analysis, cost modelling, and gap identification. They do not replace:

- Procurement judgment
- Legal advice
- Privacy, security, accessibility, or technical review
- A privacy impact assessment or an AI risk assessment
- Vendor selection or award approval
- Contract signature

A routing result is not an approval. A gap analysis is not a cleared contract. Every tool here is built to hand a human something better to judge, not to do the judging.

Do not upload confidential, supplier sensitive, or personal information into an AI service unless your organization permits it and that service is approved for that information.

Read [`DISCLAIMER.md`](DISCLAIMER.md) before using anything here on a live procurement.

## Repository structure

```
ai-procurement-toolkit/
├── README.md
├── LICENSE
├── DISCLAIMER.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── VERSION
├── skills/          # runnable instruction files
├── agent-skills/    # native Agent Skills folders
├── calculators/     # working spreadsheets
├── playbook/        # the reference playbook behind the tools
├── guides/
├── examples/
└── templates/
```

## Pricing and market figures

Any pricing, rate, or market figure in this repository is a snapshot with a stated date. Model lineups and token rates move quickly. Verify current rates against vendor documentation before any figure enters a business case.

## Contributing

Corrections, additional routes, and new tools are welcome, particularly from practitioners who have run an AI procurement and found something these tools miss. See [`CONTRIBUTING.md`](CONTRIBUTING.md).

## License

Released under the MIT License.

## Roadmap

- Complete the seven tools in the series table above
- Add a public sector governance mapping pack
- Add worked examples for each of the five routes
- Add an RFP requirements library for AI enabled applications
- Add sample vendor terms for practice runs
