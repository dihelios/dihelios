# ADR 0003: Establish master branch repository ruleset

- **Status:** Accepted
- **Date:** 2026-11-15
- **Deciders:** Project maintainers
- **Technical Story:** Define a baseline repository ruleset for the default branch to enforce pull request-based integration and protect shared history on GitHub.

## Context and Problem Statement

With merge-only integration configured (ADR 0002), the repository needs baseline protections on the default branch (`master`) to ensure changes flow through pull requests, prevent destructive history operations, and require commit signing. The project currently has no CI/status checks but wants branches kept up to date before merge where possible.

## Decision

Use a GitHub **repository ruleset** named `master`, targeting `refs/heads/master`, with **active** enforcement and **no bypass actors**.

### 1. Pull request and review requirements

- **Require a pull request before merging:** enabled.
- **Required approving reviews:** 0.
  - **Policy (not technically enforced by the ruleset):** external contribution pull requests must receive appropriate review/approval before merge, handled by maintainer process.
- **Require conversation resolution before merging:** enabled.
- **Allowed merge methods (in PR rule):** `merge` only (reinforcing ADR 0002).

### 2. Branch update and status checks

- **Require status checks to pass before merging:** enabled via a required-status-checks rule with:
  - **Strict required status checks policy (require branches to be up to date before merging):** enabled.
  - **Required status checks:** none configured (empty list) at this time.
  - **Do not enforce on create:** disabled.

As CI/status checks are introduced, they should be added as required checks under this policy as appropriate.

### 3. History and integrity protections

- **Block force pushes (non-fast-forward updates):** enabled.
- **Restrict deletions:** enabled.
- **Require signed commits:** enabled.
- **Require linear history:** not required (merge commits are allowed/expected per ADR 0002).
- **Restrict who can push:** not configured.

### 4. Bypass

- **Bypass actors:** none.
- **Current user can bypass:** never.

### 5. Additional rule parameters (as configured)

- **Dismiss stale reviews on push:** disabled.
- **Require review from Code Owners:** disabled (no `CODEOWNERS` policy established yet).
- **Require last push approval:** disabled.
- **Require approval for unattributed changes:** enabled.
- **Required reviewers:** none.

## Consequences

### Positive

- Ensures changes to `master` go through pull requests and preserves merge-commit history consistent with ADR 0001 and ADR 0002.
- Protects `master` from force pushes and deletion and requires signed commits for stronger provenance.
- Requires review conversations to be resolved and attempts to keep branches up to date before merge (strict policy), even before named checks exist.
- Reinforces merge-only integration at the ruleset level.

### Negative / Risks

- **Zero required approvals** means non-external PRs can merge without a technically enforced approval; external-review expectations rely on process until tooling/rules evolve.
- **No bypass** (including for admins) can impede urgent recovery; any future need for emergency bypass must be a deliberate, reviewed change.
- **Signed commits required** means contributors must have commit signing configured.
- Strict “up to date” behavior with an empty required-checks list depends on GitHub/platform behavior; this should be revalidated when CI checks are added.

### Neutral / Deferred

- Introducing named required status checks/CI and revisiting strict up-to-date enforcement details.
- Adding `CODEOWNERS`, required reviewers, or higher approval counts (especially for external contributions) if/when needed.
- Any future default-branch rename or additional rulesets for other branch patterns.
