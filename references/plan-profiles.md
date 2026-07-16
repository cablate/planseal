# Plan Profiles

用最小充分 profile 控制計畫深度。Profile 決定需要展開的推理，不決定固定篇幅、phase 數、檔案數，也不決定是否使用 GORE。每個 profile 都必須保留 GORE core；只調整 goal hierarchy、conflict、ownership 與 traceability 的渲染深度。

每個區段都必須改變執行決策、dependency、風險、handoff 或 evidence；否則合併或省略。計畫的停止條件是「新執行者已不需猜重大事項」，不是「所有模板欄位都填滿」。

## 選擇順序

1. 先判斷是否有 migration、長期共存、cutover 或不可逆資料變更；有則選 Migration。
2. 再判斷是否跨多個 owner、團隊、worktree 或 release，且需要集中整合；有則選 Master。
3. 再判斷是否改變多個 consumer、public contract、資料流或架構邊界；有則選 Standard。
4. 其餘使用 Focused。

若同時符合 Migration 與 Master，使用 Master 作主體，並套用 Migration gates。

## Profile Contract

| Profile | 典型訊號 | 必要展開 | 通常可省略 |
|---|---|---|---|
| Focused | 單一 bug、小型行為修正、局部設定變更 | compact GORE chain（含 product intent）、baseline／target behavior、scope、repo facts、單一或少量 work package、回歸驗證、rollback | 展開式 goal hierarchy／conflict matrix、完整 owner map、多軌整合 |
| Standard | 一般 feature、跨檔 refactor、API 或 UI flow 變更 | GORE core、requirements／invariants、target design、behavior contract、DAG、條件式 coverage、integration 與 cleanup | 無實際取捨的組織級 goal 分解、worktree topology |
| Migration | framework、platform、schema、storage、API version 或資料模型遷移 | GORE core、continuity／transition goals、source／target、共存策略、compatibility、data movement、cutover、rollback、cleanup、migration evidence | 與遷移無關的全域架構盤點 |
| Master | 跨多個 owner／surface／release 的大型計畫 | 展開式 GORE、ownership、parallel／serial tracks、integration stabilization、deferred verification、rollout governance | 無觸發的逐項 checklist |

## 升級 Profile 的風險訊號

出現下列任一情況時，考慮升級：

- 多個獨立 consumer 依賴同一 public contract；
- schema、權限、計費或資料保留規則會改變；
- 新舊系統必須共存；
- package 需要跨 release 或跨環境；
- 多個實作者可能碰同一 registry、router、migration、global config 或 shared API；
- 驗證成本高，必須延後到整合階段；
- 技術工作服務多個產品 goal，且取捨需要可追溯。

不要只因檔案多就升級；檔案數是觀察值，不是複雜度定義。

## Focused Profile 最小骨架

    Outcome
    Compact GORE: actor/job → product intent → primary goal → supporting/enabling goal → requirement/invariant → package → evidence
    Relevant soft goal / quality guardrail and non-goal boundary
    Scope / non-goals
    Verified baseline → target behavior table
    One compact work package with steps and anchors
    Validation / Done When / rollback
    Routine preflight and verdict

Focused rendering rules：

- 明確寫出 GORE chain，不把 goal 隱藏在 outcome、標題或 implementation step；同一張表可同時承載 requirement、invariant 與 evidence，避免重複章節。
- 將 identity 與 freshness 壓成一行 preflight；未提供的 branch／commit 不需展開成整張表。
- 少量 requirement 與 invariant 可直接放進 behavior table，不另建重複 traceability matrix。
- 只列真正觸發且可能被漏掉的 cross-cutting concern；不要列一排無關的 Not applicable。
- 通常以單一 coherent work package 呈現；只有 dependency、owner、rollback 或驗收邊界不同時才拆包。
- 能在短表與具體步驟中說清楚時，不重複完整 template 章節。

## Standard Profile 最小骨架

    Identity and freshness
    Outcome, scope, requirements, invariants
    GORE actors, product intent, goals, quality guardrails, boundaries, and operationalization
    Current state evidence
    Target design and behavior contract
    Decisions, assumptions, unknowns
    Work package DAG and package details
    Triggered coverage
    Integration, validation, rollback, cleanup
    Traceability and verdict

## Migration 與 Master

所有 profile 都讀 [gore-spec-plan.md](gore-spec-plan.md)。

Migration 另外讀 [migration-strategies.md](migration-strategies.md)。

Master 另外讀 [large-change-planning.md](large-change-planning.md)，並展開 GORE hierarchy、conflicts、decision owners 與跨 goal traceability。

選定 profile 後仍以一份 canonical plan 交付，不要為不同 profile 建立多份主計畫。
