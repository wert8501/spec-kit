---
name: specify
description: "透過建立規格與功能分支啟動新功能。這是規格驅動開發生命週期的第一步。"
---

透過建立規格與功能分支啟動新功能。

這是規格驅動開發（Spec-Driven Development）生命週期的第一步。

在接收到作為引數提供的功能描述後，請執行下列步驟：

1. 從版本庫根目錄執行指令：`scripts/create-new-feature.sh --json "{ARGS}"`，解析其 JSON 輸出中的 BRANCH_NAME 與 SPEC_FILE。所有檔案路徑必須為絕對路徑。
2. 載入 `templates/spec-template.md` 以理解所需章節。
3. 依模板結構將規格寫入 SPEC_FILE：以功能描述（引數）推導具體內容並取代占位符，同時保持章節順序與標題不變。
4. 回報完成：包含分支名稱、規格檔路徑，並說明已就緒可進入下一階段。

注意：該腳本會建立並切換到新分支，並在寫入前初始化規格檔。
