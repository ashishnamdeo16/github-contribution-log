# Contribution 1: todo: Migrate to Backstage UI

**Contribution Number:** 1  
**Student:** Ashish Namdeo  
**Issue:** todo: Migrate to Backstage UI  
https://github.com/backstage/community-plugins/issues/7531

**Status:** Phase I - Pull Request Submitted (Awaiting Review)

---

# Current Progress

**Pull Request:** https://github.com/backstage/community-plugins/pull/9793

Resolved Review comments and waiting for the reviewer's response   

## Progress Summary

The migration of the Todo plugin from Material UI (MUI) to Backstage UI (BUI) has been completed successfully. The Pull Request has been submitted to the Backstage Community Plugins repository and is currently awaiting maintainer review and approval.

## Completed Work

### 1. Component Migration

- Migrated Material UI `Link` components to Backstage UI (BUI) `Link`.
- Replaced applicable Material UI components throughout the Todo plugin with their BUI equivalents.
- Removed legacy Material UI dependencies wherever Backstage UI alternatives were available.

### 2. Table Migration

- Successfully migrated the existing table implementation to the Backstage UI Table.
- Preserved all existing functionality, including:
  - Sorting
  - Searching
  - Filtering
  - Pagination
- Carefully refactored the table implementation to preserve existing behavior.
- Performed end-to-end testing after migration.

### 3. Bug Fixes

During the migration, I identified issues related to search and table behavior.

These were resolved by:

- Refactoring the search implementation.
- Preserving the original filtering behavior.
- Validating sorting and pagination.
- Testing the plugin thoroughly in the Backstage development environment.

---

## Migration Comparison

### Older Version

<img width="1434" height="664" alt="Older Todo Plugin" src="https://github.com/user-attachments/assets/7c9fa253-787c-4f47-a14d-53392666e86b" />

### New Version

<img width="1438" height="670" alt="Migrated Todo Plugin" src="https://github.com/user-attachments/assets/516718ce-f941-485e-bfd6-301837a59c02" />

---

### `ResponseErrorPanel`

Backstage UI currently does not provide an equivalent replacement for `ResponseErrorPanel`.

The existing component supports:

- Expandable error details
- Stack trace display
- Copy-to-clipboard functionality
- Retry actions

Attempting to recreate this behavior using BUI `Alert` components introduced React Hooks violations and significantly increased implementation complexity.

Therefore, this component was intentionally retained from `@backstage/core-components`.

---

## Current Status

- ✅ Migration completed
- ✅ Pull Request submitted
- ✅ Build passing
- ✅ Manual testing completed
- ⏳ Awaiting maintainer review and approval

---

# Why I Chose This Issue

I chose this issue because it closely aligns with my experience in frontend development using React and modern component-based architectures. The task focuses on migrating an existing plugin from Material UI (MUI) to Backstage UI (BUI), allowing me to apply my frontend development skills while learning the Backstage ecosystem.

As I begin contributing to open source, I wanted an issue with a clearly defined scope and measurable outcomes. This migration provides an opportunity to understand Backstage's plugin architecture, UI component library, contribution workflow, and code review process while making a meaningful contribution to a widely used open source project.

---

# Understanding the Issue

## Problem Description

The Todo plugin currently relies on Material UI (MUI) components and legacy UI implementations.

Backstage is transitioning toward Backstage UI (BUI), and the Todo plugin had not yet been migrated. This resulted in inconsistency with current UI standards and prevented the plugin from fully adopting the newer component framework.

---

## Expected Behavior

The Todo plugin should:

- Use Backstage UI (BUI) components instead of Material UI.
- Preserve existing functionality.
- Maintain visual consistency.
- Build successfully without regressions.

---

## Previous Behavior

The plugin relied heavily on:

- Material UI components
- Legacy Backstage table implementations
- Older UI patterns that are no longer recommended

---

## Affected Components

- Todo Plugin UI
- Material UI imports
- Backstage UI replacements
- Table implementation
- Styling and layouts
- Related component tests

---

# Reproduction Process

## Environment Setup

- Forked the Backstage Community Plugins repository.
- Cloned the repository locally.
- Installed project dependencies.
- Started the development environment.
- Verified that the Todo plugin was functioning correctly before making changes.
- Identified all Material UI components requiring migration.

---

## Steps to Reproduce

1. Clone the repository.
2. Install project dependencies.
3. Start the Backstage development server.
4. Navigate to the Todo plugin.
5. Inspect the implementation and observe Material UI usage throughout the plugin.

---

## Findings

The Todo plugin depended on multiple Material UI components and an older table implementation that required migration to Backstage UI.

---

# Solution Approach

## Analysis

This issue was not caused by a functional bug but by a framework migration requirement.

The objective was to migrate the Todo plugin from Material UI to Backstage UI while preserving all existing functionality and visual behavior.

---

## Proposed Solution

- Replace Material UI components with Backstage UI equivalents.
- Migrate the table implementation.
- Preserve sorting, searching, filtering, and pagination.
- Retain components that currently have no BUI replacements.
- Validate functionality through testing.

---

# Implementation Plan

## Understand

Study the existing Todo plugin architecture and identify all Material UI dependencies.

---

## Match

Review previously merged Backstage UI migration Pull Requests and follow established migration patterns.

---

## Plan

1. Audit all Material UI imports.
2. Identify equivalent Backstage UI components.
3. Perform incremental component migration.
4. Migrate the table implementation.
5. Resolve styling differences.
6. Execute builds and tests.
7. Validate the UI manually.
8. Submit the Pull Request.

---

## Implement

**Branch:** `feature/todo-bui-migration`

**Pull Request:** https://github.com/backstage/community-plugins/pull/9793

---

## Review

- Followed Backstage contribution guidelines.
- Maintained existing functionality.
- Removed unnecessary Material UI dependencies.
- Preserved visual consistency.
- Verified builds and testing before submitting the Pull Request.

---

## Evaluate

### Success Criteria

- Material UI removed where BUI alternatives exist.
- Plugin builds successfully.
- Existing functionality preserved.
- Visual consistency maintained.
- Pull Request submitted successfully.
- Awaiting maintainer review.

---

# Testing Strategy

## Unit Testing

- [x] Verified Todo list rendering.
- [x] Verified migrated components render correctly.
- [x] Verified component interactions continue functioning.

---

## Integration Testing

- [x] Verified the Todo plugin loads correctly inside Backstage.
- [x] Verified complete Todo workflow after migration.

---

## Manual Testing

- [x] Verified page rendering.
- [x] Verified layout consistency.
- [x] Verified table rendering.
- [x] Verified sorting.
- [x] Verified searching.
- [x] Verified filtering.
- [x] Verified pagination.
- [x] Verified responsive behavior.
- [x] Compared the migrated UI against the original implementation.

---

# Implementation Notes

## Week 1 Progress

- Reviewed issue requirements.
- Set up the development environment.
- Explored the Todo plugin architecture.
- Identified Material UI usage.
- Researched available Backstage UI equivalents.

---

## Week 2 Progress

- Successfully configured the Backstage Community Plugins project locally.
- Studied repository guidelines and previous migration examples.
- Analyzed the Todo plugin architecture.
- Investigated table functionality, filtering, pagination, sorting, and tooltip behavior.
- Planned the migration strategy.

---

## Week 3 Progress

- Completed migration from Material UI to Backstage UI.
- Migrated the table implementation.
- Refactored search logic.
- Fixed migration-related issues.
- Completed manual testing.
- Submitted the Pull Request.
- Currently awaiting maintainer review and approval.

---

## Code Changes

### Files Modified

Multiple UI components within the Todo plugin.

### Pull Request

https://github.com/backstage/community-plugins/pull/9793

### Approach

Performed an incremental migration with continuous testing to minimize regressions while preserving feature parity.

---

# Pull Request

**PR Link**

https://github.com/backstage/community-plugins/pull/9793

---

## PR Description

This Pull Request migrates the Todo plugin from Material UI (MUI) to Backstage UI (BUI).

The migration replaces legacy Material UI components with their Backstage UI equivalents where available, updates the table implementation while preserving existing functionality, and removes obsolete dependencies.

Components without suitable BUI replacements (`OverflowTooltip` and `ResponseErrorPanel`) were intentionally retained from `@backstage/core-components` to preserve functionality until equivalent BUI components become available.

---

## Maintainer Feedback

- Pull Request submitted successfully.
- Currently awaiting maintainer review.
- Any requested changes or review comments will be addressed promptly.

---

## Status

**Awaiting Review and Approval**

---

# Learnings & Reflections

## Technical Skills Gained

- Backstage plugin architecture
- Backstage UI component library
- Large monorepo navigation
- Open source contribution workflow
- React component migration
- UI migration strategies
- Pull Request review process

---

## Challenges Overcome

- Understanding the Backstage codebase.
- Mapping Material UI components to Backstage UI equivalents.
- Migrating complex table behavior.
- Preserving existing functionality during migration.
- Handling components without BUI replacements.

---

## What I'd Do Differently Next Time

- Review previously merged migration Pull Requests before implementation.
- Create a detailed migration checklist before coding.
- Allocate additional time for edge-case testing earlier in the migration process.

---

# Resources Used

- Backstage Documentation
- Backstage UI Documentation
- Backstage Community Plugins Repository
- Existing Backstage UI migration Pull Requests
- Project Contribution Guidelines
- React Documentation
- Material UI Documentation
