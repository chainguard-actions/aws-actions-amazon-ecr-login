<!-- markdownlint-disable -->

# Hardening Report: aws-actions--amazon-ecr-login/v1.7.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **aws-actions--amazon-ecr-login/v1.7.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable version tags instead of pinned full-length SHA commit digests. This exposes the workflow to supply-chain attacks if the referenced tag is moved or overwritten. Failing references:
- check.yml: `actions/checkout@v3`, `actions/github-script@v6`
- codeql-analysis.yml: `actions/checkout@v3`, `github/codeql-action/init@v2`, `github/codeql-action/autobuild@v2`, `github/codeql-action/analyze@v2`
- package.yml: `actions/checkout@v3`

Locations:

- `.github/workflows/check.yml:11`
- `.github/workflows/check.yml:20`
- `.github/workflows/codeql-analysis.yml:29`
- `.github/workflows/codeql-analysis.yml:37`
- `.github/workflows/codeql-analysis.yml:48`
- `.github/workflows/codeql-analysis.yml:60`
- `.github/workflows/package.yml:13`

### missing-permissions (severity: medium)

None of the three workflow files declare a top-level `permissions:` block, and no job within them declares job-level permissions either. Without explicit permissions, workflows run with the default token permissions (which may be read/write depending on repository settings), violating the principle of least privilege.

Locations:

- `.github/workflows/check.yml:1`
- `.github/workflows/codeql-analysis.yml:1`
- `.github/workflows/package.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 3 workflow files:

**unpinned-uses** — Pinned all 7 action references to full commit SHAs:
- `actions/checkout@v3` → `@f43a0e5ff2bd294095638e18286ca9a3d1956744 # v3` (used in check.yml, codeql-analysis.yml, package.yml)
- `actions/github-script@v6` → `@d7906e4ad0b1822421a7e6a35d5ca353c962f410 # v6` (check.yml)
- `github/codeql-action/init@v2` → `@b8d3b6e8af63cde30bdc382c0bc28114f4346c88 # v2` (codeql-analysis.yml)
- `github/codeql-action/autobuild@v2` → `@b8d3b6e8af63cde30bdc382c0bc28114f4346c88 # v2` (codeql-analysis.yml)
- `github/codeql-action/analyze@v2` → `@b8d3b6e8af63cde30bdc382c0bc28114f4346c88 # v2` (codeql-analysis.yml)

**missing-permissions** — Added `permissions: {}` at the top level of all 3 workflow files, plus job-level permissions where needed:
- check.yml: top-level `permissions: {}`, `conventional-commits` job gets `pull-requests: read`
- codeql-analysis.yml: top-level `permissions: {}`, `analyze` job gets `actions: read`, `contents: read`, `security-events: write` (required by CodeQL)
- package.yml: top-level `permissions: {}`, `check` job gets `contents: write` (needed to push the dist commit)

