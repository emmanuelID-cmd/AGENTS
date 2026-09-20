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
