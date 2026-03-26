---
name: opsx-archive
description: Archive a completed OpenSpec change. Finalizes the change, syncs delta specs to main, and moves to openspec/changes/archive/.
---

# /opsx:archive

## Overview

Archive a completed OpenSpec change. Finalizes the work, syncs specifications, and preserves the change history.

**⚠️ FINALIZATION:** This moves the change to archive and syncs specs.

## Usage

```
/opsx:archive [change-name]
```

## What It Does

1. **Verify completion** - Check all artifacts exist
2. **Check tasks** - Verify tasks are complete (warns if not)
3. **Sync specs** - Merge delta specs to `openspec/specs/` (optional)
4. **Move to archive** - `openspec/changes/archive/YYYY-MM-DD-<name>/`
5. **Preserve history** - Full audit trail maintained

## Spec Sync Process

If requested, syncs delta specs:

```
Reading: openspec/changes/add-dark-mode/specs/ui/spec.md
Target:  openspec/specs/ui/spec.md

Changes:
✓ ADDED: Theme Selection requirement
✓ ADDED: Accessibility requirement

Merging...
✓ openspec/specs/ui/spec.md updated
```

## Spec Delta Format

Specs use ADDED/MODIFIED/REMOVED sections:

```markdown
## ADDED Requirements
New requirements added by this change

## MODIFIED Requirements
Existing requirements changed

## REMOVED Requirements
Requirements no longer needed
```

## Archive Structure

```
openspec/changes/archive/
└── 2025-01-23-add-dark-mode/
    ├── .openspec.yaml      # Original metadata
    ├── proposal.md          # Original proposal
    ├── specs/               # Original delta specs
    ├── design.md            # Original design
    └── tasks.md             # Original tasks (with completion status)
```

## Example Workflow

```
You: /opsx:archive add-dark-mode

AI:  Archiving add-dark-mode...

     Verifying completion:
     ✓ proposal.md exists
     ✓ specs/ exists
     ✓ design.md exists
     ✓ tasks.md exists (8/8 tasks complete)

     Delta specs: Not yet synced
     → Sync to main specs? (recommended)

You: Yes

AI:  Syncing specs...
     ✓ openspec/specs/ui/spec.md updated
     
     Archiving...
     ✓ Moved to openspec/changes/archive/2025-01-23-add-dark-mode/

     Change archived successfully.
     Full history preserved.
```

## Completion Check

Before archiving, verifies:
- [ ] All artifacts exist
- [ ] Tasks are complete (or warns)
- [ ] Tests pass (or warns)

**Note:** Archive won't block on incomplete tasks but will warn.

## When to Archive

**Archive when:**
- All tasks in tasks.md are complete
- Tests pass
- Code is committed
- Feature is ready/done

**Don't archive when:**
- Tasks incomplete (unless intentionally partial)
- Tests failing
- Work not committed

## Sync vs No Sync

**Sync specs when:**
- Change affects main specifications
- Other changes depend on these specs
- You want specs in main for reference

**Skip sync when:**
- Change is experimental
- Specs are temporary
- You want to keep specs in change only

## Bulk Archive

For multiple completed changes:
```
/opsx:bulk-archive
```

Handles spec conflicts between changes automatically.

## Red Flags (Don't)

**Never:**
- Archive incomplete work without note
- Delete change without archiving
- Forget to sync important spec changes
- Archive on uncommitted changes

**Always:**
- Verify tasks complete
- Sync specs when relevant
- Preserve full history
- Run tests before archive

## Integration

**Comes after:** `/opsx:apply` (implementation complete)
**May use:** `superpowers:finishing-a-development-branch` (for git workflow)
**Updates:** `openspec/specs/` (main specs)
**Final state:** Change archived with full history

## Philosophy

```
→ Preserve history
→ Sync knowledge
→ Clean workspace
→ Clear completion
```

## Complete Workflow

```
/opsx:init              → Initialize
/opsx:explore          → Explore ideas
/opsx:propose feature   → Create change
/opsx:apply feature     → Implement
/opsx:archive feature   → Finalize

Repeat for each feature.
```
