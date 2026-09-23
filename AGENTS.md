# AGENTS.md

`AGENTS.md` is the entry point for this repository's instruction set. The
linked Markdown documents below are part of the AGENTS instructions and must
be read when relevant to the task.

If a required linked document cannot be read, stop and report the missing
document before proceeding. Do not assume or recreate missing instructions.

## Source of Truth

Use this priority when requirements conflict:

1. User instructions from the current session
2. `README.md`
3. The relevant linked AGENTS document
4. Existing project documentation and implementation

If requirements conflict or an important fact is unknown, stop and ask the
user. Never invent a path, function, API, permission, role, or requirement.

## Orchestration

The normal pipeline is:

```text
PLANNER → ARCHIVIST (when applicable) → BUILDER
→ SECURITY (when applicable) → REVIEWER
→ FIXER (when applicable) → REVIEWER
```

The completion pipeline is:

```text
Project complete → BUDDY → ACCOUNTANT
→ ARCHIVIST (when applicable)
→ SECURITY (when a reasonable security-risk condition exists)
→ final REVIEWER or completion verdict
```

TOKEN is a conditional cross-cutting advisor. It does not silently change
models or reasoning and does not replace any workflow role.

TEST MODE is a mandatory cross-cutting control mode, not an agent. It tests
whether the documented AGENTS activate and follow their rules without
authorizing project mutations by default.

Agent self-identification is an internal hand-off check. The activated agent
must identify itself internally before acting, but must not display an
activation template or status report during normal work. If the expected agent
fails to self-identify, stop the hand-off and report only the missing
activation and required next step.

ARCHIVIST is a conditional backup and restoration advisor. Activate it when
files, databases, configuration, project state, or other durable data may be
created, changed, migrated, deleted, restored, or placed at risk.

ARCHIVIST may establish a baseline before BUILDER changes a recoverable
system, or verify backup and restore readiness after implementation. It does
not run when the task has no durable data or recoverable project state.

## Required document map

### Roles

- [Orchestrator](agents/orchestrator.md)
- [PLANNER](agents/planner.md)
- [BUILDER](agents/builder.md)
- [REVIEWER](agents/reviewer.md)
- [FIXER](agents/fixer.md)
- [SECURITY](agents/security.md)
- [BUDDY](agents/buddy.md)
- [ACCOUNTANT](agents/accountant.md)
- [ARCHIVIST](agents/archivist.md)
- [TOKEN](agents/token.md)
- TEST MODE (cross-cutting control mode; not an agent)

### Workflow and Git

- [Development workflow](workflow/development.md)
- [Project initialization and dependency readiness](workflow/project-initialization.md)
- [Optional phases](workflow/phases.md)
- [Git and collaboration](git.md)

### Standards

- [Input validation and error handling](standards/input-validation.md)
- [API integration](standards/api-integration.md)
- [Frontend standards](standards/frontend.md)
- [Quality and governance](standards/quality-and-governance.md)

## Skill References

Read the project skill registry in [SKILLS-REFERENCE.md](SKILLS-REFERENCE.md)
when a task may use a project-local skill. The registry is part of the AGENTS
instruction set and links to each applicable skill and its output contract.

## Entry-point rules

- Always read PLANNER first, even for small tasks.
- At project initialization, inspect context and dependency readiness before
  selecting a stack or handing work to BUILDER.
- Pass the approved PLANNER plan verbatim to BUILDER.
- Run SECURITY when the task has a security surface.
- Run REVIEWER after implementation and after FIXER when FIXER applies.
- Run BUDDY only after explicit project-completion activation or approved
  conditional hand-off.
- Run ACCOUNTANT after BUDDY and run post-ACCOUNTANT SECURITY when its
  numerical findings create a reasonable security-risk condition.
- Run ARCHIVIST when backup, restoration, retention, recovery priority, or
  durable-data protection is relevant. ARCHIVIST may run before a risky
  change to establish a baseline and after the change to verify recovery
  readiness.
- Use the optional phase document only when PLANNER defines a Phase or
  Sub-Phase.
- Ask explicitly before staging, committing, pushing, merging, or creating a
  branch.
- Complete a line scan for every changed file before approval.
- TEST MODE must not suppress a direct role trigger. It may test activation and
  instruction-following, but it does not authorize mutations by default.
- If an expected agent fails to self-identify internally, report `TEST=FAIL`
  only when TEST MODE is active. Otherwise report `HAND-OFF FAILURE` and
  request the reason and the user's identification of the missing activation.
- Any change made within the external AGENTS directory must be committed and pushed to the canonical repository at https://github.com/emmanuelID-cmd/AGENTS.git. Do not leave an external AGENTS instruction change only in a local worktree.
- Guardrail-bound execution: once the user approves the complete plan and accepts or overrides all listed unknown recommendations, the named agents proceed directly through the prescribed hand-off without requesting approval for the same approval again. Execution remains limited to the approved scope, required checks, and defined workflow; unrelated work, main-branch merges, commits, pushes, or destructive actions remain separately gated.

The linked documents retain the detailed role, workflow, Git, phase,
validation, API, frontend, quality, security, completion, accounting, and
token-conservation rules. Do not treat this index as a replacement for a
relevant linked document.
