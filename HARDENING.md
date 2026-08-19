<!-- markdownlint-disable -->

# Hardening Report: kentaro-m--auto-assign-action/v1.2.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **kentaro-m--auto-assign-action/v1.2.5** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in the workflow files are pinned to mutable tags or version strings rather than immutable 40-character SHA commit hashes. This exposes the workflows to supply-chain attacks if the referenced action tags are moved or overwritten. Failing references: `kentaro-m/auto-assign-action@v1.2.5` (pull-request.yml), `release-drafter/release-drafter@v5` (release-note.yml), `actions/checkout@v3` and `actions/setup-node@v3` (test.yml).

Locations:

- `.github/workflows/pull-request.yml:8`
- `.github/workflows/release-note.yml:11`
- `.github/workflows/test.yml:7`
- `.github/workflows/test.yml:11`

### missing-permissions (severity: medium)

None of the three workflow files define a top-level `permissions:` key, and none of the individual jobs define job-level `permissions:` keys. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege. Affected files: pull-request.yml, release-note.yml, and test.yml.

Locations:

- `.github/workflows/pull-request.yml:1`
- `.github/workflows/release-note.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 unpinned `uses:` references by resolving each tag to its full 40-character SHA (kentaro-m/auto-assign-action@v1.2.5→3e986bf, release-drafter/release-drafter@v5→09c613e, actions/checkout@v3→a37ce91, actions/setup-node@v3→3235b87). Added top-level `permissions:` blocks to all three workflow files with least-privilege scopes: pull-request.yml gets `pull-requests: write`, release-note.yml gets `contents: write`, and test.yml gets `contents: read`.

