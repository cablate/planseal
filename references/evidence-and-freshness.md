# Evidence and Freshness

計畫中的證據要足以支撐決策，但不要把每句話都變成工具輸出。區分需求來源、repo reality 與推論。

## Evidence Taxonomy

| 類型 | 可接受來源 | 計畫中的責任 |
|---|---|---|
| Requirement | 使用者指示、核准規格、政策、權威文件 | 標示來源、優先級與衝突 |
| Fact | 目前 repo、runtime、資料、測試、設定或官方文件 | 記錄定位點、驗證方式與時間／commit |
| Decision | 使用者或計畫明確選定的方案 | 記錄理由、替代方案與影響 |
| Inference | 多個 Requirement／Fact 的推導 | 展示推導鏈，不假裝是直接事實 |
| Assumption | 為了前進採用的可逆暫定值 | 記錄重驗 gate、owner 與猜錯成本 |
| Unknown | 缺少或互相衝突的資訊 | 在依賴它的工作前安排 question、spike 或 preflight |

## Evidence Loop and Tool Routing

以能支撐計畫決策的最少有效迴圈蒐證：

1. 先找會改變 outcome、GORE、scope、target behavior、DAG 或 verification 的 prerequisite；不要因預期答案明顯就略過。
2. 並行讀取互不依賴的來源；若一個結果決定下一個查詢或行動，保持序列。並行結果必須先統整成一致 current-state claim 再寫入主計畫。
3. 每批結果後判斷核心計畫是否已有足夠 evidence。若足夠，停止 retrieval；不要為措辭、例子或非必要背景再查一次。
4. 若 material fact 仍缺少，明確指出缺什麼，再使用最小的一至兩個有意義 fallback。fallback 仍失敗就標記 Unknown／Needs Revision，不無限搜尋。
5. 空白、部分或可疑地狹窄的結果不等於事實上的「不存在」。縮小 claim、報告衝突或缺證，不要猜測。

最少 tool loop 不得優先於正確性、必要證據、計算或引用。只引用實際讀取的來源，並將 Inference 與直接支持的 Fact 分開。

## Repo Reality Workflow

1. 記錄 repo、branch、base commit 或 snapshot，以及 dirty worktree 是否影響計畫。
2. 找到真正 entrypoint、owner、caller／consumer、資料來源、測試、設定與部署路徑。
3. 讀實作與關鍵分支，不只搜尋名稱。
4. 對同類路徑做 impact scan，避免只修第一個命中。
5. 把足以改變 plan 的證據放進 Current State；探索細節可留在研究筆記。
6. 每個重要 Fact 記錄穩定定位點，例如 path + symbol、schema／route 名稱、測試名稱或設定 key。

行號可附加，但不能作為唯一定位。命令只是驗證方法的例子，不是 skill 的硬依賴。

## 數量與比例

寫數字前先定義：

- 母體是檔案、symbol、call site、route、table 還是測試；
- include／exclude 規則；
- 計算命令或查詢；
- 計算時的 commit／snapshot。

若不需要精確數量來做決策，改寫為具體範圍或代表性位置。不要使用看似精確但沒有母體的 X+、約 X% 或 X/Y。

## Freshness Header

主計畫至少記錄：

| Field | 內容 |
|---|---|
| Repository / scope | 計畫適用的 repo 或子目錄 |
| Branch / base | branch 與 base commit／snapshot |
| Plan created | 建立時間 |
| Last verified | 最後一次 repo reality check |
| Inputs | 需求、規格、ADR、issue 或外部 artifact |
| Known drift | 建立後已知的 relevant change |

## Preflight

在開始或恢復執行前：

1. 比較目前 HEAD／snapshot 與 plan base。
2. 找出變更是否碰到 entrypoint、owner、public contract、schema、dependency、測試或已排 work package。
3. 重驗第一個未完成 package 的 inputs、定位點與驗證命令。
4. 若 drift 只改導航資訊，修正定位點後繼續。
5. 若 drift 改變 behavior、ownership、dependency 或 migration path，修復受影響 package 與所有下游 dependency。
6. 更新 Last verified 與 verdict。

不要因為 commit 不同就自動判定過時；判斷 relevant drift。

## 無法存取 Repo 或 Runtime

仍可建立計畫，但必須：

- 將未查證現況標為 Unknown，而不是 Fact；
- 把 repo discovery／runtime check 排在第一個 work package；
- 說明該 check 可能如何改變後續 package；
- 在 check 完成前，不把受影響 package 標為 Ready。

若 discovery 結果可能改變 target behavior、DAG、migration 或 release strategy，整份 plan 的 verdict 至多是 Needs Revision；不能因為 discovery package 本身可執行就標 Ready。

## 證據衝突

來源衝突時採以下順序處理：

1. 使用者最新且明確的意圖可覆蓋舊需求，但要標記 intentional change。
2. runtime 與目前 code 可推翻過時文件中的 current-state claim。
3. 權威規格可定義 target behavior，但不能偽裝成目前已實作。
4. 無法裁決的衝突保留為 Decision Required，不要自行混合兩個版本。
