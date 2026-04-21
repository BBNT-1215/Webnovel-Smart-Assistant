---
name: "topic-analyzer"
description: "Analyzes web novel market data to identify trending topics, track selection, and market opportunities. Invoke when user needs topic analysis, track selection, or market opportunity identification."
---

# 赛道选题分析 Skill

## 功能概述

本 skill 基于市场数据，深度分析各赛道热门趋势、竞争格局、读者需求，为创作者提供精准的选题方向和赛道建议。

## 触发条件

- 用户要求分析网文赛道趋势
- 需要确定小说题材方向
- 需要评估赛道竞争程度
- 需要发现蓝海市场机会
- 工作流接收到市场数据后自动触发

## 分析维度

### 1. 赛道分类体系
- **玄幻类**: 东方玄幻、异世大陆、王朝争霸、高武世界
- **都市类**: 都市生活、异术超能、商战职场、娱乐明星
- **仙侠类**: 古典仙侠、幻想修仙、现代修真、神话传说
- **科幻类**: 星际文明、时空穿梭、进化变异、末世危机
- **悬疑类**: 悬疑侦探、恐怖惊悚、探险生存
- **历史类**: 架空历史、历史传记、穿越历史
- **游戏类**: 游戏异界、电竞网游、虚拟现实
- **轻小说**: 原生幻想、衍生同人、搞笑吐槽

### 2. 赛道热度分析
- 搜索热度指数
- 阅读转化率
- 付费转化率
- 完读率
- 推荐点击比
- 收藏增长曲线

### 3. 竞争格局分析
- 头部作品分析（TOP10）
- 腰部作品分布
- 新书突围概率
- 作者集中度
- 题材同质化程度

### 4. 读者需求分析
- 读者年龄分层偏好
- 性别偏好差异
- 阅读动机分析
- 痛点需求挖掘
- 爽点偏好分析

### 5. 商业价值评估
- 平均订阅收入
- IP改编潜力
- 版权开发价值
- 平台扶持力度
- 变现渠道分析

## 输出格式

```json
{
  "analysis_time": "2026-04-21T14:30:00Z",
  "tracks": [
    {
      "track_name": "都市异能",
      "heat_score": 85,
      "competition_level": "中等",
      "market_opportunity": "高",
      "reader_demand": {
        "core_demands": ["快节奏", "金手指", "打脸爽"],
        "emerging_demands": ["群像", "反套路"]
      },
      "top_elements": [
        {"element": "系统流", "popularity": 92},
        {"element": "神豪", "popularity": 78},
        {"element": "直播", "popularity": 65}
      ],
      "recommended_tags": ["都市", "异能", "系统", "轻松"],
      "difficulty_score": 6.5,
      "profit_potential": "高",
      "ip_adaptability": "中等",
      "analysis_summary": "都市异能赛道当前热度稳定，系统流仍是主流，但反套路作品有突围趋势..."
    }
  ],
  "blue_ocean_opportunities": [
    {
      "track": "科幻+历史",
      "opportunity_score": 88,
      "description": "科幻元素与历史背景结合，市场空白大"
    }
  ],
  "trend_forecast": {
    "rising_tracks": ["悬疑推理", "轻小说"],
    "declining_tracks": ["传统玄幻"],
    "stable_tracks": ["都市", "仙侠"]
  }
}
```

## 选题推荐模型

### 推荐公式
```
选题得分 = 热度(30%) + 竞争度(25%) + 读者需求(20%) + 商业价值(15%) + 创作难度(10%)
```

### 选题矩阵

| 赛道 | 热度 | 竞争 | 机会 | 推荐指数 |
|------|------|------|------|----------|
| 都市系统 | 90 | 高 | 中 | 7.5 |
| 玄幻创新 | 85 | 中 | 高 | 8.2 |
| 仙侠反套路 | 78 | 低 | 高 | 8.8 |

## 使用方式

```
skill_view(topic-analyzer) --track 都市 --analysis-type 全维度分析
skill_view(topic-analyzer) --data-source 抓取数据.json --output-format 报告
skill_view(topic-analyzer) --compare-tracks 都市,玄幻,仙侠
skill_view(topic-analyzer) --blue-ocean --top-n 5
```

## 分析策略

1. 数据驱动：基于真实平台数据进行量化分析
2. 多维度交叉：热度、竞争、需求、商业价值综合评估
3. 动态更新：定期更新分析模型
4. 个性化推荐：根据创作者偏好调整推荐权重