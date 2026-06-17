# AI-Coding-VibeCoding-File-System-Index-Protocol

# AI 编程 / Vibe Coding 文件系统索引协议

一套用于 AI 编程与 Vibe Coding 的文件系统索引与代码约束协议。

它的目标不是教 AI 写代码，而是**控制 AI 如何“找到代码并修改代码”**。

---

# 🧠 这个项目解决什么问题？

在 AI 编程中，最大的问题通常不是“不会写代码”，而是：

* AI 不知道该改哪个文件
* 容易全项目扫描
* 修改范围不可控
* 代码越改越乱（屎山生成）
* 文件职责混乱
* 项目结构无法持续维护

---

# 🎯 本协议的核心作用

本协议将你的项目转化为一个：

> 📍 AI 可导航的代码系统（AI Navigable Codebase）

AI 在执行任何修改前必须：

1. 读取规则文件
2. 读取目录索引（ROOT_MAP）
3. 定位最小职责文件
4. 进行局部修改
5. 同步更新索引系统

---

# 📁 使用方式

## 1. 在项目中创建 docs 目录

```txt
your-project/
└── docs/
```

---

## 2. 放入核心规则文件

```txt
docs/AI_SYSTEM_RULES.md
```

---

## 3. 每次使用 AI 时

将 `AI_SYSTEM_RULES.md` 文件：

👉 **拖到你的 Prompt 下方**

让 AI 同时读取：

* 你的任务
* 项目规则
* 项目结构约束

---

# 🧩 AI 会自动生成的结构

AI 会在 docs 中维护：

```txt
docs/
├── AI_SYSTEM_RULES.md
├── root/
│   ├── ROOT_MAP_1.md
│   └── ROOT_MAP_2.md
└── tree/
    ├── src.md
    ├── components.md
```

---

# ⚙️ 核心设计思想

## 1️⃣ AI 不能直接“找代码”，必须“按索引找代码”

## 2️⃣ 每个文件必须只有一个职责

## 3️⃣ 所有修改必须可追踪、可定位

## 4️⃣ 结构变化必须同步更新索引系统

---

# 🚫 强约束行为

本协议禁止 AI：

* 全项目扫描代码
* 同时读取所有文件
* 修改未定位文件
* 跳过 ROOT_MAP
* 跳过 TREE_MAP
* 不更新索引结构
* 破坏单文件职责原则

---

# 📦 系统本质

本系统本质是：

> AI Coding 的“文件系统操作协议”，而不是普通开发规范

---

# 💡 一句话总结

让 AI 从“读代码的人”，变成“按地图操作代码的执行器”。

---

# 🇬🇧 English Version

---

# AI-Coding-VibeCoding-File-System-Index-Protocol

A file system indexing and coding constraint protocol for AI Coding and Vibe Coding.

Its purpose is not to help AI write code, but to control **how AI locates and modifies code**.

---

# 🧠 Problem It Solves

In AI coding, the main issues are:

* AI does not know which file to edit
* It scans the entire project unnecessarily
* Changes are not controlled
* Codebases become messy over time
* File responsibilities are unclear
* Project structure cannot be maintained

---

# 🎯 Core Function

This protocol transforms your project into:

> 📍 An AI-navigable codebase

Before making any change, AI must:

1. Read the rule file
2. Read the directory index (ROOT_MAP)
3. Locate the smallest responsible file
4. Make minimal changes
5. Sync the index system

---

# 📁 How to Use

## 1. Create docs folder

```txt
your-project/
└── docs/
```

---

## 2. Add core rule file

```txt
docs/AI_SYSTEM_RULES.md
```

---

## 3. When using AI

Attach `AI_SYSTEM_RULES.md` under your prompt so AI reads:

* Task
* Rules
* Project structure constraints

---

# 🧩 Generated Structure

```txt
docs/
├── AI_SYSTEM_RULES.md
├── root/
│   ├── ROOT_MAP_1.md
│   └── ROOT_MAP_2.md
└── tree/
    ├── src.md
    ├── components.md
```

---

# ⚙️ Core Principles

* AI must not search code freely
* Every file has exactly one responsibility
* All changes must be traceable
* Structural changes must update indexes

---

# 🚫 Forbidden Actions

AI must NOT:

* scan entire codebase
* read all files at once
* modify unlocated files
* skip ROOT_MAP
* skip TREE_MAP
* ignore index updates
* break single-responsibility rule

---

# 📦 System Essence

This is not a coding guideline.

It is a **file-system-level execution protocol for AI coding agents**.

---

# 💡 One-line Summary

Turn AI from a code reader into a map-driven code executor.
