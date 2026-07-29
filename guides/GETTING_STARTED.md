# Getting Started

This toolkit is built to be used on a real AI purchase. Ten minutes gets you a first result.

## Before you start

Take the sensitive material out. Vendor name, contract value, internal timelines, and anything that identifies a live procurement can be removed without weakening the analysis. These tools are designed to work on anonymized input.

Check your organization's position on what may be put into an AI service before you paste anything from live work.

## Running a skill

Skills are plain instruction files. There is nothing to install.

1. Open the skill file in the `skills/` folder.
2. Copy the whole file.
3. Paste it into a new conversation in Claude, ChatGPT, or any assistant that accepts a structured instruction file.
4. Below it, describe your situation. Each skill has an example request at the bottom showing the shape of input it expects.
5. Read the output against the Review Checks section of the skill before using it.

If you use Claude Projects or a custom GPT, add the skill file once as project knowledge and it is available to every conversation in that project.

## Installing as a native Agent Skill

The `agent-skills/` folder contains the same skills packaged in the Agent Skills folder format, each with a `SKILL.md` file. If your assistant supports that format, you can install them directly rather than pasting. Platform availability and administrator controls vary.

## Using a calculator

Calculators are spreadsheets. Download, open, and enter your own numbers in the input cells. Every calculator has:

- An input sheet, which is the only place you type
- A results sheet, which is calculated
- A notes sheet stating assumptions and the date of any rate used

Do not overwrite formula cells. If a number looks wrong, check the notes sheet first, because the assumption is usually the thing that needs changing rather than the formula.

## Which tool to use when

| Your situation | Start with |
|---|---|
| A request has landed and you do not know what it really is | `ai-buy-routing-diagnostic.md` |
| You need to know what a workload will cost | `token-cost-calculator.xlsx` |
| You are preparing for a commercial conversation | The model routing and reserved capacity tools |
| A vendor has sent terms | The vendor terms and contract gap tools |

If you are unsure, run the routing diagnostic first. It is the entry point and it tells you which of the others apply.

## Getting a better result

**Give the tool the real situation.** Vague input produces vague output. "A vendor wants to sell us an AI tool" gets you very little. Describing what the tool does, what data goes in, and what the output is used for gets you a usable analysis.

**Answer the questions the tool asks.** Most skills here will tell you what is missing rather than guessing. That is deliberate. Fill the gap and run it again.

**Do not accept the first output.** Push back on it. Ask the assistant why it classified something the way it did. The reasoning is often more useful than the classification.

**Check it against the source.** Every skill has a Review Checks section. It exists because these tools are run in AI assistants and AI assistants are sometimes confidently wrong.

## Boundaries

These tools prepare work for a human to judge. They do not approve purchases, clear contracts, or replace legal, privacy, or technical review. Read [`../DISCLAIMER.md`](../DISCLAIMER.md) before using any of them on live work.
