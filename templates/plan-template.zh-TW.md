# 實作計畫： [FEATURE]

**分支**: `[###-feature-name]` | **日期**: [DATE] | **規格**: [link]
**輸入**: 來源於 `/specs/[###-feature-name]/spec.md` 的功能規格

## 執行流程 (/plan 指令範圍)
```
1. 從輸入路徑載入功能規格
   → 若找不到：ERROR "No feature spec at {path}"
2. 填寫「技術脈絡」(Technical Context)（掃描 NEEDS CLARIFICATION）
   → 從上下文推斷專案型態（web=frontend+backend, mobile=app+api）
   → 依專案型態設定結構決策 (Structure Decision)
3. 評估下方「憲章檢查」(Constitution Check)
   → 若存在違規：記錄在 Complexity Tracking
   → 若無法給出正當理由：ERROR "Simplify approach first"
   → 更新 Progress Tracking：Initial Constitution Check
4. 執行 Phase 0 → 產出 research.md
   → 若仍有 NEEDS CLARIFICATION：ERROR "Resolve unknowns"
5. 執行 Phase 1 → 產出 contracts, data-model.md, quickstart.md, 以及特定代理模板檔 (例如 `CLAUDE.md`、`.github/copilot-instructions.md`、`GEMINI.md`)
6. 再次評估「憲章檢查」
   → 若有新違規：重構設計並回到 Phase 1
   → 更新 Progress Tracking：Post-Design Constitution Check
7. 規劃 Phase 2 → 描述任務生成方式（不建立 tasks.md）
8. STOP - 準備交由 /tasks 指令
```

**重要**: /plan 指令於步驟 7 停止。Phase 2-4 由其他指令或人員執行：
- Phase 2: /tasks 指令建立 tasks.md
- Phase 3-4: 實作執行（手動或工具）

## 摘要 (Summary)
[從功能規格擷取：主要需求 + 研究得出的技術方向]

## 技術脈絡 (Technical Context)
**語言/版本**: [例如 Python 3.11, Swift 5.9, Rust 1.75 或 NEEDS CLARIFICATION]  
**主要依賴**: [例如 FastAPI, UIKit, LLVM 或 NEEDS CLARIFICATION]  
**儲存**: [若適用，如 PostgreSQL, CoreData, files 或 N/A]  
**測試**: [例如 pytest, XCTest, cargo test 或 NEEDS CLARIFICATION]  
**目標平台**: [例如 Linux server, iOS 15+, WASM 或 NEEDS CLARIFICATION]
**專案型態**: [single/web/mobile - 影響原始碼結構]  
**效能目標**: [領域特定，如 1000 req/s, 10k lines/sec, 60 fps 或 NEEDS CLARIFICATION]  
**限制條件**: [領域特定，如 <200ms p95, <100MB memory, offline-capable 或 NEEDS CLARIFICATION]  
**規模/範圍**: [領域特定，如 10k users, 1M LOC, 50 screens 或 NEEDS CLARIFICATION]

## 憲章檢查 (Constitution Check)
*GATE: Phase 0 研究前必須通過；Phase 1 設計後需再檢查。*

**Simplicity（簡潔）**:
- 專案數量: [#]（最多 3，例如 api, cli, tests）
- 是否直接使用框架？（無包裝層）
- 單一資料模型？（除非序列化需求不同不額外建 DTO）
- 避免花俏模式？（無 repository/UoW 除非必要）

**Architecture（架構）**:
- 每個功能皆為函式庫？（無直接 app code）
- 函式庫列表： [名稱 + 目的]
- 每個函式庫 CLI： [commands 含 --help/--version/--format]
- 函式庫文件：是否規劃 llms.txt 格式？

**Testing（測試，非協商）**:
- 是否強制 RED-GREEN-REFACTOR？（測試必須先失敗）
- Git 提交是否顯示「測試先於實作」？
- 順序：Contract → Integration → E2E → Unit 是否嚴格遵守？
- 是否使用真實依賴？（實際 DB 而非 mocks）
- 整合測試涵蓋：新函式庫、契約變更、共享 schema？
- 禁止：實作先於測試、跳過 RED phase

**Observability（可觀察性）**:
- 有結構化日誌？
- 前端日誌 → 後端聚合？（統一流）
- 錯誤上下文充足？

**Versioning（版本）**:
- 已指定版本號？（MAJOR.MINOR.BUILD）
- BUILD 每次變更遞增？
- 破壞性變更處理？（平行測試 + 遷移計畫）

## 專案結構 (Project Structure)

### 文件（本功能）
```
specs/[###-feature]/
├── plan.md              # 本檔 (/plan 輸出)
├── research.md          # Phase 0 (/plan)
├── data-model.md        # Phase 1 (/plan)
├── quickstart.md        # Phase 1 (/plan)
├── contracts/           # Phase 1 (/plan)
└── tasks.md             # Phase 2 (/tasks - 非 /plan 產出)
```

### 原始碼（repository root）
```
# 選項 1：單一專案（預設）
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# 選項 2：Web 應用（偵測到 frontend+backend）
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# 選項 3：Mobile + API（偵測到 iOS/Android）
api/
└── [同 backend 結構]

ios/ 或 android/
└── [平台特定結構]
```

**結構決策 (Structure Decision)**: [若無明確指標預設 Option 1]

## Phase 0: 大綱與研究 (Outline & Research)
1. **擷取「技術脈絡」中的未知項**：
   - 每個 NEEDS CLARIFICATION → 研究任務
   - 每個依賴 → 最佳實務任務
   - 每個整合點 → 模式研究任務

2. **建立並派送研究代理**：
   ```
   對每個未知：
     Task: "Research {unknown} for {feature context}"
   對每個技術選擇：
     Task: "Find best practices for {tech} in {domain}"
   ```

3. **整合發現** 於 `research.md`：
   - Decision: [選擇]
   - Rationale: [理由]
   - Alternatives considered: [替代方案]

**輸出**: research.md（所有 NEEDS CLARIFICATION 已解）

## Phase 1: 設計與契約 (Design & Contracts)
*前置需求：research.md 完成*

1. **從功能規格抽取實體** → `data-model.md`：
   - 實體名稱、欄位、關係
   - 需求中的驗證規則
   - 若有狀態轉換則描述

2. **從功能需求生成 API 契約**：
   - 每個使用者動作 → 一個端點
   - 使用標準 REST/GraphQL 模式
   - 產出 OpenAPI/GraphQL schema 至 `/contracts/`

3. **從契約生成契約測試**：
   - 每個端點一個測試檔
   - 斷言請求/回應 schema
   - 測試必須失敗（尚無實作）

4. **從使用者故事萃取測試情境**：
   - 每個故事 → 整合測試情境
   - quickstart 測試 = 故事驗證步驟

5. **漸進更新代理檔（O(1) 操作）**：
   - 執行 `/scripts/update-agent-context.sh [claude|gemini|copilot]`
   - 若檔存在：僅新增新的技術
   - 保留標記區塊中的手動內容
   - 更新最近變更（保留最後 3 筆）
   - 控制在 150 行內
   - 產出於 repository root

**輸出**: data-model.md, /contracts/*, 失敗中的測試, quickstart.md, 代理特定檔案

## Phase 2: 任務規劃方法 (Task Planning Approach)
*此處描述 /tasks 將做什麼 —— /plan 不執行*

**任務生成策略**:
- 載入 `/templates/tasks-template.md` 為基底
- 從 Phase 1 產物產生任務（contracts, data model, quickstart）
- 每個契約 → 契約測試任務 [P]
- 每個實體 → 模型建立任務 [P]
- 每個使用者故事 → 整合測試任務
- 以使測試通過為目標建立實作任務

**排序策略**:
- TDD 順序：測試先於實作
- 依賴順序：模型 → 服務 → UI
- 標記 [P] 代表可平行（不同檔案、無依賴）

**預估輸出**：tasks.md 中 25-30 個具編號且排序的任務

**重要**：此階段由 /tasks 指令執行，非 /plan

## Phase 3+：後續實作 (Future Implementation)
*超出 /plan 範圍*

**Phase 3**：執行任務 (/tasks 產出 tasks.md)  
**Phase 4**：實作（遵守憲章原則）  
**Phase 5**：驗證（跑測試、執行 quickstart.md、效能驗證）

## 複雜度追蹤 (Complexity Tracking)
*僅在憲章檢查有違規且需理由時填寫*

| 違規 | 為何需要 | 捨棄較簡方案的理由 |
|------|----------|---------------------|
| [例：第 4 個專案] | [當前需求] | [為何 3 個不足] |
| [例：Repository pattern] | [特定問題] | [為何直接 DB 不足] |

## 進度追蹤 (Progress Tracking)
*執行流程期間更新*

**Phase 狀態**:
- [ ] Phase 0: Research 完成 (/plan)
- [ ] Phase 1: Design 完成 (/plan)
- [ ] Phase 2: Task planning 完成 (/plan - 僅描述)
- [ ] Phase 3: Tasks 已生成 (/tasks)
- [ ] Phase 4: Implementation 完成
- [ ] Phase 5: Validation 通過

**Gate 狀態**:
- [ ] Initial Constitution Check: PASS
- [ ] Post-Design Constitution Check: PASS
- [ ] 所有 NEEDS CLARIFICATION 已解
- [ ] 複雜度偏離已文件化

---
*基於 Constitution v2.1.1 - 參見 `/memory/constitution.md`*
