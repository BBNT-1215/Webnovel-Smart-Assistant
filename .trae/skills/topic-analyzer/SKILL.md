---
name: "topic-analyzer"
description: "Analyzes web novel market data to identify trending topics, track selection, and market opportunities. Reads platform data from data-scraper output and generates analysis report. Invoke when user needs topic analysis, track selection, or market opportunity identification."
---

# 赛道选题分析 Skill

## 功能概述

本 skill 读取 `data-scraper` 生成的平台数据，分析热门赛道、竞争格局、读者需求，生成选题分析报告。

## 执行步骤

### Step 1: 读取数据
读取 `output/platform_data.json` 文件中的数据。

如果文件不存在，告知用户需要先运行 data-scraper。

### Step 2: 分析赛道热度
从数据中提取：
- 各题材出现频率
- 热门作品共同特征
- 新兴题材趋势

### Step 3: 评估竞争程度
分析：
- 头部作品的优势
- 新入作品的突围空间
- 题材饱和度

### Step 4: 识别蓝海机会
寻找：
- 读者有需求但供给不足的题材
- 热门元素的创新组合
- 差异化创作方向

### Step 5: 生成选题报告
将分析结果保存到 `output/topic_report.json`。

## 输出格式

```json
{
  "analysis_time": "当前时间",
  "tracks": [
    {
      "track_name": "都市异能",
      "heat_level": "高",
      "competition_level": "中等",
      "opportunity_score": 8.5,
      "hot_elements": ["系统流", "神豪", "直播"],
      "recommended_angle": "反套路+群像",
      "notes": "分析说明"
    }
  ],
  "blue_ocean_opportunities": [
    {
      "direction": "科幻+历史",
      "reason": "市场空白，读者有需求",
      "difficulty": "中等"
    }
  ],
  "selection_advice": "选题建议总结"
}
```

## 选题评分标准

| 维度 | 权重 | 说明 |
|------|------|------|
| 热度 | 30% | 读者关注度 |
| 竞争度 | 25% | 作品数量和质量 |
| 差异化空间 | 20% | 能否写出新意 |
| 创作难度 | 15% | 作者擅长程度 |
| 商业价值 | 10% | 变现潜力 |

## 使用方式

用户调用此 skill 后，Agent 将：
1. 读取 `output/platform_data.json`
2. 执行多维度分析
3. 生成 `output/topic_report.json`
4. 输出分析摘要和选题建议
