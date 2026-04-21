---
name: "content-writer"
description: "Writes web novel chapter drafts based on outlines, chapter plans, and design documents. Generates engaging chapters following web novel writing conventions. Invoke when user needs chapter drafting assistance or content generation."
---

# 全文撰写 Skill

## 功能概述

本 skill 读取 `outline-planner` 生成的大纲和 `design-planner` 生成的设计方案，逐章撰写正文内容。

## 执行步骤

### Step 1: 读取输入文件
- 读取 `output/design_plan.json` 获取人物设定、世界观、金手指
- 读取 `output/outline.json` 获取章节大纲
- 如果 `output/characters_card.md` 存在，读取人物卡片用于保持一致性

### Step 2: 构建写作上下文
每次写一章前，准备以下信息：
- **人物卡片**: 主角和出场人物的姓名、性格、外貌
- **本章大纲**: 从 outline.json 中提取本章的摘要
- **前文摘要**: 前2-3章的内容摘要（用于保持连贯）
- **设定摘要**: 世界观、力量体系等关键设定

### Step 3: 撰写章节
按照网文写作规范撰写本章正文：
- 约 2000-3000 字
- 开篇有钩子
- 中间有冲突推进
- 结尾留悬念

### Step 4: 保存章节
将章节保存到 `output/chapters/第X章_章名.md`。

### Step 5: 更新人物卡片
如果本章有新的设定或人物信息，更新 `output/characters_card.md`。

## 写作规范

### 章节结构
- **开头 (10%)**: 悬念/冲突引入
- **发展 (60%)**: 情节推进
- **高潮 (20%)**: 爽点爆发
- **结尾 (10%)**: 留悬念

### 写作风格
- 通俗易懂
- 段落简短（手机阅读友好）
- 对话推动情节
- 动作描写具体

## 一致性维护机制

### 防止主角名漂移
- 每次写作前读取人物卡片
- 在写作上下文中明确主角姓名

### 防止设定矛盾
- 写作前读取设定摘要
- 涉及力量等级时查阅设定

## 批量生成策略

### 控制参数
- temperature: 0.7-0.8
- max_new_tokens: 3000

### 生成流程
1. 逐章生成，不一次生成多章
2. 每章生成后保存文件
3. 更新人物卡片和设定摘要
4. 每10章检查一次一致性

## 输出格式

保存到 `output/chapters/第X章_章名.md`：

```markdown
# 第X章 章名

[正文内容]
```

## 使用方式

用户调用此 skill 后，Agent 将：
1. 读取 `output/outline.json` 和 `output/design_plan.json`
2. 逐章撰写正文
3. 保存到 `output/chapters/` 目录
4. 维护 `output/characters_card.md`
