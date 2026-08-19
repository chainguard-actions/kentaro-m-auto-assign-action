<!-- markdownlint-disable -->

# Hardening Report: kentaro-m--auto-assign-action/v1.2.6

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **kentaro-m--auto-assign-action/v1.2.6** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in the workflow files use mutable tags instead of immutable 40-character SHA digests, making the workflows vulnerable to supply-chain attacks if the referenced tags are moved or overwritten. Failing references: `kentaro-m/auto-assign-action@v1.2.6` (pull-request.yml), `release-drafter/release-drafter@v5` (release-note.yml), `actions/checkout@v4` and `actions/setup-node@v4` (test.yml).

Locations:

- `.github/workflows/pull-request.yml:7`
- `.github/workflows/release-note.yml:12`
- `.github/workflows/test.yml:7`
- `.github/workflows/test.yml:11`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` block, and no job within any workflow defines job-level permissions. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege. Affected files: pull-request.yml, release-note.yml, test.yml.

Locations:

- `.github/workflows/pull-request.yml:1`
- `.github/workflows/release-note.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all three workflow files:
- pull-request.yml: Pinned kentaro-m/auto-assign-action@v1.2.6 → SHA ed73f90568ce37d22dbbd1a73983738fae329f53; added top-level `permissions: {}` and job-level `pull-requests: write`.
- release-note.yml: Pinned release-drafter/release-drafter@v5 → SHA 09c613e259eb8d4e7c81c2cb00618eb5fc4575a7; added top-level `permissions: {}` and job-level `contents: write` (needed to create/update draft releases).
- test.yml: Pinned actions/checkout@v4 → SHA 11d5960a326750d5838078e36cf38b85af677262 and actions/setup-node@v4 → SHA 49933ea5288caeca8642d1e84afbd3f7d6820020; added top-level `permissions: {}` and job-level `contents: read`.

