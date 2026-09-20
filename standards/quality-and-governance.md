# AGENTS Instruction Guide

## Purpose

This repository contains the instruction guide, development workflow, and collaboration conventions used by the AGENTS team.

The guide helps ensure consistent, safe, and high-quality changes while preserving existing repository behavior.

Every change should improve the repository's quality while preserving current functionality and usability.

---

# Source of Truth

When determining requirements, use the following priority:

1. User instructions from the current session
2. `README.md`
3. `design-decisions.md`
4. `component-library.md`
5. Existing implementation

Never invent requirements.

If documentation and implementation conflict, stop and ask the user for clarification before proceeding.

---

# Core Development Principles

* Preserve existing functionality unless explicitly instructed otherwise.
* Make the smallest change necessary to satisfy the request.
* Avoid unnecessary refactoring.
* Avoid unrelated code cleanup.
* Never replace an entire file when a targeted edit is sufficient.
* Keep code modular, readable, and maintainable.
* Favor consistency over cleverness.

---

# Files and Folder Organization

Place files and folders in the directory that best matches their feature,
responsibility, and existing repository conventions. Keep the project easy to
decipher by using clear, purposeful names.

* Do not overpile unrelated files into a single directory.
* Group files by the feature or responsibility they serve, such as routes,
  API handlers, shared components, authentication, messaging, or profiles.
* Reuse the repository's existing directory layout; do not create a new
  organizational pattern without a clear need.
* Keep related files close together and avoid scattering one feature across
  unrelated folders.

---

# Documentation

When behavior changes, update documentation as appropriate:

* `README.md`
* `design-decisions.md`
* `component-library.md`
* `architecture.md`

Do not modify documentation unnecessarily.

---

# Quality Checklist

Before requesting approval, verify:

* Feature implemented correctly
* No console errors
* Navigation works
* Responsive layout preserved
* Accessibility preserved
* Existing functionality preserved
* No broken links
* No unexpected visual regressions

---

# Communication

If a request is ambiguous:

Stop and ask.

If multiple implementation approaches exist:

Choose the least disruptive approach unless the user specifies otherwise.

Never make significant architectural decisions without approval.

---

# Forbidden Actions

Do not:

* Remove existing features without approval.
* Rewrite entire files unnecessarily.
* Introduce placeholder implementations.
* Leave partially completed work.
* Skip testing.
* Skip the preview.
* Commit before user approval.
* Push before user approval.
* Invent requirements.
* Ignore repository verification.

---

# Definition of Done

A task is complete only when:

* The requested feature has been implemented.
* The feature has been tested.
* A preview has been shown to the user.
* The user has approved the implementation.
* Documentation has been updated when necessary.
* A commit has been created.
* The commit has been pushed successfully.
* The repository is in a clean state.
