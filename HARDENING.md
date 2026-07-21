<!-- markdownlint-disable -->

# Hardening Report: actions--labeler/v7.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **actions--labeler/v7.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions using mutable tags or branch names instead of pinned 40-character SHA digests, making them vulnerable to supply-chain attacks if the referenced tag or branch is updated maliciously.

Failing references:
- basic-validation.yml: `uses: actions/reusable-workflows/.github/workflows/basic-validation.yml@main`
- check-dist.yml: `uses: actions/reusable-workflows/.github/workflows/check-dist.yml@main`
- codeql-analysis.yml: `uses: actions/reusable-workflows/.github/workflows/codeql-analysis.yml@main`
- licensed.yml: `uses: actions/reusable-workflows/.github/workflows/licensed.yml@main`
- publish-immutable-actions.yml: `uses: actions/checkout@v5` and `uses: actions/publish-immutable-action@0.0.3`
- release-new-action-version.yml: `uses: actions/publish-action@v0.4.0`
- update-config-files.yml: `uses: actions/reusable-workflows/.github/workflows/update-config-files.yml@main`

Locations:

- `.github/workflows/basic-validation.yml:14`
- `.github/workflows/check-dist.yml:14`
- `.github/workflows/codeql-analysis.yml:12`
- `.github/workflows/licensed.yml:13`
- `.github/workflows/publish-immutable-actions.yml:14`
- `.github/workflows/publish-immutable-actions.yml:16`
- `.github/workflows/release-new-action-version.yml:22`
- `.github/workflows/update-config-files.yml:12`

### missing-permissions (severity: medium)

Five workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege.

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

Pinned all 8 unpinned action references to full 40-character SHA digests with inline tag comments for readability. Added top-level `permissions: {}` blocks to the 5 workflow files that lacked any permissions declaration (basic-validation.yml, check-dist.yml, codeql-analysis.yml, licensed.yml, update-config-files.yml). The reusable-workflows references all resolved to the same SHA (4735e71081024a944852f4ab9d1495b6dd2de8f2) since they all used @main. Note: actions/publish-immutable-action@0.0.3 required a v-prefix lookup (v0.0.3) to resolve to SHA 4b1aa5c1cde5fedc80d52746c9546cb5560e5f53.

