---
name: "text-optimizer"
description: "Optimizes web novel text for readability, pacing, and engagement based on audit report findings. Rewrites problematic sections and enhances writing quality. Invoke when user needs text refinement or content polishing."
---

# 文字优化 Skill

## 功能概述

本 skill 读取 `content-auditor` 生成的审计报告，针对发现的问题进行针对性优化，提升内容质量。

## 执行步骤

### Step 1: 读取输入文件
- 读取 `output/audit_report.json` 获取审计发现的问题
- 读取 `output/chapters/` 目录下对应的章节文件
- 读取 `output/design_plan.json` 获取人物设定

### Step 2: 根据审计报告优化

#### 针对人物不一致问题
- 重写不符合人物性格的行为描写
- 调整对话风格符合人物设定
- 增加情绪铺垫使行为转变合理

#### 针对设定矛盾问题
- 修正力量等级错误
- 补充突破过程
- 调整不符合世界观的描写

#### 针对可读性问题
- 优化不通顺的句子
- 增强描写的画面感
- 改进对话自然度

#### 针对节奏问题
- 压缩拖沓的段落
- 增强爽点的爆发力
- 优化章末悬念

### Step 3: 保存优化后的章节
将优化后的章节保存到 `output/chapters_optimized/第X章_章名.md`。

## 优化示例

### 人物一致性修复
```
问题: 主角设定为谨慎，但行为冲动

原文:
他二话不说就冲了上去，一拳砸向对方。

优化后:
他暗中观察了片刻，确认对方只有一个，而且左腿有伤。
确认有把握后，他才缓缓走上前，一拳砸出。
```

### 描写增强
```
原文: 他打了一拳

优化后: 他一拳砸出，拳风呼啸，空气都发出爆鸣
```

### 悬念强化
```
原文: 他回家了。

优化后: 就在他转身离开的瞬间——"叮！"系统提示音骤然响起...
```

## 输出格式

优化后的章节保存到 `output/chapters_optimized/第X章_章名.md`

同时生成优化日志 `output/optimization_log.json`:
```json
{
  "optimize_time": "当前时间",
  "chapters_optimized": [1, 2, 3],
  "changes": [
    {
      "chapter": 5,
      "issue_type": "人物不一致",
      "original": "原文片段",
      "optimized": "优化后片段",
      "reason": "优化原因"
    }
  ]
}
```

## 使用方式

用户调用此 skill 后，Agent 将：
1. 读取 `output/audit_report.json`
2. 针对问题逐一优化
3. 保存到 `output/chapters_optimized/`
4. 生成 `output/optimization_log.json`
