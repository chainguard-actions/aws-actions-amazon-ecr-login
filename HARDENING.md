<!-- markdownlint-disable -->

# Hardening Report: aws-actions--amazon-ecr-login/v2.1.7

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **aws-actions--amazon-ecr-login/v2.1.7** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in the workflow files use mutable version tags instead of full 40-character SHA commit hashes, making the action vulnerable to supply-chain attacks if the referenced tag is moved or overwritten.

Failing references:
- `.github/workflows/check.yml`: `actions/checkout@v7`, `actions/github-script@v9`
- `.github/workflows/codeql-analysis.yml`: `actions/checkout@v7`, `github/codeql-action/init@v4`, `github/codeql-action/autobuild@v4`, `github/codeql-action/analyze@v4`
- `.github/workflows/package.yml`: `actions/checkout@v7`

Locations:

- `.github/workflows/check.yml:11`
- `.github/workflows/check.yml:20`
- `.github/workflows/codeql-analysis.yml:30`
- `.github/workflows/codeql-analysis.yml:38`
- `.github/workflows/codeql-analysis.yml:44`
- `.github/workflows/codeql-analysis.yml:55`
- `.github/workflows/package.yml:11`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all mutable tag references to full 40-character SHA commit hashes across three workflow files:
- `.github/workflows/check.yml`: `actions/checkout@v7` → `@3d3c42e5aac5ba805825da76410c181273ba90b1`, `actions/github-script@v9` → `@3a2844b7e9c422d3c10d287c895573f7108da1b3`
- `.github/workflows/codeql-analysis.yml`: `actions/checkout@v7` → `@3d3c42e5aac5ba805825da76410c181273ba90b1`, `github/codeql-action/init@v4`, `github/codeql-action/autobuild@v4`, `github/codeql-action/analyze@v4` → all `@ff2f1c621b7f889edc0d3c761ac2e6a3f8cdb0dd`
- `.github/workflows/package.yml`: `actions/checkout@v7` → `@3d3c42e5aac5ba805825da76410c181273ba90b1`

Original version tags are preserved as inline `# vX` comments for readability.

