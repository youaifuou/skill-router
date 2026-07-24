# Skill Router

[English](README.md) · [中文版](README_ZH.md)

> Turn overlapping Agent Skills into focused, adaptive entry points without merging or weakening them.

`skill-router` audits installed Agent Skills, finds highly similar Skills that compete for the same user requests, and proposes focused Routers. After user approval, each Router becomes a clearer entry point that can select one leaf Skill or coordinate several according to the task.

## The problem

Skill discovery works well when an Agent has only a few clearly separated Skills. As the collection grows, several problems appear:

- multiple Skills may respond to the same natural-language request;
- the Agent may select inconsistently or load overlapping instructions;
- similar Skills may repeat reading, investigation, or validation work;
- broad “mega-Routers” may reduce the number of entries while making capability boundaries less precise.

`skill-router` addresses a specific problem: **discovery conflict**. A discovery conflict exists when the same realistic request could reasonably trigger multiple Skills that pursue the same concrete outcome.

Sharing a domain, technology stack, or lifecycle is not enough. Skills that solve different subgoals can collaborate without being placed behind the same Router.

## What it does

1. **Audit** — Read the installed `SKILL.md` files and understand their triggers, outputs, distinct capabilities, constraints, and dependencies.
2. **Compare** — Test realistic requests to distinguish genuine selection conflicts from loose topical similarity.
3. **Propose** — Present focused Router candidates, included and excluded Skills, directory changes, and rollback options.
4. **Build after approval** — Create concrete Routers while preserving the complete leaf Skills and their resources.
5. **Validate** — Test single-Skill use, multi-Skill coordination, changing task conditions, and adjacent requests that should remain outside the Router.

No active Skill entry point is moved, hidden, or replaced before the user approves the plan.

## Adaptive coordination

A generated Router does not prescribe one permanent workflow. It explains:

- the narrow user intent shared by its leaf Skills;
- the distinct capability each leaf contributes;
- the task information that affects which capabilities are useful;
- what context, evidence, and artifacts should be shared;
- how to avoid duplicate work and combine results.

The Agent then decides what the current task requires:

| Task situation | Possible behavior |
| --- | --- |
| One capability is sufficient | Use one leaf Skill |
| Several capabilities add value | Coordinate the relevant subset |
| Work is independent | Proceed in parallel when useful |
| One result depends on another | Coordinate in the required order |
| The request falls outside the Router boundary | Use an independent Skill instead |

These are possible responses to task structure, not fixed routing modes. The Router does not assign permanent primary, supporting, escalation, or fallback roles.

## Example

Suppose several debugging Skills could all respond to:

> Diagnose and fix this intermittent test failure.

`skill-router` first checks whether they genuinely solve the same concrete goal. If they do, it can create a focused debugging Router that:

- preserves each Skill’s distinct investigation method;
- uses only one capability when it is enough;
- combines reproduction, root-cause analysis, and verification when they all contribute;
- shares evidence and intermediate findings across the selected Skills;
- merges their conclusions into one coherent result.

A nearby Skill for test planning would remain independent if it solves a different goal. The Router is therefore vertical and specific, not a general “software development” entry point.

## When to use it

Use `skill-router` when:

- the installed Skill list has become difficult to navigate;
- several Skills naturally match the same request;
- you want fewer exposed entry points without deleting capabilities;
- related Skills should cooperate without a hard-coded combination;
- an existing Router is too broad, generic, or locked into fixed roles.

Do not use it merely to categorize Skills by topic or place an entire domain behind one Router.

## Installation

Install with the Skills CLI:

```bash
npx skills add youaifuou/skill-router --skill skill-router
```

You can also view the listing on [skills.sh](https://www.skills.sh/youaifuou/skill-router/skill-router).

For manual installation, clone this repository and copy `skills/skill-router` into a Skill directory supported by your Agent platform.

## Usage

Ask your Agent to use `skill-router`, for example:

> Audit my installed Skills. Identify genuine discovery conflicts and propose focused Routers. Explain what each Router would include, what should remain independent, and how the entry points would change. Wait for my approval before applying anything.

The Skill reports its plan first. After approval, it creates and validates the concrete Routers and applies only the agreed entry-point changes.

## Design principles

- Keep Skills independent by default.
- Aggregate the smallest group that resolves a real conflict.
- Derive every capability description from the source `SKILL.md`.
- Keep detailed methods and constraints in the leaf Skills.
- Let task facts determine single, combined, parallel, or dependent use.
- Preserve original directories, resources, and rollback information.

## Validation

The Skill has been exercised through multiple isolated runs using third-party Skills. Generated Routers were tested against single-leaf requests, multi-leaf coordination, authorization boundaries, real task execution, and adjacent non-trigger cases.

## Repository structure

```text
skill-router/
├── LICENSE
├── README.md
├── README_ZH.md
└── skills/
    └── skill-router/
        └── SKILL.md
```

`skills/skill-router` is the canonical installable Skill package.

## License

Released under the [MIT License](LICENSE). Copyright (c) 2026 youaifuou.
