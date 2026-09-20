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
PLANNER → BUILDER → SECURITY (when applicable) → REVIEWER
→ FIXER (when applicable) → REVIEWER
```

The completion pipeline is:

```text
Project complete → BUDDY → ACCOUNTANT
→ SECURITY (when a reasonable security-risk condition exists)
→ final REVIEWER or completion verdict
```

TOKEN is a conditional cross-cutting advisor. It does not silently change
models or reasoning and does not replace any workflow role.

ARCHIVIST is a conditional backup and restoration advisor. Activate it when
files, databases, configuration, project state, or other durable data may be
created, changed, migrated, deleted, restored, or placed at risk.

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

### Workflow and Git

- [Development workflow](workflow/development.md)
- [Optional phases](workflow/phases.md)
- [Git and collaboration](git.md)

### Standards

- [Input validation and error handling](standards/input-validation.md)
- [API integration](standards/api-integration.md)
- [Frontend standards](standards/frontend.md)
- [Quality and governance](standards/quality-and-governance.md)

## Entry-point rules

- Always read PLANNER first, even for small tasks.
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

The linked documents retain the detailed role, workflow, Git, phase,
validation, API, frontend, quality, security, completion, accounting, and
token-conservation rules. Do not treat this index as a replacement for a
relevant linked document.
