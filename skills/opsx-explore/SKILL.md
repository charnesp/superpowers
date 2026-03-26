---
name: opsx-explore
description: Think through ideas, investigate problems, clarify requirements BEFORE committing to a change. No artifacts created during exploration.
---

# /opsx:explore

## Overview

Exploration phase for thinking through ideas, investigating problems, and clarifying requirements **before** committing to a change.

**⚠️ NO ARTIFACTS CREATED:** This is purely exploratory conversation.

**When ready to commit:** Transition to `/opsx:propose`

## Usage

```
/opsx:explore [topic]
```

## When to Use

- Requirements are unclear or need investigation
- Need to understand current codebase before proposing changes
- Comparing multiple approaches before deciding
- Exploring technical feasibility
- Clarifying scope and constraints

## When to Transition

**Move to `/opsx:propose` when:**
- Intent is clear (what problem we're solving)
- Scope is defined (what's in/out of bounds)
- Approach is chosen (how we'll solve it)
- Success criteria are understood

## What It Does

1. **Investigates codebase** - Reads relevant files to understand context
2. **Asks clarifying questions** - One at a time, refines understanding
3. **Compares options** - Presents 2-3 approaches with trade-offs
4. **Creates visual aids** - Diagrams if helpful (optional)
5. **Transitions to proposal** - When ready to formalize

## Example Workflow

```
You: /opsx:explore "How should we handle authentication?"

AI:  Let me investigate your current auth setup...

     [Reads codebase]

     I see you're using session-based auth. For mobile, 
     three main options:

     1. JWT tokens (stateless, works offline)
     2. OAuth2 (if you need third-party login)
     3. Extend current sessions (simpler, needs connectivity)

     Which direction interests you?

You: JWT sounds good.

AI:  Good choice. JWT will require:
     - Token generation endpoint
     - Refresh token mechanism
     - Secure storage on client
     - Middleware for validation

     Ready to formalize this in a proposal?

You: Yes.

AI:  Run `/opsx:propose add-jwt-auth` to create the change.
```

## Key Principles

- **One question at a time** - Don't overwhelm
- **Multiple choice preferred** - Easier than open-ended
- **No commitment yet** - Just exploration
- **Can go deep** - Investigation is encouraged
- **Transition when ready** - Move to propose when clear

## Red Flags (Don't)

**Never:**
- Create files during exploration
- Write implementation code
- Generate artifacts (specs, plans)
- Rush to `/opsx:propose` before clarity

**Always:**
- Answer questions completely
- Provide context when asked
- Transition explicitly when ready

## Integration

**Leads to:** `/opsx:propose` (when ready to formalize)
**Comes after:** `/opsx:init` (OpenSpec must be initialized)
**Alternative:** Can jump to `/opsx:propose` if already clear

## Philosophy

```
→ Think before building
→ Explore before committing
→ Understand before formalizing
→ Fluid not rigid
```
