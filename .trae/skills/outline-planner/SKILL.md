---
name: "outline-planner"
description: "Creates detailed web novel outlines including volume structure, chapter breakdown, and plot pacing. Reads design plan and generates structured outline. Invoke when user needs outline creation assistance or story structure planning."
---

# 大纲规划 Skill

## 功能概述

本 skill 读取 `design-planner` 生成的设计方案，生成结构化的小说大纲，包括卷纲、章纲、节奏安排。

## 执行步骤

### Step 1: 读取设计方案
读取 `output/design_plan.json`，获取人物设定、世界观、金手指等信息。

如果用户已指定卷数和每卷章数，使用用户指定的参数。

### Step 2: 规划整体结构
- 确定分几卷，每卷主题
- 每卷的核心事件和目标
- 主角成长路径
- 感情线发展

### Step 3: 生成卷纲
对每一卷规划：
- 卷名
- 核心事件
- 主要对手
- 实力成长
- 高潮场景
- 卷末悬念

### Step 4: 生成章纲
对每一章生成：
- 章名
- 一句话概括
- 主要事件
- 出场人物
- 冲突点
- 爽点类型
- 章末悬念

### Step 5: 保存大纲
将大纲保存到 `output/outline.json`。

## 输出格式

```json
{
  "outline_time": "当前时间",
  "novel_title": "书名",
  "total_volumes": 3,
  "total_chapters": 300,
  "volumes": [
    {
      "volume_number": 1,
      "volume_name": "第一卷：觉醒",
      "chapters": "1-100",
      "summary": "本卷简介",
      "core_event": "本卷核心事件",
      "main_goal": "主角本卷目标",
      "main_antagonist": "本卷主要对手",
      "power_progress": "实力成长",
      "climax_chapter": 80,
      "climax_description": "高潮场景描述",
      "ending_hook": "卷末悬念",
      "chapter_outlines": [
        {
          "chapter": 1,
          "title": "章名",
          "summary": "一句话概括",
          "characters": ["出场人物"],
          "event": "主要事件",
          "conflict": "冲突点",
          "excitement_type": "爽点类型",
          "hook": "章末悬念"
        }
      ]
    }
  ],
  "overall_pacing": {
    "excitement_interval": "每3-5章",
    "mini_climax_interval": "每10-15章",
    "major_climax_interval": "每50-80章"
  }
}
```

## 节奏设计规则

### 开篇（1-30章）
- 第1章：冲突引入
- 第2章：金手指觉醒
- 第3章：第一次打脸
- 每3-5章一个爽点
- 每10章一个小高潮

### 中期（30-100章）
- 2-3章一个爽点
- 15-20章一个中高潮
- 深化世界观

### 后期（100+章）
- 加快主线推进
- 收束支线
- 准备最终高潮

## 使用方式

用户调用此 skill 后，Agent 将：
1. 读取 `output/design_plan.json`
2. 生成完整大纲
3. 保存到 `output/outline.json`
4. 输出大纲摘要
