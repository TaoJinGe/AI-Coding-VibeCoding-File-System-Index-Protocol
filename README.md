# AI-AI-Coding-File-System-Index-Protocol

# AI 编程文件系统索引协议

A file system indexing protocol for AI-assisted coding.
一套用于 AI 编程协作的文件系统索引协议。

It helps AI coding agents understand a project before editing it: locate files precisely, avoid full-project scanning, reduce context waste, split code by responsibility, and keep directory indexes synchronized as the project evolves.
它帮助 AI 编程助手在改代码之前先理解项目：精准定位文件、避免全项目扫描、减少上下文浪费、按职责拆分代码，并在项目变化时持续同步目录索引。

## How to Use

## 使用方式

In your programming project, create a `docs` folder:

```txt
your-project/
└── docs/
```

Place this file inside the `docs` folder and name it:

```txt
docs/AI_SYSTEM_RULES.md
```

在你的编程项目中创建一个 `docs` 文件夹，并把本文件放进去：

```txt
你的项目/
└── docs/
    └── AI_SYSTEM_RULES.md
```

Every time you ask an AI to develop, modify, refactor, or debug your project, attach this file under your prompt so the AI reads both your task and this protocol before taking action.
每次让 AI 开发、修改、重构或调试项目时，把这份文件拖到你的提示词下面，让 AI 在读取你的任务后，同时读取这份协议，再开始执行。

After reading this protocol, the AI should automatically create and maintain the project index files inside the `docs` folder, including:

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

AI 读取本协议后，应根据真实项目结构，在 `docs` 文件夹中自动创建并维护目录索引文件，包括：

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

## Core Idea

## 核心思想

AI should not edit a codebase blindly.
AI 不应该盲目编辑代码库。

Before changing code, it should first read the rules, generate or update the project maps, locate the smallest responsible file, make minimal changes, and synchronize the index after structural changes.
在改代码之前，它应该先读取规则，生成或更新项目目录索引，定位最小职责文件，执行最小修改，并在结构变化后同步更新索引。

## What This Protocol Creates

## 本协议会生成什么

This protocol turns your `docs` folder into an AI-readable navigation system for your codebase.
这套协议会把你的 `docs` 文件夹变成一个 AI 可读取的代码库导航系统。

* `AI_SYSTEM_RULES.md` — the only rule file

* `ROOT_MAP_*.md` — top-level project maps

* `tree/*.md` — detailed directory maps

* `AI_SYSTEM_RULES.md` —— 唯一规则文件

* `ROOT_MAP_*.md` —— 项目一级目录索引

* `tree/*.md` —— 具体目录的二级文件索引

The result is simple:
结果很简单：

AI stops searching randomly and starts coding by map.
AI 不再乱翻项目，而是按地图编程。
