---
name: error-message-finder
description: Add consistent validation summaries and field-level feedback to required-input forms when users submit incomplete or invalid data. Do not use for passive informational fields or unrelated UI.
---

# Error Message Finder

Use this skill when a form requires user input before submission or navigation.

## Required behavior

- Keep the primary submit action active until it is processing. On an attempted invalid submission, place an accessible error summary at the top of the current form or input section.
- Identify every required missing or invalid field in that summary. Give each invalid control a red visual state and an accessible error association.
- Clear only a field's error state when that field becomes valid. Do not clear unrelated errors or discard valid user input.
- For controls with an explicit valid format or range, report the rule in the field error. For example: a future date, accepted file type, size limit, or allowed price range.
- Validate client-side for immediate feedback and server-side before mutation.
- When a text-entry field has an existing helper icon, make its visual treatment red while that field is invalid; retain its normal accessible guidance. Do not add helpers to native date/time, checkbox, radio, select, number, or file controls unless another approved requirement calls for it.

## Boundaries

- Apply this pattern to the submitted form in scope; do not retrofit unrelated forms without approval.
- Do not disable a primary submit action merely because fields are incomplete when an active submission can provide actionable feedback.
- Preserve native keyboard navigation, labels, focus behavior, and responsive layout.