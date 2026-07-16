# Mandatory GORE Core

在每個 Focused、Standard、Migration 與 Master plan 中使用 GORE。GORE 是主計畫內的 why、boundary 與 traceability 層，不是第二份規格書。Profile 只控制展開深度；不得省略 core。

## 必要 Goal Model

| Layer | 每份計畫必須回答 | 合格表達 |
|---|---|---|
| Actor and job | 誰需要完成什麼工作或承受什麼系統結果 | 具體 actor／consumer 與 job，不用「系統」代替真正受影響者 |
| Product intent | 為何值得改變、為何現在做 | 使用者、業務或營運 outcome；若來源未提供，標記 Unknown，不自行創造願景 |
| Primary goal | 完成後最重要的可觀察狀態 | 一個穩定結果，不是「實作／重構／遷移 X」 |
| Supporting／enabling goal | 哪些子結果或技術能力共同使 primary goal 成立 | 至少一個有 contribution 的 goal；有 dependency 時才展開 hierarchy |
| Soft goal／quality guardrail | 信任、清楚、速度、成本、相容性、可維護性等如何約束方案 | 可觀察品質、budget、acceptance example 或 design rule |
| Domain invariant and non-goal | 哪些規則不得繞過、哪些相鄰成果不在本計畫 | 明確邊界、反例或重新納入條件 |
| Operationalization | goal 如何成為 requirement、work package 與 evidence | 可搜尋的 Goal ID 與 traceability |

## 依 Profile 渲染

### Focused

用一張 compact GORE chain 即可；每個欄位都要有具體內容：

| Actor／job | Product intent／why now | Primary goal | Supporting／enabling goal | Quality guardrail | Invariant／non-goal | Requirement → WP → evidence |
|---|---|---|---|---|---|---|

不要為小型工作建立空的多層 hierarchy 或 conflict table。Compact 不等於省略；goal 不可只藏在 outcome 標題或 work-package contribution 中。

### Standard

分開呈現 actors、primary／supporting goals、quality guardrails、invariants／non-goals 與 final traceability。只有存在實際取捨時才加入 conflict table。

### Migration

在 Standard core 之外加入：

- continuity goal：遷移期間 actor 哪些能力必須持續成立；
- transition goal：新舊 owner、資料或流量要達到什麼可觀察狀態；
- cutover goal：哪些 evidence 成立才能切換；
- cleanup goal：哪些 transitional artifact 被刪除才算完成。

### Master

展開多 actor、多層 goal hierarchy、soft-goal conflicts、decision owners 與跨 release operationalization。只展開真實存在的分支與衝突，不用組織層級填滿模型。

## 展開格式

需要分表時使用下列最小結構。

### Actors and jobs

| Actor | Job／outcome | Current pain／risk | 不應被迫承擔 |
|---|---|---|---|

### Goal hierarchy

| Goal ID | Type | Goal | Actor | Parent／depends on | Observable outcome | Priority |
|---|---|---|---|---|---|---|

### Soft goals and conflicts

| Goal／conflict | Options | Decision／owner | Observable guardrail |
|---|---|---|---|

沒有 material conflict 時保留 quality guardrail，不建立空的 conflict table。

### Invariants and non-goals

| ID | Invariant／non-goal | Why | Evidence／revisit trigger |
|---|---|---|---|

### Goal operationalization

| Goal ID | Requirement／invariant | Work package | Outcome evidence | Status |
|---|---|---|---|---|

## Rules

- 從使用者意圖、核准需求、權威規格與目前系統證據建立 goal；不要從現有檔案、legacy 功能或偏好架構反推「一定需要」的產品目標。
- 將缺少且會改變 primary goal 或 material conflict 的意圖標為 Unknown，並詢問最小必要問題；不要用通用產品口號補洞。
- 讓每個技術 enabling work 指向 Goal ID，說明不做會阻塞哪個 outcome。
- 把 soft goal 轉成 budget、acceptance example、design rule 或 observable evidence，不只寫「高效、穩定、易維護」。
- 為會改變 public behavior、資料安全或 release strategy 的 goal conflict 指派 decision owner；未決取捨不可藏進 implementation step。
- 讓每個 primary／supporting goal 至少連到一個 requirement／invariant、work package 與 evidence；讓每個 work package 至少連回一個 Goal ID。
- 用 final Done When 證明 actor outcome、quality guardrail 與 invariant，不只證明 build、檔案或 migration artifact 存在。
- 在 scope 或需求改變後同步修正 GORE 與所有 downstream traceability；不得保留與主計畫矛盾的舊 goal。

## Readiness Gate

以下任一成立時，任何 profile 都不得標 Ready：

- primary goal 只是把技術任務換句話說，或沒有可觀察 outcome；
- actor、product intent 或 material goal 仍靠未標示的猜測；
- supporting／enabling goal 無 requirement、package 或 evidence；
- quality guardrail 無法觀察，或 domain invariant 只存在於舊 code 的隱含行為；
- package 引入無法追溯到 goal、constraint 或 intentional change 的行為；
- goal conflict 會改變 public behavior、資料安全或 release strategy，但尚未決定；
- final Done When 無法證明 actor outcome、guardrail 與 invariant。
