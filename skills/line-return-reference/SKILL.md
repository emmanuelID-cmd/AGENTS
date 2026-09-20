---
name: line-return-reference
description: Report the exact files and line ranges changed by the current action, with secondary whitespace and Markdown fence checks.
---

# Line Return Reference

Use this skill after every action that creates, edits, deletes, moves, or
generates files, and before reporting approval, completion, commit readiness,
or review readiness. Its primary purpose is to show the user exactly where
the current action changed files so the user can inspect those locations
immediately.

## Required process

1. Determine the current action boundary. Inspect only the files changed by
   the current action, while preserving the prior baseline when one exists.
2. Compare the before and after content using the repository's available
   version-control diff or an equivalent line-aware comparison.
3. Record every changed file, including created, deleted, renamed, and moved
   files. For an untracked created file, all present lines are new unless a
   prior baseline is available.
4. Collapse adjacent changed lines into contiguous ranges. Start each range
   at the first changed line, not at the unchanged context line before it.
5. Return the required report before any approval or completion statement.

## Required output

Return this section exactly as a line-reference report, adapting the entries
to the actual action:

```text
## Line Return Reference

- `path/to/file`: lines 28-35 — added or modified content
- `path/to/other-file`: line 91 — deleted content from the prior version
- `path/to/new-file`: lines 1-42 — created file; all lines are new

## Secondary Checks

- Trailing whitespace: PASS / FINDINGS
- Markdown fences: PASS / FINDINGS / NOT APPLICABLE
```

Every changed file must appear. Use a single line when exactly one line
changed and `N-M` when a contiguous range changed. Do not report an unchanged
context line before the range. For deletions, report the deleted line numbers
from the prior version and identify the entry as deleted. For replacements,
report the deleted prior range and the added current range separately when
the line-aware diff provides both.

If there are no file changes, return:

```text
## Line Return Reference

No file lines changed in the current action.
```

Do not substitute a summary, file count, `git status`, or whitespace-only
result for the line-reference report. A whitespace scan may remain as a
secondary check, but it is not the primary purpose of this skill.

## Scope and limitations

- Report only changes from the current action, not unrelated pre-existing
  work, unless the baseline cannot be separated; if it cannot, say so.
- Do not invent line numbers. If a tool cannot provide reliable line-aware
  output, report that limitation and use the closest verified diff source.
- Include generated files when the current action changed them, unless the
  project explicitly excludes them and that exclusion is reported.
- Do not expose secrets, tokens, credentials, private records, or sensitive
  file contents in the report. File paths and line ranges are sufficient.
- The skill does not authorize edits, commits, pushes, restores, or deletes.

## Secondary checks

After producing the primary line report, check changed Markdown files for
trailing whitespace and unbalanced fenced code blocks when those checks are
available. Report the result under `## Secondary Checks`; do not let a clean
secondary check replace the required line ranges.
