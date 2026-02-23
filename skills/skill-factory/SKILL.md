---
name: skill-factory
description: Create skills compatible with both OpenClaw and Claude Code (Agent Skills). Use when: (1) Building a new skill that supports dual platforms, (2) Need unified YAML frontmatter with proper validation. Not for: Single-platform skills that don't need cross-compatibility.
metadata: {"openclaw": {"emoji": "🛠"}}
---

# Skill Factory

Create dual-compatible skills following both **Agent Skills spec** (agentskills.io) and **OpenClaw** specifications.

## Core Understanding

### Two Ecosystems, One Skill

| Aspect | Agent Skills (Claude Code) | OpenClaw |
|--------|---------------------------|----------|
| **Trigger** | YAML frontmatter `description` matches user message | Commands via `/skill-cmd` |
| **Validation** | `skills-ref validate` | `openclaw skills validate` |
| **Optional dirs** | `scripts/`, `references/`, `assets/` | `scripts/`, `references/` |
| **Key extension** | - | `metadata.openclaw` for gating |

### Unified Approach

```yaml
# Always include this for both platforms
---
name: skill-name              # kebab-case, max 64 chars
description: Clear trigger... # max 1024 chars
license: Apache-2.0           # optional
compatibility:                 # optional, max 500 chars
metadata:                     # optional, client-specific
  openclaw:                   # OpenClaw-specific gating
    requires:
      bins: []
      env: []
      config: []
---
```

## When to Use

- User wants to create a new skill for both OpenClaw and Claude Code
- Need to validate skill structure before publishing
- Want to follow Agent Skills specification

## Prerequisites

- Python 3.x (for validation scripts)
- (Optional) git for version control
- (Optional) skills-ref for Claude Code validation: `pip install skills-ref`

## Examples

### Create a basic skill structure
```bash
mkdir -p my-skill/{scripts,references,assets}
# Then write SKILL.md with YAML frontmatter
```

### Validate a skill
```bash
# Claude Code
skills-ref validate ./my-skill

# OpenClaw (built-in)
openclaw skills validate
```

## Workflow: Creating a New Skill

### Step 1: Initialize

Create the skill directory manually:

```bash
mkdir -p my-skill/{scripts,references,assets}
```

### Step 2: Write SKILL.md

Follow the spec exactly:

```yaml
---
name: my-skill
description: Comprehensive description of what this skill does. Include specific triggers: (1) When user wants X, (2) For Y tasks, (3) Working with Z files.
metadata:
  {
    "openclaw": {
      "requires": { "bins": ["python3"], "env": ["API_KEY"] },
      "emoji": "🛠"
    }
  }
---

# My Skill

## Overview

[What this enables]

## When to Use

- User asks for [specific task]
- Working with [file type/domain]

## Bundled Resources

- **scripts/**: Executable utilities
- **references/**: Detailed documentation
- **assets/**: Templates
```

### Step 3: Validate

```bash
# Agent Skills validation
skills-ref validate ./my-skill

# OpenClaw validation
openclaw skills validate
```

## Validation Rules (from Specs)

### Name Validation

- **Max length**: 64 characters
- **Format**: lowercase, kebab-case (letters, digits, hyphens)
- **Rules**:
  - Must be lowercase
  - Cannot start/end with hyphen
  - No consecutive hyphens
  - Directory name must match skill name
  - Supports i18n (Unicode letters via NFKC normalization)

### Description Validation

- **Max length**: 1024 characters
- **Rules**:
  - Must be non-empty string
  - No angle brackets (`<` or `>`) - triggers XSS in some contexts

### Metadata Fields

**Allowed (Agent Skills)**:
- `name`, `description`, `license`, `compatibility`, `allowed-tools`, `metadata`

**Allowed (OpenClaw extension)**:
```yaml
metadata:
  {
    "openclaw": {
      "always": true,
      "emoji": "🎨",
      "homepage": "https://...",
      "os": ["darwin", "linux"],
      "requires": {
        "bins": [],
        "anyBins": [],
        "env": [],
        "config": []
      },
      "primaryEnv": "API_KEY",
      "install": [...]
    }
  }
```

## Progressive Disclosure Pattern

For detailed guidance, see:
- [SPEC.md](references/SPEC.md) - Complete dual-platform spec
- [VALIDATION.md](references/VALIDATION.md) - Validation rules
- [TEMPLATES.md](references/TEMPLATES.md) - Ready-to-use templates
- [EXAMPLES.md](references/EXAMPLES.md) - Real-world skills
- [BEST-PRACTICES.md](references/BEST-PRACTICES.md) - Writing effective skills

## Common Patterns

### Agent Skills Structure

```
my-skill/
├── SKILL.md               # YAML frontmatter + instructions
├── scripts/               # Executable code
├── references/            # Detailed documentation
└── assets/                # Templates
```

### OpenClaw Extension

OpenClaw adds optional metadata for gating and installation:

```yaml
---
name: my-skill
description: ...
metadata:
  {
    "openclaw": {
      "requires": { "bins": ["python3"] },
      "emoji": "🛠"
    }
  }
---
```

## Key Principles

1. **YAML Frontmatter Required** - Always include for Agent Skills compatibility
2. **OpenClaw metadata optional** - Add only if you need gating/install
3. **Avoid prompts/** - Not part of Agent Skills spec
4. **Keep SKILL.md lean** - Use references/ for detailed docs
5. **One repo, both platforms** - Both platforms read SKILL.md, scripts/, references/

## Best Practices for Writing Skills

### 1. Give AI a Way to Verify Its Work
- Include validation scripts in `scripts/`
- Add `--check` flags to CLI tools
- Provide expected output examples

### 2. Explore First, Then Plan, Then Code
- User describes problem → Skill proposes approach → Skill executes
- Write clear "When to Use" sections

### 3. Provide Specific Context
- Include specific use cases in description: `(1) When user wants X, (2) For Y tasks, (3) Working with Z files`
- Document edge cases and limitations
- List prerequisites clearly

### 4. Write Effective SKILL.md
- Overview: 1-2 sentences
- When to Use: specific scenarios
- Prerequisites: required tools/env
- Examples: with expected outputs

### 5. Use Progressive Disclosure
```
Metadata (~100 tokens) → SKILL.md body (<500 lines) → references/
```

### 6. Test Before Publishing
```bash
# Claude Code
pip install skills-ref
skills-ref validate ./my-skill

# OpenClaw
openclaw skills validate
```

See [BEST-PRACTICES.md](references/BEST-PRACTICES.md) for detailed guidance.
