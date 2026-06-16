# AI-Coding-VibeCoding-File-System-Index-Protocol

# AI 编程 / Vibe Coding 文件系统索引协议

一套用于 AI 编程、Vibe Coding、AI 辅助开发的文件系统索引协议。

它的作用很简单：让 AI 在改代码之前，先理解项目结构，先读规则，先建索引，再精准定位文件，避免全项目乱扫、上下文爆炸、越改越乱。

## 这个项目解决什么问题？

现在很多 AI 编程工具在改项目时，最大的问题不是“不会写代码”，而是：

* 不知道该改哪个文件
* 喜欢全项目扫描
* 上下文消耗太大
* 修改范围不可控
* 文件越写越大
* 项目结构越来越乱
* 改完代码后不更新目录说明

这个协议的目标，就是给 AI 一张“项目地图”。

AI 不再像盲人摸象一样翻代码，而是先看规则、查目录、定位最小职责文件，再执行修改。

## 使用方式

在你的编程项目根目录里，创建一个 `docs` 文件夹：

```txt
your-project/
└── docs/
```

把本项目里的规则文件放进去，并命名为：

```txt
docs/AI_SYSTEM_RULES.md
```

也就是：

```txt
your-project/
└── docs/
    └── AI_SYSTEM_RULES.md
```

之后，每次你让 AI 开发、修改、重构、调试项目时，把这份 `AI_SYSTEM_RULES.md` 文件拖到你的提示词下面。

也就是说，AI 每次不仅要读取你的开发需求，还要同时读取这份规则文件。

## AI 读取后应该做什么？

AI 读取本协议后，应根据真实项目结构，自动在 `docs` 文件夹中创建并维护目录索引文件：

```txt
docs/
├── AI_SYSTEM_RULES.md
├── ROOT_MAP_1.md
├── ROOT_MAP_2.md
└── tree/
    ├── src.md
    ├── components.md
    └── ...
```

这些文件的作用是：

* `AI_SYSTEM_RULES.md`：唯一规则文件
* `ROOT_MAP_*.md`：项目一级目录索引
* `tree/*.md`：具体目录的二级文件索引

## 核心思想

AI 不应该直接编辑代码库。

它应该先读取规则，生成或更新目录索引，再通过索引定位最小职责文件，最后只修改必要代码。

如果项目结构发生变化，AI 还必须同步更新对应的目录索引。

## 一句话总结

让 AI 从“全项目乱翻”，变成“按地图编程”。

---

# AI-Coding / Vibe Coding File System Index Protocol

A file system indexing protocol for AI Coding, Vibe Coding, and AI-assisted software development.

Its purpose is simple: before editing code, AI should first understand the project structure, read the rules, build the index, locate the right files precisely, and avoid blind full-codebase scanning.

## What Problem Does This Solve?

Many AI coding tools do not fail because they cannot write code.

They fail because they often:

* do not know which file to edit
* scan the whole project blindly
* waste too much context
* make uncontrolled changes
* create oversized files
* damage project structure
* forget to update directory documentation after changes

This protocol gives AI a project map.

Instead of searching randomly, AI should read the rules, follow the index, locate the smallest responsible file, and then make minimal changes.

## How to Use

Create a `docs` folder in the root of your programming project:

```txt
your-project/
└── docs/
```

Place the rule file from this repository into that folder and name it:

```txt
docs/AI_SYSTEM_RULES.md
```

The final structure should look like this:

```txt
your-project/
└── docs/
    └── AI_SYSTEM_RULES.md
```

Every time you ask an AI to develop, modify, refactor, or debug your project, attach the `AI_SYSTEM_RULES.md` file under your prompt.

This makes the AI read both your task and this protocol before taking action.

## What Should AI Do After Reading It?

After reading this protocol, the AI should automatically create and maintain project index files inside the `docs` folder based on the real project structure:

```txt
docs/
├── AI_SYSTEM_RULES.md
├── ROOT_MAP_1.md
├── ROOT_MAP_2.md
└── tree/
    ├── src.md
    ├── components.md
    └── ...
```

These files mean:

* `AI_SYSTEM_RULES.md`: the only rule file
* `ROOT_MAP_*.md`: top-level project maps
* `tree/*.md`: detailed directory maps

## Core Idea

AI should not edit a codebase directly and blindly.

It should first read the rules, generate or update directory indexes, locate the smallest responsible file through the index, and then modify only the necessary code.

If the project structure changes, AI must also update the corresponding index files.

## One-line Summary

Turn AI from a random code searcher into a map-based coding agent.
