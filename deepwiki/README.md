# DeepWiki Skill for OpenClaw

AI-powered local documentation generator.

## Quick Start

```bash
/deepwiki-scan ./my-project
/deepwiki-generate
```

## Commands

| Command | Description |
|---------|-------------|
| `/deepwiki-scan` | Analyze codebase structure |
| `/deepwiki-generate` | Generate full documentation |
| `/deepwiki-api` | Document APIs only |

## Files

```
deepwiki/
├── SKILL.md              # Main documentation
├── package.json          # Metadata
├── workflows/
│   ├── scan.md           # Scan workflow
│   └── generate.md        # Generate workflow
└── prompts/
    ├── architecture.md  # Architecture prompt
    └── api.md            # API documentation prompt
```

## See Also

- [SKILL.md](SKILL.md) for full documentation
- [workflows/](workflows/) for workflow guides
- [prompts/](prompts/) for AI prompts

## Inspired by

- DeepWiki (deepwiki.com)
- Devin by CognitionAI
