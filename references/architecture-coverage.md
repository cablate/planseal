# Conditional Architecture Coverage

只檢查被計畫內容觸發的維度。每個 trigger 記錄 Covered、Deferred 或 Not applicable，並指向負責的 work package。

## Coverage Matrix

| Trigger | 計畫必須回答 | 最小 evidence |
|---|---|---|
| UI／互動變更 | loading、success、empty、error、disabled、recovery、keyboard／accessibility、responsive 或 visual acceptance | state table、代表性流程、component／route 定位點、視覺或互動驗證 |
| 資料展示／報表 | 每個重要欄位從哪來、如何轉換、何時新鮮、缺值如何顯示 | data source map、query／schema 定位點、fixture 或查詢驗證 |
| Persistence／schema | ownership、schema、migration、backfill、consistency、retention、rollback | source／target schema、migration gate、資料驗證 |
| API／public contract | input、output、errors、versioning、consumer、compatibility | contract table、consumer list、contract／integration tests |
| 外部服務 | auth、timeout、retry、idempotency、rate limit、partial failure、reconciliation | failure map、sandbox／fixture、observability |
| Auth／authorization | actor、permission、deny path、session／token lifecycle、audit | permission matrix、negative tests、log／audit evidence |
| Security／privacy | trust boundary、validation、secret、敏感資料、logging、abuse case | threat notes、negative tests、config／policy evidence |
| 背景任務／concurrency | owner、deduplication、ordering、cancellation、status、retry、recovery | state machine、idempotency key、failure tests |
| Performance／scale | baseline、budget、代表性 workload、measurement、degradation path | benchmark／profile plan、guardrail |
| Dependency／tooling | compatibility、version、license、bundle／runtime、lockfile、fallback | official source、local compatibility check、build proof |
| Refactor／ownership | current／target owner、caller impact、public API、compat shim、deletion gate | owner map、impact scan、regression suite |
| Deploy／operations | config、environment、observability、rollout、rollback、support procedure | deploy gate、dashboard／log evidence、runbook |
| Generated／AI output | provenance、schema validation、nondeterminism、safety、cost、fallback | golden／property cases、validation boundary、usage telemetry |

## State Map

當行為跨多個非同步或 UI 狀態時使用：

| State | Entered by | User/system sees | Allowed action | Failure／recovery | Persisted where |
|---|---|---|---|---|---|

不要只畫 happy path。至少覆蓋開始前、進行中、成功、可恢復失敗與不可恢復失敗。

## Data Map

當資料跨 layer、格式或 owner 時使用：

| Field／artifact | Source owner | Transformation | Target／consumer | Freshness | Missing／invalid behavior |
|---|---|---|---|---|---|

Data map 用來阻止 hardcode、重複 source of truth、隱含轉換與無 owner 的衍生資料。

## Failure Map

當外部服務、background job、transaction 或多步 side effect 被觸發時使用：

| Failure point | Detect | User/system effect | Retry／idempotency | Recovery／reconcile | Evidence |
|---|---|---|---|---|---|

## Coverage Ledger

在主計畫保留精簡表：

| Concern | Trigger | Status | Work package／reason | Verification |
|---|---|---|---|---|

規則：

- Covered 必須指向實際 package 與 evidence，不能只寫「會注意」。
- Deferred 必須包含 owner、執行時點、原因與是否阻塞 release／cleanup。
- Not applicable 必須說明此計畫為何未改變該 concern。
- 未觸發的 concern 可完全省略。
- 需要 specialist 知識時可選擇性載入其他 skill，但把必要決策與驗證整合回主計畫；不得只留下外部連結。
