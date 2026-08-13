<!-- markdownlint-disable -->

# Hardening Report: BirthdayResearch--oss-governance-bot/v4.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **BirthdayResearch--oss-governance-bot/v4.0.0** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` keys on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions. All jobs in this workflow are affected.

Locations:

- `.github/workflows/ci.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` keys on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions.

Locations:

- `.github/workflows/draft.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` keys on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions.

Locations:

- `.github/workflows/release.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` keys on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially broad) permissions.

Locations:

- `.github/workflows/sync-labels.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions

**Notes:**

Added explicit top-level `permissions:` blocks to all four workflow files:
- ci.yml: `contents: write` (required by EndBug/add-and-commit to push build artifacts)
- draft.yml: `contents: write` + `pull-requests: read` (required by release-drafter to create draft releases and read PR data for changelogs)
- release.yml: `contents: write` (required by additional-tags-action to create/update git tags)
- sync-labels.yml: `contents: read` + `issues: write` (required to check out the repo and manage labels via the GitHub issues/labels API)

