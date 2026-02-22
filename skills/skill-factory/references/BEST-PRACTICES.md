# Skill Writing Best Practices

Guidelines for writing effective Agent Skills based on Claude Code best practices and real-world experience.

---

## 1. Give AI a Way to Verify Its Work

**Principle**: Provide tests, assertions, or validation logic so the AI can check if it did things correctly.

### Examples

- Include validation scripts in `scripts/validate.py`
- Add `--check` flags to CLI tools
- Provide expected output examples

```python
# scripts/validate.py
def validate_output(result, expected):
    """Validate that the skill produced correct results."""
    assert result == expected, f"Expected {expected}, got {result}"
    return True
```

---

## 2. Explore First, Then Plan, Then Code

**Principle**: Follow the natural workflow: Understand → Design → Implement.

### In Skill Context

1. **Explore**: User describes their problem
2. **Plan**: Skill proposes a solution approach
3. **Implement**: Skill executes the appropriate action

### Skill Description Pattern

```yaml
description: |
  Do X task. Use when: (1) User wants to accomplish X,
  (2) Working with Y type of input, (3) Need to produce Z output.
  Not for: A, B scenarios.
```

---

## 3. Provide Specific Context

**Principle**: Rich, specific descriptions trigger more accurate responses.

### Good vs Bad Descriptions

❌ Bad:
```yaml
description: A skill for processing files.
```

✅ Good:
```yaml
description: |
  Process JSON files and convert them to CSV format.
  Use when: (1) User wants to convert JSON to CSV,
  (2) Working with array-of-objects JSON files,
  (3) Need Excel-compatible output.
  Requires: Valid JSON file with .json extension.
```

### Include Edge Cases

```yaml
description: |
  ... Handles nested JSON (flatts to dot-notation),
  skips null values, truncates strings > 1000 chars.
  Not for: JSON with circular references.
```

---

## 4. Write Effective SKILL.md

### Structure

```yaml
---
name: my-skill
description: Clear trigger description with specific use cases.
metadata: {"openclaw": {...}}
---

# My Skill

## Overview
[What this enables - 1-2 sentences]

## When to Use
- User asks for [specific task]
- Working with [file type/domain]
- Need to [achieve outcome]

## Prerequisites
- [Required tool/bin]
- [Environment variable]

## Bundled Resources
- **scripts/**: [What each script does]
- **references/**: [What each doc covers]

## Examples

### Example 1: [Use Case]
```bash
[Command]
# Expected output
```

### Example 2: [Another Use Case]
...
```

### Keep It Lean

- SKILL.md body < 500 lines
- Use `references/` for detailed docs
- Progressive disclosure: Essential first, details on demand

---

## 5. Use Progressive Disclosure

### Pattern

```
Metadata (~100 tokens) → SKILL.md body (<500 lines) → references/
```

### When to Use References

- Detailed API documentation
- Multiple examples
- Troubleshooting guides
- Configuration options

### Directory Structure

```
my-skill/
├── SKILL.md              # Essential info only
├── references/
│   ├── API.md           # Full API docs
│   ├── EXAMPLES.md      # Many examples
│   └── TROUBLESHOOTING.md
└── scripts/
```

---

## 6. Write Clear Workflows

### Basic Workflow

```yaml
# workflows/convert.yaml
name: convert
description: Convert file format
arguments:
  - name: input
    type: string
    required: true
    description: Input file path
  - name: output
    type: string
    required: false
    description: Output file path
    default: "output.txt"
steps:
  - run: python3 scripts/convert.py
    args: ["{{ args.input }}", "--output", "{{ args.output }}"]
```

### Best Practices

1. **One command, one responsibility**
2. **Use descriptive argument names**
3. **Add validation for required inputs**
4. **Provide sensible defaults**
5. **Document error cases**

---

## 7. Configure Proper Gating

### Pattern

```yaml
metadata: {"openclaw": {
  "requires": {
    "bins": ["python3"],        # All must exist
    "anyBins": ["git", "gh"],  # At least one
    "env": ["API_KEY"],         # Must be set
    "config": ["browser.enabled"]
  },
  "os": ["darwin", "linux"],
  "always": false
}}
```

### When to Use Gating

- ✅ Require specific tools (ffmpeg, git, docker)
- ✅ Require API keys
- ✅ Limit to specific OS
- ❌ Don't over-restrict (avoid "anyBins" if one is sufficient)

---

## 8. Test Your Skill

### Validation Commands

```bash
# Claude Code
pip install skills-ref
skills-ref validate ./my-skill
skills-ref read-properties ./my-skill

# OpenClaw
openclaw skills validate
```

### Manual Testing

1. Create a test case
2. Run the skill
3. Verify output
4. Check error handling

---

## 9. Do's and Don'ts

### Do ✅

- Use kebab-case for names
- Write specific descriptions with use cases
- Include prerequisites
- Provide examples
- Use `references/` for detailed docs
- Test before publishing

### Don't ❌

- Use `<` or `>` in descriptions
- Exceed name/description length limits
- Use `prompts/` directory (not in Agent Skills spec)
- Mismatch directory name with skill name
- Leave description too vague

---

## 10. Common Patterns

### Pattern: CLI Tool Skill

```
cli-tool/
├── SKILL.md
├── scripts/
│   └── tool.py
└── references/
    └── COMMANDS.md
```

### Pattern: API Integration Skill

```
api-client/
├── SKILL.md
├── workflows/
│   ├── fetch.yaml
│   └── submit.yaml
├── scripts/
│   └── client.py
└── references/
    └── API.md
```

### Pattern: File Processor

```
file-processor/
├── SKILL.md
├── scripts/
│   ├── process.py
│   └── validate.py
└── references/
    ├── FORMATS.md
    └── EXAMPLES.md
```

---

## Related

- [SPEC.md](SPEC.md) - Complete dual-platform specification
- [VALIDATION.md](VALIDATION.md) - Validation rules
- [TEMPLATES.md](TEMPLATES.md) - Ready-to-use templates
- [EXAMPLES.md](EXAMPLES.md) - Real-world examples
- [WORKFLOWS.md](WORKFLOWS.md) - Workflow patterns
