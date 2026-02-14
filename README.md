# Skills

Multi-platform shared skills for OpenClaw and Claude Code (Agent Skills).

## Available Skills

### [deepwiki](./skills/deepwiki)
AI-powered codebase documentation generator.
- Deep code analysis with business logic extraction
- Architecture diagrams and data flow mapping
- API documentation with signatures
- Code patterns identification

### [prompt-optimizer](./skills/prompt-optimizer) ✨
AI 提示词优化工具 / AI Prompt Optimization Tool
- 用户提示词优化 (Basic/Planning/Professional)
- 系统提示词优化 (General/Analytical/Format)
- 图像提示词优化 (Text-to-Image/Image-to-Image)
- 提示词评估与迭代

### [skill-factory](./skills/skill-factory)
Create dual-compatible skills for OpenClaw and Claude Code.
- Unified YAML frontmatter structure
- Agent Skills spec compliance
- Workflows and validation

### [bmad](./skills/bmad)
BMad (Breakthrough Method of Agile AI Driven Development)
- AI-driven agile development framework
- PRD and architecture planning
- Agile stories with AI collaboration

## Installation

```bash
# Install all skills
npx skills install

# Or link manually
ln -sf skills/deepwiki ~/.config/claude-code/plugins/deepwiki
ln -sf skills/prompt-optimizer ~/.config/claude-code/plugins/prompt-optimizer
ln -sf skills/skill-factory ~/.config/claude-code/plugins/skill-factory
ln -sf skills/bmad ~/.config/claude-code/plugins/bmad
```

## License

See individual skills for their licenses.
