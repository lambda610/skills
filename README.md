# Skills

Multi-platform shared skills for OpenClaw and Claude Code (Agent Skills).

## Available Skills

### [deepwiki](./skills/deepwiki) 🕵️
AI-powered codebase documentation generator.
- Deep code analysis with business logic extraction
- Architecture diagrams and data flow mapping
- API documentation with signatures
- Code patterns identification

### [jujutsu](./skills/jujutsu) 🦜
Use Jujutsu (jj) for version control in jj-enabled projects.
- Command workflows and bookmark management
- Rebasing and conflict resolution
- Revsets and common pitfalls
- Colocated workspaces and multiple remotes

### [prompt-optimizer](./skills/prompt-optimizer) ✨
AI 提示词优化工具 / AI Prompt Optimization Tool
- 用户提示词优化 (Basic/Planning/Professional)
- 系统提示词优化 (General/Analytical/Format)
- 图像提示词优化 (Text-to-Image/Image-to-Image)
- 提示词评估与迭代

### [skill-factory](./skills/skill-factory) 🏭
Create dual-compatible skills for OpenClaw and Claude Code.
- Unified YAML frontmatter structure
- Agent Skills spec compliance
- Workflows and validation

### 🚧 WIP ~~[Kanban](./skills/kanban)~~
Asynchronous task management system.
- Add tasks to inbox with priority/project/category/tags
- View task progress (active/backlog)
- Async task handling (not immediate execution)

## Installation

```bash
# Install all skills
npx skills install

# Or link manually
ln -sf skills/deepwiki ~/.config/claude-code/plugins/deepwiki
ln -sf skills/jujutsu ~/.config/claude-code/plugins/jujutsu
ln -sf skills/prompt-optimizer ~/.config/claude-code/plugins/prompt-optimizer
ln -sf skills/skill-factory ~/.config/claude-code/plugins/skill-factory
```

## License

See individual skills for their licenses.
