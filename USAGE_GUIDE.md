# 爆款网文创作全流程自动化工作流使用手册

## 目录
1. [简介](#简介)
2. [前置要求](#前置要求)
3. [安装配置](#安装配置)
4. [快速开始](#快速开始)
5. [各技能详解](#各技能详解)
6. [工作流模式](#工作流模式)
7. [参数说明](#参数说明)
8. [最佳实践](#最佳实践)
9. [故障排除](#故障排除)
10. [FAQ](#faq)

## 简介

爆款网文创作全流程自动化工作流是一个端到端的AI辅助创作系统，涵盖从市场数据抓取、选题分析、全维度设计、大纲规划、正文撰写、质量审计到文字优化的完整流程。系统旨在帮助创作者高效产出具备爆款潜力的高质量网文作品。

### 核心特性
- **全自动化流程**：从数据到成品一键生成
- **爆款导向**：遵循网文爆款写作规律
- **质量保障**：多重审核与优化机制
- **AI去痕化**：消除AI生成痕迹，贴近人工创作
- **灵活调用**：支持单技能独立使用

## 前置要求

### 系统要求
- 操作系统：Windows 10+, macOS 10.14+, Linux (Ubuntu 18.04+)
- 内存：至少 8GB RAM（推荐 16GB+）
- 存储：至少 2GB 可用空间
- 网络：稳定的互联网连接（用于数据抓取）

### 软件依赖
- Python 3.8+
- 相关AI模型访问权限
- 网络爬虫运行环境

### 权限要求
- 数据抓取权限（需遵守各平台robots.txt协议）
- 文件读写权限
- 网络访问权限

## 安装配置

### 1. 环境准备
```bash
# 确保Python版本符合要求
python --version

# 安装依赖包（如有）
pip install -r requirements.txt
```

### 2. 技能目录结构
确保以下目录结构存在于项目根目录：
```
.trae/
└── skills/
    ├── data-scraper/
    ├── topic-analyzer/
    ├── design-planner/
    ├── outline-planner/
    ├── content-writer/
    ├── content-auditor/
    ├── text-optimizer/
    └── novel-workflow/
```

### 3. 配置文件
在项目根目录创建配置文件 `config.yaml`：
```yaml
workflow:
  default_volumes: 3
  default_chapters_per_volume: 100
  quality_threshold: 8.5
  ai_artifact_threshold: 2.0
  
data_scraper:
  platforms:
    - 起点中文网
    - 番茄小说
    - 七猫小说
  rate_limit: 10  # 每分钟请求次数
  
content_writer:
  default_word_count: 2000
  checkpoint_interval: 10  # 每10章检查一次质量
```

## 快速开始

### 1. 启动完整工作流（推荐新手）
```bash
# 自动模式：完全自动化执行
/novel-workflow --mode auto --track 都市异能 --volumes 2 --chapters-per-volume 100

# 半自动模式：关键节点人工确认（推荐）
/novel-workflow --mode semi-auto --platforms 起点,番茄 --volumes 2 --review-each-step
```

### 2. 分步执行
```bash
# 步骤1：数据抓取
/data-scraper --platforms 起点,番茄,七猫 --data-type 全量数据 --limit 100

# 步骤2：选题分析
/topic-analyzer --data-source 平台数据.json --output-format 选题报告 --top-tracks 5

# 步骤3：全维度设计
/design-planner --input 选题报告.json --track 都市异能 --protagonist-name 林辰

# 步骤4：大纲规划
/outline-planner --design 设计方案.json --volumes 2 --chapters-per-volume 100

# 步骤5：正文撰写
/content-writer --outline 大纲.json --design 设计方案.json --chapter-range 1-50

# 步骤6：内容审计
/content-auditor --chapters 1-50 --audit-type 全维度

# 步骤7：文字优化
/text-optimizer --chapters 1-50 --audit-report 审计报告.json --level 中度优化
```

### 3. 查看结果
生成的文件位于 `output/` 目录下：
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
│   ├── 审计报告.json
│   └── 优化后/
└── final_novel/
    ├── 小说全文_完整版.txt
    └── 质量报告.json
```

## 各技能详解

### data-scraper（数据抓取）
**功能**：抓取各网文平台热门作品、榜单、读者数据
```bash
# 基础用法
/data-scraper --platforms 起点 --data-type 榜单 --limit 50

# 多平台抓取
/data-scraper --platforms 起点,番茄,七猫 --data-type 全量数据 --limit 100

# 自定义抓取
/data-scraper --platform 番茄小说 --data-type 趋势分析
```

### topic-analyzer（选题分析）
**功能**：分析热门赛道、竞争格局、蓝海机会
```bash
# 基础分析
/topic-analyzer --data-source 平台数据.json --output-format 选题报告

# 深度分析
/topic-analyzer --data-source 平台数据.json --analysis-type 全维度分析

# 赛道对比
/topic-analyzer --compare-tracks 都市,玄幻,仙侠
```

### design-planner（全维度设计）
**功能**：人物设计、世界观、力量体系、金手指设计
```bash
# 完整设计
/design-planner --input 选题报告.json --track 都市异能

# 专注领域
/design-planner --focus 人物设计 --track 玄幻 --protagonist-name 张三
```

### outline-planner（大纲规划）
**功能**：卷纲设计、章纲规划、节奏安排、爽点排布
```bash
# 完整大纲
/outline-planner --design 设计方案.json --volumes 3 --chapters-per-volume 100

# 调整节奏
/outline-planner --adjust-pacing --fast-start --volume 1
```

### content-writer（正文撰写）
**功能**：根据大纲逐章撰写正文
```bash
# 批量生成
/content-writer --outline 大纲.json --chapter-range 1-50 --batch

# 单章生成
/content-writer --outline 大纲.json --chapter 1 --style 快节奏
```

### content-auditor（内容审计）
**功能**：质量检查、问题检测、优化建议
```bash
# 全维度审计
/content-auditor --chapters 1-50 --audit-type 全维度

# 专项审计
/content-auditor --chapter 15 --focus 情节审计

# 快速检查
/content-auditor --quick-check --chapters 1-10
```

### text-optimizer（文字优化）
**功能**：语句润色、节奏调整、爽点强化
```bash
# 中度优化
/text-optimizer --chapter 15 --level 中度优化

# 根据审计报告优化
/text-optimizer --audit-report 审计报告.json --auto-fix

# 专项优化
/text-optimizer --focus 爽点强化 --chapters 1-10
```

### novel-workflow（工作流编排）
**功能**：协调各技能执行完整创作流程
```bash
# 快速启动
/novel-workflow --quick-start --track 都市异能 --volumes 2 --chapters 200

# 精细控制
/novel-workflow --mode semi-auto --platforms 起点,番茄 --volumes 5 --review-each-step

# 批量生成
/novel-workflow --batch --tracks 都市,玄幻,仙侠 --volumes 3

# 增量更新
/novel-workflow --mode incremental --continue-from last-chapter --new-chapters 50
```

## 工作流模式

### 1. 自动模式 (`--mode auto`)
- 完全自动化执行，无需人工干预
- 使用默认配置和决策
- 适合批量生成或有明确需求的场景

### 2. 半自动模式 (`--mode semi-auto`) 
- 关键节点暂停等待人工确认
- 确认点：选题选择、设计方案、大纲确认
- 推荐大多数用户使用

### 3. 手动模式 (`--mode manual`)
- 用户手动触发每个技能
- 工作流仅做编排和进度管理
- 适合需要精细控制的场景

### 4. 增量模式 (`--mode incremental`)
- 从指定章节继续生成
- 保持已有内容不变
- 适合连载更新

## 参数说明

### 通用参数
- `--verbose`: 详细输出模式
- `--dry-run`: 仅显示执行计划，不实际执行
- `--output-dir`: 指定输出目录
- `--config`: 指定配置文件路径

### 工作流参数
- `--mode`: 执行模式 (auto|semi-auto|manual|incremental)
- `--platforms`: 数据来源平台列表
- `--track`: 选择的题材赛道
- `--volumes`: 卷数
- `--chapters-per-volume`: 每卷章数
- `--target-word-count`: 目标总字数

### 质量控制参数
- `--quality-threshold`: 质量评分阈值
- `--ai-artifact-limit`: AI痕迹数量限制
- `--consistency-check`: 一致性检查开关
- `--iteration-limit`: 迭代优化次数限制

## 最佳实践

### 1. 新手推荐流程
1. 使用半自动模式开始：`/novel-workflow --mode semi-auto`
2. 在选题阶段选择感兴趣的方向
3. 在设计方案阶段确认人物设定
4. 在大纲阶段审核章节规划
5. 启用质量检查：每10章检查一次

### 2. 提升成功率的技巧
- **选题策略**：选择竞争适中、有一定蓝海空间的赛道
- **人物设定**：确保主角目标清晰、性格统一、不能长期憋屈
- **节奏控制**：前30万字快节奏，之后张弛有度
- **爽点分布**：每3-5章安排一个爽点
- **金手指设计**：简单有效，有成长性，有代价

### 3. 质量优化建议
- 定期检查AI痕迹分数，确保低于2.0
- 关注人物一致性评分，确保高于8.5
- 保持爽点密度在合理范围内
- 每10章进行一次质量评估

### 4. 避免常见问题
- 不要选择过度饱和的赛道
- 避免设定过于复杂，难以保持一致性
- 防止前期节奏过快导致后期乏力
- 避免金手指过于强大导致战力崩坏

## 故障排除

### 常见问题

**Q: 数据抓取失败**
A: 检查网络连接，确认平台访问权限，降低抓取频率

**Q: 生成内容质量不高**
A: 调高质量阈值，启用多轮迭代优化，检查输入素材质量

**Q: AI痕迹检测分数过高**
A: 启用更多轮次的AI去痕优化，人工审核并调整生成参数

**Q: 人物OOC问题**
A: 确保人物设定文档完整，启用人物一致性检查

**Q: 工作流中断**
A: 系统支持断点续传，从上次中断位置继续执行

### 性能优化
- 增加内存分配给AI模型
- 调整并发数量避免系统过载
- 定期清理临时文件
- 使用SSD存储提升I/O性能

### 日志查看
系统会在 `logs/` 目录生成详细执行日志，包含：
- 执行时间统计
- 资源使用情况
- 错误和警告信息
- 质量评估详情

## FAQ

**Q: 这个系统生成的内容是否原创？**
A: 系统生成的内容是基于输入参数和训练数据的原创创作，但建议在发布前进行查重确认。

**Q: 如何评估生成内容的质量？**
A: 系统会自动生成质量报告，包含各维度评分。一般来说，整体评分8.5以上为高质量内容。

**Q: 可以修改已生成的内容吗？**
A: 可以。系统支持增量模式，在已有内容基础上继续生成或修改。

**Q: 对硬件配置有什么要求？**
A: 最低要求8GB内存，推荐16GB+。AI模型运行需要一定的计算资源，配置越高运行越流畅。

**Q: 如何定制自己的创作偏好？**
A: 可以通过配置文件或命令行参数指定偏好，如题材倾向、风格要求、质量标准等。

**Q: 支持哪些网文平台的数据抓取？**
A: 目前支持起点中文网、番茄小说、七猫小说等主流平台，可根据需要扩展。

**Q: 生成一部小说需要多长时间？**
A: 根据小说长度和质量要求，通常20-100万字的小说需要30分钟到2小时不等。