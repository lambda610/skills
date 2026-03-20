# 知乎案例研究

> 待补充 — 需要数据源才能完成分析

## 数据源

待确认：
- [ ] HuggingFace 是否有知乎数据集
- [ ] 知乎开放平台 API 申请方式
- [ ] 第三方数据平台

## 分析框架（待填充）

### 平台基本数据（待补充）

| 指标 | 值 |
|------|-----|
| 数据来源 | 待确认 |
| 覆盖时间 | 待确认 |
| 内容总数 | 待确认 |

### 爆款门槛

待分析

### 两种成功维度

待分析

### 高赞内容结构

待分析

---

## 数据源参考

### 可能的获取方式

1. **HuggingFace Datasets** — 搜索 "zhihu"
2. **知乎开放平台** — https://www.zhihu.com/oaths — 有部分 API
3. **第三方数据平台**（新榜、易赞等）
4. **手动采集** — 基于公开页面（注意平台 TOS）

### 核心提取字段

```
id, question_id, title, answer_text, likes, comments, 
author, publish_time, topics
```

---

*分析方法见：`../methodology.md`*
