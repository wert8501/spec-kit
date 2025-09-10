---
name: plan
description: "規劃如何實作指定的功能。這是規格驅動開發生命週期的第二步。"
---

規劃如何實作指定的功能。

這是規格驅動開發（Spec-Driven Development）生命週期的第二步。

在接收到作為引數提供的實作細節後，請執行下列步驟：

1. 從版本庫根目錄執行 `scripts/setup-plan.sh --json`，解析其 JSON 輸出中的 FEATURE_SPEC、IMPL_PLAN、SPECS_DIR、BRANCH。後續所有檔案路徑必須為絕對路徑。
2. 讀取並分析功能規格以理解：
   - 功能需求與使用者故事
   - 功能性與非功能性需求
   - 成功標準與驗收標準
   - 任何提及的技術限制或相依性
3. 讀取 `/memory/constitution.md` 的憲章以理解強制性原則。
4. 執行實作計畫模板：
   - 載入 `/templates/plan-template.md`（它已被複製到 IMPL_PLAN 路徑）
   - 將 Input path 設為 FEATURE_SPEC
   - 執行 Execution Flow (main) 函數步驟 1-10
   - 模板是自包含且可執行的
   - 嚴格遵循錯誤處理與 gate 檢查
   - 讓模板在 $SPECS_DIR 生成所需產物：
     * Phase 0 生成 research.md
     * Phase 1 生成 data-model.md、contracts/、quickstart.md
     * Phase 2 生成 tasks.md
   - 將使用者提供的實作細節（引數）併入 Technical Context: {ARGS}
   - 隨階段完成更新 Progress Tracking
5. 驗證執行完成：
   - 確認 Progress Tracking 顯示所有階段完成
   - 確認所有必要產物已生成
   - 確認無任何階段為 ERROR 狀態
6. 回報結果：包含分支名稱、檔案路徑與已生成產物清單。

所有檔案操作請使用版本庫根目錄起算的絕對路徑，避免路徑問題。
