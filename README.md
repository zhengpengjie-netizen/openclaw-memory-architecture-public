# 🦐 OpenClaw Memory Architecture

> 智能体记忆架构设计 - 借鉴 Claude Code 512K 源码泄露分析

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Stars](https://img.shields.io/github/stars/[已脱敏]/openclaw-memory-architecture)](https://github.com/[已脱敏]/openclaw-memory-architecture/stargazers)

---

## 📖 简介

这是一个基于 **Claude Code 源码泄露事件**（2026年3月31日）分析后，设计出的智能体三层记忆架构。

Claude Code 意外泄露了 512,000 行 TypeScript 源码，让社区得以窥探前沿 AI 编程工具的内部设计。本项目借鉴其核心记忆系统理念，为 OpenClaw 等智能体框架提供可参考的记忆架构方案。

> ⚠️ 本项目**不包含** Claude Code 源码，仅借鉴其**架构设计理念**

---

## 🏗️ 三层记忆架构

```
┌─────────────────────────────────────────────────────┐
│            Layer 1: MEMORY.md (长期记忆)              │
│  • 核心身份、偏好、硬规则                            │
│  • 始终加载，每轮对话强化                            │
│  • 每行 ≤150 字符，严格限制大小                      │
│  • 上下文超过 40% 时触发预警                         │
├─────────────────────────────────────────────────────┤
│            Layer 2: Topic Files (主题文件)           │
│  • 品牌/领域/运营知识                               │
│  • 按需加载，不污染工作内存                          │
│  • shared/brands/, shared/domain/                  │
├─────────────────────────────────────────────────────┤
│            Layer 3: Daily Logs (每日日志)            │
│  • 原始对话/操作记录                                │
│  • 只搜索不加载全文                                 │
│  • memory/YYYY-MM-DD.md                            │
└─────────────────────────────────────────────────────┘
```

---

## 🧠 核心原则

### 1. Trust but Verify
> "记忆只是提示，必须验证实际情况"

AI 不应盲目相信记忆。每次行动前，验证记忆中的信息是否与当前状态一致。

### 2. 容量限制
> "无限记忆 = 无效记忆"

严格的容量限制强制系统定期清理和提炼，防止上下文污染。

### 3. 分层管理
> "不同类型的信息，不同的访问模式"

长期记忆（始终加载）vs 主题文件（按需加载）vs 日志（只搜索）

---

## 🔧 核心模块

### 1. Context Injection（上下文注入）
解决"模型看不到优化"问题 - 在推理前主动注入相关上下文。

### 2. Orchestrator（统一调度器）
系统大脑 - 协调所有模块的调度和执行。

### 3. Entity Layer（实体知识图谱）
结构化知识 - 实体 + 关系，支持复杂推理。

### 4. Memory Lifecycle（记忆生命周期）
自动管理 - 过期清理、提炼归档、去重合并。

### 5. Rule Manager（规则管理）
偏好学习 - 从历史中提取规则，置信度评估。

### 6. Watchdog（看门狗）
自动运维 - 定时检查、决策记录、异常告警。

---

## 📁 目录结构

```
├── MEMORY.md              # 长期记忆（示例）
├── USER.md                # 用户画像（示例）
├── HEARTBEAT.md           # 定时任务配置
├── README.md              # 本文档
├── scripts/               # 核心脚本
│   ├── context_builder.py    # 上下文注入
│   ├── orchestrator.py       # 统一调度器
│   ├── entity_extractor.py   # 实体提取器
│   ├── memory_lifecycle.py   # 生命周期管理
│   ├── rule_manager.py       # 规则管理
│   ├── log_distiller.py      # 日志提炼
│   ├── knowledge_graph.py    # 知识图谱
│   ├── memory_watchdog.py    # 记忆看门狗
│   └── model_watchdog.py     # 模型看门狗
├── shared/                # 共享知识
│   ├── brands/           # 品牌配置
│   ├── errors/           # 错误解决方案
│   └── operations/       # 运营模板
└── memory/               # 日志存储
    └── YYYY-MM-DD.md     # 每日日志
```

---

## 🚀 快速开始

### 1. 初始化记忆目录
```bash
mkdir -p memory shared/brands shared/errors shared/operations scripts
```

### 2. 配置 MEMORY.md
创建 `MEMORY.md`，包含：
- 身份定义
- 核心偏好
- 铁律规则

### 3. 设置定时任务
参考 `HEARTBEAT.md` 配置定时任务：
- 记忆同步
- 日志清理
- 健康检查

---

## 📚 文档

- [架构设计](./ARCHITECTURE.md) - 详细架构说明
- [三层记忆](./MEMORY_LAYERS.md) - 分层设计原理
- [规则系统](./rule_system.md) - 偏好学习机制
- [上下文注入](./context_injection_layer.md) - Context Injection 原理
- [实体关系](./entity_relationship_layer.md) - 知识图谱设计

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

---

## 📄 License

MIT License
