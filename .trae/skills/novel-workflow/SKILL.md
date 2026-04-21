---
name: "novel-workflow"
description: "Orchestrates the complete web novel creation workflow from data scraping to final optimization. Chains all individual skills together for end-to-end automation. Invoke when user wants to run the full novel creation pipeline or automate the entire workflow."
---

# 爆款网文创作全流程自动化工作流

## 功能概述

本 skill 是整个网文创作工作流的编排器，将8个独立skill串联起来，实现从平台数据抓取到最终内容优化的全流程自动化。每个skill既可独立调用，也可通过工作流自动执行。

## 触发条件

- 用户要求启动完整的网文创作工作流
- 需要从0开始自动生成小说
- 需要批量生成多部小说
- 需要自动化创作流程

## 工作流架构

```
┌──────────────────────────────────────────────────────────────┐
│                  爆款网文创作全流程工作流                      │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐      │
│  │ 1.数据抓取   │───▶│ 2.选题分析   │───▶│ 3.全维度设计 │      │
│  │ data-scraper│    │topic-analyzer│   │design-planner│      │
│  └─────────────┘    └─────────────┘    └─────────────┘      │
│         │                  │                  │              │
│         ▼                  ▼                  ▼              │
│    平台数据.json      选题报告.json     设计方案.json        │
│                                                              │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐      │
│  │ 7.文字优化   │◀───│ 6.内容审计   │◀───│ 5.全文撰写   │      │
│  │text-optimizer│   │content-auditor│  │content-writer│      │
│  └─────────────┘    └─────────────┘    └─────────────┘      │
│         ▲                  │                  │              │
│         │                  │                  │              │
│         └────── 循环优化 ◀──┘                  │              │
│                                                │              │
│  ┌─────────────┐                               │              │
│  │ 4.大纲规划   │───────────────────────────────┘              │
│  │outline-planner│                                              │
│  └─────────────┘                                               │
│         │                                                      │
│         ▼                                                      │
│    大纲.json                                                   │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## 工作流阶段

### Phase 1: 数据驱动阶段

#### Step 1: 平台数据抓取 (data-scraper)
- **输入**: 目标平台列表、抓取参数
- **输出**: 平台数据.json
- **功能**: 抓取各平台热门作品、榜单、读者数据
- **执行方式**: 
  ```
  调用 data-scraper skill
  --platforms 起点,番茄,七猫
  --data-type 全量数据
  --limit 100
  ```

#### Step 2: 赛道选题分析 (topic-analyzer)
- **输入**: 平台数据.json
- **输出**: 选题报告.json
- **功能**: 分析热门赛道、竞争格局、蓝海机会
- **执行方式**:
  ```
  调用 topic-analyzer skill
  --data-source 平台数据.json
  --output-format 选题报告
  --top-tracks 5
  ```
- **人工确认点**: 用户选择最终赛道

### Phase 2: 设计规划阶段

#### Step 3: 全维度设计清单 (design-planner)
- **输入**: 选题报告.json + 用户偏好
- **输出**: 设计方案.json
- **功能**: 人物设计、世界观、力量体系、金手指、情节架构
- **执行方式**:
  ```
  调用 design-planner skill
  --input 选题报告.json
  --track [用户选择的赛道]
  --protagonist-name [可选]
  ```
- **人工确认点**: 用户确认设计方案

#### Step 4: 大纲规划 (outline-planner)
- **输入**: 设计方案.json
- **输出**: 大纲.json
- **功能**: 卷纲设计、章纲规划、节奏安排、爽点排布
- **执行方式**:
  ```
  调用 outline-planner skill
  --design 设计方案.json
  --volumes [卷数]
  --chapters-per-volume [每卷章数]
  ```
- **人工确认点**: 用户确认大纲

### Phase 3: 内容生产阶段

#### Step 5: 全文撰写 (content-writer)
- **输入**: 大纲.json + 设计方案.json
- **输出**: 初稿内容（按章节）
- **功能**: 根据大纲逐章撰写正文，严格遵循爆款网文写作规范
- **执行方式**:
  ```
  调用 content-writer skill
  --outline 大纲.json
  --design 设计方案.json
  --chapter-range [章节范围]
  --batch [批量生成]
  --quality-checkpoint [每10章进行一次质量检查]
  ```
- **说明**: 
  - 可分批生成，每批10-50章
  - 每10章进行一次质量检查，避免批量生成后发现问题过多
  - 生成过程中维护人物卡片和设定文档，确保一致性

#### Step 6: 内容审计 (content-auditor)
- **输入**: 初稿内容
- **输出**: 审计报告.json
- **功能**: 质量检查、AI写作问题检测、问题检测、优化建议
- **执行方式**:
  ```
  调用 content-auditor skill
  --chapters [章节范围]
  --audit-type 全维度
  --ai-detection true  # 检测AI写作典型问题
  --consistency-check true  # 检查人物和设定一致性
  ```
- **新增检测项**:
  - AI写作痕迹检测（机器感、重复性、情感缺失等）
  - 人物一致性检查（OOC检测）
  - 设定连贯性检查
  - 情节逻辑连贯性检查

#### Step 7: 文字优化 (text-optimizer)
- **输入**: 初稿内容 + 审计报告.json
- **输出**: 优化后内容
- **功能**: 根据审计报告进行针对性优化，特别针对AI写作问题
- **执行方式**:
  ```
  调用 text-optimizer skill
  --input 初稿内容
  --audit-report 审计报告.json
  --level 自动修复
  --ai-artifact-fix true  # 专门修复AI写作痕迹
  --character-consistency-fix true  # 修复人物一致性问题
  ```
- **优化重点**:
  - 消除AI典型痕迹和机器感
  - 强化人物对话个性化
  - 增强情感细节描写
  - 优化节奏和爽点分布

### Phase 4: 迭代优化阶段

#### 爆款质量标准
- **整体评分**: ≥ 8.5分（满分10分）
- **节奏评分**: ≥ 8.0分（爽点密度、节奏变化）
- **人物评分**: ≥ 8.5分（一致性、个性化）
- **设定评分**: ≥ 8.0分（一致性、逻辑性）
- **AI痕迹评分**: ≤ 2.0分（越低越好）

#### 质量检查与迭代
```
while (任一维度评分未达标) {
    内容审计 → 文字优化 → 质量检查 → 评分评估
    if (AI痕迹检测分数 > 2.0) {
        重点进行AI去痕优化
    }
    if (人物一致性问题 > 3个) {
        重点进行人物一致性修复
    }
    if (爽点密度不达标) {
        重新调整爽点分布
    }
    if (节奏问题严重) {
        重新优化节奏结构
    }
}
```

#### 多轮迭代机制
- **第一轮**: 修复明显的AI痕迹和逻辑错误
- **第二轮**: 优化人物一致性和对话自然度
- **第三轮**: 调整节奏和爽点分布
- **第四轮**: 细节打磨和情感深度增强
- **第五轮**: 最终质量检验

#### 质量阈值控制
- **AI痕迹检测**: 发现超过3个AI典型问题则必须重新优化
- **人物OOC检测**: 发现超过2个人物行为不符则必须修复
- **设定矛盾检测**: 发现超过2个设定冲突则必须修正
- **爽点密度**: 每3-5章必须有爽点，否则重新调整

## 工作流执行模式

### 1. 全自动模式
```
/novel-workflow --mode auto --platforms 起点,番茄 --volumes 3 --chapters-per-volume 100
```
- 所有阶段自动执行
- 使用默认配置
- 生成完整小说

### 2. 半自动模式（推荐）
```
/novel-workflow --mode semi-auto --platforms 起点 --volumes 2
```
- 关键节点暂停等待用户确认
- 确认点：选题选择、设计方案、大纲确认
- 用户可中途调整方向

### 3. 手动模式
```
/novel-workflow --mode manual --step 3
```
- 用户手动触发每个skill
- 工作流仅做编排和进度管理
- 适合精细控制

### 4. 增量模式
```
/novel-workflow --mode incremental --continue-from chapter 50
```
- 从指定章节继续生成
- 保持已有内容不变
- 适合连载更新

## 工作流状态管理

### 状态跟踪
```json
{
  "workflow_id": "WF-20260421-001",
  "status": "running",
  "current_step": 5,
  "total_steps": 7,
  "progress": "71%",
  "steps_status": [
    {"step": 1, "name": "数据抓取", "status": "completed", "output": "平台数据.json"},
    {"step": 2, "name": "选题分析", "status": "completed", "output": "选题报告.json"},
    {"step": 3, "name": "全维度设计", "status": "completed", "output": "设计方案.json"},
    {"step": 4, "name": "大纲规划", "status": "completed", "output": "大纲.json"},
    {"step": 5, "name": "全文撰写", "status": "running", "progress": "60%"},
    {"step": 6, "name": "内容审计", "status": "pending"},
    {"step": 7, "name": "文字优化", "status": "pending"}
  ],
  "outputs": {
    "novel_title": "小说名称",
    "total_chapters_generated": 60,
    "target_chapters": 100
  }
}
```

### 断点续传
- 每个阶段完成后自动保存中间产物
- 工作流中断后可从断点继续
- 中间产物可手动修改后继续执行

## 工作流配置文件

```json
{
  "workflow_config": {
    "data_scraper": {
      "platforms": ["起点中文网", "番茄小说", "七猫小说"],
      "data_types": ["榜单", "趋势", "读者画像"],
      "limit_per_platform": 100,
      "trend_analysis": true
    },
    "topic_analyzer": {
      "analysis_depth": "deep",
      "top_tracks_count": 5,
      "blue_ocean_focus": true,
      "competition_analysis": "detailed",
      "reader_demand_analysis": true
    },
    "design_planner": {
      "focus_areas": ["人物", "世界观", "力量体系", "金手指设计"],
      "protagonist_customization": true,
      "anti_automation_check": true,
      "character_card_generation": true,
      "setting_documentation": true
    },
    "outline_planner": {
      "volumes": 3,
      "chapters_per_volume": 100,
      "pace": "fast_start",
      "boom_point_placement": {
        "opening_boom": "chapter_1_to_3",
        "early_sustained_boom": "every_3_to_5_chapters",
        "mid_volume_high_boom": "every_10_to_15_chapters",
        "volume_climax": "every_30_to_50_chapters"
      },
      "hook_placement": "every_chapter_end",
      "foreshadowing_management": true
    },
    "content_writer": {
      "words_per_chapter": 2000,
      "style": "爆款网文风格",
      "batch_size": 20,
      "quality_checkpoint_interval": 10,
      "ai_artifact_prevention": true,
      "character_consistency_enforcement": true,
      "rhythm_control": "strict",
      "boom_point_density_control": true
    },
    "content_auditor": {
      "audit_level": "comprehensive",
      "quality_threshold": 8.5,
      "ai_detection_enabled": true,
      "character_ooc_detection": true,
      "setting_consistency_check": true,
      "logic_continuity_check": true,
      "boom_point_analysis": true,
      "rhythm_analysis": true,
      "reader_engagement_prediction": true
    },
    "text_optimizer": {
      "optimization_level": "high",
      "auto_fix": true,
      "iteration_limit": 5,
      "ai_artifact_removal": true,
      "dialogue_naturalization": true,
      "emotion_detail_enhancement": true,
      "rhythm_optimization": true,
      "character_voice_individualization": true
    },
    "quality_gate": {
      "minimum_overall_score": 8.5,
      "minimum_rhythm_score": 8.0,
      "minimum_character_score": 8.5,
      "maximum_ai_artifact_score": 2.0,
      "maximum_setting_inconsistency_count": 2,
      "maximum_character_ooc_count": 2,
      "minimum_boom_point_density": "every_3_to_5_chapters",
      "reader_retention_prediction": "above_70_percent"
    }
  }
}
```

## 爆款潜力保障机制

为确保最终生成的网文具备爆款潜力，工作流集成了以下保障机制：

### 1. 市场导向机制
- **趋势分析**: 实时分析热门题材和读者需求
- **竞品对比**: 与同类作品对比，寻找差异化优势
- **蓝海识别**: 识别竞争相对较小但有潜力的赛道

### 2. 质量控制机制
- **AI痕迹消除**: 专门检测和消除AI生成的典型痕迹
- **人物一致性**: 确保人物行为、语言风格始终如一
- **设定连贯性**: 保证世界观、力量体系前后一致
- **逻辑自洽性**: 避免情节逻辑漏洞和矛盾

### 3. 爽点与节奏保障
- **爽点密度控制**: 确保每3-5章有爽点，保持读者黏性
- **节奏变化管理**: 快慢结合，张弛有度，避免审美疲劳
- **高潮布局**: 每10-15章安排小高潮，每50-80章安排大高潮

### 4. 读者体验优化
- **开篇抓人**: 前3章确保有冲突、金手指、打脸爽点
- **悬念留置**: 每章结尾留悬念，促进追读
- **情感共鸣**: 增强人物情感细节，提高代入感

### 5. 迭代优化机制
- **多轮迭代**: 至少5轮质量优化，每轮聚焦不同问题
- **智能检测**: 自动识别问题并针对性优化
- **质量闸门**: 未达标的章节自动重新优化，直到合格
```

## 错误处理

### 异常类型
- **数据获取失败**: 重试3次，更换数据源
- **分析结果异常**: 调整参数，重新分析
- **生成质量不达标**: 触发迭代优化
- **工作流中断**: 断点续传

### 重试机制
```
最大重试次数: 3
重试间隔: 递增 (1min, 5min, 15min)
失败处理: 记录日志，通知用户，等待人工介入
```

## 输出产物

### 完整输出结构
```
output/
├── workflow_report.json          # 工作流执行报告
├── phase1_data/
│   ├── 平台数据.json
│   └── 选题报告.json
├── phase2_design/
│   ├── 设计方案.json
│   └── 大纲.json
├── phase3_content/
│   ├── 初稿/
│   │   ├── 第1章.txt
│   │   ├── 第2章.txt
│   │   └── ...
│   ├── 审计报告.json
│   └── 优化后/
│       ├── 第1章_优化.txt
│       ├── 第2章_优化.txt
│       └── ...
└── final_novel/
    ├── 小说全文_完整版.txt
    ├── 小说全文_分章版/
    └── 质量报告.json
```

## 使用场景

### 场景1: 快速启动一部小说
```
/novel-workflow --quick-start --track 都市异能 --volumes 2 --chapters 200
```

### 场景2: 精细化创作
```
/novel-workflow --mode semi-auto --platforms 起点,番茄 --volumes 5 --review-each-step
```

### 场景3: 批量生成
```
/novel-workflow --batch --tracks 都市,玄幻,仙侠 --volumes 3 --auto-publish
```

### 场景4: 连载更新
```
/novel-workflow --mode incremental --continue-from last-chapter --new-chapters 50
```

## 各Skill独立调用

本工作流中的所有skill均可独立调用：

| Skill | 独立调用方式 | 说明 |
|-------|-------------|------|
| data-scraper | `/data-scraper --platform 起点` | 单独抓取数据 |
| topic-analyzer | `/topic-analyzer --data-source data.json` | 单独分析选题 |
| design-planner | `/design-planner --track 都市` | 单独设计方案 |
| outline-planner | `/outline-planner --design design.json` | 单独规划大纲 |
| content-writer | `/content-writer --outline outline.json --chapter 1` | 单独撰写章节 |
| content-auditor | `/content-auditor --chapters 1-10` | 单独审计内容 |
| text-optimizer | `/text-optimizer --chapter 1 --level medium` | 单独优化文字 |

## 注意事项

1. **数据合规**: 数据抓取遵守平台规则
2. **人工审核**: 关键节点建议人工确认
3. **质量优先**: 不盲目追求速度，保证内容质量
4. **版权意识**: 生成内容为原创，不抄袭
5. **迭代优化**: 好作品是改出来的，重视优化环节
