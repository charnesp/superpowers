---
name: opsx-init
description: Initialize OpenSpec in a project. MUST run before using any other /opsx:* commands. Creates the openspec/ directory structure.
---

# /opsx:init

## Overview

Initialize OpenSpec in the current project. This creates the required directory structure and configuration for using OpenSpec workflows.

**⚠️ REQUIRED FIRST STEP:** Run this before any other OpenSpec command.

## Usage

```
/opsx:init
```

## What It Creates

```
openspec/
├── config.yaml              # Project configuration
├── specs/                   # Main specifications directory
├── schemas/                 # Custom schemas (if needed)
└── changes/
    └── archive/             # Archived changes
```

## Configuration

The `config.yaml` includes:
- Schema selection (default: spec-driven)
- Project context (tech stack, conventions)
- Rules per artifact type (proposal, specs, design, tasks)

## Integration

**Must be run before:**
- `/opsx:explore`
- `/opsx:propose`
- `/opsx:apply`
- `/opsx:archive`

**When to re-run:**
- After cloning a project that uses OpenSpec
- When setting up OpenSpec in a new project
- After major project restructuring

## Example

```
You: /opsx:init

AI:  Initializing OpenSpec...

    Created openspec/config.yaml
    Created openspec/specs/
    Created openspec/schemas/
    Created openspec/changes/
    Created openspec/changes/archive/

    ✓ OpenSpec initialized successfully!

    You can now use:
    - /opsx:explore  → Explore ideas
    - /opsx:propose  → Create changes
    - /opsx:apply    → Implement changes
    - /opsx:archive  → Archive completed changes
```

## Post-Init Checklist

After initialization:
- [ ] Verify `openspec/` directory exists
- [ ] Review and customize `openspec/config.yaml` if needed
- [ ] Commit the openspec/ directory to git

## OpenSpec Philosophy

```
→ fluid not rigid
→ iterative not waterfall
→ easy not complex
→ built for brownfield not just greenfield
→ scalable from personal projects to enterprises
```

## Learn More

- Documentation: https://github.com/Fission-AI/OpenSpec/
- Commands: https://github.com/Fission-AI/OpenSpec/blob/main/docs/commands.md
- Workflow: https://github.com/Fission-AI/OpenSpec/blob/main/docs/opsx.md
