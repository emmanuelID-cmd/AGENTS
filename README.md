# AGENTS Instruction Guide

`AGENTS.md` is a reusable operating guide for AI-assisted and human software
work. It defines how a task is investigated, planned, implemented, reviewed,
validated, committed, and communicated. Its goal is to make changes reliable,
traceable, and easy to review without turning ordinary work into unnecessary
process.

This repository contains the guide itself. Copy or adapt `AGENTS.md` into a
project when you want contributors and coding agents to follow the same
development rules.

## What This Guide Is For

The guide is designed to prevent common sources of avoidable project risk:

- editing before understanding the existing codebase;
- making broad, unrelated refactors while completing a focused request;
- relying on assumptions instead of the repository's real files and patterns;
- declaring work complete without testing or review;
- committing or pushing changes before the user has approved them;
- exposing API credentials or committing environment files;
- creating confusing folder structures or placing unrelated files together;
- losing track of changed files, changed lines, and the reason for a change.

It is especially useful when multiple people, multiple agents, or both are
working in the same repository. The guide establishes a shared vocabulary for
planning, implementation, review findings, validation, scope boundaries, and
Git collaboration.

## The Core Workflow

Every task follows this sequence:

```text
Normal: PLANNER → BUILDER → SECURITY (when applicable) → REVIEWER → FIXER (when applicable) → REVIEWER

Completion: Project complete → BUDDY (conditional) → final audit or approved after-final work

TOKEN is a conditional cross-cutting advisor. It recommends model, reasoning,
speed, and token-conservation settings without replacing any workflow role.

Post-completion audit: BUDDY → ACCOUNTANT → SECURITY when a numerical anomaly
creates a reasonable security-risk condition → final REVIEWER or completion
verdict.
```

The sequence is intentional. The PLANNER reads before proposing work. The
BUILDER follows the approved plan without redesigning it. The REVIEWER checks
the actual result rather than trusting the builder's summary. If review finds
a blocker or major issue, the work returns to the BUILDER with the original
plan. When SECURITY applies, it performs two authorized inspection rounds
before the final REVIEWER. When REVIEWER reports incomplete acceptance or any
finding, FIXER attempts only eligible in-scope corrections before returning
the work to REVIEWER. After two unsuccessful review rounds, the open findings
are escalated to the user rather than silently worked around.

If the PLANNER cannot determine an important fact from the codebase, it must
record that fact as an unknown and stop for user guidance. This avoids invented
paths, APIs, functions, or requirements.

## Roles

### PLANNER

The PLANNER is read-only. It explores the real repository before writing a
plan, including relevant entry points, affected modules, nearby tests,
configuration, and established patterns.

Its plan identifies:

- the relevant current behavior and real file paths;
- the chosen approach and a rejected alternative;
- small, independently verifiable steps;
- concrete acceptance criteria;
- explicit out-of-scope work; and
- unknowns that require user direction.

The plan is evidence-based. A path, function, API, or convention must not be
named as fact unless it was actually inspected.

### BUILDER

The BUILDER implements one approved plan step at a time. It keeps changes
small, follows existing conventions, and verifies each step before moving on.
It does not opportunistically rename files, refactor unrelated code, introduce
new abstractions, or fix adjacent issues outside the plan.

If the plan conflicts with the real code, leaves a required decision open, or
the same attempted fix fails twice, the BUILDER stops and reports the problem.

### REVIEWER

The REVIEWER is read-only and never silently fixes issues. It verifies the
plan's acceptance criteria, traces the implemented behavior, considers edge
cases and failure paths, checks for scope creep, and evaluates whether tests
demonstrate behavior rather than merely repeat implementation details.

Every review reports whether each acceptance criterion is met and uses a
severity label for concrete findings. Findings include a file and line
reference, a real consequence, and a suggested direction—not a patch.

The reviewer also performs a line scan. Each changed file must be listed with
the relevant line or line range, what was checked there, and whether it
passed. A review is incomplete until this line scan is recorded.

### SECURITY

SECURITY is a conditional, defensive role. It runs after BUILDER and before
the final REVIEWER when a change involves authentication, authorization,
identity verification, payments, sensitive data, APIs, backend services,
databases, uploads, sessions, tokens, encryption, network access, privileged
features, deployment infrastructure, or external services.

SECURITY tests only the current project and explicitly authorized local,
staging, or test environments. It uses synthetic accounts and test data when
possible. It does not scan unrelated systems, use real identity documents,
expose private information, perform destructive exploitation, or claim that
all fake identities, VPNs, proxies, or bypass attempts can be detected.

The role performs two inspection rounds. The first records authorized security
findings for BUILDER remediation; the second repeats relevant checks and
verifies the fixes. A BLOCKER prevents approval, while a MAJOR finding needs
remediation or explicit user acceptance before commit. Untested controls must
be reported as untested, never as passed.

For URL and connection coverage, SECURITY inventories the project's routes,
links, API endpoints, callbacks, redirects, and authorized integrations, then
runs applicable unit, integration, or end-to-end checks for successful and
broken connections, timeouts, unavailable states, and malformed requests.
Each break is recorded in the protected security report.

When the project has an appropriate existing location, SECURITY may create a
protected project-local report or administrator-only route. It must not invent
or publicly expose a vulnerability dashboard. The report records scope,
environment, tests, passes, failures, warnings, leaks, authentication and API
findings, identity-test results, URL-connection results, remediation, alerts,
and a verdict of `SECURITY CLEAR WITHIN TESTED SCOPE`, `SECURITY WARNING`, or
`SECURITY BLOCKER`. When an authorized alert channel exists, confirmed or
suspected breaches and security bypass attempts generate alerts without
including secrets or sensitive request data; otherwise alerting is reported as
unavailable.

### FIXER

FIXER is conditional and runs after REVIEWER when an acceptance criterion is
`PARTIAL` or `NOT MET`, or when REVIEWER reports any `BLOCKER`, `MAJOR`,
`MINOR`, or `NIT` finding. It receives the original approved PLANNER plan and
the complete REVIEWER report. It may correct an eligible in-scope issue
without requesting another approval when the change is small, immediate,
consistent with existing patterns, and directly covered by the plan.

FIXER must not redesign the implementation, change acceptance criteria, hide
or downgrade findings, expand data usage or permissions, change a Phase or
Sub-Phase, or fix an out-of-scope issue. Out-of-scope findings require user
approval or a new PLANNER decision. FIXER returns
`FIXER BLOCKED — approval or planner decision required` when it cannot safely
proceed.

FIXER runs one bounded correction pass, validates its changes, and returns the
complete result to REVIEWER. A maximum of two FIXER/REVIEWER cycles is allowed
for one approved plan. FIXER never approves, stages, commits, or pushes. If it
changes security-sensitive code after SECURITY has completed, the affected
SECURITY checks must run again before the final REVIEWER.

### BUDDY

BUDDY is the conditional project-completion auditor. It activates only when
the user declares the project complete or approves a conditional BUDDY
hand-off. A conditional request first produces an alert and waits for approval.

BUDDY begins with a read-only audit of the complete authorized project. It
checks the repository baseline, routes, links, actions, forms, UI/UX,
responsive and accessibility behavior, APIs, backend, data boundaries, error
states, tests, security findings, cleanup candidates, and unsupported or
untested areas. Every action is reported as `PASSED`, `FAILED`, `PARTIAL`,
`BLOCKED`, `NOT TESTABLE`, or `NOT APPLICABLE`.

Normal BUDDY work uses an approved `after-final` branch. Conditional BUDDY
work uses an approved `BUDDY-Only` branch or an explicitly approved
`BUDDY-Phase-<number>` branch. The exact branch name must be approved before
creation, and the completed baseline must remain recoverable.

BUDDY may recommend cleanup, security, infrastructure, UI/UX, or workflow
changes, but it does not immediately implement redesigns. UI/UX recommendations
require user approval before changes are made. BUDDY must not automatically
create a mock-up, visual, flow chart, wireframe, or similar representation;
those are created only when the user explicitly requests or approves them.

BUDDY may evaluate and recommend changes to headers, navigation, typography,
spacing, white space, component size, section density, page length, cognitive
load, 30-second comprehension, visual hierarchy, responsive behavior, and the
project's original visual intent. Recommendations must include evidence and
preserve design tokens, accessibility, navigation, and responsive behavior
unless the approved plan explicitly changes them.

BUDDY may recommend dashboard graphs, charts, or data analysis, but must first
identify the data source, freshness, sensitivity, authorized viewers, empty,
loading, error, unavailable, mobile, and accessible states. It must not invent
metrics or expand approved data usage. Supabase or other database role
recommendations must use least privilege and must not create accounts,
policies, migrations, or privileges without approval. UI restrictions must be
checked separately from backend and database enforcement, including direct URL
and API access, row-level security, cross-user access, and administrative-tier
separation.

Approved UI, dashboard, authentication, database, and privilege changes record
their affected files, routes, roles, data impact, rollback method, and whether
SECURITY must run again before REVIEWER.

After the BUDDY plan is approved, proceed directly to BUILDER without
redesigning or replacing the approved plan. Approved implementation returns to
the normal SECURITY, REVIEWER, and FIXER workflow. BUDDY never approves its
own changes, commits, or pushes.

### ACCOUNTANT

ACCOUNTANT runs after every BUDDY completion audit as a read-only database and
authentication auditor. It returns counts and category labels, not names,
usernames, emails, account IDs, IP addresses, tokens, session IDs, biometric
data, raw authentication records, or private database rows.

Every report identifies the period, time zone, environment, baseline, data
source, and completeness. It counts accounts by status and tier, login and
authentication results, database and migration changes, role and permission
changes, RLS changes, and records inserted, updated, or deleted when those
numbers are available. It distinguishes `0`, `NOT AVAILABLE`, `NOT VERIFIABLE`,
and `PARTIAL`; unavailable data is never reported as zero.

ACCOUNTANT uses an authorized baseline, roster, provisioning record, role
inventory, or audit event to identify missing or deleted accounts. It does not
infer a breach or modify accounts, roles, permissions, policies, migrations,
schemas, rows, or audit logs.

If ACCOUNTANT finds an unexpected, unexplained, conflicting, or
security-relevant numerical change—such as account deletion, missing accounts,
admin-tier changes, privilege changes, RLS changes, unexplained data deletion,
authentication spikes, login glitches, or audit-log gaps—it sets a security
trigger and runs SECURITY before the final REVIEWER. ACCOUNTANT and SECURITY
remain read-only, and completion cannot be declared while the anomaly or
required security review is unresolved.

### TOKEN

TOKEN activates only when model or reasoning guidance would materially help,
such as for large, multi-agent, high-risk, or context-heavy work, or when the
user requests a recommendation. It recommends settings based on the actual
action and risk, using only models verified as available in the current
environment. The user's explicit model choice always takes priority.

TOKEN may recommend a model, reasoning level, speed, and scope without
changing them. Automation requires explicit user approval for a defined scope,
such as one action, one agent, one phase, the current project, or all approved
actions in the task. If model switching is unavailable, TOKEN reports that
manual selection is required.

When no change is recommended, TOKEN enters `TOKEN OFF`. When the user approves
a choice, TOKEN enters `TOKEN LOCKED` for that scope. It keeps the choice
consistent across related actions and agents; it does not repeatedly ask for a
change or bounce between models. TOKEN may reconsider only when the user asks,
the scope changes, the model becomes unavailable, task risk materially
increases, or the current model cannot complete the required work.

TOKEN must not conserve tokens by skipping required planning, security checks,
review, fixes, tests, line scans, approvals, or BUDDY safeguards. It must not
claim that a model change was automated when it was not.

## Development Standards

The guide keeps implementation work conservative by default:

- preserve current behavior unless the user requests a change;
- make the smallest change that satisfies the request;
- avoid unrelated cleanup and broad rewrites;
- preserve accessibility, responsiveness, navigation, and existing patterns;
- use semantic HTML and maintain appropriate CSS and JavaScript conventions;
- keep documentation current when behavior changes.

These rules are not an instruction to avoid improvement. They make sure each
improvement has a clear purpose, a limited scope, and evidence that it did not
break existing behavior.

## Files and Folder Organization

Files belong in directories that make their purpose easy to understand. Group
related work by feature or responsibility—such as routes, API handlers, shared
components, authentication, messaging, or profiles—rather than accumulating
unrelated files in one location.

Follow the repository's established structure first. A new organizational
pattern should only be introduced when there is a clear reason, and files for
one feature should not be scattered across unrelated folders without need.

## Input Validation and Error Handling

Input validation prevents invalid work from being sent to the application or
API. The guide requires clear, actionable validation errors while preserving
valid user input.

It includes rules for:

- country-aware date formats;
- email workflows that require recipient, subject, and message before
  submission;
- country-aware numeric and alphanumeric postal-code formats; and
- date-range handling.

General dates, start dates, and end dates cannot be after the current date.
When both start and end dates are present, the start date cannot be after the
end date and the end date cannot be before the start date. Date-only Follow-up
and Schedule fields are the explicit exception and may use a future date.

## API Integration and Secrets

When a task needs an API, the PLANNER must first identify the integration
directory and provide the ordered implementation steps. This makes API work
discoverable and prevents credentials or client code from being placed without
a clear home.

Before requesting a paid API key, contributors must evaluate free options,
free tiers, and trials. If more than one viable API exists, the plan should
provide a short recommended-options list explaining purpose, cost status,
limitations, and recommendation.

API configuration uses `.env` files for secrets and environment-specific
values. Whenever any `.env` file is created—by a user or a builder—its path
must immediately be added to the applicable `.gitignore`. Secrets, tokens,
credentials, and populated `.env` files must never be committed. Documentation
may name required variables and describe where they are used, but it must not
include their values.

API-dependent user experiences must account for these states:

- **Loading:** show the application's standard animated loading indicator.
- **Temporarily unavailable:** show this state when an API request fails.
- **Live:** show current API data when a request succeeds.
- **No internet access:** clearly explain that internet access is unavailable
  and direct the user to restore or enable it before retrying.

## Git and Collaboration

The guide separates safe local work from repository publication.

Before starting, check the repository and branch state. If a branch is dirty,
identify the changed files and explain whether they affect the requested work.
Before committing or pushing, fetch and inspect the remote state so that a
needed pull, rebase, merge conflict, or pull request requirement is discovered
before publication.

Do not create branches without first naming the proposed branch and getting
approval. Do not merge into `main` without approval. User approval is also
required before staging, committing, and pushing.

For a shared change, commits use a conventional subject followed by a body
covering:

```text
What changed
Why
Collaboration
Boundaries
Validation
```

This format records not only what changed, but also who or what is affected,
what remains untouched, and the evidence used to validate the change.

## Phases and Solo Work

Phases and sub-phases are solo-project milestones unless the user explicitly
defines a collaborative phase arrangement. The PLANNER may define phases when
they help structure a task. A phase is not complete until its planned steps
and acceptance criteria are complete.

The BUILDER must not commit partial phase work. The REVIEWER refuses a commit
when the defined phase or sub-phase is incomplete. Solo phase commits identify
the completed phase, its scope, deferred work, and validation without assuming
anything about teammates' phase numbers.

## Practical Task Checklist

For a typical change, use this checklist:

1. Read the request and inspect the relevant repository files.
2. Write a PLANNER report grounded in those files.
3. Implement only the approved steps.
4. Run relevant tests, builds, or checks.
5. Review the result against acceptance criteria.
6. Produce a line scan for every changed file.
7. Present the change and wait for explicit approval before staging, committing,
   or pushing.
8. Verify branch and remote state, create a descriptive conventional commit,
   and push only after approval.

## What This Guide Does Not Do

`AGENTS.md` is a workflow and quality guide. It does not replace project
architecture, API documentation, a security policy, a test suite, or the
user's direct requirements. When the user gives a requirement that conflicts
with a general convention, the user instruction takes priority. When the code
or documentation leaves an important question unanswered, stop and ask rather
than guessing.
