# 任務清單： [FEATURE NAME]

**輸入**: 來源自 `/specs/[###-feature-name]/` 的設計文件  
**前置需求**: plan.md（必需）、research.md、data-model.md、contracts/

## 執行流程 (main)
```
1. 從功能目錄載入 plan.md
   → 若不存在：ERROR "No implementation plan found"
   → 擷取：技術棧、函式庫、結構
2. 載入可選設計文件：
   → data-model.md：擷取實體 → 建立模型任務
   → contracts/：每個檔案 → 契約測試任務
   → research.md：擷取決策 → 建立 setup 任務
   → quickstart.md：擷取測試情境
3. 依分類生成任務：
   → Setup：專案初始化、依賴、lint
   → Tests：契約測試、整合測試
   → Core：模型、服務、CLI 指令
   → Integration：資料庫、中介層、日誌
   → Polish：單元測試、效能、文件
4. 套用任務規則：
   → 不同檔案 = 標記 [P] 可平行
   → 同一檔案 = 需循序（不標 [P]）
   → 測試先於實作（TDD）
5. 按序編號 (T001, T002...)
6. 生成相依關係圖
7. 建立平行執行範例
8. 驗證任務完整性：
   → 所有契約皆有測試？
   → 所有實體皆有模型？
   → 所有端點皆有實作任務？
9. 回傳：SUCCESS（任務可執行）
```

## 格式: `[ID] [P?] Description`
- **[P]**: 可平行執行（不同檔案且無相依）
- 描述需包含精確檔案路徑

## 路徑慣例 (Path Conventions)
- **單一專案**: `src/`, `tests/` 位於 repo root
- **Web app**: `backend/src/`, `frontend/src/`
- **Mobile**: `api/src/`, `ios/src/` 或 `android/src/`
- 下列路徑假設單一專案——依 plan.md 結構調整

## Phase 3.1: Setup
- [ ] T001 依實作計畫建立專案結構
- [ ] T002 初始化 [language] 專案並安裝 [framework] 依賴
- [ ] T003 [P] 設定 lint 與格式化工具

## Phase 3.2: Tests First (TDD) ⚠️ 必須在 3.3 前完成
**關鍵：這些測試必須先寫出且必須 FAIL，才能開始任何實作**
- [ ] T004 [P] 契約測試 POST /api/users -> tests/contract/test_users_post.py
- [ ] T005 [P] 契約測試 GET /api/users/{id} -> tests/contract/test_users_get.py
- [ ] T006 [P] 整合測試 user registration -> tests/integration/test_registration.py
- [ ] T007 [P] 整合測試 auth flow -> tests/integration/test_auth.py

## Phase 3.3: 核心實作 (僅在測試已失敗後)
- [ ] T008 [P] 建立 User model -> src/models/user.py
- [ ] T009 [P] 建立 UserService CRUD -> src/services/user_service.py
- [ ] T010 [P] CLI 指令 --create-user -> src/cli/user_commands.py
- [ ] T011 實作 POST /api/users 端點
- [ ] T012 實作 GET /api/users/{id} 端點
- [ ] T013 輸入驗證 (validation)
- [ ] T014 錯誤處理與日誌

## Phase 3.4: Integration
- [ ] T015 將 UserService 連接資料庫
- [ ] T016 Auth middleware
- [ ] T017 請求/回應日誌
- [ ] T018 CORS 與安全標頭

## Phase 3.5: Polish
- [ ] T019 [P] Validation 單元測試 -> tests/unit/test_validation.py
- [ ] T020 效能測試 (<200ms)
- [ ] T021 [P] 更新文件 -> docs/api.md
- [ ] T022 移除重複程式碼
- [ ] T023 執行 manual-testing.md

## 相依關係 (Dependencies)
- 測試 (T004-T007) 在實作 (T008-T014) 前
- T008 阻擋 T009, T015
- T016 阻擋 T018
- 實作在 polish (T019-T023) 前

## 平行範例 (Parallel Example)
```
# 同時啟動 T004-T007：
Task: "契約測試 POST /api/users -> tests/contract/test_users_post.py"
Task: "契約測試 GET /api/users/{id} -> tests/contract/test_users_get.py"
Task: "整合測試 registration -> tests/integration/test_registration.py"
Task: "整合測試 auth -> tests/integration/test_auth.py"
```

## 備註 (Notes)
- [P] 任務 = 不同檔案 + 無相依
- 確認測試失敗後再實作
- 每個任務完成後提交 (commit)
- 避免：模糊任務、同檔案衝突

## 任務生成規則 (Task Generation Rules)
*main() 執行期間套用*

1. **Contracts 來源**：
   - 每個契約檔 → 契約測試任務 [P]
   - 每個端點 → 實作任務
2. **Data Model 來源**：
   - 每個實體 → 模型建立任務 [P]
   - 關係 → 服務層任務
3. **User Stories 來源**：
   - 每個故事 → 整合測試 [P]
   - quickstart 情境 → 驗證任務
4. **排序**：
   - Setup → Tests → Models → Services → Endpoints → Polish
   - 相依關係阻擋平行

## 驗證清單 (Validation Checklist)
*GATE: main() 返回前檢查*

- [ ] 所有契約均有對應測試
- [ ] 所有實體均有模型任務
- [ ] 所有測試均在實作前
- [ ] 平行任務確實獨立
- [ ] 每個任務皆指明檔案路徑
- [ ] 無任務與另一個 [P] 任務修改同檔案
