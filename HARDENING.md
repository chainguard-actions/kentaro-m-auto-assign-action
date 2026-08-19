<!-- markdownlint-disable -->

# Hardening Report: kentaro-m--auto-assign-action/v2.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **kentaro-m--auto-assign-action/v2.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in the workflow files use mutable tag refs instead of pinned 40-character SHA commit hashes, making the action vulnerable to supply-chain attacks if the referenced tags are moved or overwritten.

Failing references:
- `.github/workflows/pull-request.yml`: `uses: kentaro-m/auto-assign-action@v2.0.1`
- `.github/workflows/release-note.yml`: `uses: release-drafter/release-drafter@v6`
- `.github/workflows/test.yml`: `uses: actions/checkout@v4`
- `.github/workflows/test.yml`: `uses: actions/setup-node@v4`

Each should be pinned to a full 40-character commit SHA, e.g. `uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/pull-request.yml:7`
- `.github/workflows/release-note.yml:12`
- `.github/workflows/test.yml:7`
- `.github/workflows/test.yml:11`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` block, and none of the individual jobs define job-level `permissions:` blocks. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege.

Affected files:
- `.github/workflows/pull-request.yml` — no permissions defined
- `.github/workflows/release-note.yml` — no permissions defined
- `.github/workflows/test.yml` — no permissions defined

Locations:

- `.github/workflows/pull-request.yml:1`
- `.github/workflows/release-note.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 unpinned action references by resolving their full SHA hashes: kentaro-m/auto-assign-action@v2.0.1 → a6d59add3a817df08cafa9b166367768d2c337f8, release-drafter/release-drafter@v6 → 6a93d829887aa2e0748befe2e808c66c0ec6e4c7, actions/checkout@v4 → 11d5960a326750d5838078e36cf38b85af677262, actions/setup-node@v4 → 49933ea5288caeca8642d1e84afbd3f7d6820020. Added top-level permissions blocks to all 3 workflow files with least-privilege permissions: pull-request.yml gets pull-requests:write (needed for auto-assign), release-note.yml gets contents:write (needed for release-drafter to create/update draft releases), and test.yml gets contents:read (only needs to read the repo).

