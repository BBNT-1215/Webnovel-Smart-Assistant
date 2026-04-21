---
name: "data-scraper"
description: "Scrapes web novel platform data including trending novels, ranking lists, reader demographics, and market trends. Invoke when user needs platform data collection, market research, or trending novel analysis."
---

# 平台数据抓取 Skill

## 功能概述

本 skill 负责从各大网文平台抓取热门作品数据、榜单信息、读者画像、市场趋势等关键数据，为后续的选题分析提供数据支撑。

## 触发条件

- 用户要求抓取网文平台数据
- 需要分析市场趋势和热门题材
- 需要收集竞品小说信息
- 需要获取榜单数据（月票榜、推荐榜、畅销榜等）
- 工作流自动化启动时作为第一步

## 支持平台

- 起点中文网
- 番茄小说
- 七猫小说
- 纵横中文网
- 晋江文学城
- 潇湘书院
- 其他主流网文平台

## 抓取数据维度

### 1. 榜单数据
- 月票榜 TOP100
- 推荐榜 TOP100
- 畅销榜 TOP100
- 新书榜 TOP100
- 完本榜 TOP100
- 各大分类榜单

### 2. 作品数据
- 书名、作者、分类标签
- 字数、更新频率
- 收藏数、推荐票、月票数
- 评分、评论数、读者互动数据
- 简介、题材标签
- 更新时间、连载状态

### 3. 读者数据
- 读者画像（年龄、性别、地域）
- 阅读偏好分析
- 活跃时间段
- 付费意愿数据
- 评论情感分析

### 4. 市场趋势
- 热门题材趋势
- 新兴标签识别
- 题材饱和度分析
- 蓝海市场发现
- 周期性趋势（节日、季节影响）

## 输出格式

```json
{
  "scrape_time": "2026-04-21T14:00:00Z",
  "platform": "起点中文网",
  "data_type": "榜单数据",
  "novels": [
    {
      "title": "小说名称",
      "author": "作者名",
      "category": "玄幻/都市/仙侠等",
      "tags": ["标签1", "标签2"],
      "word_count": 1000000,
      "collect_count": 500000,
      "recommend_count": 300000,
      "monthly_ticket": 80000,
      "rating": 9.2,
      "status": "连载/完结",
      "update_frequency": "日更/周更",
      "synopsis": "简介内容"
    }
  ],
  "trend_data": {
    "hot_tags": ["标签1", "标签2"],
    "emerging_tags": ["新标签1"],
    "market_saturation": {
      "玄幻": "高",
      "都市": "中",
      "科幻": "低"
    }
  }
}
```

## 使用方式

```
/data-scraper --platform 起点中文网 --data-type 月票榜 --limit 100
/data-scraper --platform 番茄小说 --data-type 趋势分析
/data-scraper --multi-platform 起点,番茄,七猫 --data-type 全量数据
```

## 数据处理规则

1. 自动去重：同一作品多次抓取时自动去重
2. 数据清洗：过滤异常数据、刷榜数据
3. 数据标准化：统一各平台数据格式
4. 增量更新：仅更新变动数据
5. 异常检测：识别数据异常并标记

## 注意事项

- 遵守平台 robots.txt 协议
- 控制抓取频率，避免对目标服务器造成压力
- 数据仅用于分析研究，不得商业用途
- 定期更新抓取策略以应对平台反爬机制
