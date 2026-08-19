<!-- markdownlint-disable -->

# Hardening Report: kentaro-m--auto-assign-action/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **kentaro-m--auto-assign-action/v2.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable tag/version refs instead of pinned full-length SHA commit hashes. This exposes the workflow to supply-chain attacks if the referenced tag is moved or overwritten. Failing references: pull-request.yml uses `kentaro-m/auto-assign-action@v2.0.0`; release-note.yml uses `release-drafter/release-drafter@v5`; test.yml uses `actions/checkout@v4` and `actions/setup-node@v4`. Each should be replaced with the corresponding 40-character hex commit SHA.

Locations:

- `.github/workflows/pull-request.yml:8`
- `.github/workflows/release-note.yml:12`
- `.github/workflows/test.yml:8`
- `.github/workflows/test.yml:12`

### missing-permissions (severity: medium)

None of the three workflow files define a top-level `permissions:` block, and none of the individual jobs define job-level `permissions:` blocks. Without explicit permissions, workflows run with the default (often broad) token permissions, violating the principle of least privilege. Each workflow should declare the minimal permissions required (e.g., `permissions: contents: read`).

Locations:

- `.github/workflows/pull-request.yml:1`
- `.github/workflows/release-note.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all three workflow files:

1. pull-request.yml: Pinned kentaro-m/auto-assign-action@v2.0.0 → @f4648c0a9fdb753479e9e75fc251f507ce17bb7e and added `permissions: pull-requests: write` (needed for auto-assigning reviewers).

2. release-note.yml: Pinned release-drafter/release-drafter@v5 → @09c613e259eb8d4e7c81c2cb00618eb5fc4575a7 and added `permissions: contents: write, pull-requests: read` (needed for creating/updating draft releases and reading PR info).

3. test.yml: Pinned actions/checkout@v4 → @34e114876b0b11c390a56381ad16ebd13914f8d5 and actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020, and added `permissions: contents: read` (minimal permission needed to check out code).

All original tags are preserved as inline comments for readability.

