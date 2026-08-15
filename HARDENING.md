<!-- markdownlint-disable -->

# Hardening Report: aws-actions--amazon-ecr-login/v2.1.6

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **aws-actions--amazon-ecr-login/v2.1.6** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable version tags instead of full 40-character commit SHA digests. This exposes the workflow to supply-chain attacks where a tag could be silently moved to point to malicious code.

.github/workflows/check.yml:
  - uses: actions/checkout@v6 (line 16)
  - uses: actions/github-script@v9 (line 24)

.github/workflows/codeql-analysis.yml:
  - uses: actions/checkout@v6 (line 35)
  - uses: github/codeql-action/init@v4 (line 46)
  - uses: github/codeql-action/autobuild@v4 (line 55)
  - uses: github/codeql-action/analyze@v4 (line 65)

.github/workflows/package.yml:
  - uses: actions/checkout@v6 (line 19)

All of these should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/check.yml:16`
- `.github/workflows/check.yml:24`
- `.github/workflows/codeql-analysis.yml:35`
- `.github/workflows/codeql-analysis.yml:46`
- `.github/workflows/codeql-analysis.yml:55`
- `.github/workflows/codeql-analysis.yml:65`
- `.github/workflows/package.yml:19`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all 7 unpinned action references to full commit SHAs:
- .github/workflows/check.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6; actions/github-script@v9 → @3a2844b7e9c422d3c10d287c895573f7108da1b3 # v9
- .github/workflows/codeql-analysis.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6; github/codeql-action/init@v4, /autobuild@v4, /analyze@v4 → all @e4fba868fa4b1b91e1fdab776edc8cfbe6e9fb81 # v4
- .github/workflows/package.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6
All SHAs were resolved via lookup_action_sha. check.yml required a full rewrite after an edit corruption; the regex content was preserved faithfully.

