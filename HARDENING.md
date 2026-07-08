<!-- markdownlint-disable -->

# Hardening Report: aws-actions--amazon-ecr-login/v1.7.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **aws-actions--amazon-ecr-login/v1.7.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file has no top-level 'permissions:' key and no job-level 'permissions:' key on any job. This means the workflow runs with default (potentially broad) GitHub token permissions. A minimal permissions block should be added.

Locations:

- `.github/workflows/check.yml:1`
- `.github/workflows/codeql-analysis.yml:1`
- `.github/workflows/package.yml:1`

### unpinned-uses (severity: high)

Multiple 'uses:' references across workflow files are pinned to mutable tags rather than full 40-character SHA digests, making them vulnerable to supply-chain attacks if the referenced tag is moved or overwritten. Failing references: check.yml — 'actions/checkout@v3' (line 12), 'actions/github-script@v6' (line 22); codeql-analysis.yml — 'actions/checkout@v3' (line 31), 'github/codeql-action/init@v2' (line 43), 'github/codeql-action/autobuild@v2' (line 52), 'github/codeql-action/analyze@v2' (line 64); package.yml — 'actions/checkout@v3' (line 13). All should be pinned to their full commit SHA.

Locations:

- `.github/workflows/check.yml:12`
- `.github/workflows/check.yml:22`
- `.github/workflows/codeql-analysis.yml:31`
- `.github/workflows/codeql-analysis.yml:43`
- `.github/workflows/codeql-analysis.yml:52`
- `.github/workflows/codeql-analysis.yml:64`
- `.github/workflows/package.yml:13`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions, unpinned-uses

**Notes:**

Fixed all three workflow files: (1) Added top-level 'permissions: {}' to check.yml, codeql-analysis.yml, and package.yml. For codeql-analysis.yml, added job-level permissions (actions: read, contents: read, security-events: write) required by CodeQL. For package.yml, added job-level 'contents: write' needed to push commits. (2) Pinned all 7 unpinned action references to full 40-character SHA digests: actions/checkout@v3 → f43a0e5ff2bd294095638e18286ca9a3d1956744, actions/github-script@v6 → d7906e4ad0b1822421a7e6a35d5ca353c962f410, github/codeql-action/{init,autobuild,analyze}@v2 → b8d3b6e8af63cde30bdc382c0bc28114f4346c88. Original tags preserved as inline comments.

