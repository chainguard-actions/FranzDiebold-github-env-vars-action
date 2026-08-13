<!-- markdownlint-disable -->

# Hardening Report: FranzDiebold--github-env-vars-action/v2.6.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **FranzDiebold--github-env-vars-action/v2.6.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference Actions using mutable version tags instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced tag is moved or the repository is compromised. Failing references: ci.yml — `actions/checkout@v2` (line 9), `actions/setup-node@v2` (line 12); demo.yml — `FranzDiebold/github-env-vars-action@v2` (lines 7, 44, 81).

Locations:

- `.github/workflows/ci.yml:9`
- `.github/workflows/ci.yml:12`
- `.github/workflows/demo.yml:7`
- `.github/workflows/demo.yml:44`
- `.github/workflows/demo.yml:81`

### missing-permissions (severity: medium)

Neither workflow file declares a top-level `permissions:` key, and no job-level `permissions:` keys are present in any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (broad) permissions, violating the principle of least privilege. Both `ci.yml` and `demo.yml` are affected.

Locations:

- `.github/workflows/ci.yml:1`
- `.github/workflows/demo.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files: (1) Pinned all 5 unpinned action references to full 40-char commit SHAs — actions/checkout@v2 → ee0669bd1cc54295c223e0bb666b733df41de1c5, actions/setup-node@v2 → 7c12f8017d5436eb855f1ed4399f037a36fbd9e8, FranzDiebold/github-env-vars-action@v2 → e8118971bd6b60524ae66a2d870bc83088e3a3c9 (3 occurrences in demo.yml). (2) Added `permissions: {}` top-level block to both ci.yml and demo.yml to enforce least-privilege GITHUB_TOKEN access.

