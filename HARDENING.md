<!-- markdownlint-disable -->

# Hardening Report: actions--labeler/v6.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **actions--labeler/v6.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference actions/reusable-workflows and other actions using mutable branch or tag refs instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced branch or tag is updated with malicious code.

Failing references:
- basic-validation.yml: uses: actions/reusable-workflows/.github/workflows/basic-validation.yml@main
- check-dist.yml: uses: actions/reusable-workflows/.github/workflows/check-dist.yml@main
- codeql-analysis.yml: uses: actions/reusable-workflows/.github/workflows/codeql-analysis.yml@main
- licensed.yml: uses: actions/reusable-workflows/.github/workflows/licensed.yml@main
- publish-immutable-actions.yml: uses: actions/checkout@v5
- publish-immutable-actions.yml: uses: actions/publish-immutable-action@0.0.3
- release-new-action-version.yml: uses: actions/publish-action@v0.4.0
- update-config-files.yml: uses: actions/reusable-workflows/.github/workflows/update-config-files.yml@main

Locations:

- `.github/workflows/basic-validation.yml:16`
- `.github/workflows/check-dist.yml:16`
- `.github/workflows/codeql-analysis.yml:13`
- `.github/workflows/licensed.yml:14`
- `.github/workflows/publish-immutable-actions.yml:14`
- `.github/workflows/publish-immutable-actions.yml:16`
- `.github/workflows/release-new-action-version.yml:21`
- `.github/workflows/update-config-files.yml:10`

### missing-permissions (severity: medium)

Five workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, GitHub Actions grants the default token permissions (which may be read/write depending on repository settings), violating the principle of least privilege.

Affected files:
- basic-validation.yml
- check-dist.yml
- codeql-analysis.yml
- licensed.yml
- update-config-files.yml

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

Fixed all 8 unpinned action references by resolving them to full 40-character commit SHAs using lookup_action_sha. Note: actions/publish-immutable-action@0.0.3 required trying v0.0.3 (with 'v' prefix) to resolve successfully. Added `permissions: {}` top-level blocks to the 5 workflow files that lacked any permissions declaration (basic-validation.yml, check-dist.yml, codeql-analysis.yml, licensed.yml, update-config-files.yml). The publish-immutable-actions.yml already had job-level permissions and release-new-action-version.yml already had a top-level permissions block, so those were not modified for the permissions finding.

