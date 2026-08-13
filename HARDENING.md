<!-- markdownlint-disable -->

# Hardening Report: BirthdayResearch--oss-governance-bot/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **BirthdayResearch--oss-governance-bot/v3.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any of its jobs. Without explicit permissions, the GITHUB_TOKEN is granted default (often write) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/ci.yml:1`
- `.github/workflows/draft.yml:1`
- `.github/workflows/release.yml:1`
- `.github/workflows/sync-labels.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions

**Notes:**

Added explicit `permissions:` blocks to all four workflow files:
- ci.yml: top-level `contents: read` with a job-level `contents: write` override on the Build job (needed by EndBug/add-and-commit); lint and test jobs inherit the restrictive read-only default.
- draft.yml: `contents: write` and `pull-requests: write` at the top level for release-drafter.
- release.yml: `contents: write` at the top level for vweevers/additional-tags-action to push tags.
- sync-labels.yml: `contents: read` and `issues: write` at the top level for micnncim/action-label-syncer (GitHub labels are managed via the issues API scope).

