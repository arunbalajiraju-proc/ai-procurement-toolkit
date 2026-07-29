# Governance and Safety

How to use these tools without creating a new problem.

## The core principle

Every tool in this repository prepares work for a human to judge. None of them judge. A routing result is not an approval, a gap analysis is not a reviewed contract, and a cost model is not a business case.

This matters more here than in most AI tooling, because the outputs touch contract positions, privacy obligations, and in the public sector, decisions that affect people. An output that looks authoritative and is wrong does real damage.

## Where human review is not optional

| Output | Who owns it |
|---|---|
| Data tier classification | Privacy |
| Decision level classification | The accountable business owner, in writing |
| Clause positions | Legal |
| Route and commercial path | Procurement |
| Anything routed Elevated or High | Legal, before it goes further |

The decision level is the one to be careful about. It is the input a regulator will ask about, and it is not procurement's to assert on someone else's behalf. Get it confirmed by the person accountable for the decision.

## Classification honesty

There is a natural pull toward the lighter governance track, because the heavier one is slower. Resist it.

Understating a data tier or a decision level does not remove risk. It moves the risk to a place where nobody is looking at it, and it puts the person who signed the classification in a difficult position later.

If you are between two tiers, take the higher one and let the reviewers argue it down.

## Public sector users

Where these tools reference governance requirements, they indicate what may be triggered. Confirming what actually applies to your organization is your responsibility.

Ontario public sector users should read tool outputs against the Responsible Use of Artificial Intelligence Directive and the joint IPC and OHRC Principles for the Responsible Use of AI. Where a directive and a tool in this repository disagree, the directive wins.

The six principles in that joint guidance, valid and reliable, safe, privacy protective, human rights affirming, transparent, and accountable, also make a workable evaluation criteria structure. Using them is more defensible than inventing your own framework.

## What not to put into an AI service

Do not paste confidential, supplier identifying, or personal information into an AI assistant unless your organization permits it and that specific service is approved for that class of information.

These tools are designed to work on anonymized input. Removing the vendor name, the contract value, and the internal timeline does not weaken the analysis.

For a live procurement, be particularly careful with anything that could identify a bidder, an evaluation position, or a negotiation stance. Indirect identifiers count. An unusual contract size or a distinctive timeline can be enough.

## Checking an output

Every skill has a Review Checks section. Use it. AI assistants produce confident output that is sometimes wrong, and these tools are no exception.

Two habits worth building:

Ask the assistant why it classified something the way it did. The reasoning exposes bad classifications faster than the classification does.

Put your name on anything that reaches a decision maker. It is a small thing that changes how carefully the output gets read before it is sent.
