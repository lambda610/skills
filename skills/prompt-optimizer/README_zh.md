# prompt-optimizer

> Prompt Optimizer，但适用于 AI Skills

AI 提示词优化工具，基于 [linshenkx/prompt-optimizer](https://github.com/linshenkx/prompt-optimizer) 项目内置模板。

[English Version](./README.md)

## 概述

本技能提供全面的提示词优化能力，可直接在 AI 对话中使用。它将模糊或简单的提示词转化为结构化、有效的提示词。

## 特性

- **零配置** - 无需 Python 环境或 API Key，开箱即用
- **对话式交互** - 通过自然语言触发优化
- **渐进披露** - 详细文档位于 references/，按需查看
- **双平台支持** - 兼容 OpenClaw 和 Claude Code (Agent Skills)
- **中文优化** - 专门针对中文提示词优化场景

## 支持的操作

| 类别 | 模板数 | 描述 |
|------|--------|------|
| 用户提示词优化 | 6 | 基础/规划/专业 + 上下文版 |
| 系统提示词优化 | 6 | 通用/分析/格式 + 上下文版 |
| 迭代改进 | 3 | 通用/上下文/图像 |
| 文生图优化 | 5 | 通用/中文/摄影/创意/JSON |
| 图生图优化 | 3 | 通用/文案替换/JSON |
| 提示词评估 | 20+ | 原始/优化后/对比/直接/迭代 |
| 变量处理 | 2 | 提取/值生成 |

## 快速开始

```bash
# 用户提示词优化
优化：帮我写个文章
规划：帮我做一个旅行计划
专业优化：帮我处理数据

# 系统提示词优化
系统提示词：你是一个助手

# 图像优化
/image 一只猫
图生图：把背景换成夜景

# 评估对比
评估：
原始提示词：帮我写个文章
优化后提示词：请写一篇关于AI的文章...
```

## 触发关键词

| 功能 | 关键词 |
|------|--------|
| 用户优化 | `优化：`, `基础优化：`, `规划：`, `专业优化：` |
| 系统优化 | `系统提示词：`, `/system`, `格式化：`, `分析型：` |
| 迭代 | `迭代：`, `改进：` |
| 文生图 | `/image`, `图像：` |
| 图生图 | `图生图：`, `编辑：` |
| 评估 | `评估：`, `对比：` |
| 变量 | `提取变量：`, `生成变量：` |

## 项目结构

```
prompt-optimizer/
├── SKILL.md              # 主技能定义
├── workflows/           # OpenClaw 命令定义
│   ├── optimize.yaml
│   ├── system.yaml
│   ├── image.yaml
│   └── evaluate.yaml
└── references/          # 详细文档
    ├── templates.md      # 完整模板清单
    ├── user-optimize.md
    ├── system-optimize.md
    ├── image-optimize.md
    ├── iterate.md
    ├── evaluate.md
    └── variables.md
```

## 模板来源

本技能使用 prompt-optimizer 项目的内置模板：

- `user-optimize` - 用户提示词优化
- `optimize` - 系统提示词优化
- `iterate` - 迭代优化
- `image-optimize` - 图像优化
- `evaluation` - 提示词评估
- `variable-*` - 变量处理

完整模板列表见 [references/templates.md](references/templates.md)。

## License

本项目基于 [linshenkx/prompt-optimizer](https://github.com/linshenkx/prompt-optimizer)，遵循 **GNU Affero General Public License v3.0 (AGPL-3.0)**。

详见 [LICENSE](LICENSE)。

```
prompt-optimizer
Copyright (C) 2025 linshenkx

This program is licensed under the GNU Affero General Public License v3.0 only.
```

## 相关项目

- [prompt-optimizer](https://github.com/linshenkx/prompt-optimizer) - 原版项目
- [Agent Skills 规范](https://agentskills.io/specification) - 技能格式规范
- [OpenClaw](https://openclaw.ai) - AI 助手平台
