<!-- markdownlint-disable -->

# Hardening Report: aws-actions--amazon-ecr-login/v2.1.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **aws-actions--amazon-ecr-login/v2.1.5** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable version tags instead of pinned full-length SHA digests. This exposes the workflow to supply-chain attacks where a tag could be silently moved to point to malicious code. Failing references:
- check.yml: `actions/checkout@v6` (line 15), `actions/github-script@v9` (line 24)
- codeql-analysis.yml: `actions/checkout@v6` (line 34), `github/codeql-action/init@v4` (line 43), `github/codeql-action/autobuild@v4` (line 51), `github/codeql-action/analyze@v4` (line 62)
- package.yml: `actions/checkout@v6` (line 17)
All should be pinned to a full 40-character commit SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/check.yml:15`
- `.github/workflows/check.yml:24`
- `.github/workflows/codeql-analysis.yml:34`
- `.github/workflows/codeql-analysis.yml:43`
- `.github/workflows/codeql-analysis.yml:51`
- `.github/workflows/codeql-analysis.yml:62`
- `.github/workflows/package.yml:17`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all 7 unpinned action references across 3 workflow files to full 40-character commit SHAs:
- check.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6; actions/github-script@v9 → @3a2844b7e9c422d3c10d287c895573f7108da1b3 # v9
- codeql-analysis.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6; github/codeql-action/init@v4, autobuild@v4, analyze@v4 → all @e4fba868fa4b1b91e1fdab776edc8cfbe6e9fb81 # v4
- package.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6
All SHAs were resolved via lookup_action_sha. The codeql-analysis.yml file was rewritten after an edit corruption was detected during verification.

