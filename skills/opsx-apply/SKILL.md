---
name: opsx-apply
description: Implement tasks from an OpenSpec change using STRICT TDD. Follows RED-GREEN-REFACTOR cycle. NO production code without failing test first.
---

# /opsx:apply

## ⚠️ TDD IS MANDATORY

**NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST.**

Every task MUST follow the TDD cycle:
```
RED → Verify RED → GREEN → Verify GREEN → REFACTOR → Commit
```

**If you write code before the test:** Delete it. Start over.

## Overview

Implement tasks from an OpenSpec change. Reads `tasks.md` and works through incomplete tasks.

**⚠️ WRITES CODE:** This creates/modifies files in the project.

## Usage

```
/opsx:apply [change-name]
```

## Execution Modes

### Mode 1: Inline (Default)
- Execute in current session
- Best for: Simple changes, <5 tasks, clear requirements
- Direct control and visibility

### Mode 2: Subagent-Driven
- Dispatch fresh subagent per task
- Best for: Complex changes, >5 tasks, independent tasks
- Higher quality via two-stage review
- Use: `superpowers:subagent-driven-development`

## TDD Process (STRICT)

For each task, follow EXACTLY:

1. **RED** - Write failing test first (never skip)
2. **Verify RED** - Run test, confirm it fails for expected reason
3. **GREEN** - Write minimal code to pass (no more)
4. **Verify GREEN** - Run test, confirm it passes
5. **REFACTOR** - Clean up, keep tests green (optional but recommended)
6. **Mark complete** - Update `[ ]` → `[x]` in tasks.md
7. **Commit** - Commit after each working cycle

**⚠️ Iron Law:** If you didn't watch the test fail, you don't know if it tests the right thing.

## Task Status Tracking

Tasks use checkbox syntax:
```markdown
- [ ] Task 1: Not started
- [x] Task 2: Complete
- [-] Task 3: In progress (non-standard, avoid)
```

## Example Workflow

```
You: /opsx:apply add-dark-mode

AI:  Implementing add-dark-mode...

     Reading tasks.md:
     - [ ] 1.1 Create ThemeContext
     - [ ] 1.2 Add CSS variables
     - [ ] 1.3 Implement toggle
     - [ ] 1.4 Add persistence

     Working on 1.1: Create ThemeContext...
     [Creates src/context/ThemeContext.tsx]

     ✓ 1.1 Complete

     Working on 1.2: Add CSS variables...
     [Updates src/styles/globals.css]

     ✓ 1.2 Complete
     ...

     All tasks complete!

     Run `/opsx:archive add-dark-mode` to finalize.
```

## Resuming

If interrupted, `/opsx:apply` will:
- Re-read tasks.md
- Identify remaining `[ ]` tasks
- Continue from where it left off

## Task Structure (TDD Format)

Each task MUST follow TDD steps:

Example:
```markdown
- [ ] **Step 1: RED - Write failing test**
  Create: `src/example.test.ts`
  ```typescript
  test('example returns true', () => {
    expect(example()).toBe(true);
  });
  ```

- [ ] **Step 2: Verify RED**
  Run: `npm test src/example.test.ts`
  Expected: FAIL with "example is not defined"

- [ ] **Step 3: GREEN - Minimal implementation**
  Create: `src/example.ts`
  ```typescript
  export function example() { return true; }
  ```

- [ ] **Step 4: Verify GREEN**
  Run: `npm test src/example.test.ts`
  Expected: PASS

- [ ] **Step 5: REFACTOR (if needed)**
  Improvements while keeping tests green

- [ ] **Step 6: Commit**
  ```bash
  git add src/example.test.ts src/example.ts
  git commit -m "feat: add example function"
  ```
```

## Subagent Mode

For complex work, use subagent-driven development:

```
You: /opsx:apply add-dark-mode --mode subagent

AI:  Using subagent-driven-development mode...

     Dispatching fresh subagent for Task 1...
     [Subagent implements Task 1]
     [Two-stage review: spec compliance, then code quality]
     ✓ Task 1 complete

     Dispatching fresh subagent for Task 2...
     ...
```

## Red Flags (TDD Violations - STOP!)

**NEVER (Iron Law):**
- ❌ Write code before test
- ❌ Skip "Verify RED" step
- ❌ Skip "Verify GREEN" step
- ❌ Test passes immediately (proves nothing)
- ❌ Keep code written before tests
- ❌ Add features beyond what test requires (YAGNI violation)
- ❌ Mark tasks complete without watching tests pass

**ALWAYS:**
- ✅ Write failing test FIRST
- ✅ Watch test FAIL (correctly)
- ✅ Write minimal code to pass
- ✅ Watch test PASS
- ✅ Commit after each cycle
- ✅ Delete any code written before tests

**If you violate TDD:** Delete code. Start over.

## Integration

**Comes after:** `/opsx:propose` (change created)
**Leads to:** `/opsx:archive` (when complete)
**Uses (REQUIRED):**
- `superpowers:test-driven-development` - TDD cycle enforcement
- `superpowers:subagent-driven-development` - For complex tasks
- `superpowers:using-git-worktrees` - For isolation

**Subagent Instructions:**
When dispatching subagents for implementation, they MUST:
1. Follow `superpowers:test-driven-development` skill
2. Write failing test first
3. Watch it fail
4. Write minimal code
5. Watch it pass
6. Only then mark task complete

## When to Stop

**STOP immediately when:**
- Task is unclear or blocked
- Tests fail repeatedly
- Plan has critical gaps
- Implementation diverges from spec

**Ask for clarification rather than guessing.**

## Philosophy

```
→ Follow the plan
→ Verify as you go
→ Incremental progress
→ Quality over speed
```
