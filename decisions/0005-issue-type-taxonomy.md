# ADR 0005: Define organization issue type and issue field taxonomy

- **Status:** Accepted
- **Date:** 2026-11-15
- **Deciders:** Project maintainers
- **Technical Story:** Reset and define the `dihelios` organization's GitHub Issue Types (and related org issue fields) from scratch to align issue classification with the project's Conventional Commit taxonomy (ADR 0001) and planned PR/label conventions (ADR 0004).

## Context and Problem Statement

The organization previously had a small default set of Issue Types (`Task`, `Bug`, `Feature`) and org-level Issue Fields (`Priority`, `Start date`, `Target date`, `Effort`). The project wants a clean, intentional Issue Type taxonomy aligned to Conventional Commit types and to defer field complexity until needed.

## Decision

### 1. Remove existing org Issue Types and Issue Fields

Delete the following from the `dihelios` organization (org-level):

- **Issue Types:**
  - `Task` (id: 940939592, yellow, "A specific piece of work")
  - `Bug` (id: 940939593, red, "An unexpected problem or behavior")
  - `Feature` (id: 940939594, blue, "A request, idea, or new functionality")
- **Issue Fields:**
  - `Priority` (id: 49953241, single_select: Urgent/High/Medium/Low)
  - `Start date` (id: 49953242, date)
  - `Target date` (id: 49953243, date)
  - `Effort` (id: 49953244, single_select: High/Medium/Low)

### 2. Create new Issue Types (from scratch)

Create the following Issue Types for the `dihelios` organization:

| Issue Type | Commit mapping (intent) | Description | Color |
| --- | --- | --- | --- |
| Bug | `fix` | An unexpected problem or behavior | red |
| Task | `ci`, `chore`, `build` | A specific piece of work | yellow |
| Feature | `feat` | A request, idea, or new functionality | blue |
| Documentation | `docs` | Documentation changes and improvements | green |
| Refactor | `perf`, `refactor`, `style` | Code refactoring, performance, or style-only changes | purple |
| Testing | `test` | Adding or correcting tests | orange |
| Reversion | `revert` | Reverts a previous change | gray |

- `Bug`, `Task`, and `Feature` are recreated as new Issue Types (new identifiers) rather than reused.
- Commit mappings express intended alignment with ADR 0001; GitHub Issue Types store name, description, and color.

### 3. Related conventions (deferred/linked)

- **PR labels:** pull requests continue to use `type:*` labels per ADR 0004; issues use Issue Types.
- **Issue Fields:** no org Issue Fields are defined by this decision; they may be introduced later if needed.

## Consequences

### Positive

- Provides a clean, explicit Issue Type taxonomy aligned with Conventional Commit categories and project intent.
- Removes unused/default org Issue Fields and types to reduce ambiguity.

### Negative / Risks

- Deleting org Issue Fields removes their definitions and any associated data/usage at the org level.
- Org-level changes apply across the `dihelios` organization, not just this repository.

### Neutral / Deferred

- Reintroduction or redesign of Issue Fields and any project/field workflows.
- Automation or enforcement mapping commits/PRs/issues to types.
