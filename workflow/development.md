# Required Development Workflow

Every development task must follow this workflow.

### Codex Command Runner Fallback

First attempt safe, read-only Git checks with the normal Codex command runner. If it fails, Codex may request temporary elevated sandbox permission for narrowly scoped, read-only Git checks using clear wording such as: "Allow read-only Git checks outside the sandbox?"

This is not Windows "Run as Administrator" and does not change the user’s Windows account permissions. It must not be used for writing, staging, committing, pushing, deleting, merging, or any other state-changing command.

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
