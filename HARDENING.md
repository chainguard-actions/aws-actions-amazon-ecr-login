<!-- markdownlint-disable -->

# Hardening Report: aws-actions--amazon-ecr-login/v2.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **aws-actions--amazon-ecr-login/v2.1.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in the workflow files are pinned to mutable version tags rather than immutable 40-character SHA commit hashes. This exposes the action to supply-chain attacks where a tag can be silently moved to point to malicious code.

Failing references:
- `.github/workflows/check.yml`: `actions/checkout@v6`, `actions/github-script@v8`
- `.github/workflows/codeql-analysis.yml`: `actions/checkout@v6`, `github/codeql-action/init@v4`, `github/codeql-action/autobuild@v4`, `github/codeql-action/analyze@v4`
- `.github/workflows/package.yml`: `actions/checkout@v6`

Each should be replaced with a full SHA pin, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/check.yml:11`
- `.github/workflows/check.yml:21`
- `.github/workflows/codeql-analysis.yml:35`
- `.github/workflows/codeql-analysis.yml:50`
- `.github/workflows/codeql-analysis.yml:57`
- `.github/workflows/codeql-analysis.yml:67`
- `.github/workflows/package.yml:16`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all mutable tag references to immutable SHA hashes across 3 workflow files:
- `.github/workflows/check.yml`: `actions/checkout@v6` → `@d23441a48e516b6c34aea4fa41551a30e30af803 # v6`; `actions/github-script@v8` → `@ed597411d8f924073f98dfc5c65a23a2325f34cd # v8`
- `.github/workflows/codeql-analysis.yml`: `actions/checkout@v6` → `@d23441a48e516b6c34aea4fa41551a30e30af803 # v6`; `github/codeql-action/init@v4`, `github/codeql-action/autobuild@v4`, `github/codeql-action/analyze@v4` all → `@ff2f1c621b7f889edc0d3c761ac2e6a3f8cdb0dd # v4`
- `.github/workflows/package.yml`: `actions/checkout@v6` → `@d23441a48e516b6c34aea4fa41551a30e30af803 # v6`
All SHAs were resolved via lookup_action_sha. Original version tags preserved as inline comments for readability.

