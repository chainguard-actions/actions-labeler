<!-- markdownlint-disable -->

# Hardening Report: actions--labeler/v6.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **actions--labeler/v6.2.0** was hardened automatically. 12 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow references action using mutable branch ref (@main) instead of a pinned 40-character SHA digest, making it vulnerable to supply-chain attacks. Failing reference: 'actions/reusable-workflows/.github/workflows/basic-validation.yml@main'

Locations:

- `.github/workflows/basic-validation.yml:17`

### unpinned-uses (severity: high)

Workflow references action using mutable branch ref (@main) instead of a pinned 40-character SHA digest. Failing reference: 'actions/reusable-workflows/.github/workflows/check-dist.yml@main'

Locations:

- `.github/workflows/check-dist.yml:17`

### unpinned-uses (severity: high)

Workflow references action using mutable branch ref (@main) instead of a pinned 40-character SHA digest. Failing reference: 'actions/reusable-workflows/.github/workflows/codeql-analysis.yml@main'

Locations:

- `.github/workflows/codeql-analysis.yml:13`

### unpinned-uses (severity: high)

Workflow references action using mutable branch ref (@main) instead of a pinned 40-character SHA digest. Failing reference: 'actions/reusable-workflows/.github/workflows/licensed.yml@main'

Locations:

- `.github/workflows/licensed.yml:13`

### unpinned-uses (severity: high)

Workflow references actions using version tags instead of pinned 40-character SHA digests. Failing references: 'actions/checkout@v5' (line 16), 'actions/publish-immutable-action@0.0.3' (line 19)

Locations:

- `.github/workflows/publish-immutable-actions.yml:16`
- `.github/workflows/publish-immutable-actions.yml:19`

### unpinned-uses (severity: high)

Workflow references action using a version tag instead of a pinned 40-character SHA digest. Failing reference: 'actions/publish-action@v0.4.0'

Locations:

- `.github/workflows/release-new-action-version.yml:24`

### unpinned-uses (severity: high)

Workflow references action using mutable branch ref (@main) instead of a pinned 40-character SHA digest. Failing reference: 'actions/reusable-workflows/.github/workflows/update-config-files.yml@main'

Locations:

- `.github/workflows/update-config-files.yml:13`

### missing-permissions (severity: medium)

Workflow has no top-level 'permissions:' key and no job-level 'permissions:' key on any job, meaning the workflow runs with default (potentially broad) GITHUB_TOKEN permissions.

Locations:

- `.github/workflows/basic-validation.yml:1`

### missing-permissions (severity: medium)

Workflow has no top-level 'permissions:' key and no job-level 'permissions:' key on any job, meaning the workflow runs with default (potentially broad) GITHUB_TOKEN permissions.

Locations:

- `.github/workflows/check-dist.yml:1`

### missing-permissions (severity: medium)

Workflow has no top-level 'permissions:' key and no job-level 'permissions:' key on any job, meaning the workflow runs with default (potentially broad) GITHUB_TOKEN permissions.

Locations:

- `.github/workflows/codeql-analysis.yml:1`

### missing-permissions (severity: medium)

Workflow has no top-level 'permissions:' key and no job-level 'permissions:' key on any job, meaning the workflow runs with default (potentially broad) GITHUB_TOKEN permissions.

Locations:

- `.github/workflows/licensed.yml:1`

### missing-permissions (severity: medium)

Workflow has no top-level 'permissions:' key and no job-level 'permissions:' key on any job, meaning the workflow runs with default (potentially broad) GITHUB_TOKEN permissions.

Locations:

- `.github/workflows/update-config-files.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 7 unpinned-uses findings by replacing mutable branch/tag references with pinned 40-character SHA digests: (1) actions/reusable-workflows@main -> @4735e71081024a944852f4ab9d1495b6dd2de8f2 in basic-validation.yml, check-dist.yml, codeql-analysis.yml, licensed.yml, and update-config-files.yml; (2) actions/checkout@v5 -> @93cb6efe18208431cddfb8368fd83d5badbf9bfd in publish-immutable-actions.yml; (3) actions/publish-immutable-action@0.0.3 -> @4b1aa5c1cde5fedc80d52746c9546cb5560e5f53 (resolved as v0.0.3) in publish-immutable-actions.yml; (4) actions/publish-action@v0.4.0 -> @23f4c6f12633a2da8f44938b71fde9afec138fb4 in release-new-action-version.yml. Fixed all 5 missing-permissions findings by adding 'permissions: {}' top-level blocks to basic-validation.yml, check-dist.yml, codeql-analysis.yml, licensed.yml, and update-config-files.yml. The release-new-action-version.yml already had a permissions block (contents: write) so it was not modified for permissions.

