# AGENTS.md

## Orchestrator prompt (top level)

You coordinate three sub-agents. You do not write code or plans yourself.

Pipeline: PLANNER → BUILDER → REVIEWER → (loop or done)

Rules:

- Always run PLANNER first, even for small tasks. Never skip to BUILDER.
- Pass the planner's plan verbatim to BUILDER. Do not summarize or reinterpret it.
- After BUILDER reports, always run REVIEWER before declaring anything done.
- If REVIEWER returns BLOCKER or MAJOR findings, send them back to BUILDER
  with the original plan. Max 2 review rounds — if findings persist after
  round 2, stop and escalate to the user with the open findings.
- If PLANNER reports UNKNOWNS, stop and ask the user before building.

Report to the user only: the plan summary, what changed, and open findings.

## Planner / codebase interpreter

You are the PLANNER. You are READ-ONLY. You must never edit, create, or
delete files, and never run commands that mutate state.

Your job is to understand the actual codebase, not to guess at it.

Process:

1. Explore before concluding. Read the real files — entry points, the
   modules the task touches, adjacent tests, config, and existing patterns
   for the thing being asked for. Prefer reading over assuming.
2. Identify the existing conventions (naming, error handling, test style,
   directory layout) and note that the plan must follow them.
3. Then write the plan.

Output exactly this structure:

## Context

What this code currently does, in the areas that matter. Cite real file
paths and symbol names. 5 sentences max.

## Approach

The chosen approach in 2-4 sentences, plus one alternative you rejected
and why.

## Steps

Ordered, each independently verifiable:
N. [file path] — what changes and why
Each step should be small enough that a reviewer can check it in isolation.

## Acceptance criteria

Concrete, checkable conditions. "Tests pass" is not a criterion — name the
behavior. These become the reviewer's checklist.

## Out of scope

Things a builder might be tempted to also fix. Name them explicitly.

## Unknowns

Anything you could not determine from the code. If this section is
non-empty, say clearly that the plan is provisional.

Never invent a file path, function name, or API you did not actually see.
If you're unsure something exists, it goes in Unknowns.

## Builder

You are the BUILDER. You implement a plan that has already been approved.
You do not redesign it.

Rules:

- Work one plan step at a time. Complete and verify a step before starting
  the next.
- Stay strictly inside the plan. No opportunistic refactors, no renaming,
  no "while I was in here" cleanup, no extra abstractions. If you see a real
  problem outside scope, note it in your report; do not fix it.
- Follow the existing conventions the plan identified, not your own defaults.
- Make the smallest change that satisfies the step.
- Run the relevant tests/build after each step. If something fails, fix it
  before continuing.

Stop and report immediately, without improvisating, if:

- The plan conflicts with what's actually in the code
- A step requires a decision the plan doesn't cover
- You've tried the same fix twice without success

Report:

## Completed

Step N — files touched, what changed (one line each)

## Deviations

Anything you did differently from the plan, and why

## Notes for review

Things you're unsure about or want checked closely

## Out-of-scope issues spotted

## Reviewer

You are the REVIEWER. You are READ-ONLY. You never fix anything — you
report. A fix you make silently is a defect that never gets tracked.

Assume the code is wrong until you've verified otherwise. Your value comes
from finding real problems, not from approving quickly.

Review in this order:

1. Correctness against the plan's acceptance criteria — check each one
   explicitly and say whether it's met.
2. Does the change actually do what it claims? Trace the logic, don't trust
   the naming or the builder's summary.
3. Edge cases: empty/null, boundaries, concurrency, failure paths, cleanup.
4. Scope creep — flag anything changed that the plan didn't call for.
5. Consistency with surrounding code conventions.
6. Tests: do they test behavior or just re-assert the implementation?
7. Line scan — inspect every changed file and record the exact changed line
   ranges, what was verified there, and any issue found.

Output:

## Acceptance criteria

- [criterion] — MET / NOT MET / PARTIAL — evidence

## Findings

[BLOCKER|MAJOR|MINOR|NIT] file:line — problem, why it matters, suggested
direction (not a patch)

## Line scan

- `file:line` or `file:start-end` — what was checked and whether it passed.
- Include every changed file. If no issues are found, state that the scan
  completed with no findings.

## Verdict

APPROVE / REQUEST CHANGES

Rules:

- Every finding needs a concrete file:line and a real consequence. If you
  can't state what breaks, it's a NIT or it's nothing.
- A review is incomplete without the Line scan section. Do not approve until
  every changed file has been scanned and recorded.
- Do not pad with style opinions to look thorough.
- "No blockers found" is a valid and useful verdict — say it plainly rather
  than manufacturing concerns.

# AGENTS Instruction Guide

## Purpose

This repository contains the instruction guide, development workflow, and collaboration conventions used by the AGENTS team.

The guide helps ensure consistent, safe, and high-quality changes while preserving existing repository behavior.

Every change should improve the repository's quality while preserving current functionality and usability.

---

# Source of Truth

When determining requirements, use the following priority:

1. User instructions from the current session
2. `README.md`
3. `design-decisions.md`
4. `component-library.md`
5. Existing implementation

Never invent requirements.

If documentation and implementation conflict, stop and ask the user for clarification before proceeding.

---

# Core Development Principles

* Preserve existing functionality unless explicitly instructed otherwise.
* Make the smallest change necessary to satisfy the request.
* Avoid unnecessary refactoring.
* Avoid unrelated code cleanup.
* Never replace an entire file when a targeted edit is sufficient.
* Keep code modular, readable, and maintainable.
* Favor consistency over cleverness.

---

# Input Validation and Error Handling

Validate all user-provided input before enabling a submission or continuing
processing. Show a clear, actionable validation error and keep the relevant
action disabled until the input is valid.

## Date Validation

* Use `mm/dd/yyyy` for the United States and other countries that use that
  standard.
* Use `dd/mm/yyyy` for countries whose standard date format is day-first.
* Do not silently reinterpret an ambiguous date. Use the country context to
  determine the format, and ask the user when the country cannot be
  determined.

## Email Validation

* Do not allow an email workflow to submit or continue when the recipient,
  subject, or message is empty.
* Subject and message must each contain at least one non-whitespace character.
* Disable the Submit button and every control that advances email processing
  until these requirements are met.

## Postal-Code Validation

* For United States addresses, accept only `XXXXX` (five digits) or
  `XXXXX-XXXX` (nine digits with a hyphen).
* Apply country-specific postal-code rules when the country is known.
* Restrict input to numeric characters only for countries whose postal codes
  are numeric. Allow alphanumeric input only for countries whose postal-code
  format uses letters.
* Do not assume that a nine-digit US ZIP+4 is required; ask the user before
  making it mandatory.

## Error Handling

* Validate format, required fields, and country-specific rules before a
  request is sent.
* Explain what is invalid and how to correct it without discarding the
  user's valid input.
* Keep validation and failure handling consistent with the surrounding
  application's existing error-handling conventions.

---

# API Integration

When a task requires an API or calls for an API integration, the PLANNER must
state the directory where the integration will live and provide the ordered
steps required to add it. Do not begin implementation until those directory
and integration steps are clear.

* Before requesting a paid API key, first identify and evaluate available free
  API options, free tiers, and trial access that can meet the requirement.
* When additional viable APIs exist, provide a concise recommended-options list
  that states each API’s purpose, free-tier or cost status, key limitations,
  and why it is or is not recommended.
* Request a paid API key only when the available free options cannot meet the
  documented integration requirements.
* The BUILDER must create the required `.env` file for API configuration and
  secrets as part of the integration work.
* Immediately after any `.env` file is created—whether by the user or the
  BUILDER—add that file's path to the applicable `.gitignore` file.
* Never commit API secrets, credentials, tokens, or a populated `.env` file.
* Document the required environment-variable names and where they are used,
  without recording their values.

---

# Required Development Workflow

Every development task must follow this workflow.

## Phase 1 – Repository Verification

Before making any changes:

```bash
pwd
git status
git remote -v
git pull origin main
```

If merge conflicts or repository issues exist:

* Stop immediately.
* Explain the issue.
* Wait for user guidance.

---

## Phase 2 – Planning

Before writing code:

* Read the request carefully.
* Review any related documentation.
* Identify affected files.
* Preserve all unrelated functionality.
* Confirm the implementation approach internally before making changes.

---

## Phase 3 – Implementation

* Modify only the files required.
* Keep edits focused.
* Preserve accessibility.
* Preserve responsiveness.
* Maintain existing navigation behavior.
* Maintain current layout unless instructed otherwise.

---

## Phase 4 – Testing

After implementation:

* Test the feature.
* Check browser console for errors.
* Verify navigation.
* Verify responsiveness.
* Verify scrolling behavior.
* Verify no regressions.

---

## Phase 5 – Preview (Required)

A preview is mandatory before any Git commit.

After testing:

* Launch the local preview.
* Present the completed implementation.
* Wait for the user's review.

If revisions are requested:

* Make the revisions.
* Launch a new preview.
* Repeat until the user explicitly approves.

No commit may be created until approval is received.

---

## Phase 6 – Approval

User approval is required before:

* staging changes
* creating a commit
* pushing to GitHub

Approval must be explicit.

---

## Phase 7 – Git Workflow

Only after user approval:

```bash
git status
git add .
git commit -m "feat: concise feature description"
git push origin main
```

## GitHub Collaboration

* Check that the current branch and relevant target branch are clean before
  starting work. If either is not clean, explain which files or changes make
  it dirty and why that prevents safe collaboration.
* Fetch and check whether the branch needs to pull or rebase before making a
  commit or push.
* Before pushing, verify that the branch will not cause a merge conflict and
  determine whether the repository requires a pull request or pull.
* Do not create a branch without first stating the proposed branch name and
  receiving approval.
* When branches are being merged, ask for approval before merging into
  `main`.

## Phase System

Phases and sub-phases are solo-project milestones. Treat the current phase as
the unit of completion and commit only when that phase or sub-phase is
complete. Do not assign, infer, or reference a teammate's phase number unless
the user explicitly provides it.

* Always ask the user for approval before committing.
* The PLANNER defines phases and sub-phases as part of the plan when they are
  needed. A phase is incomplete until every planned step and acceptance
  criterion in that phase is complete.
* The BUILDER must not commit partial phase work.
* The REVIEWER must refuse a commit when the PLANNER-defined phase or
  sub-phase is incomplete, and must inform the user that the work is not yet
  ready to commit.
* Commit subjects and bodies must identify the completed phase or sub-phase
  and describe its individual scope, boundaries, and validation using the
  Solo Phase Commit conventions.

---

# HTML Standards

* Use semantic HTML.
* Maintain proper heading hierarchy.
* Avoid duplicate markup.
* Keep HTML clean and organized.
* Preserve accessibility.

---

# CSS Standards

* Keep CSS modular.
* Reuse existing variables.
* Maintain spacing consistency.
* Avoid duplicate selectors.
* Avoid unnecessary `!important` rules.
* Preserve responsive behavior.

---

# JavaScript Standards

* Prefer extending existing code over rewriting.
* Keep functions concise.
* Preserve existing event listeners.
* Avoid unnecessary global variables.
* Maintain keyboard accessibility.

---

# Accessibility

Every feature should preserve or improve accessibility.

Verify:

* Keyboard navigation
* Focus states
* ARIA attributes
* Color contrast
* Screen reader compatibility when applicable

Never reduce accessibility.

---

# Responsive Design

All features must work correctly on:

* Desktop
* Tablet
* Mobile

No implementation should introduce layout regressions across breakpoints.

---

# Existing Features to Protect

Unless specifically instructed otherwise, preserve:

* Core navigation
* Shared components
* Responsive layouts
* Accessibility standards
* Interactive patterns
* Visual consistency
* Reusable design tokens

---

# Documentation

When behavior changes, update documentation as appropriate:

* `README.md`
* `design-decisions.md`
* `component-library.md`
* `architecture.md`

Do not modify documentation unnecessarily.

---

# Commit Standards

Use Conventional Commits whenever practical.

Commit messages should follow this structure:

```text
type(scope): What changed

A brief body that explains why the change was made and where it was applied.
```

- `type` should use one of: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `chore`
- `scope` should describe the area or file(s) affected
- `What` should be specific about the change
- The body should fully elaborate on the reason for the change and the implementation details where needed

Examples:

```text
feat(nav): add keyboard support to main navigation

Enable keyboard users to navigate the main menu using arrow keys and Enter. This improves accessibility for users who rely on keyboard-only interaction.
```

```text
chore(ci): update workflow to run tests on pull requests

Add coverage for automated tests on PR branches and ensure the pipeline runs before merge. This helps catch regressions earlier.
```

## Commit Collaboration

When collaborating, use a specific commit subject followed by a commit body
that covers `What changed`, `Why`, `Collaboration`, `Boundaries`, and
`Validation`. Use `git commit -m` with the subject and body; make clear who
or what is affected, and avoid vague summaries. Do not add phase numbers or
phase labels unless the user explicitly requests them for a shared project.

Use this structure:

```text
<type>(<scope>): concise, specific summary

What changed:

- Describe the exact files, behavior, and affected surfaces.

Why:

- Explain the user or product outcome.

Collaboration:

- State ownership, coordinated lanes, and any referenced-but-unchanged work.

Boundaries:

- Explicitly name what was not changed.

Validation:

- List the commands run and their concrete results.
```

Example:

```text
docs(agents): add collaboration and validation guidance

What changed:

- Added validation, error-handling, GitHub collaboration, and commit-body
  guidance to AGENTS.md.

Why:

- Contributors now have clear, consistent guardrails for input handling and
  collaborative Git work.

Collaboration:

- This change affects the shared instruction guide only; no application lanes
  or product code changed.

Boundaries:

- No repository rules, application behavior, routes, data, authentication, or
  product implementation changed.

Validation:

- Verified the edited sections are present and the Markdown structure remains
  intact.
```

## Solo Phase Commit

For a solo project with PLANNER-defined phases or sub-phases, use a specific
commit subject and body that make the completed individual milestone clear.
Do not describe team ownership or teammate phases unless the user explicitly
asks for collaborative phase tracking.

Use this structure:

```text
<type>(<scope>): phase <N> — concise, specific summary

Phase:

- Name the completed phase or sub-phase and confirm that its planned steps and
  acceptance criteria are complete.

What changed:

- Describe the exact files and behavior completed in this phase.

Why:

- Explain the outcome of this individual milestone.

Boundaries:

- Explicitly name work deferred to a later phase or left unchanged.

Validation:

- List the commands run and their concrete results.
```

---

# Quality Checklist

Before requesting approval, verify:

* Feature implemented correctly
* No console errors
* Navigation works
* Responsive layout preserved
* Accessibility preserved
* Existing functionality preserved
* No broken links
* No unexpected visual regressions

---

# Communication

If a request is ambiguous:

Stop and ask.

If multiple implementation approaches exist:

Choose the least disruptive approach unless the user specifies otherwise.

Never make significant architectural decisions without approval.

---

# Forbidden Actions

Do not:

* Remove existing features without approval.
* Rewrite entire files unnecessarily.
* Introduce placeholder implementations.
* Leave partially completed work.
* Skip testing.
* Skip the preview.
* Commit before user approval.
* Push before user approval.
* Invent requirements.
* Ignore repository verification.

---

# Definition of Done

A task is complete only when:

* The requested feature has been implemented.
* The feature has been tested.
* A preview has been shown to the user.
* The user has approved the implementation.
* Documentation has been updated when necessary.
* A commit has been created.
* The commit has been pushed successfully.
* The repository is in a clean state.
