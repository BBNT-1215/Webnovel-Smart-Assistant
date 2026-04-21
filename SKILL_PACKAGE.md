# 爆款网文创作全流程自动化工作流 - Hermes Agent 技能包

## 包含的技能文件

### 1. 数据抓取技能
- **文件**: `.trae/skills/data-scraper/hermes_skill.json`
- **功能**: 从网文平台抓取数据
- **用途**: 市场研究和趋势分析

### 2. 选题分析技能
- **文件**: `.trae/skills/topic-analyzer/hermes_skill.json`
- **功能**: 分析市场数据，识别机会
- **用途**: 赛道选择和方向规划

### 3. 设计规划技能
- **文件**: `.trae/skills/design-planner/hermes_skill.json`
- **功能**: 创建人物、世界观、力量体系等
- **用途**: 创作蓝图设计

### 4. 大纲规划技能
- **文件**: `.trae/skills/outline-planner/hermes_skill.json`
- **功能**: 生成卷纲、章纲、节奏规划
- **用途**: 章节结构设计

### 5. 内容撰写技能
- **文件**: `.trae/skills/content-writer/hermes_skill.json`
- **功能**: 生成章节内容
- **用途**: 正文创作

### 6. 内容审计技能
- **文件**: `.trae/skills/content-auditor/hermes_skill.json`
- **功能**: 质量检查和问题检测
- **用途**: 内容质量控制

### 7. 文字优化技能
- **文件**: `.trae/skills/text-optimizer/hermes_skill.json`
- **功能**: 文字润色和优化
- **用途**: 提升内容质量

### 8. 工作流编排技能
- **文件**: `.trae/skills/novel-workflow/hermes_skill.json`
- **功能**: 协调所有技能执行完整流程
- **用途**: 端到端自动化

## 打包结构

```
novel-creation-suite/
├── manifest.json                 # 技能包清单文件
├── README.md                    # 使用说明
├── skills/
│   ├── data-scraper/
│   │   └── hermes_skill.json
│   ├── topic-analyzer/
│   │   └── hermes_skill.json
│   ├── design-planner/
│   │   └── hermes_skill.json
│   ├── outline-planner/
│   │   └── hermes_skill.json
│   ├── content-writer/
│   │   └── hermes_skill.json
│   ├── content-auditor/
│   │   └── hermes_skill.json
│   ├── text-optimizer/
│   │   └── hermes_skill.json
│   └── novel-workflow/
│       └── hermes_skill.json
└── config/
    └── default_settings.json
```

## manifest.json (技能包清单)

```json
{
  "package_name": "novel-creation-suite",
  "version": "1.0.0",
  "description": "爆款网文创作全流程自动化工作流技能包",
  "author": "Webnovel Smart Assistant",
  "license": "MIT",
  "skills": [
    {
      "name": "novel_data_scraper",
      "path": "./skills/data-scraper/hermes_skill.json",
      "dependencies": []
    },
    {
      "name": "novel_topic_analyzer", 
      "path": "./skills/topic-analyzer/hermes_skill.json",
      "dependencies": ["novel_data_scraper"]
    },
    {
      "name": "novel_design_planner",
      "path": "./skills/design-planner/hermes_skill.json", 
      "dependencies": ["novel_topic_analyzer"]
    },
    {
      "name": "novel_outline_planner",
      "path": "./skills/outline-planner/hermes_skill.json",
      "dependencies": ["novel_design_planner"]
    },
    {
      "name": "novel_content_writer",
      "path": "./skills/content-writer/hermes_skill.json",
      "dependencies": ["novel_outline_planner", "novel_design_planner"]
    },
    {
      "name": "novel_content_auditor",
      "path": "./skills/content-auditor/hermes_skill.json",
      "dependencies": ["novel_content_writer"]
    },
    {
      "name": "novel_text_optimizer",
      "path": "./skills/text-optimizer/hermes_skill.json",
      "dependencies": ["novel_content_auditor"]
    },
    {
      "name": "novel_workflow_orchestrator",
      "path": "./skills/novel-workflow/hermes_skill.json",
      "dependencies": ["novel_data_scraper", "novel_topic_analyzer", "novel_design_planner", "novel_outline_planner", "novel_content_writer", "novel_content_auditor", "novel_text_optimizer"]
    }
  ],
  "metadata": {
    "category": "content_creation",
    "tags": ["novel", "writing", "automation", "creative"],
    "complexity": "advanced",
    "estimated_runtime": "variable"
  }
}
```

## 安装说明

### 方法1: 直接复制
将整个 `novel-creation-suite` 文件夹复制到Hermes Agent的技能目录。

### 方法2: 压缩包安装
1. 将整个技能包压缩为ZIP文件
2. 使用Hermes Agent的技能包安装功能导入

### 方法3: Git集成
如果Hermes Agent支持Git集成，可以将此技能包作为一个Git仓库进行管理。

## 验证安装

安装完成后，可以通过以下命令验证技能是否正确加载：

```bash
# 验证所有技能是否可用
hermes list skills | grep novel

# 测试单个技能
hermes call novel_data_scraper --help

# 执行完整工作流测试
hermes call novel_workflow_orchestrator --mode manual --track 都市 --volumes 1
```

## 更新说明

当需要更新技能包时：
1. 下载最新版本的技能包
2. 替换现有文件
3. 重启Hermes Agent以加载更新后的技能
4. 验证更新是否成功

## 技能协同工作示例

以下是Hermes Agent如何使用这些技能协同工作的示例：

```json
{
  "workflow": "complete_novel_creation",
  "steps": [
    {
      "skill": "novel_data_scraper",
      "params": {
        "platforms": ["起点中文网", "番茄小说"],
        "data_type": "全量数据",
        "limit": 100
      }
    },
    {
      "skill": "novel_topic_analyzer", 
      "params": {
        "data_source": "previous_output",
        "analysis_type": "全维度分析",
        "top_tracks": 5
      }
    },
    {
      "skill": "novel_design_planner",
      "params": {
        "track": "selected_track_from_analysis",
        "focus_areas": ["人物设计", "世界观", "金手指"]
      }
    },
    {
      "skill": "novel_outline_planner",
      "params": {
        "design_plan": "generated_design",
        "volumes": 3,
        "chapters_per_volume": 100
      }
    },
    {
      "skill": "novel_content_writer",
      "params": {
        "outline": "generated_outline",
        "chapter_range": "1-50",
        "style": "快节奏"
      }
    },
    {
      "skill": "novel_content_auditor",
      "params": {
        "chapters": [1, 2, 3, 4, 5],
        "audit_type": "全维度"
      }
    },
    {
      "skill": "novel_text_optimizer", 
      "params": {
        "chapters": [1, 2, 3, 4, 5],
        "optimization_level": "中度优化",
        "audit_report": "audit_results"
      }
    }
  ]
}
```

这个技能包使Hermes Agent能够完全自主地执行从市场分析到内容生成再到质量优化的完整网文创作流程。