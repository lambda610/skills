# prompt-optimizer

> Prompt Optimizer, but works with AI Skills

[中文版本](./README_zh.md)

A skill for AI prompt optimization, powered by the built-in templates from [linshenkx/prompt-optimizer](https://github.com/linshenkx/prompt-optimizer).

## Overview

This skill provides comprehensive prompt optimization capabilities directly within AI conversation contexts. It transforms vague or simple prompts into well-structured, effective prompts based on established optimization patterns.

## Features

- **Zero Configuration** - Works out of the box without Python environments or API keys
- **Conversational Interface** - Trigger optimization through natural language
- **Progressive Disclosure** - Detailed documentation available in references/ as needed
- **Dual Platform Support** - Compatible with both OpenClaw and Claude Code (Agent Skills)
- **Chinese Language Focus** - Optimized for Chinese prompt engineering

## Supported Operations

| Category | Templates | Description |
|----------|-----------|-------------|
| User Prompt Optimization | 6 | Basic / Planning / Professional + Context variants |
| System Prompt Optimization | 6 | General / Analytical / Format + Context variants |
| Iteration | 3 | General / Context / Image |
| Text-to-Image | 5 | General / Chinese / Photography / Creative / JSON |
| Image-to-Image | 3 | General / Design Copy / JSON |
| Evaluation | 20+ | Original / Optimized / Compare / Direct / Iterative |
| Variable Handling | 2 | Extraction / Value Generation |

## Quick Start

```bash
# User prompt optimization
optimize: write an article for me
plan: create a travel plan
professional: process this data

# System prompt optimization
system prompt: you are an assistant

# Image optimization
/image: a cute cat
image2image: change the background to night scene

# Evaluation
evaluate:
original prompt: write an article for me
optimized prompt: write an article about AI development, 1000 words...
```

## Trigger Keywords

| Feature | Keywords (Chinese) | Keywords (English) |
|---------|-------------------|-------------------|
| User Optimization | `优化：`, `基础优化：`, `规划：`, `专业优化：` | `optimize:`, `plan:`, `professional:` |
| System Optimization | `系统提示词：`, `/system`, `格式化：`, `分析型：` | `system prompt:`, `/system` |
| Iteration | `迭代：`, `改进：` | `iterate:`, `improve:` |
| Text-to-Image | `/image`, `图像：` | `/image`, `image:` |
| Image-to-Image | `图生图：`, `编辑：` | `image2image:`, `edit:` |
| Evaluation | `评估：`, `对比：` | `evaluate:`, `compare:` |
| Variables | `提取变量：`, `生成变量：` | `extract variables:`, `generate variables:` |

## Project Structure

```
prompt-optimizer/
├── SKILL.md              # Main skill definition
├── workflows/           # OpenClaw command definitions
│   ├── optimize.yaml
│   ├── system.yaml
│   ├── image.yaml
│   └── evaluate.yaml
└── references/          # Detailed documentation
    ├── templates.md      # Complete template catalog
    ├── user-optimize.md
    ├── system-optimize.md
    ├── image-optimize.md
    ├── iterate.md
    ├── evaluate.md
    └── variables.md
```

## Template Sources

This skill leverages built-in templates from the prompt-optimizer project:

- `user-optimize` - User prompt optimization
- `optimize` - System prompt optimization
- `iterate` - Iterative optimization
- `image-optimize` - Image generation optimization
- `evaluation` - Prompt evaluation
- `variable-*` - Variable processing

See [references/templates.md](references/templates.md) for the complete template list.

## License

This project is based on [linshenkx/prompt-optimizer](https://github.com/linshenkx/prompt-optimizer), which is licensed under **GNU Affero General Public License v3.0 (AGPL-3.0)**.

See [LICENSE](LICENSE) for the full license text.

```
prompt-optimizer
Copyright (C) 2025 linshenkx

This program is licensed under the GNU Affero General Public License v3.0 only.
```

## Related

- [prompt-optimizer](https://github.com/linshenkx/prompt-optimizer) - Original project
- [Agent Skills Specification](https://agentskills.io/specification) - Skill format specification  
- [OpenClaw](https://openclaw.ai) - AI assistant platform
