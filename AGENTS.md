# AGENTS.md - Superpowers Project

> **AI Agent Instructions for the Superpowers Project**

## ⚠️ CRITICAL: OpenSpec + TDD are MANDATORY

**All development work MUST use the OpenSpec framework with STRICT TDD. NO EXCEPTIONS.**

### TDD Requirements (IRON LAW)

**NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST.**

Every task MUST follow RED-GREEN-REFACTOR:
1. **RED** - Write failing test
2. **Verify RED** - Watch it fail correctly
3. **GREEN** - Write minimal code to pass
4. **Verify GREEN** - Watch it pass
5. **REFACTOR** - Clean up while staying green
6. **Commit** - Frequent commits

**⚠️ If you write code before the test:** Delete it. Start over.
**⚠️ If test passes immediately:** It proves nothing. Start over.
**⚠️ If you skip verification steps:** You're not doing TDD.

**Required skill:** `superpowers:test-driven-development`

### Required Workflow

```
/opsx:init              → Initialize (first time only)
/opsx:explore          → Explore ideas (optional, for unclear requirements)
/opsx:propose <name>   → Create change with specs
/opsx:apply <name>     → Implement
/opsx:archive <name>   → Finalize
```

### Prohibited Actions

**NEVER do these directly - always use OpenSpec:**

- ❌ Use `brainstorming` skill → **Use `/opsx:explore` or `/opsx:propose`**
- ❌ Use `writing-plans` skill → **Use `/opsx:propose`**
- ❌ Use `executing-plans` skill → **Use `/opsx:apply`**
- ❌ Create specs in `docs/superpowers/specs/` → **Use `/opsx:propose` → `openspec/changes/<name>/`**
- ❌ Create plans in `docs/superpowers/plans/` → **Use `/opsx:propose` → `openspec/changes/<name>/tasks.md`**
- ❌ Start implementation without a change → **Use `/opsx:propose` first**

### When a User Requests Legacy Skills

If the user invokes a deprecated skill, you MUST:

1. **REFUSE** to execute the legacy workflow
2. **EXPLAIN** why OpenSpec is required
3. **REDIRECT** to the equivalent OpenSpec command

**Example response:**
```
⚠️ The brainstorming skill is DEPRECATED.

This project now requires OpenSpec for all development work.

Instead of brainstorming, please use:
- /opsx:explore "your idea"  → For exploration
- /opsx:propose your-name    → For creating the spec

Would you like me to run one of these instead?
```

## Project Context

### About Superpowers
- **Type:** AI Assistant Skills Framework
- **Tech Stack:** TypeScript/JavaScript, Node.js, Markdown
- **Architecture:** Modular skills system with subagent support

### Key Directories
- `skills/` - All skills (SKILL.md format)
- `commands/` - Command definitions
- `hooks/` - Hook configurations
- `openspec/` - **OpenSpec directory (REQUIRED)**
- `docs/` - Documentation
- `tests/` - Test suites

### Skill Structure
Each skill is self-contained:
```
skills/<name>/
└── SKILL.md     # Complete skill definition with YAML frontmatter
```

### OpenSpec Structure
```
openspec/
├── config.yaml              # Project configuration
├── specs/                   # Main specifications
├── schemas/                 # Custom schemas
└── changes/
    ├── <change-name>/       # Active changes
    └── archive/             # Completed changes
```

## OpenSpec Commands Reference

### `/opsx:init`
**When:** First time setup, or after cloning
**What:** Creates `openspec/` directory structure
**Required before:** All other OpenSpec commands

**Status in this project:** ✅ Already initialized. The `openspec/` directory exists with config.yaml.

### `/opsx:explore`
**When:** Requirements unclear, need investigation
**What:** Exploratory conversation, no artifacts created
**Leads to:** `/opsx:propose`

### `/opsx:propose <name>`
**When:** Ready to formalize a change
**What:** Creates complete change with:
- `proposal.md` - Problem, solution, scope
- `specs/` - Requirements and scenarios
- `design.md` - Technical approach
- `tasks.md` - Implementation checklist
**Required:** `/opsx:init` first

### `/opsx:apply <name>`
**When:** Ready to implement
**What:** Executes tasks from `tasks.md`
**Modes:** Inline (default) or subagent-driven
**Required:** `/opsx:propose` first

### `/opsx:archive <name>`
**When:** Implementation complete
**What:** Finalizes change, syncs specs, moves to archive
**Optional:** Syncs delta specs to `openspec/specs/`
**Required:** `/opsx:apply` complete

## Legacy Skills (DEPRECATED)

The following skills exist for reference but **MUST NOT BE USED**:

| Skill | Status | Replacement |
|-------|--------|-------------|
| `brainstorming` | ⚠️ DEPRECATED | `/opsx:explore` → `/opsx:propose` |
| `writing-plans` | ⚠️ DEPRECATED | `/opsx:propose` |
| `executing-plans` | ⚠️ DEPRECATED | `/opsx:apply` |

**If these skills are referenced in old plans:**
- Treat them as historical reference only
- Do not execute their workflows
- Redirect to OpenSpec equivalents

## Active Skills (Usable Within OpenSpec)

These skills can be used **within** the OpenSpec framework:

- `subagent-driven-development` - Used by `/opsx:apply` for complex tasks
- `using-git-worktrees` - Used for isolation in `/opsx:apply`
- `finishing-a-development-branch` - Used by `/opsx:archive`
- `test-driven-development` - Used during implementation
- `requesting-code-review` - Used for reviews

## Workflow Examples

### Example 1: Simple Feature

```
User: "Add a dark mode toggle"

AI:  I'll use OpenSpec to handle this feature.

     /opsx:explore "dark mode implementation options"
     → [Discussion about approaches]

     /opsx:propose add-dark-mode
     → [Creates change with all artifacts]

     /opsx:apply add-dark-mode
     → [Implements tasks]

     /opsx:archive add-dark-mode
     → [Finalizes and syncs specs]
```

### Example 2: Clear Requirements

```
User: "Fix the login bug where session expires too fast"

AI:  Requirements are clear, skipping exploration.

     /opsx:propose fix-session-timeout
     → [Creates change with proposal, specs, design, tasks]

     /opsx:apply fix-session-timeout
     → [Implements the fix]

     /opsx:archive fix-session-timeout
     → [Archives completed change]
```

## Critical Rules

1. **Always check for `openspec/` directory** before any new feature
2. **If `openspec/` missing:** Run `/opsx:init` first
3. **Never create specs outside `openspec/changes/`**
4. **Never start implementation without a change**
5. **Always archive completed changes**

## Error Scenarios

### "Use brainstorming skill"
```
User: "Use brainstorming skill"

AI:  ⚠️ The brainstorming skill is DEPRECATED.

     This project now uses OpenSpec for all development:
     - /opsx:explore "your idea" → For exploration
     - /opsx:propose your-name → For creating specs

     Which would you like to use?
```

### "Create a plan for..."
```
User: "Create a plan for the new feature"

AI:  I'll create an OpenSpec change for this feature.

     /opsx:propose new-feature-name
     → [Creates complete change package]
```

### OpenSpec Not Initialized
```
User: "Add authentication"

AI:  ⚠️ OpenSpec is not initialized in this project.

     Let me initialize it first:

     /opsx:init
     → [Creates openspec/ structure]

     Now we can proceed:
     /opsx:explore "authentication options"
     ...
```

## Resources

- OpenSpec Documentation: https://github.com/Fission-AI/OpenSpec/
- Commands Reference: https://github.com/Fission-AI/OpenSpec/blob/main/docs/commands.md
- Workflow Guide: https://github.com/Fission-AI/OpenSpec/blob/main/docs/opsx.md

## Philosophy

```
→ fluid not rigid
→ iterative not waterfall
→ easy not complex
→ built for brownfield not just greenfield
→ scalable from personal projects to enterprises
```

**OpenSpec ensures:**
- Clear specs before implementation
- Traceable changes
- Preserved history
- Quality through review
- No lost context

---

**Last Updated:** 2025-03-26
**Version:** 1.0 (OpenSpec Integration)
