<!-- markdownlint-disable -->

# Hardening Report: yc-actions--yc-lockbox/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **yc-actions--yc-lockbox/v2.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple `uses:` references in workflow files are pinned to mutable tags or version strings instead of immutable 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced action tag is moved or compromised.

check-dist.yml:
- Line 22: `uses: actions/checkout@v4` (tag)
- Line 25: `uses: actions/setup-node@v4.0.2` (version tag)
- Line 44: `uses: actions/upload-artifact@v4` (tag)

test.yml:
- Line 13: `uses: actions/checkout@v4` (tag)

All should be replaced with full 40-character commit SHAs, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/check-dist.yml:22`
- `.github/workflows/check-dist.yml:25`
- `.github/workflows/check-dist.yml:44`
- `.github/workflows/test.yml:13`

### missing-permissions (severity: medium)

Neither `.github/workflows/check-dist.yml` nor `.github/workflows/test.yml` has a top-level `permissions:` key, and neither of their jobs defines job-level `permissions:`. Without explicit permissions, workflows inherit the repository's default token permissions (often `write-all`), granting unnecessary broad access. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level of each workflow.

Locations:

- `.github/workflows/check-dist.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 unpinned action references by replacing mutable tags with full 40-character commit SHAs (preserving original tags as comments). Added top-level `permissions: contents: read` to both check-dist.yml and test.yml to enforce least-privilege access.

