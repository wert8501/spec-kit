---
name: tasks
description: "將實作計畫拆解為可執行任務。這是規格驅動開發生命週期的第三步。"
---

將實作計畫拆解為可執行任務。

這是規格驅動開發（Spec-Driven Development）生命週期的第三步。

給定作為引數傳入的上下文，請執行：

1. 從版本庫根目錄執行 `scripts/check-task-prerequisites.sh --json` 並解析輸出中的 FEATURE_DIR 與 AVAILABLE_DOCS 清單。所有路徑必須為絕對路徑。
2. 載入並分析可用設計文件：
   - 永遠讀取 plan.md（技術棧與函式庫）
   - 若存在：讀取 data-model.md（實體）
   - 若存在：讀取 contracts/（API 端點）
   - 若存在：讀取 research.md（技術決策）
   - 若存在：讀取 quickstart.md（測試情境）

   注意：不是所有專案都具備所有文件。例如：
   - CLI 工具可能沒有 contracts/
   - 簡單函式庫可能不需要 data-model.md
   - 依據可用文件生成任務

3. 依模板生成任務：
   - 使用 `/templates/tasks-template.md` 做為基礎
   - 以實際任務取代範例，基於：
     * **Setup 任務**：專案初始化、依賴、lint
     * **Test 任務 [P]**：每個契約一個、每個整合情境一個
     * **Core 任務**：每個實體、服務、CLI 指令、端點各一
     * **Integration 任務**：資料庫連線、中介層、日誌
     * **Polish 任務 [P]**：單元測試、效能、文件

4. 任務生成規則：
   - 每個契約檔 → 一個契約測試任務，標記 [P]
   - 每個資料模型實體 → 一個模型建立任務，標記 [P]
   - 每個端點 → 一個實作任務（若共享檔案則不可平行，不標 [P]）
   - 每個使用者故事 → 一個整合測試任務，標記 [P]
   - 不同檔案 = 可平行 [P]
   - 相同檔案 = 須循序（不標 [P]）

5. 依相依順序排序：
   - Setup 在最前
   - 測試先於實作（TDD）
   - 模型先於服務
   - 服務先於端點
   - Core 先於 Integration
   - 全部完成後才是 polish

6. 包含平行執行範例：
   - 將可平行 [P] 任務分組
   - 展示實際 Task agent 指令

7. 建立 FEATURE_DIR/tasks.md，內容包含：
   - 從實作計畫取得正確功能名稱
   - 編號任務（T001, T002, ...）
   - 每個任務的明確檔案路徑
   - 相依說明
   - 平行執行指引

任務生成上下文：{ARGS}

產生的 tasks.md 應可直接執行——每個任務需具體到 LLM 不再需要額外上下文即可完成。
