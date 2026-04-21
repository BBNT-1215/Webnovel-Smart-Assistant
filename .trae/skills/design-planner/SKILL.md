---
name: "design-planner"
description: "Creates comprehensive design checklists for web novels including character design, world building, power systems, and story elements. Reads topic analysis and generates detailed design document. Invoke when user needs novel design planning, character creation, world building, or story element design."
---

# 全维度设计清单 Skill

## 功能概述

本 skill 读取 `topic-analyzer` 的选题报告，生成完整的设计方案文档，包括人物设定、世界观、力量体系、金手指设计等。

## 执行步骤

### Step 1: 读取选题报告
读取 `output/topic_report.json`，获取用户选择的赛道方向。

如果用户已指定赛道，可直接使用。

### Step 2: 生成人物设计
根据赛道和题材，设计：
- **主角**: 姓名、年龄、外貌、性格、背景、金手指
- **核心配角** (3-5个): 功能定位、与主角关系
- **反派**: 动机、能力、对立点
- **人物关系网**: 各角色关联

### Step 3: 构建世界观
设计：
- **世界类型**: 现代都市、异世界、未来科幻等
- **社会体系**: 权力结构、阶级划分
- **文化特色**: 信仰、习俗、禁忌

### Step 4: 设计力量体系
- **等级划分**: 从低到高的明确等级
- **力量类型**: 修炼、技能、天赋
- **克制关系**: 相生相克规则
- **成长曲线**: 前中后期节奏

### Step 5: 设计金手指
- **类型**: 系统流、重生流、穿越流等
- **规则**: 如何运作，有什么限制
- **成长性**: 解锁路径
- **代价**: 使用代价

### Step 6: 生成设计方案
将设计结果保存到 `output/design_plan.json`。

## 输出格式

```json
{
  "design_time": "当前时间",
  "track": "都市异能",
  "novel_title": "建议书名",
  "protagonist": {
    "name": "主角姓名",
    "age": 22,
    "personality": "性格描述",
    "background": "背景故事",
    "golden_finger": {
      "type": "系统流",
      "description": "金手指描述",
      "rules": ["规则1", "规则2"],
      "limitations": ["限制1"]
    }
  },
  "supporting_characters": [
    {
      "name": "配角名",
      "role": "功能定位",
      "relationship": "与主角关系",
      "personality": "性格"
    }
  ],
  "antagonist": {
    "name": "反派名",
    "motivation": "动机",
    "power": "能力",
    "conflict": "与主角的冲突点"
  },
  "world_building": {
    "type": "世界类型",
    "power_system": "力量体系描述",
    "social_structure": "社会结构",
    "key_rules": ["世界规则1", "规则2"]
  },
  "selling_points": ["卖点1", "卖点2", "卖点3"]
}
```

## 使用方式

用户调用此 skill 后，Agent 将：
1. 读取 `output/topic_report.json` 或用户指定的赛道
2. 生成完整的设计方案
3. 保存到 `output/design_plan.json`
4. 输出设计摘要供用户确认

## 设计注意事项

- 人物设计要贴近目标读者群体
- 金手指要简单易懂，有爽感
- 力量体系要有明确的成长路径
- 设定要留有扩展空间
