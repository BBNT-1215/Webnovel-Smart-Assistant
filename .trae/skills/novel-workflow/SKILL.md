---
name: "novel-workflow"
description: "Orchestrates the complete web novel creation workflow from market research to final optimized chapters. Chains all individual skills together with file-based data flow. Invoke when user wants to run the full novel creation pipeline."
---

# 爆款网文创作全流程自动化工作流

## 功能概述

本 skill 串联所有独立 skill，通过文件系统传递中间结果，实现从市场研究到最终优化的完整创作流程。

## 数据流设计

所有 skill 通过 `output/` 目录传递数据，形成完整流水线：

```
data-scraper          →  output/platform_data.json
topic-analyzer        →  output/topic_report.json
design-planner        →  output/design_plan.json
                      →  output/characters_card.md
outline-planner       →  output/outline.json
content-writer        →  output/chapters/第X章_章名.md
                      →  output/characters_card.md (更新)
content-auditor       →  output/audit_report.json
text-optimizer        →  output/chapters_optimized/第X章_章名.md
                      →  output/optimization_log.json
```

## 执行步骤

### Phase 1: 市场研究

#### Step 1: 数据抓取 (data-scraper)
Agent 执行：
1. 使用 WebSearch 搜索各平台热门作品
2. 搜索行业趋势和读者偏好
3. 整理数据并保存到 `output/platform_data.json`

```
搜索关键词:
- "起点中文网 月票榜 2026"
- "番茄小说 热门小说排行"
- "七猫小说 畅销榜 最新"
- "2026年网文热门题材趋势"
```

#### Step 2: 选题分析 (topic-analyzer)
Agent 执行：
1. 读取 `output/platform_data.json`
2. 分析各赛道热度、竞争度、机会
3. 生成 `output/topic_report.json`
4. **向用户展示 Top 3 推荐赛道，等待用户选择**

### Phase 2: 设计规划

#### Step 3: 全维度设计 (design-planner)
Agent 执行：
1. 根据用户选择的赛道
2. 生成人物设定、世界观、力量体系、金手指
3. 保存 `output/design_plan.json`
4. 生成 `output/characters_card.md`（人物卡片）
5. **向用户展示设计方案，等待确认**

#### Step 4: 大纲规划 (outline-planner)
Agent 执行：
1. 读取 `output/design_plan.json`
2. 生成卷纲、章纲
3. 保存 `output/outline.json`
4. **向用户展示大纲摘要，等待确认**

### Phase 3: 内容创作

#### Step 5: 正文撰写 (content-writer)
Agent 执行：
1. 读取 `output/outline.json`、`output/design_plan.json`、`output/characters_card.md`
2. 逐章撰写正文：
   - 每次写一章
   - 写入上下文（人物卡片 + 本章大纲 + 前文摘要）
   - 保存到 `output/chapters/第X章_章名.md`
   - 更新 `output/characters_card.md`
3. **每10章暂停，让用户检查质量**

#### Step 6: 内容审计 (content-auditor)
Agent 执行：
1. 读取所有章节文件
2. 读取 `output/design_plan.json` 和 `output/characters_card.md`
3. 检查一致性、可读性、节奏
4. 生成 `output/audit_report.json`

#### Step 7: 文字优化 (text-optimizer)
Agent 执行：
1. 读取 `output/audit_report.json`
2. 针对发现的问题优化
3. 保存到 `output/chapters_optimized/`
4. 生成 `output/optimization_log.json`

## 用户交互点

工作流在以下节点暂停等待用户确认：

| 节点 | 交互内容 |
|------|---------|
| 选题分析后 | 选择最终赛道 |
| 设计方案后 | 确认人物设定和世界观 |
| 大纲规划后 | 确认章节结构 |
| 每10章生成后 | 检查内容质量 |
| 审计完成后 | 确认是否需要优化 |

## 文件结构

```
output/
├── platform_data.json          # Step 1 输出
├── topic_report.json           # Step 2 输出
├── design_plan.json            # Step 3 输出
├── characters_card.md          # Step 3/5 输出（持续更新）
├── outline.json                # Step 4 输出
├── chapters/                   # Step 5 输出
│   ├── 第1章_章名.md
│   ├── 第2章_章名.md
│   └── ...
├── audit_report.json           # Step 6 输出
├── chapters_optimized/         # Step 7 输出
│   ├── 第1章_章名.md
│   └── ...
└── optimization_log.json       # Step 7 输出
```

## 使用方式

用户调用此 skill 后，Agent 将：
1. 依次执行上述 7 个步骤
2. 在交互点暂停等待用户确认
3. 生成完整的小说文件和配套文档

## API 调用策略

### 批量生成注意事项
- 每章单独调用 API，不要一次生成多章
- temperature: 0.7-0.8
- max_new_tokens: 3000
- 请求间隔 2-5 秒
- 每10章检查人物一致性

### 防止主角名漂移
- 维护 `output/characters_card.md`
- 每次写作前读取人物卡片
- 在上下文中明确主角姓名

### 防止设定矛盾
- 维护设定摘要
- 涉及力量等级时查阅设定
- 每30章重新生成设定摘要

## 断点续传

如果工作流中断，可以从断点继续：
- 检查 `output/` 目录中已有的文件
- 从最后一个完整完成的步骤继续
- 已生成的章节不会被覆盖
