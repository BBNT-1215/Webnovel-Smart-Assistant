# 爆款网文创作全流程自动化工作流

> 基于 AI Agent 的网文创作系统，通过文件系统传递数据，实现从市场研究到最终优化的完整流程。

<p align="center">
  <img src="https://img.shields.io/badge/version-2.0.0-blue" alt="Version">
  <img src="https://img.shields.io/badge/platform-Trae%20Agent-orange" alt="Platform">
  <img src="https://img.shields.io/badge/license-MIT-green" alt="License">
</p>

## 📖 项目简介

本项目是一套**可实际执行的 AI Agent 工作流**，包含 8 个 SKILL.md 文件，定义了从市场研究到内容优化的完整创作流程。Agent 通过 WebSearch、文件读写等实际工具能力执行每个步骤，通过 `output/` 目录传递中间结果。

## 🏗️ 工作流架构

```
┌─────────────────────────────────────────────────────────────────────┐
│                         Phase 1: 市场研究                           │
│  ┌─────────────────┐          ┌─────────────────┐                  │
│  │  1.数据抓取      │ ─文件→   │  2.选题分析      │                  │
│  │  WebSearch搜索  │          │  分析赛道机会    │                  │
│  └─────────────────┘          └─────────────────┘                  │
│         ↓                            ↓                             │
│  output/platform_data.json    output/topic_report.json             │
├─────────────────────────────────────────────────────────────────────┤
│                         Phase 2: 设计规划                           │
│  ┌─────────────────┐          ┌─────────────────┐                  │
│  │  3.全维度设计    │ ─文件→   │  4.大纲规划      │                  │
│  │  人物+世界观     │          │  卷纲+章纲       │                  │
│  └─────────────────┘          └─────────────────┘                  │
│         ↓                            ↓                             │
│  output/design_plan.json      output/outline.json                  │
│  output/characters_card.md                                         │
├─────────────────────────────────────────────────────────────────────┤
│                         Phase 3: 内容创作                           │
│  ┌─────────────────┐          ┌─────────────────┐                  │
│  │  5.正文撰写      │ ─文件→   │  6.内容审计      │                  │
│  │  逐章生成        │          │  质量检查        │                  │
│  └─────────────────┘          └─────────────────┘                  │
│         ↓                            ↓                             │
│  output/chapters/*.md         output/audit_report.json             │
│  output/characters_card.md (更新)                                  │
├─────────────────────────────────────────────────────────────────────┤
│                         Phase 4: 优化                              │
│  ┌─────────────────┐                                               │
│  │  7.文字优化      │                                               │
│  │  针对性修改      │                                               │
│  └─────────────────┘                                               │
│         ↓                                                          │
│  output/chapters_optimized/*.md                                    │
│  output/optimization_log.json                                      │
└─────────────────────────────────────────────────────────────────────┘
```

## 📦 包含的 Skill

| Skill | 输入 | 输出 | 能力 |
|-------|------|------|------|
| `data-scraper` | 无 | `platform_data.json` | 使用 WebSearch 搜索市场数据 |
| `topic-analyzer` | `platform_data.json` | `topic_report.json` | 分析赛道热度、竞争、机会 |
| `design-planner` | `topic_report.json` | `design_plan.json`<br>`characters_card.md` | 生成人物设定、世界观、力量体系 |
| `outline-planner` | `design_plan.json` | `outline.json` | 生成卷纲、章纲、节奏安排 |
| `content-writer` | `outline.json`<br>`design_plan.json`<br>`characters_card.md` | `chapters/`<br>`characters_card.md`(更新) | 逐章撰写正文 |
| `content-auditor` | `chapters/`<br>`design_plan.json` | `audit_report.json` | 检查一致性、可读性、节奏 |
| `text-optimizer` | `audit_report.json`<br>`chapters/` | `chapters_optimized/`<br>`optimization_log.json` | 针对性优化内容 |
| `novel-workflow` | 用户输入 | 全部 | 串联全流程，自动执行 |

## 🚀 快速开始

### 在 Trae Agent 中使用

#### 方式一：执行完整工作流
Agent 会自动执行所有 7 个步骤，在关键节点暂停等待用户确认。

#### 方式二：分步执行
用户可以单独调用任意 skill 执行特定步骤。

### 输出文件结构

```
output/
├── platform_data.json          # 市场数据
├── topic_report.json           # 选题报告
├── design_plan.json            # 设计方案
├── characters_card.md          # 人物卡片（持续更新）
├── outline.json                # 完整大纲
├── chapters/                   # 初稿章节
│   ├── 第1章_章名.md
│   └── ...
├── audit_report.json           # 审计报告
├── chapters_optimized/         # 优化后章节
│   ├── 第1章_章名.md
│   └── ...
└── optimization_log.json       # 优化日志
```

## 🔧 关键技术设计

### 1. 文件系统数据流
所有 skill 通过 `output/` 目录传递数据，形成完整流水线：
- 每个 skill 有明确的输入和输出文件
- 后续 skill 依赖前置 skill 的输出
- 支持断点续传

### 2. 一致性维护机制
- **人物卡片**: 维护主角姓名、性格、外貌，每次写作前读取
- **设定摘要**: 维护世界观、力量体系，防止设定矛盾
- **每10章检查**: 定期检查人物一致性

### 3. API 调用策略
- 每章单独调用，不一次生成多章
- temperature: 0.7-0.8
- max_new_tokens: 3000
- 请求间隔 2-5 秒

### 4. 用户交互点
工作流在关键节点暂停：
| 节点 | 交互内容 |
|------|---------|
| 选题分析后 | 选择最终赛道 |
| 设计方案后 | 确认人物设定和世界观 |
| 大纲规划后 | 确认章节结构 |
| 每10章生成后 | 检查内容质量 |
| 审计完成后 | 确认是否需要优化 |

## ⚠️ 限制说明

- **数据来源**: 通过 WebSearch 获取公开信息，无法获取平台内部精确数据
- **反爬限制**: 起点、番茄等平台有严格反爬，只能获取有限公开信息
- **内容质量**: AI 生成内容需要人工审核，不能直接发布
- **读者偏好**: 读者只在乎内容好不好看，不在乎是否为 AI 生成

## 📁 项目结构

```
Webnovel-Smart-Assistant/
├── .trae/
│   └── skills/
│       ├── data-scraper/           # 数据抓取
│       │   ├── SKILL.md
│       │   ├── hermes_skill.json
│       │   └── openclaw_skill.json
│       ├── topic-analyzer/         # 选题分析
│       ├── design-planner/         # 设计规划
│       ├── outline-planner/        # 大纲规划
│       ├── content-writer/         # 内容撰写
│       ├── content-auditor/        # 内容审计
│       ├── text-optimizer/         # 文字优化
│       └── novel-workflow/         # 工作流编排
├── USAGE_GUIDE.md                  # 使用手册
├── TECHNICAL_CONFIG.md             # 技术配置
├── SKILL_PACKAGE.md                # 技能包说明
├── HERMES_INTEGRATION_GUIDE.md    # Hermes集成指南
├── OPENCLAW_INTEGRATION_GUIDE.md  # OpenCLAW集成指南
├── 项目说明.md                     # 项目说明
├── 审计报告.md                     # 审计报告
└── README.md                       # 项目说明
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

MIT License

## 👤 作者

- **BBNT-1215** - [GitHub](https://github.com/BBNT-1215)

---

<p align="center">AI Agent 驱动 · 文件系统数据流 · 完整创作流水线</p>