# Contribution 1: todo: Migrate to Backstage UI

**Contribution Number:** 1  
**Student:** Ashish Namdeo  
**Issue:** [backstage/community-plugins#7531](https://github.com/backstage/community-plugins/issues/7531)  
**Status:** Phase I — Pull Request Submitted (Awaiting Re-review)
**Forked Repo** (https://github.com/ashishnamdeo16/community-plugins)

**Pull Request:** [backstage/community-plugins#9793](https://github.com/backstage/community-plugins/pull/9793)

---

## Why I Chose This Issue

I chose this issue because it closely aligns with my experience in frontend development using React and modern component-based architectures. The task focuses on migrating an existing plugin from Material UI (MUI) to Backstage UI (BUI), which let me apply my frontend skills while learning the Backstage ecosystem.

As I begin contributing to open source, I wanted an issue with a clearly defined scope and measurable outcomes. This migration provided an opportunity to understand Backstage's plugin architecture, UI component library, contribution workflow, and code review process while making a meaningful contribution to a widely used open source project.

---

## Understanding the Issue

### Problem Description

The Todo plugin currently relies on Material UI (MUI) components and legacy `@backstage/core-components` table implementations. Backstage is transitioning toward Backstage UI (BUI), and the Todo plugin had not yet been migrated. This resulted in inconsistency with current UI standards and prevented the plugin from fully adopting the newer component framework.

### Expected Behavior

The Todo plugin should:

- Use Backstage UI (BUI) components instead of Material UI where equivalents exist
- Preserve existing functionality (sorting, filtering, pagination)
- Maintain visual consistency with other migrated plugins
- Build successfully without regressions

### Current Behavior (Before Migration)

The plugin relied heavily on:

- `@backstage/core-components` `Table` with `TableColumn` definitions
- Material UI patterns via `@backstage/core-components`
- Built-in Material Table per-column filtering in the table header row

### Affected Components

- `workspaces/todo/plugins/todo/src/components/TodoList/TodoList.tsx` — main UI component
- `workspaces/todo/plugins/todo/package.json` — dependencies
- `workspaces/todo/plugins/todo/README.md` — adopter documentation
- `workspaces/todo/plugins/todo/src/components/TodoList/TodoList.test.tsx` — unit tests
- `workspaces/todo/.changeset/` — release notes

---

## Reproduction Process

### Environment Setup

- Forked the [Backstage Community Plugins](https://github.com/backstage/community-plugins) repository
- Cloned locally: `git clone git@github.com:ashishnamdeo16/community-plugins.git`
- Navigated to the todo workspace: `cd community-plugins/workspaces/todo`
- Installed dependencies: `yarn install`
- Started the plugin dev app: `yarn start` from `plugins/todo`
- Verified the Todo plugin rendered correctly before making changes

Challenges encountered:

- The plugin-only workspace requires running commands from `workspaces/todo/`, not the repository root
- Dev app initially failed with `Missing required config value at 'app.title'` — resolved locally with a dev-only `app-config.yaml` (not included in the PR)
- After rebasing onto latest `main`, `yarn.lock` conflicted due to `@backstage/ui` version bumps — resolved by regenerating the lockfile with `yarn install`

### Steps to Reproduce

1. Clone the repository and navigate to `workspaces/todo`
2. Run `yarn install` and `yarn start` from `plugins/todo`
3. Open the dev app and navigate to **Entity Todo Content**
4. Inspect `TodoList.tsx` and observe Material UI / `@backstage/core-components` `Table` usage
5. Compare with migrated plugins such as Azure DevOps `PullRequestTable` which use `@backstage/ui`

**Expected (after migration):** TodoList uses BUI `Card`, `Table`, `useTable`, `SearchField`, and `ColumnConfig`.

**Actual (before migration):** TodoList used `@backstage/core-components` `TableColumn` with Material Table filtering built into the table.

### Reproduction Evidence

- **Branch:** `ashishnamdeo16/bui-migration`
- **Pull Request:** [#9793](https://github.com/backstage/community-plugins/pull/9793)
- **Screenshots:** before/after comparison included in PR description
- **Findings:** TodoList is the only shipped UI component in this plugin — migration scope is well-defined

---

## Solution Approach

### Analysis

This issue was not caused by a functional bug but by a framework migration requirement. The objective was to migrate the Todo plugin UI from Material UI / `@backstage/core-components` Table to Backstage UI while preserving all existing server-side sorting, filtering, and pagination behavior.

I studied previously merged BUI migrations in the same repository — notably [Azure DevOps #7599](https://github.com/backstage/community-plugins/pull/7599) — and the [BUI Table documentation](https://ui.backstage.io/components/table).

### Proposed Solution

- Replace `@backstage/core-components` `Table` with BUI `Table` + `useTable` (`mode: 'offset'` for server-side pagination)
- Define columns using BUI `ColumnConfig` with `Cell`, `CellText`, and BUI `Link`
- Preserve per-column filters (Text, File, Author) with `SearchField` components in `CardHeader`
- Add `@backstage/ui` as a direct dependency
- Keep `ResponseErrorPanel` from `@backstage/core-components` (no BUI equivalent)
- Document BUI requirement in README (Backstage ≥ 1.41.0)

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** TodoList is the only user-facing component. It uses server-side offset pagination, wildcard filters (`*value*`), and sort translation to the todo backend API.

**Match:** Studied Azure DevOps `PullRequestTable`, GitHub Actions `WorkflowRunsTable` (offset mode), and BUI Table docs for `ColumnConfig`, `useTable`, and `Card` layout patterns.

**Plan:**

1. Replace `TableColumn` with `ColumnConfig` column definitions
2. Wire `useTable({ mode: 'offset', getData })` to existing `todoApi.listTodos` API
3. Move filters to `CardHeader` with `SearchField` components aligned to column widths
4. Add accessibility: `aria-label` on table and filters, `rel="noopener noreferrer"` on external links
5. Update tests for filter → API and sort → API translation
6. Add changeset, README note, and update `package.json` dependencies

**Implement:** [PR #9793](https://github.com/backstage/community-plugins/pull/9793) on branch `ashishnamdeo16/bui-migration`

**Review:** Addressed Copilot and maintainer (`awanlin`) feedback across multiple commits.

**Evaluate:** CI passing, manual testing completed, awaiting maintainer re-review.

---

## Testing Strategy

### Unit Tests

- [x] `TodoList` renders and requests todos for the entity
- [x] Filter inputs translate to wildcard server-side filters (`*text*`, `*file*`, `*author*`)
- [x] Table sort translates to server-side `orderBy` (asc/desc toggle)
- [x] Uses `jest.runOnlyPendingTimers()` for debounced table reload (not hard-coded timer values)
- [x] Full plugin test suite passes

Run from `workspaces/todo`:

```bash
yarn test plugins/todo/src/components/TodoList/TodoList.test.tsx
```

### Integration Tests

- [x] Plugin loads in dev app via `createDevApp()` harness
- [x] Mocked API page renders TodoList with table data
- [x] Server-side pagination, sort, and filter wired through `useTable` → `todoApi.listTodos`

### Manual Testing

- [x] Table renders with Tag, Text, File, Author columns
- [x] Per-column filters work (Text, File, Author)
- [x] Column sorting works
- [x] Pagination works with `totalCount > pageSize`
- [x] Empty states: no TODOs vs no matches with active filters
- [x] File links open in new tab
- [x] Long text truncates with tooltips
- [x] Compared migrated UI against original implementation (screenshots in PR)

---

## Implementation Notes

### Week 1 Progress

- Reviewed issue requirements and explored Todo plugin architecture
- Set up Backstage Community Plugins workspace locally
- Identified Material UI / `@backstage/core-components` usage in `TodoList.tsx`
- Researched BUI equivalents and studied Azure DevOps BUI migration PR

### Week 2 Progress

- Implemented initial BUI migration of `TodoList.tsx`
- Migrated table, links, text display, and filter fields
- Added `@backstage/ui` dependency and README documentation
- Created changeset and submitted [PR #9793](https://github.com/backstage/community-plugins/pull/9793)

### Week 3 Progress

- Addressed Copilot review feedback: accessibility labels, stable row IDs, filter/sort tests
- Addressed maintainer review from `awanlin`:
  - Updated changeset to describe full plugin UI migration
  - Dropped React 16 from peer dependency ranges (React 17+)
  - Removed `@material-ui/icons` from dev harness (dev-only)
  - Removed `columnWidths` constant; inlined `width` directly on each `ColumnConfig`
- Rebased onto latest `main` and resolved `yarn.lock` conflict
- Replied to review threads and requested re-review

### `ResponseErrorPanel`

Backstage UI currently does not provide an equivalent replacement for `ResponseErrorPanel`. The existing component supports expandable error details, stack trace display, and copy-to-clipboard functionality. This component was intentionally retained from `@backstage/core-components`, matching other BUI migrations (e.g. Azure DevOps).

### Migration Comparison

**Before (Material UI / core-components Table):**

<img width="1434" height="664" alt="Older Todo Plugin" src="https://github.com/user-attachments/assets/7c9fa253-787c-4f47-a14d-53392666e86b" />

**After (Backstage UI):**

<img width="1438" height="670" alt="Migrated Todo Plugin" src="https://github.com/user-attachments/assets/516718ce-f941-485e-bfd6-301837a59c02" />

### Code Changes

**Files modified:**

| File | Change |
|---|---|
| `plugins/todo/src/components/TodoList/TodoList.tsx` | MUI Table → BUI Card/Table/useTable/ColumnConfig |
| `plugins/todo/src/components/TodoList/TodoList.test.tsx` | Added filter/sort API translation tests |
| `plugins/todo/package.json` | Added `@backstage/ui`; React 17+ peers; removed MUI icons |
| `plugins/todo/README.md` | Documented BUI requirement |
| `plugins/todo/dev/index.tsx` | Removed `@material-ui/icons` (dev-only) |
| `.changeset/migrate-todo-mui-to-bui.md` | Major bump; migration description |
| `yarn.lock` | Updated for new dependencies and peer ranges |

**Branch:** `ashishnamdeo16/bui-migration`

**Approach:** Incremental migration with continuous testing. Preserved server-side offset pagination and per-column filter UX from the original Material Table.

---

## Pull Request

**PR Link:** [backstage/community-plugins#9793](https://github.com/backstage/community-plugins/pull/9793)

**PR Description:** Migrates the Todo plugin UI from Material UI to Backstage UI (`@backstage/ui`). Replaces the table, links, text display, and filter fields in `TodoList`. Adds `@backstage/ui` as a dependency and documents the BUI requirement in the README. Closes #7531.

**Maintainer Feedback (`awanlin` — Changes Requested):**

| Comment | Response |
|---|---|
| Use `ColumnConfig` / question about `columnWidths` | Removed `columnWidths`; set `width` directly on each `ColumnConfig` entry |
| Migrate the entire plugin | Shipped UI fully migrated; `ResponseErrorPanel` and dev harness remain on legacy components (intentional) |
| Drop React 16 from `@types/react` | Updated peer ranges to React 17+; regenerated `yarn.lock` |
| Full migration for small plugin | Removed `@material-ui/icons` from dev dependencies |

**Status:** Review feedback addressed and pushed; re-review requested from `@awanlin`

---

## Current Status

- ✅ Migration completed (shipped UI)
- ✅ Pull Request submitted ([#9793](https://github.com/backstage/community-plugins/pull/9793))
- ✅ CI passing
- ✅ Manual testing completed
- ✅ Review comments addressed
- ⏳ Awaiting maintainer re-review and approval

---

## Learnings & Reflections

### Technical Skills Gained

- Backstage plugin architecture and independent workspace structure
- Backstage UI component library (`Table`, `useTable`, `ColumnConfig`, `Card`, `SearchField`)
- Server-side table patterns with `useTable` offset mode
- Open source contribution workflow: fork, branch, changesets, DCO sign-off, rebase, force-push
- React component migration strategies
- Reading and matching patterns from previously merged PRs

### Challenges Overcome

- Understanding the Backstage community-plugins monorepo (107 independent workspaces)
- Mapping Material UI `TableColumn` to BUI `ColumnConfig`
- Preserving per-column server-side filters without built-in Material Table filter UI
- Generating stable row IDs for paginated server-side data
- Resolving `yarn.lock` conflicts after rebase onto updated `main`
- Interpreting maintainer review comments and iterating on feedback

### What I'd Do Differently Next Time

- Review previously merged BUI migration PRs before starting implementation
- Run `yarn install --immutable` locally before every push to catch lockfile drift early
- Ask clarifying questions on ambiguous review comments sooner
- Create a migration checklist before coding (ColumnConfig, useTable mode, tests, changeset, README)

---

## Resources Used

- [Backstage Documentation](https://backstage.io/docs)
- [Backstage UI Table / ColumnConfig](https://ui.backstage.io/components/table#columnconfig)
- [Backstage Community Plugins Repository](https://github.com/backstage/community-plugins)
- [Issue #7531 — todo: Migrate to Backstage UI](https://github.com/backstage/community-plugins/issues/7531)
- [PR #9793](https://github.com/backstage/community-plugins/pull/9793)
- [Azure DevOps BUI Migration #7599](https://github.com/backstage/community-plugins/pull/7599)
- [Community Plugins CONTRIBUTING.md](https://github.com/backstage/community-plugins/blob/main/CONTRIBUTING.md)
- [React Documentation](https://react.dev)
