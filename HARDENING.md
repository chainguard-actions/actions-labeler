<!-- markdownlint-disable -->

# Hardening Report: actions--labeler/v6.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **actions--labeler/v6.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference actions and reusable workflows using mutable tags or branch names instead of pinned 40-character commit SHAs, making them vulnerable to supply-chain attacks.

- basic-validation.yml: `uses: actions/reusable-workflows/.github/workflows/basic-validation.yml@main`
- check-dist.yml: `uses: actions/reusable-workflows/.github/workflows/check-dist.yml@main`
- codeql-analysis.yml: `uses: actions/reusable-workflows/.github/workflows/codeql-analysis.yml@main`
- licensed.yml: `uses: actions/reusable-workflows/.github/workflows/licensed.yml@main`
- update-config-files.yml: `uses: actions/reusable-workflows/.github/workflows/update-config-files.yml@main`
- publish-immutable-actions.yml: `uses: actions/checkout@v5` and `uses: actions/publish-immutable-action@0.0.3`
- release-new-action-version.yml: `uses: actions/publish-action@v0.4.0`

All of these should be replaced with full 40-character commit SHA digests (e.g. `uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v5`).

Locations:

- `.github/workflows/basic-validation.yml:14`
- `.github/workflows/check-dist.yml:14`
- `.github/workflows/codeql-analysis.yml:12`
- `.github/workflows/licensed.yml:12`
- `.github/workflows/update-config-files.yml:10`
- `.github/workflows/publish-immutable-actions.yml:14`
- `.github/workflows/publish-immutable-actions.yml:17`
- `.github/workflows/release-new-action-version.yml:20`

### missing-permissions (severity: medium)

Five workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, the GITHUB_TOKEN inherits the repository's default permissions (which may be broad). Each workflow should declare the minimal permissions required.

- basic-validation.yml: no permissions declared
- check-dist.yml: no permissions declared
- codeql-analysis.yml: no permissions declared
- licensed.yml: no permissions declared
- update-config-files.yml: no permissions declared

Locations:

- `.github/workflows/basic-validation.yml:1`
- `.github/workflows/check-dist.yml:1`
- `.github/workflows/codeql-analysis.yml:1`
- `.github/workflows/licensed.yml:1`
- `.github/workflows/update-config-files.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 8 unpinned action references by replacing mutable tags/branches with full 40-character commit SHAs (using lookup_action_sha for each). Added `permissions: {}` top-level blocks to the 5 workflow files that had no permissions declared (basic-validation.yml, check-dist.yml, codeql-analysis.yml, licensed.yml, update-config-files.yml). The publish-immutable-actions.yml already had job-level permissions and release-new-action-version.yml already had top-level permissions, so those were left as-is for the permissions finding. Note: actions/publish-immutable-action tag '0.0.3' resolved to 'v0.0.3' (with the 'v' prefix) which returned SHA 4b1aa5c1cde5fedc80d52746c9546cb5560e5f53.

