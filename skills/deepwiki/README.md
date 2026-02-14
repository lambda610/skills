# DeepWiki Skill

AI-powered local documentation generator.

## Slash Command

`/deepwiki` - Invokes the skill (describe what you need, e.g., "scan my codebase" or "generate docs for this project")

## Structure

```
deepwiki/
├── SKILL.md              # Main skill definition
├── workflows/            # OpenClaw workflows
├── prompts/              # Reference prompts
└── references/           # Documentation
```

## Note

Claude Code skills use the pattern `/<skill-name>` — one skill directory creates one slash command. Multiple commands require multiple skill directories.

For OpenClaw, multiple commands are supported via `workflows/*.yaml` files.
