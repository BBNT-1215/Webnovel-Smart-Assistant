---
name: "data-scraper"
description: "Provides web novel market research guidance and data collection strategies. Helps users understand platform data structures and effective scraping methodologies. Invoke when user needs platform data collection strategies or market research approaches."
---

# 平台数据抓取指导 Skill

## 功能概述

本 skill 提供网文平台数据收集的指导和策略，帮助用户理解各平台数据结构和有效的数据收集方法。重点在于提供合规、高效的数据收集策略指导，而非直接执行抓取操作。

## 触发条件

- 用户要求了解平台数据收集策略
- 需要分析市场趋势和热门题材的数据来源
- 需要获取平台数据收集的最佳实践
- 工作流中市场研究阶段需要数据收集指导

## 数据收集策略指导

### 1. 合规数据收集原则
- **遵守robots.txt**: 严格遵循各平台的robots.txt协议
- **频率控制**: 实施合理的请求间隔，避免对目标服务器造成压力
- **用户代理**: 使用恰当的User-Agent标识
- **数据用途**: 仅用于研究分析，不用于商业用途

### 2. 平台数据结构分析
- **起点中文网**:
  - 公开API接口：月票榜、推荐榜、新书榜
  - 数据字段：书名、作者、分类、字数、收藏数、推荐票、评分
  - 更新频率：榜单每小时更新一次

- **番茄小说**:
  - 公开数据：免费榜、新书榜、畅销榜
  - 数据字段：书名、作者、分类、字数、阅读量、点赞数
  - 特殊关注：免费模式下的数据指标

- **七猫小说**:
  - 公开数据：热门榜、新书榜、完结榜
  - 数据字段：书名、作者、分类、字数、阅读数、分享数
  - 广告模式数据特点

### 3. 数据收集方法论
- **官方API优先**: 优先使用平台提供的官方API
- **公开数据利用**: 利用平台公开展示的数据
- **第三方数据源**: 使用合法的第三方数据聚合服务
- **用户调研**: 通过问卷等方式收集读者偏好数据

### 4. 反爬应对策略
- **IP轮换**: 使用代理IP池分散请求
- **请求模拟**: 模拟真实用户浏览行为
- **验证码处理**: 集成验证码识别服务
- **延迟策略**: 实施智能延迟，避免被识别为爬虫

## 实际可行的数据源

### 1. 官方开放数据
- **官方排行榜**: 各平台公布的排行榜数据
- **作家公告**: 作者发布的创作计划和更新信息
- **社区讨论**: 论坛、评论区的读者反馈数据

### 2. 第三方聚合数据
- **行业报告**: 艾瑞、QuestMobile等发布的网文行业报告
- **数据聚合平台**: 合法的第三方数据聚合服务
- **社交媒体**: 微博、知乎等平台的网文讨论数据

### 3. 用户行为数据
- **评论分析**: 分析读者评论中的偏好表达
- **互动数据**: 收藏、推荐、打赏等互动行为数据
- **阅读时长**: 分析不同类型内容的阅读完成率

## 输出格式

```json
{
  "research_time": "2026-04-21T14:00:00Z",
  "data_collection_strategy": {
    "platforms": ["起点中文网", "番茄小说", "七猫小说"],
    "legal_sources": ["官方API", "公开排行榜", "第三方聚合"],
    "collection_method": "合规数据收集策略",
    "frequency": "每日更新",
    "rate_limit": "每分钟10次请求"
  },
  "market_insights": {
    "hot_genres": ["都市", "玄幻", "仙侠"],
    "trending_topics": ["系统流", "重生", "穿越"],
    "reader_preferences": ["快节奏", "爽点密集", "情节紧凑"]
  },
  "compliance_notes": {
    "terms_compliance": true,
    "privacy_respect": true,
    "fair_use_adherence": true
  }
}
```

## 使用方式

```
skill_view(data-scraper) --platform 起点中文网 --data-type 榜单数据 --strategy 合规收集
skill_view(data-scraper) --focus 市场趋势 --sources 第三方聚合
skill_view(data-scraper) --method 反爬策略 --frequency 每日
```

## 注意事项

- 数据收集必须遵守各平台的服务条款
- 不应尝试绕过平台的安全措施
- 应尊重用户隐私和数据保护法规
- 数据仅用于分析研究目的