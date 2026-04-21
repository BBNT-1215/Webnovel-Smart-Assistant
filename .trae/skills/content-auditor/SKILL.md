---
name: "content-auditor"
description: "Reviews web novel content for common issues including character consistency, plot coherence, pacing, and writing quality. Reads generated chapters and produces audit report. Invoke when user wants content review or quality feedback."
---

# 内容审计 Skill

## 功能概述

本 skill 读取已生成的章节内容，进行多维度质量检查，生成审计报告。

## 执行步骤

### Step 1: 读取输入文件
- 读取 `output/design_plan.json` 获取人物设定
- 读取 `output/chapters/` 目录下的章节文件
- 读取 `output/characters_card.md` 获取人物卡片

### Step 2: 一致性检查

#### 人物一致性
- 对比章节中人物行为与人物卡片中的性格设定
- 检查主角姓名是否漂移
- 检查人物关系是否正确

#### 设定一致性
- 检查力量等级是否前后一致
- 检查金手指使用是否符合规则
- 检查世界观设定是否矛盾

### Step 3: 可读性检查
- 文字是否流畅
- 对话是否自然
- 描写是否有画面感

### Step 4: 节奏检查
- 开篇是否有冲突/悬念
- 爽点间隔是否合理
- 章末是否有钩子

### Step 5: 生成审计报告
将检查结果保存到 `output/audit_report.json`。

## 输出格式

```json
{
  "audit_time": "当前时间",
  "chapters_audited": [1, 2, 3],
  "issues": [
    {
      "chapter": 5,
      "type": "人物不一致",
      "severity": "中",
      "description": "主角在第3章设定为谨慎，但第5章行为冲动且无铺垫",
      "suggestion": "建议增加情绪铺垫或调整行为"
    },
    {
      "chapter": 8,
      "type": "设定矛盾",
      "severity": "高",
      "description": "主角实力在第6章为二级，第8章突然出现三级技能",
      "suggestion": "补充突破过程或修改技能描述"
    }
  ],
  "strengths": [
    "爽点分布合理，平均每4章一个",
    "章末悬念设置到位"
  ],
  "readability_score": 8.0,
  "consistency_score": 7.5,
  "pacing_score": 8.5,
  "overall_score": 8.0
}
```

## 评分标准

| 维度 | 评分项 | 说明 |
|------|--------|------|
| 可读性 | 文字流畅度 | 是否通顺自然 |
| | 对话自然度 | 对话是否符合人物 |
| | 描写具体度 | 描写是否有画面感 |
| 一致性 | 人物一致性 | 行为是否符合设定 |
| | 设定一致性 | 世界观是否前后统一 |
| 节奏 | 开篇吸引力 | 前几章是否有冲突 |
| | 爽点分布 | 爽点间隔是否合理 |

## 使用方式

用户调用此 skill 后，Agent 将：
1. 读取章节内容和设定文件
2. 执行多维度检查
3. 生成 `output/audit_report.json`
4. 输出审计报告摘要
