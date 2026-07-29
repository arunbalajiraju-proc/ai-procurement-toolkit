# Calculators

Working spreadsheets. Download, enter your own numbers, get your own answer.

Every calculator in this folder has the same three sheet structure:

- **Inputs.** The only sheet you type in.
- **Results.** Calculated. Do not overwrite.
- **Notes.** Assumptions, and the date of any rate used.

If a result looks wrong, check the Notes sheet first. The assumption usually needs changing, not the formula.

## Available

None yet. The first calculator ships with post 2 of the Procuring AI series.

## Planned

| Calculator | What it answers |
|---|---|
| `token-cost-calculator.xlsx` | What will this workload actually cost per month, including reasoning tokens and cache effects |
| `reserved-vs-consumption-calculator.xlsx` | Should we commit to reserved capacity, and at what utilization does it break even |
| `finetune-hosting-cost-calculator.xlsx` | What does a fine tuned model cost to keep alive over 36 months |

## A caution on rates

Any pricing built into these calculators is a snapshot with a stated date. Model rates move quickly. Check the Notes sheet for the date, and verify against vendor documentation before a number goes into a business case.
