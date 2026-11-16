# ADR 0004: Define PR type labels and label taxonomy

- **Status:** Accepted
- **Date:** 2026-11-15
- **Deciders:** Project maintainers
- **Technical Story:** Establish a consistent label taxonomy for the repository, using `type:*` labels on pull requests to reflect Conventional Commit types while reserving GitHub Issue Types for issues.

## Context and Problem Statement

The repository uses Conventional Commits (ADR 0001) and GitHub Issue Types are available at the organization level for issues. Pull requests do not have Issue Types, so a labeling scheme is needed to classify PRs consistently. Existing default and custom labels overlap with or diverge from the intended type taxonomy and must be rationalized.

A future mapping is intended between Conventional Commit types and Issue Types (e.g. Bug/Fix, Task for `ci`/`chore`/`build`, Feature/`feat`, Documentation/`docs`, Refactor for `perf`/`refactor`/`style`, Testing/`test`, Reversion/`revert`), but creating additional org-level Issue Types is deferred.

## Decision

### 1. PR type labels (Option A)

Use **one `type:*` label per Conventional Commit type** for pull requests, aligned 1:1 with the commit types defined in ADR 0001.

| Label | Description |
| --- | --- |
| `type:feat` | New feature (`feat`) |
| `type:fix` | Bug fix (`fix`) |
| `type:docs` | Documentation (`docs`) |
| `type:style` | Style/formatting only (`style`) |
| `type:refactor` | Code refactoring (`refactor`) |
| `type:perf` | Performance improvement (`perf`) |
| `type:test` | Tests (`test`) |
| `type:build` | Build system or dependencies (`build`) |
| `type:ci` | CI configuration (`ci`) |
| `type:chore` | Maintenance (`chore`) |
| `type:revert` | Revert changes (`revert`) |

Pull requests should carry the appropriate `type:*` label(s) corresponding to their primary Conventional Commit type(s).

### 2. Label taxonomy changes

- **Create:** `type:feat`, `type:fix`, `type:style`, `type:refactor`, `type:perf`, `type:test`, `type:build`, `type:ci`, `type:chore`, `type:revert`.
- **Keep and update:** `type:docs` (retain as the PR label for documentation changes; ensure description reflects “Documentation (`docs`)”); `decisions` (ensure description reflects “Project decisions and ADRs”).
- **Remove:** `documentation`, `bug`, `enhancement` (to avoid ambiguity with Issue Types and the `type:*` PR labeling scheme).
- **Keep unchanged:** `accessibility`, `duplicate`, `good first issue`, `help wanted`, `invalid`, `wontfix`.

Label colors and other cosmetic presentation details are implementation choices and are not prescribed by this ADR.

### 3. Deferred decisions

- Adding org-level Issue Types `Documentation`, `Refactor`, `Testing`, and `Reversion` (and finalizing issue/PR type alignment around them) is deferred to a later step.
- Existing org Issue Types (`Task`, `Bug`, `Feature`) remain available for issues; detailed usage conventions may be defined separately.

## Consequences

### Positive

- Provides a clear, granular PR classification scheme that maps directly to Conventional Commit types (ADR 0001).
- Reduces label/type ambiguity by removing overlapping default labels (`documentation`, `bug`, `enhancement`) in favor of `type:*` labels for PRs and Issue Types for issues.
- Preserves useful workflow/community labels (`good first issue`, `help wanted`, etc.) and clarifies the purpose of the `decisions` label.

### Negative / Risks

- Introduces more PR labels (11 `type:*` labels) to maintain and apply consistently.
- Pull requests spanning multiple commit types may require multiple `type:*` labels or a convention for selecting a primary type (not specified here).
- Until additional Issue Types are created and aligned, the relationship between PR `type:*` labels and issue categorization is only partially unified.

### Neutral / Deferred

- Org-level Issue Type additions and their final mapping to commit types/PR labels.
- Label colors, automation (e.g. auto-labeling), and conventions for multi-type PRs.
