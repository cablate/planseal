# Large Change Planning

用於跨多個 owner、surface、agent／worktree 或 release 的 Master plan。目標是讓平行施工不破壞單一架構方向，並讓集中整合可追責。

## 目錄

- [先定義 Ownership](#先定義-ownership)
- [建立衝突圖](#建立衝突圖)
- [三類 Execution Track](#三類-execution-track)
- [Integration Stages](#integration-stages)
- [Deferred Verification](#deferred-verification)
- [Cleanup and Exit](#cleanup-and-exit)
- [Execution Handoff](#execution-handoff)

## 先定義 Ownership

先列 current owner 與 target owner：

| Capability／artifact | Current owner | Target owner | Reuse／wrap／move／replace | Public contract | Deletion condition |
|---|---|---|---|---|---|

規則：

- 先重用已乾淨且有 consumer 的 owner；不要因新資料夾或新框架就重造。
- Transitional owner、shim 或 legacy path 必須有 owner 與刪除條件。
- Target owner 要描述責任與 forbidden responsibility，不只寫目錄名稱。
- State、decision 與 side effect 各自只有一個 canonical owner；projection 或 cache 要明說來源。

## 建立衝突圖

在切 agent／worktree 前列出共享交會點：

- router、registry、schema migration；
- package manifest、lockfile、build config；
- global CSS、app shell、shared public API；
- generated schema／client；
- feature flag、deploy pipeline、legacy deletion；
- 同一資料表或 source of truth。

兩個 package 若會同時修改同一交會點，預設不可直接平行寫入。可先平行做 discovery、impact map、API proposal、fixture 或 migration rehearsal，再由 serial owner 落地。

## 三類 Execution Track

| Track | 適用 | 必要欄位 |
|---|---|---|
| Parallel implementation | owner 與 allowed surface 不重疊，contract 已固定 | allowed／forbidden scope、public input/output、light gates、handoff |
| Parallel planning／spike | 實作交會但研究可分離 | question、evidence、decision format、serial consumer |
| Serial coordinator | 共享 SSOT、不可逆 migration、全域 contract 或 final merge | inputs、順序、conflict resolution、integration gates、rollback |

平行度由 dependency 與衝突面決定，不由可用 agent 數決定。

## Integration Stages

大型計畫通常分三種完成狀態：

| Stage | 代表 | 不能宣稱 |
|---|---|---|
| Architecture／owner landing | code 與 public contract 到正確 owner，局部 gate 通過 | 不等於跨 surface behavior 已驗收 |
| Integration stabilization | import、type、schema、router、config、build 與 shared contract 整合 | 不等於真實使用流程或營運已驗證 |
| Behavior／operational verification | e2e、runtime、visual、migration、deploy、telemetry 與 rollback evidence 成立 | 才能宣稱相關 outcome 完成 |

主計畫要指出每個 package 完成到哪一 stage，以及誰負責後續 stage。

## Deferred Verification

每個 landing package 留下：

| Check | 為何需整合後 | Integration owner | Evidence | Blocks | Failure repair owner |
|---|---|---|---|---|---|

不可延後：

- scope 與 dirty-worktree 安全檢查；
- 低成本 syntax／type／unit／component gate；
- public contract 與 forbidden dependency 檢查；
- 不可逆 schema、權限、production data 或 secret 風險評估。

可依條件延後：

- 需要多 package 的 full e2e；
- live browser／device／visual comparison；
- 大資料量 rehearsal 或 load test；
- production-like canary、telemetry 與 rollback rehearsal。

## Cleanup and Exit

為每個 transitional 元件定義：

| Transitional item | Created by | Exit criteria | Deletion owner | Deletion evidence |
|---|---|---|---|---|

Final plan 要包含：

- legacy imports／routes／tables／flags／adapters 的清理；
- temporary test fixture、dual-write、shadow compare 或 compatibility window 的收尾；
- 文件與 ownership map 更新；
- 未完成 cleanup 如何阻塞 final Done。

## Execution Handoff

交給下一個 session／agent 的 package 摘要至少包含：

    Package ID and outcome
    Goal / requirement contribution
    Dependencies and current status
    Allowed and forbidden surfaces
    Existing owners to reuse
    Public contract and invariants
    Ordered implementation steps
    Lightweight gates
    Deferred verification
    Integration owner and risks
    Done When and cleanup

Handoff 只摘錄 canonical plan 的單一 package，不另建新的架構方向。
