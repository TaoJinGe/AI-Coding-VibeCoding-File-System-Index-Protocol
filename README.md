# AI 编程 / Vibe Coding 文件系统索引协议

一套用于 AI 编程与 Vibe Coding 的项目索引、功能链路追踪和代码修改约束协议。

它的目标不是教 AI 写代码，而是控制 AI：

- 如何找到代码
- 如何判断影响范围
- 如何避免乱改
- 如何持续维护项目结构
- 如何在多年后仍能理解功能链路

一句话：

> 让 AI 不靠记忆写代码，而是按地图和链路执行修改。

---

## 这个项目解决什么问题？

在 AI 编程中，真正危险的通常不是 AI 不会写代码，而是：

- AI 不知道该改哪个文件
- AI 不知道按钮背后牵动哪些接口和数据
- AI 容易全项目扫描，浪费上下文
- AI 修改范围不可控
- 新功能覆盖旧功能
- 页面、接口、数据库、状态互相纠缠
- 项目越改越乱
- 几个月后，连开发者自己也忘了原来的业务设计

本协议要解决的是：

> AI 开发中的“项目失忆”和“牵一发动全身”。

---

## 核心思想

本协议把项目拆成两张地图：

| 地图 | 作用 |
|---|---|
| 文件地图 | 告诉 AI 文件在哪里、文件负责什么 |
| 功能链路地图 | 告诉 AI 用户动作会触发哪些代码、接口、数据和状态变化 |

文件地图解决：

```text
我该改哪个文件？

功能链路地图解决：

我改这里会影响谁？
docs 目录结构

推荐在项目中维护以下结构：

docs/
├── AI_SYSTEM_RULES.md
├── AI项目开发补充指南.md
├── root/
│   ├── ROOT_MAP_1.md
│   └── ROOT_MAP_2.md
├── tree/
│   ├── src.md
│   ├── components.md
│   └── api.md
├── flow-root/
│   ├── FLOW_ROOT_MAP_1.md
│   └── FLOW_ROOT_MAP_2.md
└── flow-tree/
    ├── auth.md
    ├── user-profile.md
    ├── upload.md
    ├── wallet.md
    └── admin.md
文件地图：root / tree

文件地图用于控制 AI 如何定位代码。

root

/docs/root/ROOT_MAP_*.md

负责一级目录索引，告诉 AI 项目有哪些主要区域。

示例：

/src/ —— 前端源码目录，负责页面、组件和状态逻辑（修改影响前端功能）
/api/ —— 后端接口目录，负责业务 API 和数据处理（修改影响接口行为）
/docs/tree/ —— 二级文件索引目录，负责定位具体文件
tree

/docs/tree/*.md

负责具体目录下的文件说明。

示例：

LoginButton.tsx —— 登录按钮组件，只负责登录动作入口（关联 FLOW_ID：AUTH_LOGIN_001）
useAuth.ts —— 登录状态 Hook，只负责维护当前用户登录态（关联 FLOW_ID：AUTH_LOGIN_001）
profileApi.ts —— 用户资料接口封装，只负责资料读取和保存（关联 FLOW_ID：PROFILE_SAVE_001）
功能链路地图：flow-root / flow-tree

功能链路地图用于控制 AI 理解业务因果关系。

它记录：

页面 -> 按钮/动作 -> 前端函数 -> API -> 后端文件 -> 数据表/状态 -> 关联功能 -> 验证方式
flow-root

/docs/flow-root/FLOW_ROOT_MAP_*.md

负责功能域总览。

示例：

用户认证链路 —— 登录、注册、退出、会话校验。详见 /docs/flow-tree/auth.md（影响权限和用户状态）
文件上传链路 —— 上传、进度、历史任务、下载。详见 /docs/flow-tree/upload.md（影响文件、任务和用户记录）
钱包积分链路 —— 余额查询、积分扣除、充值订单、流水。详见 /docs/flow-tree/wallet.md（影响用户资产）
flow-tree

/docs/flow-tree/*.md

负责记录具体功能链路。

示例：

FLOW_ID：AUTH_LOGIN_001
功能名称：用户登录
入口页面：/login
触发点：登录按钮
前端文件：/src/pages/login/LoginForm.tsx
前端函数或事件：submitLogin
API/后端入口：POST /api/login
后端核心文件：/api/auth/login.ts
数据影响：users、sessions
状态变化：写入 session，刷新登录态
关联功能：PROFILE_VIEW_001、AUTH_LOGOUT_001
风险等级：高
验证方式：输入账号密码后检查登录态、跳转、个人中心访问权限
AI 修改前必须执行

AI 在修改任何代码前，必须先判断：

1. 本次修改涉及哪些文件？
2. 本次修改涉及哪些 FLOW_ID？
3. 是否新增 FLOW_ID？
4. 是否影响已有功能链路？
5. 是否影响 API、数据库、状态、权限、跳转或公共区域？
6. 是否需要同步更新 root/tree？
7. 是否需要同步更新 flow-root/flow-tree？

没有完成影响分析，禁止直接修改代码。

AI 修改后必须同步

只要发生以下变化，必须更新索引：

新增文件
删除文件
移动文件
拆分文件
新增按钮
修改按钮行为
新增页面动作
修改表单
修改 API
修改数据库影响
修改状态变化
修改上传、下载、登录、注册、保存、删除、扣费、充值、后台操作

必须同步：

/docs/root/
/docs/tree/
/docs/flow-root/
/docs/flow-tree/
核心约束

AI 必须遵守：

不得跳过规则文件
不得跳过 ROOT_MAP / TREE_MAP
不得跳过 FLOW_ROOT_MAP / FLOW_TREE
不得盲目全项目扫描
不得一次性读取大量无关文件
不得修改未定位文件
不得破坏单文件职责
不得让一个文件承担多个无关业务职责
不得改完代码不更新索引
文件职责规则

每个文件必须尽量只承担一个明确职责。

如果一个文件同时承担：

UI + 业务逻辑 + API 调用 + 数据处理

应优先拆分。

示例：

ProfilePage.tsx
ProfileForm.tsx
saveProfile.ts
profileApi.ts
useProfileState.ts

目标是：

修改一个按钮时，只影响这个按钮和它明确关联的链路。

推荐使用流程
第一次接入项目

让 AI 执行：

请严格读取 AI_SYSTEM_RULES.md，并基于当前真实项目生成：

1. /docs/root/ROOT_MAP_*.md
2. /docs/tree/*.md
3. /docs/flow-root/FLOW_ROOT_MAP_*.md
4. /docs/flow-tree/*.md

本次只生成索引文档，不修改业务代码。
如果无法确认某条链路，请标记为“待确认”，不得编造。
后续开发功能

让 AI 执行：

请先读取：

1. /docs/AI_SYSTEM_RULES.md
2. /docs/root/ROOT_MAP_*.md
3. 相关 /docs/tree/*.md
4. /docs/flow-root/FLOW_ROOT_MAP_*.md
5. 相关 /docs/flow-tree/*.md

修改前先说明本次涉及哪些文件和 FLOW_ID。
确认影响范围后再修改代码。
修改完成后同步更新文件地图和功能链路地图。
适合什么项目？

适合：

AI 辅助开发项目
Vibe Coding 项目
中大型网站
SaaS 项目
管理后台
多页面工具站
有登录、上传、支付、任务、后台、API 的项目
长期维护、多人维护、反复迭代的项目

不适合：

一次性小 Demo
极小型静态页面
不需要长期维护的临时代码
本协议的本质

这不是普通开发规范。

它是：

AI Coding 的项目记忆系统。

更准确地说：

root/tree = 文件空间记忆
flow-root/flow-tree = 业务因果记忆

当项目变大后，真正救命的不是让 AI 多读代码，而是让 AI 先读地图。

一句话总结

让 AI 从“凭感觉改代码”，变成“按文件地图定位，按功能链路判断影响，再小步修改”。

AI-Coding / Vibe Coding File System Index Protocol

A project indexing, functional flow tracking, and code modification constraint protocol for AI Coding and Vibe Coding.

Its purpose is not to teach AI how to write code.

Its purpose is to control:

how AI locates code
how AI understands impact
how AI avoids unsafe edits
how project structure stays maintainable
how functional behavior remains traceable over time

In one sentence:

Make AI modify code through maps and flows, not memory and guessing.

What Problem Does This Solve?

In AI coding, the dangerous part is usually not that AI cannot write code.

The real problems are:

AI does not know which file to edit
AI does not know what a button triggers behind the scenes
AI scans the entire project unnecessarily
change scope becomes uncontrollable
new features break old features
pages, APIs, databases, and states become tangled
the codebase gets worse over time
even the original developer forgets the system design after a few months

This protocol solves:

project amnesia and hidden functional coupling in AI coding.

Core Idea

This protocol creates two maps for your project:

Map	Purpose
File Map	Tells AI where files are and what they do
Functional Flow Map	Tells AI what user actions trigger across code, APIs, data, and state

The file map answers:

Which file should I edit?

The functional flow map answers:

What will this change affect?
docs Structure

Recommended structure:

docs/
├── AI_SYSTEM_RULES.md
├── AI项目开发补充指南.md
├── root/
│   ├── ROOT_MAP_1.md
│   └── ROOT_MAP_2.md
├── tree/
│   ├── src.md
│   ├── components.md
│   └── api.md
├── flow-root/
│   ├── FLOW_ROOT_MAP_1.md
│   └── FLOW_ROOT_MAP_2.md
└── flow-tree/
    ├── auth.md
    ├── user-profile.md
    ├── upload.md
    ├── wallet.md
    └── admin.md
File Map: root / tree

The file map controls how AI locates code.

root

/docs/root/ROOT_MAP_*.md

Root maps provide top-level project navigation.

Example:

/src/ —— frontend source directory for pages, components, and state logic
/api/ —— backend API directory for business endpoints and data processing
/docs/tree/ —— second-level file index directory
tree

/docs/tree/*.md

Tree maps describe files inside specific directories.

Example:

LoginButton.tsx —— login button component, only responsible for the login action entry (FLOW_ID: AUTH_LOGIN_001)
useAuth.ts —— auth state hook, only responsible for current user session state (FLOW_ID: AUTH_LOGIN_001)
profileApi.ts —— profile API wrapper, only responsible for reading and saving profile data (FLOW_ID: PROFILE_SAVE_001)
Functional Flow Map: flow-root / flow-tree

The functional flow map records business behavior and impact chains.

It tracks:

page -> button/action -> frontend function -> API -> backend file -> database/state -> related flows -> verification
flow-root

/docs/flow-root/FLOW_ROOT_MAP_*.md

Flow root maps provide functional domain navigation.

Example:

Authentication flows —— login, register, logout, session validation. See /docs/flow-tree/auth.md
Upload flows —— upload, progress, task history, download. See /docs/flow-tree/upload.md
Wallet flows —— balance query, point deduction, recharge order, ledger entries. See /docs/flow-tree/wallet.md
flow-tree

/docs/flow-tree/*.md

Flow tree files record concrete functional chains.

Example:

FLOW_ID: AUTH_LOGIN_001
Feature Name: User Login
Entry Page: /login
Trigger: Login button
Frontend File: /src/pages/login/LoginForm.tsx
Frontend Function/Event: submitLogin
API/Backend Entry: POST /api/login
Backend Core File: /api/auth/login.ts
Data Impact: users, sessions
State Change: create session and refresh auth state
Related Flows: PROFILE_VIEW_001, AUTH_LOGOUT_001
Risk Level: High
Verification: submit credentials, check session, redirect, and profile access
Required Before Any AI Edit

Before changing code, AI must answer:

1. Which files are involved?
2. Which FLOW_IDs are involved?
3. Is a new FLOW_ID required?
4. Will existing flows be affected?
5. Will APIs, database, state, permissions, routing, or shared UI be affected?
6. Should root/tree be updated?
7. Should flow-root/flow-tree be updated?

No impact analysis, no code modification.

Required After Any AI Edit

The index must be updated when any of the following changes:

new file
deleted file
moved file
split file
new button
changed button behavior
new page action
changed form
changed API
changed database impact
changed state transition
changed upload, download, login, register, save, delete, deduction, recharge, or admin operation

Required updates:

/docs/root/
/docs/tree/
/docs/flow-root/
/docs/flow-tree/
Core Constraints

AI must not:

skip the rule file
skip ROOT_MAP / TREE_MAP
skip FLOW_ROOT_MAP / FLOW_TREE
blindly scan the whole project
read too many unrelated files at once
modify unlocated files
break single-file responsibility
put unrelated responsibilities into one file
change code without updating indexes
File Responsibility Rule

Each file should have one clear responsibility.

If a file mixes:

UI + business logic + API calls + data processing

it should be split.

Example:

ProfilePage.tsx
ProfileForm.tsx
saveProfile.ts
profileApi.ts
useProfileState.ts

The goal:

Editing one button should only affect that button and its clearly related flow.

Recommended Workflow
First-time Project Setup

Ask AI:

Please strictly read AI_SYSTEM_RULES.md and generate the following based on the real current project:

1. /docs/root/ROOT_MAP_*.md
2. /docs/tree/*.md
3. /docs/flow-root/FLOW_ROOT_MAP_*.md
4. /docs/flow-tree/*.md

Only generate index documents in this task. Do not modify business code.
If a flow cannot be confirmed from code, mark it as "To Be Confirmed". Do not invent behavior.
Future Feature Development

Ask AI:

Please read:

1. /docs/AI_SYSTEM_RULES.md
2. /docs/root/ROOT_MAP_*.md
3. relevant /docs/tree/*.md
4. /docs/flow-root/FLOW_ROOT_MAP_*.md
5. relevant /docs/flow-tree/*.md

Before editing, explain which files and FLOW_IDs are involved.
Only modify code after the impact scope is clear.
After modification, update both the file map and the functional flow map.
Best For

This protocol is useful for:

AI-assisted coding projects
Vibe Coding projects
medium and large websites
SaaS projects
admin dashboards
multi-page tool sites
projects with login, upload, payment, tasks, admin panels, or APIs
long-term projects with repeated iteration

Not ideal for:

one-off demos
tiny static pages
temporary code that does not need maintenance
System Essence

This is not a normal coding guideline.

It is:

a project memory system for AI Coding.

More precisely:

root/tree = file-space memory
flow-root/flow-tree = business-causality memory

As a project grows, the solution is not to make AI read more code.

The solution is to make AI read the maps first.

One-line Summary

Turn AI from a guess-based code editor into a map-driven, flow-aware code executor.
