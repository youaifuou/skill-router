# Skill Router

[English](README.md) · [中文版](README_ZH.md)

`skill-router` is a platform-neutral Agent Skill that inventories installed Skills, identifies highly similar capabilities that genuinely compete for the same user requests, and creates focused vertical Routers when needed. It reduces entry-point conflicts while preserving the complete capabilities of every original Skill.

## Highlights

`skill-router` does more than place similar Skills behind one entry point. It turns capabilities with genuine discovery conflicts into an adaptive capability cluster. Based on the current task, the Agent may use one leaf Skill, combine several Skills, investigate different directions in parallel, and merge their results through shared context.

- **Precise aggregation**: Consolidate only Skills that compete for the same real request, avoiding broad groupings that reduce selection accuracy.
- **Adaptive composition**: Do not impose permanent primary/supporting roles, fixed sequences, or predefined bundles; let task facts determine single, combined, or parallel use.
- **Shared state**: Reuse the same inputs, evidence, and progress across participating Skills to reduce duplicate reading and investigation.
- **Unified results**: Coordinate findings, disagreements, and actions into one coherent response.
- **Capability preservation**: Keep every original Skill and its resources intact; the Router does not copy, weaken, or override leaf methods.
- **Safe rollout**: Report the plan and wait for approval before changing entry points, while retaining paths and rollback information.

## Why it exists

Agents usually select Skills from their names and descriptions. That works well with a small collection, but as the installed list grows, several Skills may claim the same request. This can lead to:

- inconsistent Skill selection;
- duplicate loading or repeated work;
- context consumed by overlapping instructions;
- multiple near-identical entry points users must remember;
- broad aggregation that reduces precision instead of improving it.

`skill-router` is not a general-purpose Skill categorizer. It addresses a narrower question: **which Skills have a genuine discovery conflict, and how can those entry points be consolidated while enabling useful composition without losing capability?**

| Common pain point | How `skill-router` responds |
| --- | --- |
| Several Skills match the same natural-language request | Compare real overlapping requests and aggregate only true selection competitors |
| A task benefits from several similar capabilities, but users do not know how to combine them | Let task facts drive single- or multi-Skill use, with shared state and merged results |
| Skills are grouped broadly because they share a domain | Keep them independent by default and create only focused vertical Routers |
| A Router forces permanent primary, supporting, or escalation roles | Let current task facts determine whether one or multiple leaf Skills add value |
| A Router copies leaf workflows and gradually drifts out of sync | Keep the Router as a coordination layer and treat each leaf `SKILL.md` as authoritative |
| Reorganizing entry points may disrupt an existing setup | Report the plan first, require approval, and retain migration and rollback information |

## How it works

1. **Inventory**: Read every in-scope `SKILL.md` in full and inspect direct dependencies when needed.
2. **Identify**: Test genuine discovery conflicts with realistic user requests instead of clustering by names, domains, or technology stacks.
3. **Plan**: Report candidate Routers, overlapping requests, unique capability contributions, directory changes, and rollback options.
4. **Build**: After approval, create a concise concrete Router while preserving the complete original Skills and their resources.
5. **Validate**: Check paths, dependencies, single-leaf use, multi-leaf coordination, task changes, and adjacent negative cases.

A concrete Router does not impose a fixed workflow. It coordinates only what must be shared across capabilities: inputs and state, task facts that affect capability value, duplicate-work control, authorization boundaries, and result merging. The Agent can use one leaf Skill, combine several sequentially, investigate in parallel, or adopt another task-appropriate arrangement, reducing selection cost, duplicate work, and context waste.

## When to use it

- Your installed Skill collection has grown and descriptions increasingly overlap.
- The same user request can naturally trigger several similar Skills.
- You want fewer exposed entry points without deleting or weakening capabilities.
- You want related capabilities to work together without hard-coding one composition pattern.
- An existing Router has become too broad, template-driven, or locked into fixed roles and sequences.
- You need to review a Router's boundary, paths, or internal coordination.

## What it does not do

- It does not merge Skills merely because they share a domain, stack, or lifecycle.
- It does not confuse “can collaborate” with “should be aggregated.”
- It does not create a single mega-Router for an entire domain.
- It does not copy detailed leaf workflows into the Router.
- It does not force one permanent Skill-combination pattern.
- It does not move or rewrite original Skills before user approval.

## Installation

Clone the repository and place the repository directory where your Agent platform discovers Skills. Platforms may use different directory layouts or additional metadata; the core entry point is always the root `SKILL.md`.

```bash
git clone https://github.com/youaifuou/skill-router.git
```

## Usage

Example request:

> Review my installed Skills, identify capabilities with genuine discovery conflicts, and propose focused vertical Routers. Report the plan first and wait for my approval before applying changes.

`skill-router` analyzes the collection and reports a proposal before reorganizing anything. Only after approval does it create concrete Routers, validate internal paths, and consolidate active entry points where the target platform supports it.

## Validation

The Skill was tested through multiple isolated runs with 12 third-party Skills. A generated debugging Router also passed single-leaf selection, multi-leaf coordination, authorization-boundary, real-fix, and adjacent non-trigger tests.

## Repository structure

```text
skill-router/
├── LICENSE
├── SKILL.md
├── README.md
└── README_ZH.md
```

Platform-specific metadata may be added by users when needed and is not required by the core Skill.

## License

Released under the [MIT License](LICENSE). Copyright (c) 2026 youaifuou.
