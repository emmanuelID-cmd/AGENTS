# Input Validation and Error Handling

Validate all user-provided input before enabling a submission or continuing
processing. Show a clear, actionable validation error and keep the relevant
action disabled until the input is valid.

## Date Validation

* Use `mm/dd/yyyy` for the United States and other countries that use that
  standard.
* Use `dd/mm/yyyy` for countries whose standard date format is day-first.
* Do not silently reinterpret an ambiguous date. Use the country context to
  determine the format, and ask the user when the country cannot be
  determined.

## Date Error Handling

* Do not allow a general date, start date, or end date to be after the
  current date.
* When both a start date and end date are present, do not allow the end date
  to be before the start date or the start date to be after the end date.
* A date-only Follow-up or Schedule field is the exception: it may allow a
  date after the current date.

## Time Editor and Error Handling

* Validate date and time together as one date/time value. Do not compare a
  time-of-day by itself to the current clock time.
* Do not allow a general date/time, start date/time, or end date/time to be
  after the current date/time.
* When both a start date/time and end date/time are present, do not allow the
  end date/time to be before the start date/time or the start date/time to be
  after the end date/time.
* A Follow-up or Schedule date/time field is the exception: it may allow a
  date/time after the current date/time.

## Email Validation

* Do not allow an email workflow to submit or continue when the recipient,
  subject, or message is empty.
* Subject and message must each contain at least one non-whitespace character.
* Disable the Submit button and every control that advances email processing
  until these requirements are met.

## Postal-Code Validation

* For United States addresses, accept only `XXXXX` (five digits) or
  `XXXXX-XXXX` (nine digits with a hyphen).
* Apply country-specific postal-code rules when the country is known.
* Restrict input to numeric characters only for countries whose postal codes
  are numeric. Allow alphanumeric input only for countries whose postal-code
  format uses letters.
* Do not assume that a nine-digit US ZIP+4 is required; ask the user before
  making it mandatory.

## Error Handling

* Validate format, required fields, and country-specific rules before a
  request is sent.
* Explain what is invalid and how to correct it without discarding the
  user's valid input.
* Keep validation and failure handling consistent with the surrounding
  application's existing error-handling conventions.

---
