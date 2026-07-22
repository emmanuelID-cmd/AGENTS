# AGENTS.md

# Personal Website – AI Development Guide

## Project Mission

This repository contains the personal portfolio website for Emmanuel De Jesus.

The website's primary purpose is to communicate Emmanuel's journey into technology, demonstrate his ability as a builder and problem solver, and present a polished, professional experience for hiring managers.

Every change should improve the quality of the website while preserving its existing functionality, design language, and user experience.

---

# Source of Truth

When determining requirements, use the following priority:

1. User instructions from the current session
2. `website-itinerary.md`
3. `website-content.md`
4. `design-decisions.md`
5. `component-library.md`
6. Existing implementation

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

# Required Development Workflow

Every development task must follow this workflow.

## Phase 1 – Repository Verification

Before making any changes:

```bash
pwd
git status
git remote -v
git pull origin main
```

If merge conflicts or repository issues exist:

* Stop immediately.
* Explain the issue.
* Wait for user guidance.

---

## Phase 2 – Planning

Before writing code:

* Read the request carefully.
* Review any related documentation.
* Identify affected files.
* Preserve all unrelated functionality.
* Confirm the implementation approach internally before making changes.

---

## Phase 3 – Implementation

* Modify only the files required.
* Keep edits focused.
* Preserve accessibility.
* Preserve responsiveness.
* Maintain existing navigation behavior.
* Maintain current layout unless instructed otherwise.

---

## Phase 4 – Testing

After implementation:

* Test the feature.
* Check browser console for errors.
* Verify navigation.
* Verify responsiveness.
* Verify scrolling behavior.
* Verify no regressions.

---

## Phase 5 – Preview (Required)

A preview is mandatory before any Git commit.

After testing:

* Launch the local preview.
* Present the completed implementation.
* Wait for the user's review.

If revisions are requested:

* Make the revisions.
* Launch a new preview.
* Repeat until the user explicitly approves.

No commit may be created until approval is received.

---

## Phase 6 – Approval

User approval is required before:

* staging changes
* creating a commit
* pushing to GitHub

Approval must be explicit.

---

## Phase 7 – Git Workflow

Only after user approval:

```bash
git status
git add .
git commit -m "feat: concise feature description"
git push origin main
```

---

# HTML Standards

* Use semantic HTML.
* Maintain proper heading hierarchy.
* Avoid duplicate markup.
* Keep HTML clean and organized.
* Preserve accessibility.

---

# CSS Standards

* Keep CSS modular.
* Reuse existing variables.
* Maintain spacing consistency.
* Avoid duplicate selectors.
* Avoid unnecessary `!important` rules.
* Preserve responsive behavior.

---

# JavaScript Standards

* Prefer extending existing code over rewriting.
* Keep functions concise.
* Preserve existing event listeners.
* Avoid unnecessary global variables.
* Maintain keyboard accessibility.

---

# Accessibility

Every feature should preserve or improve accessibility.

Verify:

* Keyboard navigation
* Focus states
* ARIA attributes
* Color contrast
* Screen reader compatibility when applicable

Never reduce accessibility.

---

# Responsive Design

All features must work correctly on:

* Desktop
* Tablet
* Mobile

No implementation should introduce layout regressions across breakpoints.

---

# Existing Features to Protect

Unless specifically instructed otherwise, preserve:

* Main navigation
* Secondary navigation
* Home tab
* About tab
* Projects tab
* Contact tab
* Hero section
* Adventure Banner
* Journey timeline
* Contact form
* Existing animations
* Responsive layouts
* Color system
* Typography hierarchy

---

# Documentation

When behavior changes, update documentation as appropriate:

* `website-itinerary.md`
* `website-content.md`
* `component-library.md`
* `design-decisions.md`

Do not modify documentation unnecessarily.

---

# Commit Standards

Use Conventional Commits whenever practical.

Examples:

```text
feat:
fix:
docs:
style:
refactor:
perf:
```

Commit messages should describe what changed, not every implementation detail.

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
