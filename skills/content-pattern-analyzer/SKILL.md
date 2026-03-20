---
name: content-pattern-analyzer
description: 对任意内容平台做结构化规律分析，帮助创作者理解什么内容能火。触发：用户说"分析X平台内容规律" / "帮我理解X平台什么内容能火" / "Content Pattern Analyzer" 时使用。
---

# Content Pattern Analyzer

对内容平台进行结构化规律分析的框架。输入平台 + 数据，输出可操作的创作者指南。

## 工作流

```
1. 数据提取 — 从平台数据集提取原始数据
2. 定量发现 — 算分数/点赞分布、互动率等核心指标
3. 跨分段对比 — 高赞 vs 中赞内容结构差异
4. 人工精读（采样）— 理解"为什么能火"
5. 模式合成 — 建立可操作的规律库
```

## 常用数据源

- 平台官方 API（有速率限制）
- 第三方数据平台（千瓜、蝉妈妈、新榜等）
- HuggingFace Datasets（很多平台有现成的）
- 浏览器采集 — 使用 Agent 本身已配置的浏览器工具直接读取页面，无需 API key

## 已知案例

- **小红书**：参考 `references/xiaohongshu_case_study.md`
- **知乎**：参考 `references/zhihu_case_study.md`
- **微信公众号**：参考 `references/wechat_case_study.md`

## 注意事项

- 分析结论有时效性，平台算法会变，应定期重新分析一次
- 互动率和点赞数是两个不同维度，不要混为一谈
