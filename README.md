# Skill Router

[中文](#中文) · [English](#english)

## 中文

`skill-router` 是一个平台中立的 Agent Skill。它帮助 Agent 盘点已经安装的 Skills，识别真正会竞争同一用户请求的高度相似能力，并在必要时创建垂直 Router，减少入口冲突，同时保留每个原始 Skill 的完整能力。

### 为什么需要它

Agent 通常根据 Skill 的名称和描述判断该调用哪一个。安装的 Skill 较少时，这种方式足够有效；但随着 Skill 数量增加，多个 Skill 可能同时声称能够处理同一请求，导致：

- Agent 难以稳定选择最合适的 Skill；
- 相似 Skill 被重复读取或重复执行；
- 上下文被大量重叠说明占用；
- 用户需要记住多个近似入口；
- 为了减少数量而进行的宽泛聚合，反而会模糊能力边界。

`skill-router` 解决的不是“如何把所有 Skills 分组”，而是更具体的问题：**哪些 Skills 之间存在真实的发现冲突，以及如何在不损失能力的情况下收敛这些入口。**

| 常见痛点 | `skill-router` 的处理方式 |
| --- | --- |
| 多个 Skill 会响应同一条自然指令 | 比较真实重叠请求，只聚合确有选择竞争的能力 |
| 同领域 Skill 被粗暴合并 | 默认保持独立，只创建边界垂直的 Router |
| Router 把能力固定成主线、辅助或升级流程 | 根据当前任务事实动态采用单个或多个叶子 Skill |
| Router 复制叶子工作流，后续容易失真 | Router 只协调，具体方法仍以叶子 `SKILL.md` 为准 |
| 调整入口可能破坏现有环境 | 执行前汇报计划，获得批准后落地，并保留回滚信息 |

### 它如何工作

1. **盘点**：完整读取整理范围内的 `SKILL.md`，必要时检查其直接依赖。
2. **判断**：用真实用户请求识别发现冲突，而不是根据名称、领域或技术栈直接聚类。
3. **规划**：向用户说明候选 Router、重叠请求、各能力的独特贡献、目录变化和回滚方式。
4. **落地**：用户批准后创建精炼的具体 Router，并保留原 Skill 的完整内容和资源。
5. **验证**：检查路径、依赖、单项调用、多项协同、任务变化和相邻反例。

具体 Router 不替 Agent 规定固定工作流。它只提供完成当前任务所需的协调信息：共享输入与状态、影响能力价值的任务事实、重复控制、授权边界和结果合并。Agent 仍可以根据任务选择一个叶子 Skill、多个 Skill 协同、并行调查或其他合理方式。

### 什么时候适合使用

- 已安装很多 Skills，开始出现相似描述和选择冲突；
- 同一种请求可能触发多个近似 Skill；
- 想减少暴露给 Agent 的入口，但不希望删除或弱化原能力；
- 已有 Router 过于宽泛、模板化，或固化了主辅与调用顺序；
- 需要重新审查 Router 的边界、路径和内部协调方式。

### 它不会做什么

- 不会因为 Skills 属于同一领域、技术栈或生命周期就自动合并；
- 不会把“能够协作”误判为“应该聚合”；
- 不会创建覆盖整个领域的超级 Router；
- 不会复制叶子 Skill 的详细流程；
- 不会在用户批准前移动或改写原 Skill。

### 安装

克隆仓库，并将仓库目录放入你的 Agent 平台能够发现的 Skills 目录。不同平台的目录结构和附加元数据可能不同；核心入口始终是根目录下的 `SKILL.md`。

```bash
git clone https://github.com/youaifuou/skill-router.git
```

### 使用

可以直接提出类似请求：

> 盘点我已经安装的 Skills，找出真正存在发现冲突的能力，提出垂直 Router 方案。先汇报计划，等我批准后再执行。

`skill-router` 会先分析并汇报方案，而不是立即重组目录。只有得到批准后，才会创建具体 Router、验证内部路径，并在目标平台支持时收敛活动入口。

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

`skill-router` is a platform-neutral Agent Skill that inventories installed Skills, identifies highly similar capabilities that genuinely compete for the same user requests, and creates focused vertical Routers when needed. It reduces entry-point conflicts without removing or weakening the original Skills.

### Why it exists

Agents usually select Skills from their names and descriptions. That works well with a small collection, but as the installed list grows, several Skills may claim the same request. This can lead to:

- inconsistent Skill selection;
- duplicate loading or repeated work;
- context consumed by overlapping instructions;
- multiple near-identical entry points users must remember;
- broad aggregation that reduces precision instead of improving it.

`skill-router` is not a general-purpose Skill categorizer. It addresses a narrower question: **which Skills have a genuine discovery conflict, and how can those entry points be consolidated without losing capability?**

| Common pain point | How `skill-router` responds |
| --- | --- |
| Several Skills match the same natural-language request | Compare real overlapping requests and aggregate only true selection competitors |
| Skills are grouped broadly because they share a domain | Keep them independent by default and create only focused vertical Routers |
| A Router forces permanent primary, supporting, or escalation roles | Let current task facts determine whether one or multiple leaf Skills add value |
| A Router copies leaf workflows and gradually drifts out of sync | Keep the Router as a coordination layer and treat each leaf `SKILL.md` as authoritative |
| Reorganizing entry points may disrupt an existing setup | Report the plan first, require approval, and retain migration and rollback information |

### How it works

1. **Inventory**: Read every in-scope `SKILL.md` in full and inspect direct dependencies when needed.
2. **Identify**: Test genuine discovery conflicts with realistic user requests instead of clustering by names, domains, or technology stacks.
3. **Plan**: Report candidate Routers, overlapping requests, unique capability contributions, directory changes, and rollback options.
4. **Build**: After approval, create a concise concrete Router while preserving the complete original Skills and their resources.
5. **Validate**: Check paths, dependencies, single-leaf use, multi-leaf coordination, task changes, and adjacent negative cases.

A concrete Router does not impose a fixed workflow on the Agent. It coordinates only what must be shared across capabilities: inputs and state, task facts that affect capability value, duplicate-work control, authorization boundaries, and result merging. The Agent remains free to use one leaf Skill, combine several Skills, investigate in parallel, or choose another task-appropriate arrangement.

### When to use it

- Your installed Skill collection has grown and descriptions increasingly overlap.
- The same user request can naturally trigger several similar Skills.
- You want fewer exposed entry points without deleting or weakening capabilities.
- An existing Router has become too broad, template-driven, or locked into fixed roles and sequences.
- You need to review a Router's boundary, paths, or internal coordination.

### What it does not do

- It does not merge Skills merely because they share a domain, stack, or lifecycle.
- It does not confuse “can collaborate” with “should be aggregated.”
- It does not create a single mega-Router for an entire domain.
- It does not copy detailed leaf workflows into the Router.
- It does not move or rewrite original Skills before user approval.

### Installation

Clone the repository and place the repository directory where your Agent platform discovers Skills. Platforms may use different directory layouts or additional metadata; the core entry point is always the root `SKILL.md`.

```bash
git clone https://github.com/youaifuou/skill-router.git
```

### Usage

Example request:

> Review my installed Skills, identify capabilities with genuine discovery conflicts, and propose focused vertical Routers. Report the plan first and wait for my approval before applying changes.

`skill-router` analyzes the collection and reports a proposal before reorganizing anything. Only after approval does it create concrete Routers, validate internal paths, and consolidate active entry points where the target platform supports it.

### Validation

The Skill was tested through multiple isolated runs with 12 third-party Skills. A generated debugging Router also passed single-leaf selection, multi-leaf coordination, authorization-boundary, real-fix, and adjacent non-trigger tests.

### Repository structure

```text
skill-router/
├── SKILL.md
└── README.md
```

Platform-specific metadata may be added by users when needed and is not required by the core Skill.
