---
name: planseal
description: >-
  Create, review, repair, and preflight executable technical plans with mandatory GORE goal traceability, grounded evidence, work-package DAGs, verification, rollback, and readiness verdicts. Use when Codex needs an implementation plan, refactor plan, migration plan, architecture plan, handoff, phased delivery plan, plan review, plan repair, or execution-readiness preflight. Produces one canonical plan and works without Spectra or any companion skill.
---

# PlanSeal

## 交付成果與權限

產出一份新的執行者只靠計畫與計畫指向的證據，就能開始工作、做出必要決策、逐包驗收並安全收尾的 canonical executable plan。

成功代表：

- 使用者可觀察的 outcome、重要 constraints、可用 evidence 與完成標準明確；
- 每個 requirement、work package 與驗證都能追溯到 GORE goal；
- 實作者不需自行發明重大產品行為、public contract、資料來源或失敗策略；
- material unknown 已解決，或計畫誠實降級並提供可執行的 resolution path；
- 內容足以安全執行，但沒有不影響 implementation、sequencing、risk、handoff 或 verification 的重複段落。

遵守以下權限邊界：

- 保持一份主計畫。研究筆記、審查發現與外部 artifact 只作為 input 或 evidence，不建立第二份 SSOT。
- 獨立完成規劃。Spectra 與其他 specialist skill 只能補強；不可用時不得阻止本 skill 產出 Ready 計畫。
- Plan、Review、Repair 與 Preflight 只檢查或修改 plan artifact；除非使用者另外要求，不實作產品程式碼。
- 可直接執行必要的唯讀蒐證與非破壞性驗證。外部寫入、破壞性操作或實質擴張範圍仍需另行授權。

## 選擇模式與 Profile

| 模式 | 何時使用 | 必要結果 |
|---|---|---|
| Create | 尚無可信計畫 | 建立完整主計畫 |
| Review | 使用者提供既有計畫 | 列出影響執行的發現，並把修正整合回主計畫 |
| Repair | 已知計畫有缺口或過時 | 重寫受影響區段，重驗所有下游依賴 |
| Preflight | 即將開始或恢復執行 | 依目前 repo 重驗 freshness、blocker 與第一個可執行 work package |

先讀 [plan-profiles.md](references/plan-profiles.md) 選擇 Focused、Standard、Migration 或 Master，再讀 [gore-spec-plan.md](references/gore-spec-plan.md)。

每個 profile 都必須使用 GORE core。Profile 只決定 goal model、DAG、coverage 與 coordination 的展開深度，不決定是否使用 GORE。Focused 可以壓成一條 compact goal chain，但不得省略 actor／job、product intent、primary goal、supporting／enabling goal、品質 guardrail、邊界與 operationalization。

若使用者明確要求 read-only review，保留原檔不寫入；仍在回覆中提供可直接套用的修訂內容與 verdict。

## 形成必要結果

把下表視為交付前必須成立的結果，不要視為每次都要照抄的固定操作序列。依現有證據與 dependency 選擇最有效路徑：獨立蒐證可並行，後一步取決於前一步結論時保持序列；蒐證後先統整，再寫入同一主計畫。

| 必要結果 | 完成標準 |
|---|---|
| Plan identity and outcome | 記錄可觀察成果、repo／snapshot、scope、non-goals、invariants、profile、owner 與 freshness |
| Mandatory GORE core | 定義 actor／job、product intent、primary goal、supporting／enabling goals、soft goal／品質 guardrail、domain invariant／non-goal，並規劃 goal → requirement → package → evidence |
| Grounded current state | 依 [evidence-and-freshness.md](references/evidence-and-freshness.md) 區分 Requirement、Fact、Decision、Inference、Assumption、Unknown，保留能改變計畫的穩定定位點 |
| Target behavior and design | 說明 actor／entrypoint、input、state、output、side effect、error／recovery、owner、public contract、相容性、intentional change 與 forbidden shortcut |
| Executable work graph | 依 [execution-readiness.md](references/execution-readiness.md) 建立可獨立驗收的 work packages、dependency DAG、verification、Done When、failure／rollback 與 handoff |
| Triggered coverage and release path | 只處理被觸發的架構／安全／資料／運維 concern；需要時定義 integration、rollout／cutover、rollback、cleanup 與 deferred verification |
| Rechecked canonical plan | forward／backward 重驗 goal traceability、dependency、unknown、驗證與收尾，修復主計畫後再給 readiness verdict |

沒有 repo 或 runtime 時，不把未查證現況寫成 Fact。若 discovery 結果可能改變 target behavior、DAG、資料安全、migration 或 release strategy，將計畫標為 Needs Revision，並把 discovery／spike 放在受影響 package 之前。

## 控制首版範圍

每份功能計畫都要標示 release intent：`MVP`、`production slice` 或 `platform foundation`。未指定時預設為 `production slice`，先交付最小但可正式使用的垂直切片。

將候選工作分成 `release blocker`、`first-release value`、`hardening`、`future expansion`。首版只納入前兩類；後兩類可以記錄為 deferred scope，但除非 owner 明確提升優先級，不得轉成首版 work package。

出現下列任一訊號時，加入 complexity checkpoint：

- 同時新增超過一個核心 domain，或超過三張資料表；
- 同時建立 public、user、admin 三套完整操作面；
- 同時引入資料庫、外部儲存與部署責任；
- 預估影響超過十個操作或五十個檔案。

這些是提醒門檻，不是禁止線。先顯示新增範圍與較小方案，再由 owner 決定是否繼續並標記 Ready。不得只因治理、抽象或擴充能力「未來可能有用」就自動納入首版。

## 控制蒐證與停止

依 [evidence-and-freshness.md](references/evidence-and-freshness.md) 的 Evidence Loop 蒐證。每批結果後判斷核心計畫是否已有足夠 evidence；足夠就停止。material fact 仍缺少時只使用一至兩個有意義的 fallback，之後標記 Unknown／Needs Revision；不要為措辭、例子或非必要背景繼續搜尋，也不要把空白結果解讀成「不存在」。

資訊足以改變、排序、驗證與安全回復工作後，停止展開；移除空章節、重複表格與無理由的 Not applicable。最少工具迴圈不得優先於正確性、必要證據或必要引用。

## 處理 Unknown 與 Readiness

只有 unknown 會改變核心 outcome、GORE goal／conflict、不可逆資料操作、public contract、安全邊界或整體 DAG 時，才阻塞並詢問最小必要問題。

- 可安全且可逆：記錄 Assumption、recheck point 與猜錯成本後繼續。
- 可先驗證：建立有 hypothesis、timebox、成功／失敗分支、輸出 evidence 與 plan-update owner 的 spike。
- 執行前才能知道：加入 preflight gate，不把 unknown 藏在 implementation step。

只使用以下 verdict；詳細 rubric 以 [execution-readiness.md](references/execution-readiness.md) 為準。

| Verdict | 判定 |
|---|---|
| Ready | 所有 material goal、decision 與 unknown 已關閉；goal → requirement → package → evidence 完整，實作者可直接進入 implementation |
| Needs Revision | resolution／repair package 可執行，但結論仍可能改變 goal、target design、DAG、migration、release 或驗收 |
| Not Executable | 連 resolution path 都缺少必要輸入、權限、owner 或安全邊界，無法可靠開始 |

First executable package 是 discovery／spike，不代表整份計畫 Ready。不要使用沒有明確母體與判準的「事實準確率 X/Y」或「架構覆蓋率 X/Y」。

## 輸出 Canonical Plan

- Focused 使用 [plan-profiles.md](references/plan-profiles.md) 的 compact skeleton。
- Standard、Migration 與 Master 使用 [executable-plan-template.md](references/executable-plan-template.md)。
- 所有 profile 都明確呈現 GORE core 與 goal operationalization；不得只把技術工作改寫成 goal 名稱。
- Review／Repair 可在主計畫前加入精簡 findings table，但 findings 不是交付物本體；修復後的 canonical plan 與 verdict 才是。
- 同一 fact 可在 traceability 中引用，不要在 summary、requirements、coverage 與 package 逐字重複。
- 每段內容都必須改變執行決策、依賴、風險、handoff 或驗證；否則合併或刪除。

交付前讀 [planning-failure-modes.md](references/planning-failure-modes.md)，至少做一次 forward pass 與 backward pass。修復後只重驗受影響區段與所有 downstream package；最多兩輪，仍有 blocker 就誠實降級 verdict。

## Reference Routing

| 何時讀取 | Reference |
|---|---|
| 每次：選擇規模與渲染深度 | [plan-profiles.md](references/plan-profiles.md) |
| 每次：建立必要 GORE core 與 goal traceability | [gore-spec-plan.md](references/gore-spec-plan.md) |
| 每次：證據、repo freshness、retrieval budget、preflight | [evidence-and-freshness.md](references/evidence-and-freshness.md) |
| 每次：DAG、work package、驗證、readiness | [execution-readiness.md](references/execution-readiness.md) |
| 被 concern 觸發：架構、資料、UI、安全與運維覆蓋 | [architecture-coverage.md](references/architecture-coverage.md) |
| 多 owner、平行施工或集中整合 | [large-change-planning.md](references/large-change-planning.md) |
| 平台、框架、schema 或資料遷移 | [migration-strategies.md](references/migration-strategies.md) |
| Standard／Migration／Master 最終格式 | [executable-plan-template.md](references/executable-plan-template.md) |
| 每次交付前：反向檢查常見失敗 | [planning-failure-modes.md](references/planning-failure-modes.md) |
