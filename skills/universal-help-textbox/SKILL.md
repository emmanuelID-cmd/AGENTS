---
name: universal-help-textbox
description: Add concise helper guidance only to text-entry fields whose accepted format, limits, or requirements are not already clear from the interface.
---

# Universal Help Textbox

Use a `?` helper only when a text-entry field has non-obvious acceptance rules that a short label, placeholder, or native control cannot clearly communicate.

## Use a helper for

- Free-form text, email, password, or textarea fields with meaningful format, character, length, or acceptance constraints.
- Text-entry fields where a concise example will prevent likely mistakes.

## Do not use a helper for

- Select menus, radio groups, checkboxes, toggles, buttons, or other controls whose available choices explain themselves.
- Native date or time editors.
- Number inputs, steppers, or sliders when visible minimum, maximum, unit, and increment rules are clear.
- A text-entry field when its label and placeholder already make the requirement clear enough.

## When a helper is used

1. Keep the message concise and accessible.
2. Explain required status, meaningful limits, accepted or rejected format, and one safe example when useful.
3. Preserve keyboard and screen-reader access for the helper until a separate approved interaction change replaces that behavior.
4. Do not reveal secrets or sensitive values in examples.
5. Validate the same rule at submission and show clear errors without discarding valid user input.
6. Prevent disallowed characters only when the product requirement explicitly requires blocking them.

## Error handling

- Prefer an active submit control with a visible top error summary and invalid-field highlighting when the user submits incomplete or invalid required data.
- Do not rely only on a disabled submit button when the user needs feedback about what is missing.