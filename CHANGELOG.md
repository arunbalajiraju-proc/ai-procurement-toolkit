# Changelog

All notable changes to this project are recorded here.

This project uses semantic versioning. Tools are released alongside the Procuring AI post series, so minor versions generally correspond to a new tool.

## [0.5.0]

### Added

- `skills/vendor-terms-review-skill.md`. Reviews AI vendor terms against
  the six data rights, separates binding commitments from policy
  statements, tests indemnity conditions against the customer's actual
  workflow, and produces prioritized redline asks.

## [0.4.0]

### Added

- `skills/finetune-vs-rag-skill.md`. Tests whether a proposed fine tune
  is justified against a retrieval baseline, sizes the full thirty six
  month cost including hosting and retraining, and identifies what the
  vendor's quote left out.

## [0.3.0]

### Added

- `skills/model-routing-skill.md`. Classifies AI workloads to the
  cheapest viable model tier, applies risk adjustments for review
  posture and decision impact, sizes the cost difference against a
  vendor's recommendation, and produces the questions to send back.

## [0.2.0]

### Added

- `calculators/token-cost-calculator.xlsx`. Sizes an AI workload from
  transactions and token counts. Models input, output, and reasoning
  meters separately, with cache, batch, and residency levers, a lever
  comparison, and volume sensitivity.

## [0.1.0]

Initial release.

### Added

- `skills/ai-buy-routing-diagnostic.md`, the entry point tool. Routes an AI purchase to one of five commercial paths, sets a data and decision risk tier, names the load bearing clauses, and identifies triggered governance steps.
- `agent-skills/ai-buy-routing-diagnostic/`, the same skill in native Agent Skills format.
- `playbook/`, the reference material behind the tools.
- `guides/GETTING_STARTED.md`
- `examples/quick-start-prompts.md`
- Repository scaffolding: README, LICENSE, DISCLAIMER, CONTRIBUTING.

### Planned

See the series progress table in the README.
