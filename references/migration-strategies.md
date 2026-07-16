# Migration Strategies

Migration plan 必須說清楚新舊系統如何共存、如何取得可信證據、何時切換、失敗如何回復、何時刪除 transitional 路徑。

## Strategy Matrix

| Strategy | 適用 | 主要風險 | 必要 gate |
|---|---|---|---|
| Additive foundation | 先建立新 schema／service／API，不立即替換舊路徑 | 新模型成為無 consumer 的孤島 | 明確 adoption package 與 cleanup |
| Adapter／compatibility bridge | 需要保持舊 contract，內部 owner 改變 | shim 永久化、語意不完全相容 | contract tests、deletion criteria |
| Strangler by slice | 可按 route、tenant、feature 或 actor 漸進切換 | routing split 與行為漂移 | routing ownership、parity evidence |
| Backfill then cutover | 歷史資料需遷入新模型 | 資料漏失、順序、長時間執行 | rehearsal、checkpoint、reconcile |
| Dual-write | 新舊 store 必須短期同步 | partial write、ordering、長期 divergence | idempotency、reconciliation、短期 window |
| Shadow read／compare | 可同時讀新舊結果驗證 parity | 比較噪音、額外成本、敏感資料 | comparison rules、telemetry、exit threshold |
| Feature flag／canary | 可按流量或 cohort 漸進推出 | flag 組合、觀測不足 | cohort、guardrail、rollback trigger |
| Big-bang replacement | 無法共存，且範圍小、可完整 rehearsal、可迅速 rollback | blast radius 最大 | 明確理由、完整 rehearsal、停機／回復方案 |

不要預設某策略必然最佳。依 reversibility、observability、data criticality、compatibility window 與營運限制選擇。

## Source-to-Target Map

| Capability／data | Source owner | Target owner | Transform／compatibility | Coexistence window | Source deletion gate |
|---|---|---|---|---|---|

## Migration Work Package Contract

每個 migration package 另外回答：

- preconditions 與 production safety；
- source／target schema 或 contract；
- data／traffic movement 的順序與 checkpoint；
- old read、old write、new read、new write 各自何時啟用；
- retry、idempotency、partial failure 與 reconciliation；
- backward／forward compatibility；
- verification query、sample、parity 或 runtime evidence；
- rollback 或 roll-forward 決策；
- 下一 package 的 entry criteria；
- transitional artifact 的 owner 與刪除條件。

## 建議階段

依實際策略組合，不強制全部使用：

1. Baseline and rehearsal：量測現況、fixture、backup／restore、容量與時間。
2. Add target foundation：建立新 owner，不改變既有流量。
3. Populate／bridge：backfill、adapter、write-through 或 dual-write。
4. Observe parity：shadow read、reconcile、contract／behavior evidence。
5. Controlled cutover：依 cohort、route 或時間窗切換。
6. Stabilize：觀察 error、latency、data drift 與 support signal。
7. Cleanup：移除舊寫入、讀取、shim、flag、table 或 dependency。

## Cutover Gate

切換前明列：

| Gate | Required evidence | Decision owner | Abort／rollback trigger |
|---|---|---|---|

至少處理：

- 資料完整性與可恢復性；
- contract／behavior parity；
- performance 與容量；
- observability 與 on-call／support；
- rollback 是否仍可用，以及 rollback 會否造成反向資料遺失。

## Cleanup Gate

不要在「新路徑可以運作」時就宣稱 migration 完成。完成還包括：

- 舊路徑無剩餘 caller／traffic；
- reconciliation 無未處理差異；
- compatibility window 已滿足；
- rollback policy 已更新；
- legacy data／code／flag／dependency 依保留政策清理；
- 文件、runbook、owner 與監控指向新系統。
