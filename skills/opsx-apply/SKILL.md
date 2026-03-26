---
name: opsx-apply
description: Implement tasks from an OpenSpec change. Works through tasks.md, writing code and checking off items. Supports inline and subagent modes.
---

# /opsx:apply

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

## Process

1. **Read tasks.md** - Identify incomplete tasks (`- [ ]`)
2. **Work through tasks** - One by one, in order
3. **Write code** - Create/modify files as specified
4. **Run tests** - Verify as specified in tasks
5. **Mark complete** - Update `[ ]` → `[x]` in tasks.md
6. **Commit** - Frequent commits as specified

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

## Task Structure

Each task should specify:
- **What** to implement
- **Files** to create/modify
- **Tests** to run
- **Expected** results
- **Commit** command

Example:
```markdown
- [ ] **Step 1: Create file**
  Create: `src/example.ts`
  ```typescript
  export function example() { return true; }
  ```
  
  Test: `npm test src/example.test.ts`
  Expected: PASS
  
  Commit: `git add src/example.ts && git commit -m "feat: add example"`
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

## Red Flags (Don't)

**Never:**
- Skip tasks out of order
- Mark tasks complete without verification
- Skip tests specified in tasks
- Implement on main/master without worktree

**Always:**
- Follow task order
- Run specified tests
- Mark tasks `[x]` when complete
- Use worktrees for isolation

## Integration

**Comes after:** `/opsx:propose` (change created)
**Leads to:** `/opsx:archive` (when complete)
**May use:** `superpowers:subagent-driven-development`
**Requires:** `superpowers:using-git-worktrees` (for isolation)

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
