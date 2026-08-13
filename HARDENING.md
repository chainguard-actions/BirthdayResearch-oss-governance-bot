<!-- markdownlint-disable -->

# Hardening Report: BirthdayResearch--oss-governance-bot/v2.0.9

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **BirthdayResearch--oss-governance-bot/v2.0.9** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow runs with the default (potentially broad) GITHUB_TOKEN permissions, which may grant more access than necessary.

Locations:

- `.github/workflows/ci-use.yml:1`
- `.github/workflows/ci.yml:1`
- `.github/workflows/draft.yml:1`
- `.github/workflows/release.yml:1`
- `.github/workflows/sync-labels.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions

**Notes:**

Added top-level `permissions:` blocks to all five workflow files with minimal required permissions:
- ci-use.yml: `contents: read`, `issues: write`, `pull-requests: write` (governance bot needs to manage labels/comments on issues and PRs)
- ci.yml: `contents: write` (EndBug/add-and-commit needs to push commits)
- draft.yml: `contents: write`, `pull-requests: read` (release-drafter needs to create/update draft releases and read PR metadata)
- release.yml: `contents: write` (additional-tags-action needs to create git tags)
- sync-labels.yml: `contents: read`, `issues: write` (action-label-syncer needs to read labels.yml and manage repository labels)

