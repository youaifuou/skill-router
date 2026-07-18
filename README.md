# Skill Router

[中文](#中文) · [English](#english)

## 中文

一个平台中立的 Agent Skill，用于整理已经安装的 Skills，并只在存在真实发现冲突时创建垂直 Router，收敛高度相似能力的入口。

它不会按照领域、技术栈或“能够协作”进行宽泛分组，也不会用固定模板、主辅关系或调用顺序限制 Agent。具体 Router 只负责共享状态、任务事实、重复控制、授权边界和结果合并；具体方法仍保留在各叶子 Skill 中。

### 核心原则

- 默认保持 Skill 独立。
- 只聚合会自然响应同一类真实请求、解决同一种具体任务的 Skills。
- 先向用户汇报候选方案，获得批准后再调整入口。
- 根据任务事实决定使用单个或多个叶子 Skill，不预设组合模式。
- 引用叶子能力，不复制其工作流。
- 核心 `SKILL.md` 不依赖特定 Agent 平台。

### 安装

克隆仓库，并将仓库目录放入你的 Agent 平台能够发现的 Skills 目录。不同平台的目录结构和附加元数据可能不同；核心入口始终是根目录下的 `SKILL.md`。

```bash
git clone https://github.com/youaifuou/skill-router.git
```

### 使用

可以直接提出类似请求：

> 盘点我已经安装的 Skills，找出真正存在发现冲突的能力，提出垂直 Router 方案。先汇报计划，等我批准后再执行。

`skill-router` 会先完整读取相关 Skill，判断哪些能力确有必要聚合，并说明候选 Router、重叠请求、能力贡献、目录变化和回滚方法。

### 验证情况

本 Skill 使用 12 个第三方 Skills 进行了多轮隔离测试。生成的调试 Router 进一步通过了单叶子调用、多叶子协同、授权边界、真实修复和相邻触发反例测试。

### 仓库结构

```text
skill-router/
├── SKILL.md
└── README.md
```

平台专属元数据可以由使用者按需添加，不属于核心 Skill 的必要组成部分。

## English

A platform-neutral Agent Skill for organizing installed Skills and creating focused, vertical Routers only when genuine discovery conflicts exist between highly similar capabilities.

It does not group Skills broadly by domain, technology stack, or mere ability to collaborate. It also avoids fixed templates, permanent primary/supporting roles, and predetermined invocation sequences. A concrete Router coordinates shared state, task facts, duplicate work, authorization boundaries, and result merging, while each leaf Skill remains the source of its own methods.

### Core principles

- Keep Skills independent by default.
- Aggregate only Skills that naturally respond to the same real-world requests and solve the same specific task.
- Present the proposed Router plan before changing exposed Skill entry points.
- Let task facts determine whether one or multiple leaf Skills are used.
- Reference leaf capabilities instead of copying their workflows.
- Keep the core `SKILL.md` independent of any specific Agent platform.

### Installation

Clone the repository and place the repository directory where your Agent platform discovers Skills. Platforms may use different directory layouts or additional metadata; the core entry point is always the root `SKILL.md`.

```bash
git clone https://github.com/youaifuou/skill-router.git
```

### Usage

Example request:

> Review my installed Skills, identify capabilities with genuine discovery conflicts, and propose focused vertical Routers. Report the plan first and wait for my approval before applying changes.

`skill-router` reads the relevant Skills in full, determines which capabilities genuinely need aggregation, and reports the proposed Routers, overlapping requests, capability contributions, directory changes, and rollback approach.

### Validation

The Skill was tested through multiple isolated runs with 12 third-party Skills. A generated debugging Router also passed single-leaf selection, multi-leaf coordination, authorization-boundary, real-fix, and adjacent non-trigger tests.

### Repository structure

```text
skill-router/
├── SKILL.md
└── README.md
```

Platform-specific metadata may be added by users when needed and is not required by the core Skill.
