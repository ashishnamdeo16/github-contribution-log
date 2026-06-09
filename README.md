# Contribution 1: todo: Migrate to Backstage UI

**Contribution Number:** 1  
**Student:** Ashish Namdeo  
**Issue:** todo: Migrate to Backstage UI  
**Status:** Phase I - In Progress

---

## Why I Chose This Issue

I chose this issue because it closely aligns with my experience in frontend development with React and modern component-based architectures. The task focuses on migrating an existing plugin from Material UI (MUI) to Backstage UI (BUI), which allows me to apply my frontend skills while becoming familiar with the Backstage ecosystem.

As I begin my open source contributions, I'm looking for an issue with a clearly defined scope and measurable outcomes. This migration provides an opportunity to learn Backstage's plugin architecture, UI component library, contribution workflow, and code review process while making a meaningful contribution to a widely used open source project.

---

## Understanding the Issue

### Problem Description

The Todo plugin currently relies on Material UI (MUI) components and legacy UI implementations. Backstage is moving toward the newer Backstage UI (BUI) framework, and the Todo plugin has not yet been migrated. This results in inconsistency with current Backstage UI standards and prevents the plugin from fully leveraging the newer component system.

### Expected Behavior

The Todo plugin should use Backstage UI (BUI) components instead of Material UI (MUI) components while maintaining existing functionality and visual consistency. Any applicable table implementations should also be migrated to the corresponding BUI table components. The plugin should continue to build and function correctly after the migration.

### Current Behavior

The plugin currently imports and uses Material UI components throughout its interface. It also relies on older table implementations from Backstage core components. As a result, the plugin does not conform to the newer Backstage UI framework and design standards.

### Affected Components

- Todo Plugin UI Components
- Material UI (MUI) imports
- Backstage UI (BUI) component replacements
- Table implementations
- Related styling and layout components
- Component tests impacted by UI migration

---

## Reproduction Process

### Environment Setup

- Forked the Backstage Community Plugins repository.
- Cloned the repository locally.
- Installed dependencies using the project setup instructions.
- Started the development environment and verified that the Todo plugin runs successfully.
- Explored the plugin structure and identified areas using Material UI components.

### Steps to Reproduce

1. Clone and set up the repository.
2. Start the development environment.
3. Navigate to the Todo plugin.
4. Inspect the plugin source code.
5. Observe Material UI component usage throughout the plugin.

### Reproduction Evidence

- **Commit showing reproduction:** To be added
- **Screenshots/logs:** To be added
- **My findings:** Multiple UI components currently depend on Material UI and will require migration to their Backstage UI equivalents.

---

## Solution Approach

### Analysis

The issue is not caused by a bug but by a framework migration requirement. The Todo plugin was built using Material UI components before Backstage UI became the preferred component system. The plugin needs to be updated to align with current platform standards.

### Proposed Solution

Replace Material UI components with their Backstage UI equivalents, update table implementations where applicable, verify styling consistency, and ensure all existing functionality continues to work after migration.

### Implementation Plan

#### Understand

Migrate the Todo plugin from Material UI to Backstage UI while preserving behavior and visual consistency.

#### Match

Review other Backstage plugins that have already been migrated to BUI and follow established migration patterns.

#### Plan

1. Audit all Material UI imports within the Todo plugin.
2. Identify corresponding Backstage UI components.
3. Replace component implementations incrementally.
4. Migrate table implementations where applicable.
5. Resolve styling and layout differences.
6. Run tests and build verification.
7. Perform manual UI validation.
8. Submit PR and address review feedback.

#### Implement

- Branch: To be added
- Commits: To be added

#### Review

- Follow Backstage contribution guidelines.
- Maintain existing functionality.
- Remove unnecessary Material UI dependencies.
- Ensure consistent code style.
- Verify successful builds and tests.

#### Evaluate

Success criteria:
- No Material UI usage remains where BUI alternatives exist.
- Plugin builds successfully.
- Existing functionality remains unchanged.
- UI appearance remains consistent.
- Maintainer review feedback is addressed.

---

## Testing Strategy

### Unit Tests

- [ ] Verify Todo list rendering.
- [ ] Verify component interactions continue working.
- [ ] Verify migrated components render correctly.

### Integration Tests

- [ ] Plugin loads successfully within Backstage.
- [ ] Todo workflow functions correctly after migration.

### Manual Testing

- Verify page rendering.
- Verify layout consistency.
- Verify table functionality.
- Verify responsiveness and visual appearance.
- Compare the migrated UI against the original implementation.

---

## Implementation Notes

### Week 1 Progress

- Reviewed issue requirements.
- Set up development environment.
- Explored Todo plugin architecture.
- Identified files using Material UI components.
- Researched available Backstage UI component equivalents.

### Code Changes

- **Files modified:** In progress
- **Key commits:** To be added
- **Approach decisions:** Prioritize incremental migration and validation to minimize regression risk.

---

## Pull Request

**PR Link:** To be added

**PR Description:**

Migrates the Todo plugin from Material UI (MUI) to Backstage UI (BUI) components. Updates applicable table implementations, removes legacy UI dependencies where possible, and preserves existing functionality and visual behavior.

**Maintainer Feedback:**

- Pending review

**Status:** In Progress

---

## Learnings & Reflections

### Technical Skills Gained

- Backstage plugin architecture
- Backstage UI component system
- Open source contribution workflow
- Large monorepo navigation
- UI migration strategies

### Challenges Overcome

- Understanding the Backstage codebase structure.
- Identifying equivalent component mappings between MUI and BUI.
- Maintaining visual consistency during migration.

### What I'd Do Differently Next Time

- Spend additional time reviewing previously merged migration PRs before implementation.
- Create a migration checklist before making code changes.

---

## Resources Used

- Backstage Documentation
- Backstage UI Documentation
- Backstage Community Plugins Repository
- Existing migrated Backstage plugins
- Project contribution guidelines
