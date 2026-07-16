# Planning Failure Modes

用此清單做最後一輪反向審查；不要把它當成先填滿的模板。

| Failure mode | 症狀 | 修復 |
|---|---|---|
| Checklist 取代理解 | 每項都勾選，但 outcome 或方向不清 | 回到 actor、outcome、invariant 與 non-goal |
| 儀式化 GORE | goal 只是把「實作／重構／遷移 X」換句話說，或每份 plan 都複製相同 actor／soft goal | 回到真實 actor、job 與可觀察結果；以 profile 壓縮渲染，但保留 goal → requirement → package → evidence |
| 固定流程取代必要結果 | 不論證據與 dependency 都機械地跑同一串步驟 | 先定義必須成立的計畫結果，再依 prerequisite 選擇並行或序列路徑 |
| 蒐證沒有停止條件 | 為措辭、例子或完整感持續搜尋 | 每批結果後判斷是否足以支撐核心計畫；material fact 缺少時最多使用一至兩個 fallback，之後標 Unknown |
| 檔案清單偽裝成計畫 | 只寫新增／修改檔案，沒有行為與驗收 | 補 baseline、target behavior、owner、evidence、Done When |
| 先選架構再找理由 | plan 強迫某 pattern、folder 或 library，repo evidence 不支持 | 比較 options，記錄 decision 與最小必要 abstraction |
| 固定大小規則 | 以七個檔案、五百字或固定 phase 數判定拆分 | 按 coherent outcome、owner、dependency、risk 與可驗收性切包 |
| 工具指令成為方法 | 只會用特定 grep、wc 或 subagent 波次 | 保留驗證目的，依環境選工具 |
| 所有 claim 都假裝是 Fact | requirement、inference、assumption 混在 repo facts | 套用 evidence taxonomy |
| 虛假精度 | X+、約 X%、X/Y 無母體或 snapshot | 定義 denominator 與重跑方式，或移除數字 |
| 過期定位 | 行號、route、schema 或 package 已漂移 | 加 base commit、stable anchor 與 preflight |
| 外部 skill 成為依賴 | 沒有 Spectra 或 specialist 就不能 Ready | 把必要內容納入主計畫；外部 skill 只補強 |
| 多份 SSOT | review report、migration doc、task list 各自有不同 phase | 選一份 canonical plan，其餘只作 input／evidence |
| Unknown 藏在步驟 | 實作者做到一半才要決定資料來源或 public contract | 提前建立 question、spike 或 decision gate |
| Happy path-only | 有步驟與測試，但沒有 failure、retry、recovery | 補 state／failure map 與 negative evidence |
| Build 等於完成 | 只跑 compile／typecheck 即宣稱產品完成 | 分開 structural、integration、behavior evidence |
| 延後但無 owner | 寫「之後做 e2e／cleanup」 | 建 deferred ledger、owner、時點與阻塞條件 |
| Review 只列問題 | findings 很完整，原 plan 仍不可執行 | 把 repair 整合回 canonical plan，再判 verdict |
| 完成沒有清理 | shim、flag、dual-write、legacy 永久留下 | 定義 cleanup owner、entry criteria 與 deletion evidence |
| 固定 specialist routing | plan 強制不存在或不相關的 skill | 以條件式 coverage 自給自足；必要時才選擇性補強 |

## 最後三問

1. 新執行者會在哪一點被迫自行發明重要決策？
2. 哪個失敗仍可能在所有列出的驗證都通過後發生？
3. 哪個 transitional 元件可能因沒有刪除條件而永久存在？

任何答案指向實際風險，就修復主計畫並重驗下游 package。
