---
name: failure-explanation
description: Explain debugging failures, bugs, rejected actions, dismissed changes, and patch or tool failures in plain language using WHO, WHAT, WHEN, WHERE, WHY, and HOW, with a safe next action.
---

# Failure Explanation

Use this skill whenever a debugging attempt, bug fix, required patch, tool call,
command, build, deployment, review, or requested action fails, is rejected, is
dismissed, or is blocked.

## Required response

State the problem before proposing the next step. Explain it in non-technical
language and cover these questions as applicable:

- WHO — which user, agent, system, service, file, or role is involved.
- WHAT — what failed, was rejected, changed, or did not happen.
- WHEN — when it occurred in the workflow, using an exact time or stage when
  available.
- WHERE — the page, command, file, repository, branch, environment, or service
  involved.
- WHY — the confirmed cause; if it is not confirmed, label the explanation as
  an inference and name the evidence still needed.
- HOW — how the failure affects the work and the safest next action.

Do not ask the user to answer these questions. Provide the answers using the
available evidence. Use `Unknown` when evidence is missing and give the
smallest safe verification step. Do not invent logs, file paths, causes, or
successful actions.

## Countermeasure and next move

An explanation is incomplete without forward motion. After explaining the
failure, state the countermeasure that addresses the confirmed cause or safely
circumvents the blocked path, then state the next concrete move to advance the
work. The countermeasure may be a code fix, a different command, a permission
change, a read-only diagnostic, a rollback, or a request for a specific user
decision. Prefer the smallest safe action that can disprove the suspected
cause or restore progress.

Use these distinct labels:

- `Countermeasure:` what will prevent, repair, or safely bypass the failure.
- `Next move:` the exact next action, command, file, page, or verification to
  perform.

If no safe countermeasure exists, say so plainly and identify the blocker or
permission required. Do not stop after explaining the problem, and do not
suggest an unrelated workaround merely to appear actionable.
## Scope and safety

Keep the explanation proportional to the failure. For a minor, obvious failure,
use a compact explanation; for a security, data, deployment, or destructive
failure, provide all six categories explicitly. Separate completed actions
from attempted actions, and state whether any files, branches, databases,
secrets, deployments, or external services were changed.

Never expose secret values in the explanation. Do not retry a failed mutation
indefinitely: after two materially similar failures, reconsider the method or
stop and report the blocker. If a safe fallback exists, state it; otherwise
identify the exact permission, tool, or user decision required.

## Output shape

Use this structure when the failure is consequential:

`Problem:` one-sentence plain-language summary.

- `WHO:` ...
- `WHAT:` ...
- `WHEN:` ...
- `WHERE:` ...
- `WHY:` ...
- `HOW:` ...
- `State change:` what did and did not change.
- `Countermeasure:` ...
- `Next move:` one concrete next step.

For routine failures, the labels may be combined into a short paragraph, but
the six questions must still be answered or explicitly marked Unknown.