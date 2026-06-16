# AI-Coding-VibeCoding-File-System-Index-Protocol

# AI 编程 / Vibe Coding 文件系统索引协议

一套用于 AI 编程、Vibe Coding、AI 辅助开发的文件系统索引协议。

它的核心作用很简单：

让 AI 在改代码前，先读规则、建索引、查目录、定位最小职责文件，再执行修改。

避免 AI 全项目乱扫、上下文爆炸、文件越写越大、结构越改越乱。

---

## 这个项目解决什么问题？

现在很多 AI 编程工具的问题，不是不会写代码，而是：

* 不知道该改哪个文件
* 喜欢全项目扫描
* 上下文消耗过大
* 修改范围不可控
* 文件职责越来越混乱
* 单文件越写越大
* 项目结构逐渐失控
* 改完代码后不更新目录说明

这个协议给 AI 一张“项目地图”。

AI 不再盲目翻代码，而是先读取规则，再通过目录索引精准定位目标文件，只修改必要范围。

---

## 核心思想

AI 不应该直接编辑代码库。

AI 应该先读取规则文件，再根据真实项目结构创建或更新索引文件，通过索引定位最小职责文件，最后执行修改。

如果项目结构发生变化，AI 必须同步更新对应目录索引。

一句话：

让 AI 从“全项目乱翻”，变成“按地图编程”。

---

## 使用方式

在你的项目根目录创建 `docs` 文件夹：

```txt
your-project/
└── docs/
```

把本项目的规则文件放进去，并命名为：

```txt
docs/AI_SYSTEM_RULES.md
```

推荐结构如下：

```txt
your-project/
└── docs/
    ├── AI_SYSTEM_RULES.md
    ├── root/
    │   ├── ROOT_MAP_1.md
    │   └── ROOT_MAP_2.md
    └── tree/
        ├── src.md
        ├── components.md
        └── ...
```

每次让 AI 开发、修改、重构、调试项目时，都把 `AI_SYSTEM_RULES.md` 附加到提示词中。

AI 必须先读取这份规则，再开始处理代码。

---

## 文件结构说明

本协议由三类文件组成：

### 1. 规则文件

固定路径：

```txt
/docs/AI_SYSTEM_RULES.md
```

作用：

* 定义所有规则
* 定义所有约束
* 定义目录生成逻辑
* AI 每次任务前必须优先读取

这是整个系统唯一规则文件，不可拆分、不可省略。

---

### 2. 总目录文件 Root Maps

固定目录：

```txt
/docs/root/
```

命名规则：

```txt
/docs/root/ROOT_MAP_*.md
```

示例：

```txt
/docs/root/ROOT_MAP_1.md
/docs/root/ROOT_MAP_2.md
/docs/root/ROOT_MAP_admin.md
```

作用：

* 管理项目一级目录结构
* 帮助 AI 快速判断应该进入哪个模块
* 避免 AI 一开始就扫描整个项目

重要规则：

* 所有 `ROOT_MAP_*.md` 必须放在 `/docs/root/`
* 不允许直接堆放在 `/docs` 根目录
* 每个 ROOT_MAP 不超过 300 行
* 超过必须拆分
* 不同 ROOT_MAP 不允许重复覆盖同一目录

ROOT_MAP 不能只写路径，必须包含一句话说明：

```txt
/src/user.ts —— 用户模块主入口，负责用户基础能力聚合（修改影响用户数据层）
/src/components/NavBar.tsx —— 顶部导航栏组件，控制全局导航结构（修改影响全局 UI）
/utils/auth.ts —— 登录鉴权工具函数集合（修改影响登录与权限判断）
```

---

### 3. 子目录文件 Tree Maps

固定目录：

```txt
/docs/tree/
```

命名规则：

```txt
/docs/tree/<directory>.md
```

示例：

```txt
/docs/tree/src.md
/docs/tree/components.md
/docs/tree/features-user.md
```

作用：

* 管理具体目录下的文件索引
* 说明每个文件的真实职责
* 帮助 AI 定位最小修改文件

TREE_MAP 不能只列路径，必须说明文件作用：

```txt
NavBar.tsx —— 顶部导航栏 UI 组件，控制主站导航结构（修改影响全局布局）
Sidebar.tsx —— 侧边栏导航组件，负责二级菜单展示与路由入口
hooks/useAuth.ts —— 登录状态 Hook，提供全局鉴权状态（修改影响权限判断）
```

---

## 模块化拆分原则

开发任何项目时，必须按“按钮、功能、职责”进行最小模块拆分。

核心规则：

* 每一个按钮尽量拆成独立组件文件
* 每一个独立功能尽量拆成独立模块文件
* 相关模块可以用文件夹分类管理
* 不得把多个无关按钮堆进同一个大文件
* 不得把多个无关功能堆进同一个大模块
* 不得为了方便一次性修改而合并不同职责

目标是：

修改某个按钮，只影响这个按钮文件。

修改某个功能，只影响这个功能模块。

修改某个目录，不应连锁破坏其他目录。

示例：

```txt
/src/components/buttons/ —— 按钮组件目录，集中管理可复用按钮 UI（修改影响按钮视觉与交互）
/src/components/buttons/SubmitButton.tsx —— 提交按钮组件，只负责提交动作入口与禁用状态
/src/features/user/profile/ —— 用户资料功能目录，管理资料查看与编辑流程
/src/features/user/profile/ProfileEditor.tsx —— 用户资料编辑模块，只负责资料表单编辑 UI
/src/features/user/profile/saveProfile.ts —— 保存用户资料功能，只负责提交资料 API 调用
```

---

## 300 行限制

所有 AI 可编辑代码文件原则上必须：

```txt
≤ 300 行
```

如果超过 300 行，必须优先拆分。

拆分方式：

* 按职责拆分
* 按功能拆分
* 按逻辑区域拆分
* 保持调用关系清晰
* 不允许功能重复
* 不允许隐藏副作用

示例：

```txt
user.ts
```

拆分为：

```txt
user.create.ts
user.update.ts
user.query.ts
```

例外：

```txt
build/
dist/
.next/
自动生成文件
```

这些文件不限制行数，但 AI 禁止修改。

---

## AI 执行流程

AI 每次执行任务必须遵守以下流程：

```txt
Step 1：读取 /docs/AI_SYSTEM_RULES.md

Step 2：读取 /docs/root/ROOT_MAP_*

Step 3：定位对应 /docs/tree/*.md

Step 4：只读取最少必要代码文件，通常 1~3 个

Step 5：执行修改

Step 6：同步更新 ROOT_MAP 和 TREE_MAP
```

AI 不允许跳过目录系统直接改代码。

---

## 目录生成规则

目录索引必须来源于真实文件系统。

不允许预设不存在的结构。

当发生以下变化时：

* 新增文件
* 删除文件
* 移动文件
* 重构目录
* 拆分模块
* 合并模块

必须同步更新：

```txt
/docs/root/ROOT_MAP_*.md
/docs/tree/*.md
```

---

## Tree Map 生成条件

当某个目录出现以下情况时，必须生成 TREE_MAP：

* 文件数超过 5 个
* 结构复杂
* 经常被修改
* 涉及多个功能模块
* AI 经常需要定位其中的文件

TREE_MAP 内容必须包含：

* 当前目录文件列表
* 子目录结构
* 每个文件夹的一句话功能说明
* 每个文件的一句话职责说明
* 必要的修改影响范围提示

禁止纯路径堆叠。

---

## 禁止行为

AI 禁止：

* 全项目扫描
* 一次性打开所有目录文件
* 忽略 ROOT_MAP
* 跳过 TREE_MAP 直接改代码
* 不更新目录系统
* 破坏 300 行限制
* 把多个无关功能写进同一个大文件
* 只列文件路径，不写职责说明
* 创建不存在于真实项目中的虚假目录结构

---

## 适合哪些项目？

适合所有需要 AI 参与开发、重构、维护的项目，尤其适合：

* 前端项目
* 后端项目
* 全栈项目
* SaaS 项目
* 管理后台
* AI 应用
* Chrome 插件
* 小程序
* 多模块复杂项目
* 长期迭代项目

项目越大，收益越明显。

---

## 本协议的本质

AI 不是编辑器。

AI 是文件系统导航执行器。

```txt
AI_SYSTEM_RULES.md = 行为规则
ROOT_MAP = 一级磁盘索引
TREE_MAP = 二级文件索引
CODE = 实际执行层
```

先导航，再修改。

先定位，再动手。

先拆职责，再写代码。

---

## One-line Summary

Turn AI from a random code searcher into a map-based coding agent.

---

# AI-Coding / Vibe Coding File System Index Protocol

A file system indexing protocol for AI Coding, Vibe Coding, and AI-assisted software development.

Its purpose is simple:

Before editing code, AI should read the rules, build or update the project index, locate the smallest responsible file, and only then modify the code.

This avoids blind full-codebase scanning, context explosion, oversized files, uncontrolled changes, and structural decay.

---

## What Problem Does This Solve?

Many AI coding tools do not fail because they cannot write code.

They fail because they often:

* do not know which file to edit
* scan the whole project blindly
* waste too much context
* make uncontrolled changes
* create oversized files
* damage project structure
* mix unrelated responsibilities
* forget to update directory documentation after changes

This protocol gives AI a project map.

Instead of searching randomly, AI reads the rules, follows the index, locates the smallest responsible file, and makes minimal changes.

---

## Core Idea

AI should not edit a codebase directly and blindly.

AI should first read the rule file, create or update project indexes based on the real file system, locate the smallest responsible file through the index, and then modify only what is necessary.

If the project structure changes, AI must update the corresponding index files.

In one sentence:

Turn AI from blind code searching into map-based coding.

---

## How to Use

Create a `docs` folder in the root of your project:

```txt
your-project/
└── docs/
```

Place the rule file from this repository into that folder and name it:

```txt
docs/AI_SYSTEM_RULES.md
```

Recommended structure:

```txt
your-project/
└── docs/
    ├── AI_SYSTEM_RULES.md
    ├── root/
    │   ├── ROOT_MAP_1.md
    │   └── ROOT_MAP_2.md
    └── tree/
        ├── src.md
        ├── components.md
        └── ...
```

Every time you ask an AI to develop, modify, refactor, or debug your project, attach `AI_SYSTEM_RULES.md` under your prompt.

The AI must read this rule file before touching the code.

---

## File Structure

This protocol consists of three types of files.

### 1. Rule File

Fixed path:

```txt
/docs/AI_SYSTEM_RULES.md
```

Purpose:

* define all rules
* define all constraints
* define index generation logic
* act as the first file AI must read

This is the only rule file in the system. It must not be split or omitted.

---

### 2. Root Maps

Fixed directory:

```txt
/docs/root/
```

Naming rule:

```txt
/docs/root/ROOT_MAP_*.md
```

Examples:

```txt
/docs/root/ROOT_MAP_1.md
/docs/root/ROOT_MAP_2.md
/docs/root/ROOT_MAP_admin.md
```

Purpose:

* map top-level project structure
* help AI decide which module to enter
* prevent AI from scanning the whole codebase first

Rules:

* all `ROOT_MAP_*.md` files must be placed under `/docs/root/`
* they must not be placed directly under `/docs`
* each ROOT_MAP must be 300 lines or less
* if it exceeds 300 lines, it must be split
* different ROOT_MAP files must not cover the same directory repeatedly

A ROOT_MAP must not contain paths only. Each entry must include a short natural-language description:

```txt
/src/user.ts —— user module entry, aggregates core user capabilities（affects user data layer）
/src/components/NavBar.tsx —— top navigation component, controls global navigation structure（affects global UI）
/utils/auth.ts —— authentication utility functions（affects login and permission checks）
```

---

### 3. Tree Maps

Fixed directory:

```txt
/docs/tree/
```

Naming rule:

```txt
/docs/tree/<directory>.md
```

Examples:

```txt
/docs/tree/src.md
/docs/tree/components.md
/docs/tree/features-user.md
```

Purpose:

* map files inside a specific directory
* explain the responsibility of each file
* help AI locate the smallest file to edit

A TREE_MAP must not contain paths only. Each entry must explain what the file does:

```txt
NavBar.tsx —— top navigation UI component, controls main site navigation（affects global layout）
Sidebar.tsx —— sidebar navigation component, handles secondary menus and route entries
hooks/useAuth.ts —— authentication state hook, provides global auth status（affects permission checks）
```

---

## Modular Development Rules

Any project should be developed by splitting code according to buttons, features, and responsibilities.

Core rules:

* each button should preferably be an independent component file
* each independent feature should preferably be an independent module file
* related modules can be grouped into folders
* unrelated buttons must not be stacked into one large file
* unrelated features must not be mixed into one large module
* different responsibilities must not be merged just for convenience

Goal:

Changing one button should only affect that button file.

Changing one feature should only affect that feature module.

Changing one directory should not unexpectedly break unrelated directories.

Example:

```txt
/src/components/buttons/ —— reusable button UI components（affects button visuals and interactions）
/src/components/buttons/SubmitButton.tsx —— submit button component, only handles submit entry and disabled state
/src/features/user/profile/ —— user profile feature directory, manages profile viewing and editing
/src/features/user/profile/ProfileEditor.tsx —— profile editor module, only handles profile form UI
/src/features/user/profile/saveProfile.ts —— save profile function, only handles profile API submission
```

---

## 300-Line Limit

All AI-editable code files should follow this rule:

```txt
≤ 300 lines
```

If a file exceeds 300 lines, it must be split first.

Split by:

* responsibility
* feature
* logical section
* clear call relationships
* no duplicated functionality
* no hidden side effects

Example:

```txt
user.ts
```

Split into:

```txt
user.create.ts
user.update.ts
user.query.ts
```

Exceptions:

```txt
build/
dist/
.next/
generated files
```

These files are not limited by line count, but AI must not edit them.

---

## AI Execution Flow

Every AI task must follow this process:

```txt
Step 1: Read /docs/AI_SYSTEM_RULES.md

Step 2: Read /docs/root/ROOT_MAP_*

Step 3: Locate the corresponding /docs/tree/*.md

Step 4: Read only the minimum necessary code files, usually 1–3 files

Step 5: Make the change

Step 6: Update ROOT_MAP and TREE_MAP
```

AI must not skip the directory system and edit code directly.

---

## Index Generation Rules

Directory indexes must come from the real file system.

AI must not invent nonexistent structures.

When any of the following changes happen:

* file added
* file deleted
* file moved
* directory refactored
* module split
* module merged

AI must update:

```txt
/docs/root/ROOT_MAP_*.md
/docs/tree/*.md
```

---

## When to Generate a Tree Map

A TREE_MAP must be generated when a directory:

* contains more than 5 files
* has complex structure
* is frequently modified
* contains multiple feature modules
* is often needed for AI file targeting

TREE_MAP content must include:

* current directory files
* subdirectory structure
* one-line description for each folder
* one-line responsibility description for each file
* necessary modification impact hints

Pure path lists are forbidden.

---

## Forbidden Behaviors

AI must not:

* scan the whole project blindly
* open all directory files at once
* ignore ROOT_MAP
* skip TREE_MAP and edit code directly
* fail to update the index system
* break the 300-line limit
* put unrelated features into one large file
* list file paths without responsibility descriptions
* create fake structures that do not exist in the real project

---

## Suitable Projects

This protocol is suitable for any project involving AI-assisted development, especially:

* frontend projects
* backend projects
* full-stack projects
* SaaS products
* admin dashboards
* AI applications
* Chrome extensions
* mini programs
* complex multi-module systems
* long-term maintained projects

The larger the project, the greater the benefit.

---

## Essence of This Protocol

AI is not an editor.

AI is a file-system navigation executor.

```txt
AI_SYSTEM_RULES.md = behavior rules
ROOT_MAP = first-level disk index
TREE_MAP = second-level file index
CODE = execution layer
```

Navigate first, then modify.

Locate first, then edit.

Split responsibilities first, then write code.

---

## One-line Summary

Turn AI from a random code searcher into a map-based coding agent.
