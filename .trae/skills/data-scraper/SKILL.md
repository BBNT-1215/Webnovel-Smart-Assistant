---
name: "data-scraper"
description: "Scrapes web novel platform data using web search and fetch tools to collect trending novels, rankings, and market trends. Invoke when user needs platform data collection, market research, or trending novel analysis."
---

# 平台数据抓取 Skill

## 功能概述

本 skill 使用 AI Agent 的 WebSearch 和 WebFetch 工具，从各大网文平台抓取热门作品数据、榜单信息、市场趋势。

## 执行步骤

Agent 按以下步骤执行：

### Step 1: 搜索热门榜单
使用 WebSearch 搜索各平台的实时数据：
```
搜索关键词示例:
- "起点中文网 月票榜 2026"
- "番茄小说 热门小说排行"
- "七猫小说 畅销榜 最新"
- "2026年网文热门题材趋势"
```

### Step 2: 获取详细数据
使用 WebFetch 获取相关页面内容，提取：
- 书名、作者、分类
- 排名数据
- 读者讨论热度

### Step 3: 整理数据
将搜索到的数据整理为结构化格式，保存到文件。

## 输出格式

将数据保存到 `output/platform_data.json`：

```json
{
  "scrape_time": "当前时间",
  "platforms": {
    "起点中文网": {
      "top_novels": [
        {
          "rank": 1,
          "title": "书名",
          "author": "作者",
          "category": "分类",
          "tags": ["标签"],
          "description": "简介"
        }
      ]
    },
    "番茄小说": { ... }
  },
  "trends": {
    "hot_genres": ["热门题材"],
    "emerging_tags": ["新兴标签"],
    "market_notes": "市场趋势观察"
  }
}
```

## 数据源策略

由于平台有反爬机制，采用以下策略：

1. **搜索引擎聚合**: 通过 Google/Bing 搜索获取公开的排行信息
2. **第三方数据站**: 获取合法的第三方聚合数据
3. **社交媒体**: 从微博、知乎获取讨论热度数据
4. **行业报告**: 搜索艾瑞、QuestMobile 等发布的报告

## 使用方式

用户调用此 skill 后，Agent 将：
1. 执行 WebSearch 获取各平台热门作品数据
2. 整理数据并保存到 `output/platform_data.json`
3. 输出数据摘要给用户

## 限制说明

- 无法获取平台的内部数据（收藏数、订阅数等精确数字）
- 数据来自公开搜索结果，可能不是最新
- 反爬严重的平台（起点、番茄）只能获取有限的公开信息
- 建议用户结合自己的手动调研补充数据
