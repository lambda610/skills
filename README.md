# Skills

Multi-platform shared skills for OpenClaw and Claude Code.

## Skills

### deepwiki

AI-powered codebase documentation generator.

**Features:**
- Scan codebase structure
- Generate comprehensive documentation
- Create API references and architecture diagrams

**Usage:**

Claude Code:
```
"Scan this codebase and generate documentation"
```

OpenClaw:
```
/deepwiki-scan [path]
/deepwiki-generate
```

## Structure

```
skills/
├── deepwiki/
│   ├── SKILL.md           # Skill definition
│   ├── package.json       # Metadata
│   ├── workflows/        # OpenClaw workflows
│   ├── references/       # Claude Code references
│   └── prompts/          # AI prompts
├── another-skill/
└── yet-another-skill/
```

## Adding New Skills

1. Create a new subdirectory
2. Add SKILL.md with YAML frontmatter
3. Include workflows/, references/, or prompts/ as needed
4. Test with both OpenClaw and Claude Code

## License

MIT
