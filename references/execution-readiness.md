# Execution Readiness

本文件定義 work package、DAG、驗證與 verdict 的品質。核心問題是：新的執行者是否能在不發明重大需求或設計的前提下，從第一個 package 開始並逐步證明完成？

## 目錄

- [Work Package Contract](#work-package-contract)
- [切包原則](#切包原則)
- [Dependency DAG](#dependency-dag)
- [Unknown 與 Spike](#unknown-與-spike)
- [Verification Design](#verification-design)
- [Deferred Verification](#deferred-verification)
- [Self-Review and Repair](#self-review-and-repair)
- [Verdict Rubric](#verdict-rubric)

## Work Package Contract

Standard、Migration 與 Master 的每個 package 應包含：

| Field | 必須回答 |
|---|---|
| ID / outcome | 完成後哪個可觀察狀態成立 |
| Contribution | 支援哪個 Goal ID，以及哪個 requirement／invariant；純技術 enabling work 也必須指出所服務的 goal |
| Dependencies | 開始前需要哪些 package、decision、artifact 或環境 |
| Parallel / owner | 是否可平行；誰負責整合與衝突面 |
| Scope anchors | 哪些 path、symbol、route、schema、consumer 或新 owner 會動 |
| Non-changes | 哪些相鄰行為或 owner 明確不得改 |
| Steps | 以決策與行為為中心的實作順序 |
| Constraints | public contract、compatibility、data、failure、security 或 pattern 邊界 |
| Verification | 要跑什麼、觀察什麼、證明哪個 claim |
| Failure / recovery | package 失敗、部分完成或回歸時如何處理 |
| Done When | 可由他人判定的完成條件 |
| Handoff | 產出什麼給下游 package，仍有哪些 deferred item |

定位點未知時，將 discovery 寫成先行步驟與 exit criteria；不要虛構檔案。

Focused 的 compact subset：

| Field | 必須回答 |
|---|---|
| Outcome / contribution | 完成後哪個 Goal ID、requirement／invariant 與可觀察狀態成立 |
| Scope anchors | 哪些 path、symbol、contract 或測試會動；哪些相鄰行為不動 |
| Steps | 可直接依序執行的改動 |
| Verification / Done When | 如何證明 target 與 regression safety |
| Failure / rollback | 失敗如何停下、修復或回退 |

只有真的存在多 owner、dependency、parallel work、integration point 或 downstream consumer 時，Focused 才加入相應 coordination／handoff 欄位。

## 切包原則

以 coherent, reviewable, verifiable outcome 切包。好的 package：

- 有單一主要成果與清楚 owner；
- 可在 dependency 就緒後獨立開始；
- 驗證失敗時能定位回此 package；
- 不把未決產品或 public contract 決策塞進 implementation；
- 合併後能留下穩定的下游 input。

需要拆分的訊號：

- 同時擁有互不相干的 outcome；
- 需要不同 decision owner；
- schema、service、UI、deploy 彼此不能獨立驗收；
- 一半可安全平行，另一半必須碰 serial integration point；
- rollback 邊界不同；
- package 內仍有會推翻整體方向的 spike。

檔案數、文字長度與 agent 數只能提示風險，不能作硬門檻。

## Dependency DAG

建立一張表：

| ID | Depends on | Produces | Parallel with | Serial integration point |
|---|---|---|---|---|

檢查：

1. 無循環 dependency。
2. 每個 dependency 指向具體 artifact、contract、decision 或環境狀態。
3. 每個 root package 都有足夠 input。
4. 每個 leaf package 都連到 integration、release、cleanup 或 final evidence。
5. 共享 router、registry、migration、global config、lockfile 或 public API 有單一 serial owner。
6. Parallel 不代表同時寫相同檔案或相同 source of truth。
7. 每個 package 至少連回一個 Goal ID；每個 primary／supporting goal 都連到 requirement／invariant、package 與 outcome evidence。

## Unknown 與 Spike

將未知分為：

| 類型 | 處理 |
|---|---|
| Material decision | 詢問最小必要問題；未決前整份 plan 不得 Ready |
| Technical feasibility | 建 timeboxed spike；結論可能改變設計時 verdict 為 Needs Revision |
| Freshness / environment | 建 preflight gate；若會改變 DAG／migration／release，verdict 為 Needs Revision |
| Reversible detail | 記錄 Assumption 與 recheck point |

一個合格 spike 要寫：

- hypothesis；
- 最小實驗與 timebox；
- 成功／失敗判準；
- 輸出 artifact 或 evidence；
- 被阻塞 package；
- 成功分支與 fallback 分支；
- 誰把結論修回主計畫。

Spike 的完成不是「研究過」，而是得到可採用的決策與證據。

## Verification Design

每項驗證要連回 claim：

| Layer | 證明內容 | 例子 |
|---|---|---|
| Static / structural | syntax、type、schema、forbidden dependency、owner 邊界 | typecheck、lint、architecture rule、schema diff |
| Unit / component | 局部規則與 edge case | focused tests、property cases、component states |
| Integration / contract | consumer、資料、API、外部邊界協作 | contract test、integration fixture、migration rehearsal |
| Behavior / runtime | actor 可觀察 outcome 與 failure recovery | e2e、CLI run、browser／device QA、runtime probe |
| Operational | deploy、telemetry、rollback、support | canary、dashboard、log query、rollback rehearsal |

不要只列命令。寫清楚命令或觀察會證明哪個 requirement／invariant，失敗時回到哪個 owner。

## Deferred Verification

只有在 package 內執行成本不合理、需要整合環境或依賴其他 package 時才能延後。每筆記錄：

| ID | Deferred check | Reason | Owner / when | Command／evidence | Blocks | Failure returns to |
|---|---|---|---|---|---|---|

規則：

- 低成本且能提早阻止錯誤的驗證不要延後。
- Deferred 不等於 optional。
- 阻塞 release、migration cutover 或 legacy deletion 的項目要明標。
- Integration owner 必須能把失敗追到原 package。

## Self-Review and Repair

由兩個方向重驗：

### Forward pass

從 root package 依 DAG 走到 release，確認每個 input 會先產生、每個 gate 有 owner。

### Backward pass

從 final actor outcome、GORE goals、quality guardrails 與 invariants 反查 evidence、package 與 requirement，確認沒有孤兒 goal、孤兒 package 或無證據目標。

修復後重驗：

- 被修改 package；
- 所有直接與間接 downstream package；
- traceability、rollout、rollback、cleanup 與 verdict。

## Verdict Rubric

| 類型 | 定義 | 對 verdict 的影響 |
|---|---|---|
| Blocker | 會迫使實作者猜重大行為、碰不可接受風險或根本無法開始 | 有可靠 resolution package 時 Needs Revision；連 resolution 都不能安全開始時 Not Executable |
| Execution risk | 可開始但高機率返工、漏驗或整合失敗 | Needs Revision，除非已修復 |
| Note | 不影響可靠執行的資訊或優化 | 不阻止 Ready |

Ready 的判斷對象是整份 canonical plan，不是某幾個 package「看起來可以」。First executable package 若只是 discovery、spike 或 material decision gate，代表計畫有進展路徑，不代表 plan Ready。

同時套用 [gore-spec-plan.md](gore-spec-plan.md) 的 Readiness Gate。任何無法 operationalize 的 primary／supporting goal，或無法追溯到 Goal ID 的 work package，至少構成 Execution risk；若會迫使實作者發明產品行為、取捨或完成證據，視為 Blocker。
