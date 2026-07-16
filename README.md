<p align="center">
  <img src="assets/planseal-cover.jpg" alt="PlanSeal — Intent in. Execution-ready plan out." width="100%">
</p>

<p align="center">
  PlanSeal turns intent and repository reality into one goal-traced, evidence-grounded plan the next coding agent can execute without guessing—and does not call it `Ready` until the proof closes.
</p>

<p align="center">
  <a href="https://github.com/cablate/planseal/releases/latest"><img src="https://img.shields.io/github/v/release/cablate/planseal?display_name=tag&sort=semver" alt="Latest release"></a>
  <a href="https://github.com/cablate/planseal/stargazers"><img src="https://img.shields.io/github/stars/cablate/planseal?style=social" alt="GitHub stars"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License"></a>
</p>

<p align="center">
  <strong>English</strong> · <a href="README.zh-TW.md">繁體中文</a>
</p>

<p align="center">
  <a href="#quick-start">Quick start</a> ·
  <a href="#what-a-sealed-plan-contains">Output contract</a> ·
  <a href="#core-operating-model">How it works</a> ·
  <a href="#installation">Install</a> ·
  <a href="docs/TRUST.md">Trust &amp; security</a>
</p>

| Goal-traced | Evidence-grounded | Verdict-gated |
|---|---|---|
| Every requirement, package, and check connects to an actor outcome through mandatory GORE. | Requirements, repository facts, decisions, inferences, assumptions, and unknowns stay distinct. | A plan ends as `Ready`, `Needs Revision`, or `Not Executable`—never vague confidence. |

> A plan is not sealed because it is detailed. It is sealed only when its goals, decisions, dependencies, recovery paths, and completion evidence close.

**Works alone.** Spectra, OpenSpec, Baton, subagents, and specific models can help, but none is required.

## Quick start

Install the pinned release from the skill directory used by your agent harness:

```bash
git clone --branch v0.1.0 --depth 1 https://github.com/cablate/planseal.git planseal
```

Then ask for a plan:

```text
Use $planseal to inspect this repository and create an executable plan for
adding organization-scoped API keys. Do not implement code.
```

PlanSeal will select the smallest sufficient profile, ground the current state, trace goals into work packages and evidence, and return one canonical plan with a readiness verdict.

## What a sealed plan contains

```text
Observable outcome + scope + non-goals
└── GORE: actor/job → product intent → goals
    └── requirements + invariants
        └── verified current state → target behavior
            └── dependency-aware work packages
                └── validation + rollback + cleanup
                    └── traceability + readiness verdict
```

The result is an executor-independent implementation contract—not a task dump, a planner transcript, or a second specification system.

## A task list is not an executable plan

Many AI-generated plans look complete while leaving the next executor to invent the important parts:

- the user or operator outcome behind the technical request;
- which repository claims are verified facts and which are guesses;
- the intended behavior, public contract, and preserved invariants;
- dependency order and safe parallel boundaries;
- failure, rollback, migration, cleanup, and handoff behavior;
- what evidence proves the result instead of merely proving that code compiles.

PlanSeal treats a plan as an **executor-independent contract**, not a transcript of planner reasoning. A plan is ready only when material goals, decisions, unknowns, dependencies, and evidence are closed well enough for implementation to begin without inventing major product or architecture decisions.

## What changes

| Without PlanSeal | With PlanSeal |
|---|---|
| Technical activity is mistaken for the goal | Actor outcome and product intent lead the plan |
| Requirements, facts, assumptions, and guesses blur together | Evidence is classified and tied to stable repository anchors |
| A file list stands in for implementation design | Baseline, target behavior, ownership, state, and failure paths are explicit |
| Tasks are ordered by prose or intuition | Work packages form a dependency DAG with integration ownership |
| Unknowns appear halfway through implementation | Material unknowns become decisions, spikes, or preflight gates |
| Build or typecheck is treated as completion | Validation maps commands and observations to claims and outcomes |
| Review produces a second document full of findings | Repairs are integrated into the same canonical plan |
| Every plan is declared ready | The verdict is `Ready`, `Needs Revision`, or `Not Executable` |

## Core operating model

PlanSeal requires seven outcomes while allowing the agent to choose the most efficient evidence path:

1. **Identity and outcome** — observable result, scope, non-goals, invariants, owner, repository snapshot, and freshness.
2. **Mandatory GORE core** — actor and job, product intent, primary and supporting goals, quality guardrails, domain invariants, and goal operationalization.
3. **Grounded current state** — requirements, facts, decisions, inferences, assumptions, and unknowns are separated.
4. **Target behavior and design** — entrypoint, inputs, state, outputs, side effects, failure, recovery, ownership, compatibility, and forbidden shortcuts.
5. **Executable work graph** — independently verifiable work packages, dependency DAG, scope anchors, handoffs, rollback, and `Done When` conditions.
6. **Triggered coverage and release path** — security, data, UI, operations, migration, rollout, cutover, cleanup, and deferred verification only when relevant.
7. **Rechecked canonical plan** — forward and backward traceability passes followed by an honest readiness verdict.

The skill stops gathering evidence when additional retrieval would no longer change sequencing, risk, verification, recovery, or the final verdict.

## GORE is mandatory

PlanSeal uses Goal-Oriented Requirements Engineering as the plan's why, boundary, and traceability layer. Every profile preserves this chain:

```text
actor / job
  → product intent
  → primary and supporting goals
  → requirement or invariant
  → work package
  → outcome evidence
```

GORE is not a second specification and is not an excuse for ceremonial diagrams. A focused bug fix may express the entire chain in one compact row. A migration or multi-owner change expands only the real goal hierarchy, conflicts, continuity requirements, and decision ownership.

## Four plan profiles

| Profile | Use for | Required depth |
|---|---|---|
| **Focused** | Isolated bug, small behavior correction, local configuration change | Compact GORE chain, verified baseline and target, focused package, regression evidence, rollback |
| **Standard** | Feature, cross-file refactor, API or UI flow change | Full GORE core, behavior contract, DAG, triggered coverage, integration and cleanup |
| **Migration** | Framework, platform, schema, storage, API version, or data-model migration | Continuity, transition, cutover, compatibility, data movement, rollback, and cleanup gates |
| **Master** | Multiple owners, surfaces, workspaces, releases, or centralized integration | Expanded goals, ownership and conflict maps, parallel and serial tracks, integration governance |

Profile controls depth, not whether goals, evidence, or readiness matter.

## Readiness verdicts

| Verdict | Meaning |
|---|---|
| `Ready` | Material goals, decisions, and unknowns are closed; goal → requirement → package → evidence is complete; implementation can begin |
| `Needs Revision` | A resolution path exists, but its result may still change target behavior, architecture, DAG, migration, release, or acceptance |
| `Not Executable` | Required input, authority, ownership, or safety boundaries are missing and no reliable resolution path can start |

A runnable discovery task does not make the whole plan ready if its result can still overturn the design.

## Independent by design

PlanSeal does not require:

- Spectra, OpenSpec, or another specification framework;
- a particular model, agent runtime, IDE, or orchestration system;
- subagents or parallel execution;
- repository write access during planning.

External artifacts and specialist skills may provide evidence, but the final deliverable remains one self-contained canonical plan.

PlanSeal complements [Baton](https://github.com/cablate/baton): PlanSeal defines work that is ready to execute; Baton decides whether and how that work should be delegated. Neither is required by the other.

## GPT-5.6 alignment

PlanSeal is model-agnostic, but its structure is especially compatible with the [OpenAI GPT-5.6 prompt guidance](https://developers.openai.com/api/docs/guides/prompt-guidance-gpt-5p6): state the outcome, important constraints, available evidence, and completion bar, then allow the model to choose the efficient path. PlanSeal turns those inputs into a durable implementation contract instead of a one-session prompt.

This is a design alignment claim, not an OpenAI endorsement or a claim that one model is required.

## Installation

### Approval-gated agent install

Ask your agent to inspect the versioned runbook, show an exact plan, and wait before writing:

```text
Read https://raw.githubusercontent.com/cablate/planseal/v0.1.0/install/AGENT-INSTALL.md
and prepare a plan to install PlanSeal as $planseal.

Inspect my current skill directories first. Do not overwrite existing files.
Show the source, destination, changed files, non-changes, and verification steps.
Wait for my approval before writing anything.
```

Review the [installation manifest](install/MANIFEST.md) and [trust boundary](docs/TRUST.md) before installation.

### Manual install

Clone the tagged release into the skill directory used by your agent harness:

```bash
git clone --branch v0.1.0 --depth 1 https://github.com/cablate/planseal.git planseal
```

Place or link the cloned folder where your product discovers `SKILL.md` packages. Discovery paths vary by product, so follow the current documentation for your harness. If skill discovery is cached, start a fresh session and run the [smoke tests](install/SMOKE-TESTS.md).

The runtime entrypoint is [SKILL.md](SKILL.md). README, release, and installation documents are human-facing and are not required in normal model context.

## More ways to use it

Review and repair an existing plan:

```text
Use $planseal to review this migration plan. Integrate every material repair
into one canonical plan and return its readiness verdict.
```

Preflight before execution:

```text
Use $planseal to preflight this plan against the current repository. Repair
relevant drift and identify the first executable work package.
```

## Repository structure

```text
.
├── SKILL.md
├── VERSION
├── assets/
│   ├── planseal-cover.jpg
│   └── planseal-cover.zh-TW.jpg
├── agents/
│   └── openai.yaml
├── references/
│   ├── plan-profiles.md
│   ├── gore-spec-plan.md
│   ├── evidence-and-freshness.md
│   ├── execution-readiness.md
│   ├── architecture-coverage.md
│   ├── large-change-planning.md
│   ├── migration-strategies.md
│   ├── executable-plan-template.md
│   └── planning-failure-modes.md
├── install/
└── docs/
```

The runtime instructions are currently authored in Traditional Chinese. Multilingual agents should follow them and answer in the user's language. The English README documents the same public contract without adding a second planning standard.

## Design principles

- **Plan outcomes, not activity.**
- **Every plan keeps a real GORE chain.**
- **Evidence must be sufficient, fresh, and honestly classified.**
- **One canonical plan; external artifacts are inputs, not competing truth.**
- **Unknowns become decisions, spikes, or gates before implementation depends on them.**
- **Work packages are cut by outcome, dependency, ownership, rollback, and verification—not file count.**
- **Completion proves actor outcomes and invariants, not only build artifacts.**
- **A plan may be useful without being ready; the verdict must say so.**

## License

MIT © 2026 CabLate. See [LICENSE](LICENSE).
