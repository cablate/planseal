# Executable Plan Template

此模板是 Standard、Migration 與 Master 的唯一 canonical plan。Conditional 區段只在觸發時展開。Focused plan 改用 [plan-profiles.md](plan-profiles.md) 的 compact skeleton。

不要為了填滿模板重複同一事實。某段若不改變 implementation、sequencing、risk、handoff 或 evidence，合併或省略。

## 目錄

- [Plan Identity](#plan-identity)
- [Outcome and Scope](#outcome-and-scope)
- [GORE Core](#gore-core)
- [Requirements and Invariants](#requirements-and-invariants)
- [Verified Current State](#verified-current-state)
- [Target Behavior and Design](#target-behavior-and-design)
- [Decisions and Unknowns](#decisions-and-unknowns)
- [Work Package DAG](#work-package-dag)
- [Work Package Details](#work-package-details)
- [Conditional Coverage](#conditional-coverage)
- [Integration, Rollout, and Cleanup](#integration-rollout-and-cleanup)
- [Validation and Deferred Verification](#validation-and-deferred-verification)
- [Traceability](#traceability)
- [Readiness Verdict](#readiness-verdict)

# Plan: [Outcome-oriented title]

## Plan Identity

| Field | Value |
|---|---|
| Lifecycle | Draft／Active／Complete／Superseded |
| Profile | Focused／Standard／Migration／Master |
| Owner | |
| Repository／scope | |
| Branch／base commit | |
| Created | |
| Last verified | |
| Inputs | |
| Known relevant drift | None／details |

Lifecycle 描述文件所處階段，不表示 execution readiness。Readiness 只由文末的 Verdict 宣告。

## Outcome and Scope

### Outcome

[描述 actor 完成後可觀察到的結果，不只寫技術動作。]

### Success evidence

- [最終 outcome evidence]

### In scope

- [scope item]

### Out of scope / non-goals

- NG-01：

### Constraints

- [constraint]

## GORE Core

### Actors and intent

| Actor／consumer | Job／outcome | Product intent／why now | Source／evidence |
|---|---|---|---|
| | | | |

### Goal model

| Goal ID | Type | Goal | Actor | Parent／depends on | Observable outcome | Quality guardrail | Boundary IDs |
|---|---|---|---|---|---|---|---|
| G-01 | Primary | | | | | | I-01／NG-01 |
| G-02 | Supporting／enabling | | | G-01 | | | |

至少保留一個 primary goal 與一個 supporting／enabling goal。Migration 加入 continuity、transition、cutover 與 cleanup goals；Master 依真實 dependency 展開 hierarchy。

### Material goal conflicts

| Conflict | Options | Decision／owner | Observable guardrail |
|---|---|---|---|

只有存在會改變 public behavior、資料安全、成本、相容性或 release strategy 的實際取捨時才保留此表；不要建立空 conflict table。

## Requirements and Invariants

| ID | Type | Requirement／invariant | Source | Priority | Outcome evidence |
|---|---|---|---|---|---|
| R-01 | Requirement | | | | |
| I-01 | Invariant | | | | |

## Verified Current State

| ID | Type | Claim | Evidence／stable anchor | Verified at | Planning impact |
|---|---|---|---|---|---|
| F-01 | Fact | | path + symbol／contract／test | commit／time | |

### Current flow / ownership

[用精簡 sequence、tree 或 owner table描述會影響計畫的現況。]

### Relevant gaps

| Gap | Evidence | Requirement affected | Consequence if unchanged |
|---|---|---|---|

## Target Behavior and Design

### Behavior contract

| Surface／entrypoint | Baseline | Target | Inputs／state | Outputs／side effects | Error／recovery | Evidence |
|---|---|---|---|---|---|---|

### Intentional changes and preserved behavior

| Item | Preserve／change | Reason | Consumer impact |
|---|---|---|---|

### Target ownership / contracts

| Capability／artifact | Target owner | Responsibility | Public contract | Forbidden responsibility |
|---|---|---|---|---|

### Conditional maps

[需要時加入 state map、data map、failure map、permission matrix 或 source-to-target migration map。]

## Decisions and Unknowns

### Decisions

| ID | Decision | Options considered | Reason | Consequence |
|---|---|---|---|---|

### Assumptions

| ID | Assumption | Why safe／reversible | Recheck point | If wrong |
|---|---|---|---|---|

### Unknowns / spikes

| ID | Question／hypothesis | Resolution owner／method | Blocks | Success／fallback | Plan update point |
|---|---|---|---|---|---|

## Work Package DAG

| ID | Outcome | Depends on | Produces | Parallel with | Serial owner／integration point |
|---|---|---|---|---|---|

[用簡短箭頭或 Mermaid 補充複雜 dependency；表格仍是可搜尋的 source of truth。]

## Work Package Details

### WP-[ID]: [Outcome]

**Contribution**

- Goal IDs（必要）：
- Requirements／invariants：

**Dependencies and coordination**

- Depends on：
- Parallel／serial：
- Integration owner：

**Scope**

- Change anchors：
- Create anchors：
- Do not touch／non-changes：
- Existing owners to reuse：

**Implementation**

1. [implementation step]
2. [implementation step]

**Design and behavior constraints**

- Public contract：
- Data／state／side effects：
- Failure／recovery：
- Forbidden shortcuts：

**Verification**

| Check | Method／command | Proves | Failure returns to |
|---|---|---|---|

**Rollback / recovery**

- [rollback／recovery action]

**Done When**

- [可由他人觀察與判定的條件]

**Handoff / deferred**

- Produces：
- Deferred checks：
- Downstream notes：

[為每個 package 重複本區塊。]

## Conditional Coverage

| Concern | Trigger | Status | Work package／reason | Verification |
|---|---|---|---|---|

只列被觸發或需要明確 Not applicable 的 concern。

## Integration, Rollout, and Cleanup

### Integration sequence

1. [integration step]

### Rollout / cutover

| Stage／cohort | Entry criteria | Action | Guardrail | Abort／rollback |
|---|---|---|---|---|

### Cleanup

| Transitional item | Exit criteria | Owner | Deletion evidence | Blocks final Done |
|---|---|---|---|---|

若 Focused profile 沒有 rollout 或 transitional item，說明直接交付與 rollback 邊界即可。

## Validation and Deferred Verification

### Final validation

| Layer | Check | Proves requirement／invariant | Required evidence |
|---|---|---|---|

### Deferred verification ledger

| ID | Check | Reason deferred | Owner／when | Blocks | Failure repair owner |
|---|---|---|---|---|---|

沒有 deferred item 時明寫 None。

## Traceability

| Goal ID | Requirement／invariant | Work package | Verification／outcome evidence | Status |
|---|---|---|---|---|

## Readiness Verdict

### Verdict: Ready／Needs Revision／Not Executable

**Blockers**

- None／details

**Execution risks**

- None／details

**First executable package**

- WP-[ID]，因為其 dependencies 已滿足：[evidence]

**Preflight before execution**

- [需重驗的 freshness、environment、permission 或 migration state]

**Verdict rationale**

[用可觀察缺口與 readiness 規則說明；不要使用沒有母體的分數。]

若 first executable package 的主要產出是關閉會改變 target design、DAG、migration、資料安全或 release strategy 的 Unknown，Verdict 應為 Needs Revision，而不是 Ready。
