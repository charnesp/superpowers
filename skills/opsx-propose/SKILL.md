---
name: opsx-propose
description: Create a new OpenSpec change with all planning artifacts. Generates proposal, specs, design, and tasks in openspec/changes/<name>/.
---

# /opsx:propose

## Overview

Create a complete OpenSpec change with all planning artifacts. This is the formalization step that creates the structure for implementation.

**⚠️ CREATES ARTIFACTS:** This generates files in `openspec/changes/<name>/`

## Usage

```
/opsx:propose [change-name-or-description]
```

## What It Creates

```
openspec/changes/<change-name>/
├── .openspec.yaml              # Change metadata
├── proposal.md                  # Why we're doing this
├── specs/
│   └── <capability>/
│       └── spec.md              # Requirements & scenarios
├── design.md                    # Technical approach
└── tasks.md                     # Implementation checklist
```

## Process

1. **Creates change directory** - `openspec/changes/<name>/`
2. **Generates .openspec.yaml** - Metadata (schema, created date)
3. **Writes proposal.md** - Problem, solution, scope, success criteria
4. **Writes specs/** - Requirements with Given/When/Then scenarios
5. **Writes design.md** - Architecture, components, data flow
6. **Writes tasks.md** - Implementation steps with checkboxes

## Artifact Templates

### .openspec.yaml
```yaml
schema: spec-driven
name: add-dark-mode
created: 2025-01-23T10:00:00Z
```

### proposal.md
```markdown
# Proposal: [Change Name]

## Problem
What problem are we solving?

## Solution
How will we solve it?

## Scope
- In scope: ...
- Out of scope: ...

## Success Criteria
How do we know it's done?
```

### specs/<capability>/spec.md
```markdown
# [Capability] Specification

## ADDED Requirements

### Requirement: [Name]
**Status:** NEW

**Scenarios:**
1. [Scenario name]
   - Given [context]
   - When [action]
   - Then [expected result]
```

### design.md
```markdown
# Technical Design: [Change Name]

## Overview
High-level approach

## Architecture
System design

## Components
Key components and responsibilities

## Data Flow
How data moves through the system

## Error Handling
Error scenarios and responses

## Testing Strategy
How we'll test this
```

### tasks.md (TDD REQUIRED)
```markdown
# Implementation Tasks: [Change Name]

## Task 1: [Component Name]

- [ ] **Step 1: RED - Write failing test**
  Create: `src/example.test.ts`
  ```typescript
  test('specific behavior', () => {
    const result = functionUnderTest(input);
    expect(result).toBe(expected);
  });
  ```

- [ ] **Step 2: Verify RED - Watch it fail**
  Run: `npm test src/example.test.ts`
  Expected: FAIL with "function not defined"

- [ ] **Step 3: GREEN - Write minimal implementation**
  Create: `src/example.ts`
  ```typescript
  export function functionUnderTest(input) {
    return expected;
  }
  ```

- [ ] **Step 4: Verify GREEN - Watch it pass**
  Run: `npm test src/example.test.ts`
  Expected: PASS

- [ ] **Step 5: REFACTOR - Clean up (if needed)**
  - Remove duplication
  - Improve names
  - Keep tests green

- [ ] **Step 6: Commit**
  ```bash
  git add src/example.test.ts src/example.ts
  git commit -m "feat: add specific feature"
  ```
```

**⚠️ TDD IS MANDATORY:** Every task MUST follow RED-GREEN-REFACTOR cycle.
**⚠️ NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST.**

## Example

```
You: /opsx:propose add-dark-mode

AI:  Creating openspec/changes/add-dark-mode/

     ✓ .openspec.yaml
     ✓ proposal.md
     ✓ specs/ui/spec.md
     ✓ design.md
     ✓ tasks.md

     Change created with 8 tasks.
     Ready for implementation.

     Run `/opsx:apply add-dark-mode` to begin.
```

## Tips

- Use descriptive kebab-case names: `add-feature`, `fix-bug`, `refactor-module`
- Avoid generic names: `update`, `changes`, `wip`
- Can edit artifacts after creation before `/opsx:apply`
- Each change should be focused and completable

## TDD Requirements

**MANDATORY:** All tasks.md MUST use strict TDD (RED-GREEN-REFACTOR):

1. **RED** - Write failing test first
2. **Verify RED** - Watch it fail for expected reason
3. **GREEN** - Write minimal code to pass
4. **Verify GREEN** - Watch it pass
5. **REFACTOR** - Clean up while staying green
6. **Commit** - Frequent commits

**⚠️ Iron Law:** NO production code without a failing test first.
**⚠️ If code exists before test:** Delete it. Start over.

## Integration

**Comes after:** `/opsx:explore` (or directly if already clear)
**Leads to:** `/opsx:apply` (implementation with TDD)
**Requires:** 
- `/opsx:init` (OpenSpec initialized)
- `superpowers:test-driven-development` (TDD skill)

## Red Flags (Don't)

**Never:**
- Skip creating all artifacts
- Start implementing before `/opsx:apply`
- Create multiple changes for the same feature
- Use vague change names

**Always:**
- Create complete artifacts
- Define clear scope
- Include verification steps in tasks
- Reference required skills in tasks

## Philosophy

```
→ Agree before building
→ Specs drive implementation
→ Clear scope prevents scope creep
→ Document for future maintainers
```
