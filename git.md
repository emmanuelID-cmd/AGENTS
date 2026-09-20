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

## Isolated Multi-Task Commit Grouping

Before staging or committing, inspect the complete change set from the last
commit, including unstaged and already-staged changes. Report every changed
file and its changed line ranges, then determine whether the changes belong to
one cohesive task or to multiple independent tasks or actions.

- Keep one cohesive task in one commit when the files support the same approved
  outcome and cannot be meaningfully reviewed or reverted separately.
- Recommend separate commits for independent tasks, unrelated fixes, separate
  roles or policies, or changes with different validation or approval
  boundaries.
- Do not stage unrelated or pre-existing work merely to complete the current
  task. Identify it separately and preserve it unless the user authorizes its
  inclusion.
- For every recommended commit, list the exact files, changed line ranges,
  purpose, validation, and proposed Conventional Commit subject and body.
- If no changes exist since `HEAD`, report that no commit is recommended. If
  the working tree contains changes but their baseline cannot be separated,
  report that limitation before staging anything.

The commit-grouping report must distinguish:

1. Changes already present in `HEAD`.
2. Unstaged changes in the working tree.
3. Staged changes awaiting commit.
4. Independent commit groups recommended from the current change set.

Do not claim that a commit group is isolated without checking the complete
diff and repository status first.

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
