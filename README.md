# 爆款网文创作全流程自动化工作流

<p align="center">
  <img src="https://img.shields.io/badge/version-1.0.0-blue" alt="Version">
  <img src="https://img.shields.io/badge/python-3.8+-green" alt="Python">
  <img src="https://img.shields.io/badge/license-MIT-orange" alt="License">
</p>

## 📖 项目简介

爆款网文创作全流程自动化工作流是一个基于AI的网文创作辅助系统，涵盖从平台数据抓取、选题分析、全维度设计、大纲规划、正文撰写、质量审计到文字优化的完整创作流程。系统旨在帮助创作者高效产出具备爆款潜力的高质量网文作品。

### 核心特性

- 🤖 **全自动化流程**：从数据到成品一键生成
- 📈 **爆款导向**：遵循网文爆款写作规律
- ✅ **质量保障**：多重审核与优化机制
- 🚫 **AI去痕化**：消除AI生成痕迹，贴近人工创作
- 🔧 **灵活调用**：支持单技能独立使用

## 🏗️ 系统架构

```
┌─────────────────────────────────────────────────────────────┐
│                    工作流控制器                              │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐       │
│  │  数据抓取    │  │  选题分析   │  │  设计规划   │       │
│  │data-scraper │  │topic-analyzer│ │design-planner│       │
│  └─────────────┘  └─────────────┘  └─────────────┘       │
│         │                 │                 │              │
│         ▼                 ▼                 ▼              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐       │
│  │  大纲规划    │  │  正文撰写   │  │  内容审计   │       │
│  │outline-planner│ │content-writer│ │content-auditor│      │
│  └─────────────┘  └─────────────┘  └─────────────┘       │
│         │                 │                 │              │
│         └─────────────────┼─────────────────┘              │
│                           ▼                                │
│                    ┌─────────────┐                        │
│                    │  文字优化   │                        │
│                    │text-optimizer│                       │
│                    └─────────────┘                        │
└─────────────────────────────────────────────────────────────┘
```

## 📦 包含的技能

| 技能名称 | 功能描述 | 用途 |
|---------|---------|------|
| `data-scraper` | 平台数据抓取 | 从各网文平台抓取热门作品、榜单、读者数据 |
| `topic-analyzer` | 赛道选题分析 | 分析热门赛道、竞争格局、蓝海机会 |
| `design-planner` | 全维度设计清单 | 人物设定、世界观、力量体系、金手指设计 |
| `outline-planner` | 大纲规划 | 卷纲设计、章纲规划、节奏安排、爽点排布 |
| `content-writer` | 全文撰写 | 根据大纲逐章撰写正文内容 |
| `content-auditor` | 内容审计 | 质量检查、情节连贯性、人物一致性检测 |
| `text-optimizer` | 文字优化 | 语句润色、节奏调整、爽点强化 |
| `novel-workflow` | 工作流编排 | 串联所有Skill实现全流程自动化 |

## 🚀 快速开始

### 安装

```bash
# 克隆项目
git clone https://github.com/BBNT-1215/Webnovel-Smart-Assistant.git
cd Webnovel-Smart-Assistant

# 安装依赖
pip install -r requirements.txt
```

### 使用方式

#### 1. 完整工作流（推荐）
```bash
/novel-workflow --mode semi-auto --platforms 起点,番茄 --track 都市 --volumes 2
```

#### 2. 分步执行
```bash
# 步骤1：数据抓取
/data-scraper --platforms 起点,番茄,七猫 --data-type 全量数据

# 步骤2：选题分析
/topic-analyzer --data-source 平台数据.json --output-format 选题报告

# 步骤3：全维度设计
/design-planner --input 选题报告.json --track 都市

# 步骤4：大纲规划
/outline-planner --design 设计方案.json --volumes 2

# 步骤5：正文撰写
/content-writer --outline 大纲.json --chapter-range 1-50

# 步骤6：内容审计
/content-auditor --chapters 1-50 --audit-type 全维度

# 步骤7：文字优化
/text-optimizer --chapters 1-50 --audit-report 审计报告.json --level 中度优化
```

## 📚 文档

- [📖 使用手册](USAGE_GUIDE.md) - 详细的工作流使用说明
- [⚙️ 技术配置文档](TECHNICAL_CONFIG.md) - 完整的技术架构和配置说明
- [📦 技能包说明](SKILL_PACKAGE.md) - Hermes Agent技能包集成指南
- [🔗 Hermes集成指南](HERMES_INTEGRATION_GUIDE.md) - 如何集成到Hermes Agent

## 🎯 爆款质量保障

### 1. 市场导向机制
- 实时分析热门题材和读者需求
- 与同类作品对比，寻找差异化优势
- 识别竞争相对较小但有潜力的蓝海赛道

### 2. 质量控制机制
- 专门检测和消除AI生成的典型痕迹
- 确保人物行为、语言风格始终如一
- 保证世界观、力量体系前后一致

### 3. 爽点与节奏保障
- 确保每3-5章有爽点，保持读者黏性
- 快慢结合，张弛有度，避免审美疲劳
- 每10-15章安排小高潮，每50-80章安排大高潮

### 4. 迭代优化机制
- 至少5轮质量优化，每轮聚焦不同问题
- 自动识别问题并针对性优化
- 质量闸门：未达标的章节自动重新优化

## 📊 质量标准

| 维度 | 最低要求 | 说明 |
|-----|---------|------|
| 整体评分 | ≥ 8.5分 | 满分10分 |
| 节奏评分 | ≥ 8.0分 | 爽点密度、节奏变化 |
| 人物评分 | ≥ 8.5分 | 一致性、个性化 |
| AI痕迹评分 | ≤ 2.0分 | 越低越好 |

## 🛠️ 技术栈

- **编程语言**: Python 3.8+
- **AI模型**: Transformer-based 文本生成模型
- **数据处理**: Pandas, NumPy
- **网络请求**: Requests, aiohttp
- **配置管理**: PyYAML

## 📁 项目结构

```
Webnovel-Smart-Assistant/
├── .trae/
│   └── skills/
│       ├── data-scraper/           # 数据抓取技能
│       │   ├── SKILL.md
│       │   └── hermes_skill.json
│       ├── topic-analyzer/         # 选题分析技能
│       │   ├── SKILL.md
│       │   └── hermes_skill.json
│       ├── design-planner/         # 设计规划技能
│       │   ├── SKILL.md
│       │   └── hermes_skill.json
│       ├── outline-planner/        # 大纲规划技能
│       │   ├── SKILL.md
│       │   └── hermes_skill.json
│       ├── content-writer/         # 内容撰写技能
│       │   ├── SKILL.md
│       │   └── hermes_skill.json
│       ├── content-auditor/       # 内容审计技能
│       │   ├── SKILL.md
│       │   └── hermes_skill.json
│       ├── text-optimizer/         # 文字优化技能
│       │   ├── SKILL.md
│       │   └── hermes_skill.json
│       └── novel-workflow/         # 工作流编排技能
│           ├── SKILL.md
│           └── hermes_skill.json
├── USAGE_GUIDE.md                  # 使用手册
├── TECHNICAL_CONFIG.md             # 技术配置文档
├── SKILL_PACKAGE.md                # 技能包说明
├── HERMES_INTEGRATION_GUIDE.md    # Hermes集成指南
└── README.md                       # 项目说明
```

## 🤝 贡献

欢迎提交Issue和Pull Request！

## 📄 许可证

MIT License

## 👤 作者

- **BBNT-1215** - [GitHub](https://github.com/BBNT-1215)

---

<p align="center">Made with ❤️ for web novel creators</p>