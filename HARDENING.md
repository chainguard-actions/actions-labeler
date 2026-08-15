<!-- markdownlint-disable -->

# Hardening Report: actions--labeler/v6.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **actions--labeler/v6.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference actions and reusable workflows using mutable tags or branch names (@main, @v5, @v0.4.0, @0.0.3) instead of full 40-character commit SHA digests. This exposes the workflow to supply-chain attacks where a tag or branch can be silently updated to point to malicious code.

Failing references:
- basic-validation.yml: actions/reusable-workflows/.github/workflows/basic-validation.yml@main
- check-dist.yml: actions/reusable-workflows/.github/workflows/check-dist.yml@main
- codeql-analysis.yml: actions/reusable-workflows/.github/workflows/codeql-analysis.yml@main
- licensed.yml: actions/reusable-workflows/.github/workflows/licensed.yml@main
- publish-immutable-actions.yml: actions/checkout@v5, actions/publish-immutable-action@0.0.3
- release-new-action-version.yml: actions/publish-action@v0.4.0
- update-config-files.yml: actions/reusable-workflows/.github/workflows/update-config-files.yml@main

Locations:

- `.github/workflows/basic-validation.yml:14`
- `.github/workflows/check-dist.yml:14`
- `.github/workflows/codeql-analysis.yml:12`
- `.github/workflows/licensed.yml:13`
- `.github/workflows/publish-immutable-actions.yml:13`
- `.github/workflows/publish-immutable-actions.yml:15`
- `.github/workflows/release-new-action-version.yml:22`
- `.github/workflows/update-config-files.yml:11`

### missing-permissions (severity: medium)

Five workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, workflows inherit the default repository permissions (which may be broad), violating the principle of least privilege.

Affected files:
- basic-validation.yml: no permissions block
- check-dist.yml: no permissions block
- codeql-analysis.yml: no permissions block
- licensed.yml: no permissions block
- update-config-files.yml: no permissions block

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

Fixed all 8 unpinned action references by resolving full 40-character commit SHAs via lookup_action_sha: actions/reusable-workflows@main→4735e71081024a944852f4ab9d1495b6dd2de8f2 (used in 5 workflow files), actions/checkout@v5→93cb6efe18208431cddfb8368fd83d5badbf9bfd, actions/publish-immutable-action@0.0.3→4b1aa5c1cde5fedc80d52746c9546cb5560e5f53 (tag 0.0.3 not found; resolved via v0.0.3), actions/publish-action@v0.4.0→23f4c6f12633a2da8f44938b71fde9afec138fb4. Added top-level `permissions: {}` to the 5 workflow files that lacked any permissions block (basic-validation.yml, check-dist.yml, codeql-analysis.yml, licensed.yml, update-config-files.yml). The remaining two files (publish-immutable-actions.yml, release-new-action-version.yml) already had explicit permissions blocks.

