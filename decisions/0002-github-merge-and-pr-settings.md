# ADR 0002: Configure GitHub merge and pull request settings

- **Status:** Accepted
- **Date:** 2026-11-15
- **Deciders:** Project maintainers
- **Technical Story:** Enforce a merge-only integration strategy and baseline pull request behavior for the DiHelios repository on GitHub.

## Context and Problem Statement

The project follows Conventional Commits (ADR 0001) and requires a merge strategy that preserves commit history as authored. GitHub repository settings must be configured consistently to prevent squash or rebase merges, define predictable merge commit messages, and establish baseline pull request hygiene.

## Decision

Configure the `dihelios/dihelios` GitHub repository with the following merge and pull request settings.

### 1. Allowed merge methods

- **Allow merge commits:** enabled
- **Allow squash merging:** disabled
- **Allow rebase merging:** disabled

Pull requests MUST be integrated using merge commits only.

### 2. Default merge commit message

- **Merge commit title:** Pull request title (`PR_TITLE`)
- **Merge commit message:** Pull request description/body (`PR_BODY`)

This corresponds to GitHub’s “Pull request title and description” default merge commit message option.

### 3. Pull request branch hygiene

- **Automatically delete head branches:** enabled

Head branches are deleted automatically after pull requests are merged to keep the remote tidy.

### 4. Auto-merge

- **Allow auto-merge:** enabled

Auto-merge may be used when pull request requirements are satisfied; enabling it at the repository level does not by itself merge changes without meeting applicable requirements.

## Consequences

### Positive

- Preserves individual commit history and Conventional Commit messages in the shared branch (consistent with ADR 0001).
- Prevents accidental squash or rebase merges that could rewrite or collapse commit intent.
- Produces consistent, informative merge commits derived from pull request title and description.
- Reduces stale remote branches through automatic head branch deletion.

### Negative / Risks

- Merge commits add merge nodes to history, which some contributors may find noisier than linear/squashed history.
- Commit-level discipline is important because commits are not squashed away at merge time (reinforced by ADR 0001).

### Neutral / Deferred

- Branch protection/rulesets (e.g. required reviews, status checks, restrictions on force-push/deletion) are out of scope for this decision and will be addressed separately.
- Default branch naming/management and additional repository collaboration settings may be covered in subsequent ADRs.
