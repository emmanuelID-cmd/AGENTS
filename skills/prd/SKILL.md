---
name: prd
description: Create or review a Product Requirements Document using the required PRD structure whenever a PRD is requested.
---

# Product Requirements Document

Invoke this skill whenever the user requests a PRD, product requirements document, product brief intended to guide a build, or an update/review of an existing PRD.

## How to use the template

Work from a copy of the requested template. Preserve its structure and intent, but remove instructional boxes, examples, and placeholder text from the completed PRD. Do not edit an original template in place.

Every PRD must contain these sections unless the user explicitly requests a different structure:

1. Problem — include the user, pain, context/root cause, consequence, and optional supporting context.
2. Opportunity — state what becomes possible and include market opportunity context where available.
3. Users & Needs — identify primary and secondary users and write needs as “As [user], I need to [goal] because [reason].”
4. Proposed Solution — explain the product as a whole in plain language, not as a feature list.
5. Value Proposition — state audience, problem, core action, differentiator, and benefit.
6. Top 3 MVP Value Props — one sentence each for the Vitamin, Painkiller, and Steroid.
7. Goals & Non-Goals — list outcome-oriented goals and explicit MVP exclusions.
8. Success Metrics — provide numeric targets connecting each goal to a signal, metric, and threshold.
9. Requirements — organize requirements by user journey and sub-journey. Write user-centered actions such as “User can [action]” and tag each `[P0]` must ship, `[P1]` important, or `[P2]` nice-to-have.
10. Appendix — include supporting research, competitive analysis, constraints, open questions, and links when useful; remove it when empty.

## Quality checks

- Separate the problem from the solution and outcomes from features.
- Ensure every goal has a numeric success target or an explicit open question.
- Ensure each requirement belongs to a journey and sub-journey and has a priority.
- Cover critical loading, empty, error, permission, accessibility, and recovery behavior where relevant.
- Keep assumptions, dependencies, risks, and unresolved questions visible.
- Confirm the delivered document contains no template directions or placeholder markers.

## Source

The structure is based on the supplied `Original PRD Template.md`, which is authoritative for section order and writing instructions when present in task context.
