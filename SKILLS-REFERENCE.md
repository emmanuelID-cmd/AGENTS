# SKILLS-REFERENCE.md

Project-local skills are part of the AGENTS instruction set when their stated
trigger applies. Read the relevant skill before using it and follow its output
contract. Do not assume a skill was used unless its required result is
returned.

## Line Return Reference

- [Line Return Reference skill](skills/line-return-reference/SKILL.md) — run
  after each file-changing action and before approval. It returns every
  changed file and the exact edited line number or contiguous line range,
  beginning with the first changed line. It also performs the secondary
  whitespace and Markdown fence checks.

The primary line-reference report is mandatory. A whitespace scan may remain
as a secondary check, but it must not replace the file-and-line report.

## universal-help-textbox

- [universal-help-textbox skill](skills/universal-help-textbox/SKILL.md) — use
  for concise, accessible helper guidance on text-entry fields when accepted
  formats, limits, or requirements are not already clear.

## error-message-finder

- [error-message-finder skill](skills/error-message-finder/SKILL.md) — use for
  accessible validation summaries and field-level feedback on submitted forms
  with missing or invalid required input.

## Adding requested skills

When a skill is approved for this project, keep the project copy in
`C:\Users\Github\AGENTS\skills\<skill-name>\SKILL.md` using the skill's
original lowercase name. Immediately synchronize that approved project copy
one way into `C:\Users\dejes\.codex\skills\<skill-name>\SKILL.md` as a
byte-for-byte copy and verify matching SHA-256 hashes.

The synchronization direction is always:

```text
C:\Users\Github\AGENTS\skills → C:\Users\dejes\.codex\skills
```

Do not automatically copy Codex-only skills back into the AGENTS project. If
a skill exists in Codex but not in AGENTS and is explicitly requested for the
project, follow this registry before adding it. Add one registry entry using
the original lowercase name and path. Do not invent aliases, alternate
labels, duplicate names, or summarized versions. Verify both copies before
reporting the skill complete.
