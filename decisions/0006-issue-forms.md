# ADR 0006: Define issue forms, one per Issue Type

- **Status:** Accepted
- **Date:** 2026-11-15
- **Deciders:** Project maintainers
- **Technical Story:** Provide structured issue intake aligned with the organization's Issue Types (ADR 0005) by defining one GitHub YAML issue form per Issue Type, auto-applying the Issue Type, and disabling blank issues.

## Context and Problem Statement

The repository had no `.github/ISSUE_TEMPLATE/` directory, no issue templates/forms, and blank issues enabled by default. The `dihelios` organization defines seven Issue Types (ADR 0005: `Bug`, `Task`, `Feature`, `Documentation`, `Refactor`, `Testing`, `Reversion`). The project wants consistent, structured issue intake that maps directly to those Issue Types, without duplicating classification via labels (ADR 0004 reserves `type:*` labels for pull requests).

## Decision

### 1. One YAML issue form per Issue Type

Create seven GitHub **YAML issue forms** in `.github/ISSUE_TEMPLATE/`, one per Issue Type, with numeric filename prefixes to control chooser order:

| File | Chooser name | Auto-applied Issue Type |
| --- | --- | --- |
| `1-bug.yml` | Bug report | `Bug` |
| `2-task.yml` | Task | `Task` |
| `3-feature.yml` | Feature | `Feature` |
| `4-documentation.yml` | Documentation | `Documentation` |
| `5-refactor.yml` | Refactor | `Refactor` |
| `6-testing.yml` | Testing | `Testing` |
| `7-reversion.yml` | Reversion | `Reversion` |

- YAML forms are used (not Markdown templates) for structured, required fields and Issue Type auto-application.
- Each form sets `type:` to its Issue Type so classification is automatic and authoritative (the source of truth), rather than relying on free-text titles or labels.
- Forms set **no** `labels`, `title` prefix, `assignees`, or `projects`.

### 2. Blank issues and contact links

- `blank_issues_enabled: false` in `.github/ISSUE_TEMPLATE/config.yml`. Contributors with read/triage roles see only the configured forms; users with write access or above still see a **Maintainers only** blank option.
- No `contact_links` are defined at this time (to be added when Discussions and other channels are set up).

### 3. Form contents (required core, optional context)

Each form opens with a short Markdown intro and has required core fields plus optional context:

| Form | Required | Optional |
| --- | --- | --- |
| Bug | What happened; Steps to reproduce; duplicate-check preflight checkbox | Environment; Relevant logs (`shell`); Additional context |
| Task | Description; Scope / acceptance criteria | Additional context |
| Feature | Problem / motivation; Proposed solution | Alternatives considered; Additional context |
| Documentation | What documentation needs changing; Current vs. expected | Additional context |
| Refactor | What should be refactored; Why / motivation | Scope, risks, and non-goals; Additional context |
| Testing | What needs testing; Test scenarios / coverage | Additional context |
| Reversion | Commit / PR / issue being reverted (`input`); Reason for revert | Additional context |

- Only **Bug** includes the "searched existing issues" preflight checkbox.

## Consequences

### Positive

- Provides consistent, structured issue intake that maps 1:1 to the organization's Issue Types (ADR 0005).
- Issue classification is automatic and authoritative via `type:`, keeping `type:*` labels reserved for pull requests (ADR 0004).
- Required fields improve report completeness; disabling blank issues nudges contributors toward the forms.

### Negative / Risks

- Issue forms and the `type:` key are in public preview and may change.
- Forms are only served from the default branch (`master`), so changes take effect only after merge.
- Contributors with write access or above can still bypass forms via the "Maintainers only" blank option.
- Renaming or removing an Issue Type requires updating the corresponding form's `type:` (and name) to stay aligned.

### Neutral / Deferred

- Adding `contact_links` once Discussions (and other channels) are available.
- Adding, removing, or refining form fields, and adding the duplicate-check preflight to other forms.
- Pull request templates and any additional templates for future Issue Types.
