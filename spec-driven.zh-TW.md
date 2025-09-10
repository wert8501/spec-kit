# 規格驅動開發（Specification-Driven Development, SDD）

## 權力的反轉（The Power Inversion）

數十年來，程式碼至高無上。規格文件服務於程式碼——它們只是鷹架：在「真正的工作」(coding) 開始前搭起，之後常被丟棄。我們寫 PRD（產品需求文件）指引開發、寫設計文件協助實作、畫架構圖協助理解。但這些始終隸屬於程式碼。程式碼是真理。其他充其量是「良好意圖」。程式碼成為唯一的真實來源，往前演進；規格很少跟得上。因為資產（code）與實作合而為一，要在外圍維護一個平行的實作真實來源其實很難。

規格驅動開發（SDD）顛覆這個權力結構：規格不是服務程式碼，而是程式碼服務規格。PRD（產品需求文件／規格）不再只是實作的參考——它是產生實作的來源。技術計畫不再是協助人類寫程式的文件——它們是足以直接產生程式碼的形式化定義。這不是對傳統開發的漸進式改善，而是對「什麼驅動開發」的根本再思考。

規格與實作之間的落差，自軟體誕生以來反覆困擾我們。我們試過更完整的文件、更細的需求、更嚴謹的流程；它們失敗，因為它們預設「落差是必然」。它們嘗試縮小落差，但從未消除。SDD 透過讓規格（以及由規格衍生的具體實作計畫）可執行而將落差移除。當從規格到實作計畫再到程式碼的過程是生成式且可再生的，就不存在「落差」，只剩「轉換」。

這種轉換如今可行，是因為 AI 已能理解並實作複雜規格，並產生詳細實作計畫。但**沒有結構的原始 AI 生成會導致混亂**。SDD 透過「足夠精確、完整、無歧義」的規格與後續實作計畫提供結構，使其可產生可運行系統。規格成為主要產出；程式碼只是它在特定語言與框架中的表達（由實作計畫落地）。

在這個新世界，維護軟體意味著演進規格。團隊意圖以自然語言（「意圖驅動開發」）、設計資產、核心原則與其他指引呈現。開發的 **lingua franca（共同語言）** 上移一個層次；程式碼是「最後一哩」手段。

除錯意味著修正產生錯誤程式碼的規格與實作計畫。重構意味著為清晰重組。整個開發工作流圍繞規格為中心：實作計畫與程式碼是可連續再生的輸出。要更新 app 或新增平行實作（因為我們具創造力）時，回到規格並建立新的實作計畫。這是一個 0 -> 1, (1', ..), 2, 3, N 的過程。

開發團隊聚焦於創造力、實驗與批判思考。

## SDD 工作流程實務化（Workflow in Practice）

流程從一個想法開始——常常模糊且不完整。透過與 AI 的迭代對話，想法成為一份完整 PRD。AI 會提問澄清、辨識邊界情境、協助定義精確可驗收的標準。傳統需要數天的會議與文件，轉為數小時專注的規格工作。這改造了傳統 SDLC ——需求與設計變成連續活動，而非離散階段。這支持 **團隊流程**：團隊審查的規格以分支方式建立、版控、合併。

當產品經理更新驗收標準，實作計畫自動標記受影響的技術決策。當架構師發現更佳模式，PRD 更新以反映新可能。

在規格過程中，研究代理（research agents）持續蒐集關鍵上下文：套件相容性、效能基準、安全影響。組織約束（公司資料庫標準、驗證要求、部署政策）被自動發現並整合進每份規格。

從 PRD，AI 生成實作計畫，將需求映射到技術決策。每個技術選擇具備文件化理由。每個架構決策可追溯到特定需求。此過程中，一致性驗證持續運行：AI 針對模糊、矛盾、缺口做分析——不是一次性的 gate，而是持續精煉。

當規格與實作計畫達到「足夠穩定」時程式碼生成即可開始，無須「完全完成」。早期生成可能是探索性的——測試規格在實務上是否合理。領域概念轉為資料模型。使用者故事轉為 API。驗收情境轉為測試。這透過規格融合了開發與測試——測試情境不是在程式碼後撰寫，而是規格的一部分，驅動實作與測試的同時生成。

回饋循環延伸到初始開發之外。上線後的指標與事故不只是觸發 hotfix——它們更新規格，成為下一次再生的輸入。效能瓶頸轉成新的非功能性需求。安全弱點成為影響所有未來生成的約束。規格、實作與營運實際之間的迭代舞動，孕育真實理解，並將傳統 SDLC 轉為連續演化。

## 為何現在是 SDD 的時刻（Why SDD Matters Now）

三個趨勢讓 SDD 不只可行更是必要：

首先，AI 能力已達門檻，使自然語言規格可可靠生成可運行程式碼。這不是取代開發者，而是放大其效能，將「從規格到程式碼」的機械翻譯自動化。它放大探索與創造力，支援「重新開始」，支援加減、批判思考。

第二，軟體複雜度呈指數成長。現代系統整合數十個服務、框架與依賴。透過人工流程讓這些部件與原始意圖保持一致愈來愈困難。SDD 透過規格驅動的生成提供系統化對齊。框架可能會演進出「AI 第一」支援，而非「人類第一」，或以可重用組件為核心來架構。

第三，變化速度加快。需求比以往更加頻繁改變。Pivot 不再例外，而是預期。現代產品開發要求基於使用者回饋、市場、競爭的快速迭代。傳統開發將這些變更視為干擾。每次 pivot 需要手動將變化傳播到文件、設計、程式碼。結果要麼慢而謹慎（壓低速度），要麼快而魯莽（累積技術債）。

SDD 可支援 what-if／模擬實驗：「如果我們要重構或調整應用以促進賣更多 T-shirt 的商務需求，我們會怎麼實驗？」

SDD 把需求變更從障礙變成正常工作流。當規格驅動實作，pivot 變成系統化再生成，而非人工重寫。改 PRD 的核心需求，受影響的實作計畫自動更新。修改使用者故事，對應 API 端點再生。這不只是初始開發——而是面對不可避免變化仍維持工程速度。

## 核心原則（Core Principles）

**規格作為共同語言**：規格是主要產物。程式碼是它在某語言與框架的表達。維護軟體即演進規格。

**可執行規格**：規格必須足夠精確、完整、無歧義，以生成可運作系統。消除意圖與實作之間的落差。

**持續精煉**：一致性驗證是持續行為，不是一次 gate。AI 持續分析規格中的模糊、矛盾、缺口。

**研究驅動上下文**：研究代理持續蒐集技術選項、效能影響、組織約束。

**雙向回饋**：營運實際反饋規格演進。指標、事故、運維學習成為精煉輸入。

**分支探索**：從同一規格產生多個實作方法，探索不同最佳化目標——效能、可維護性、使用者體驗、成本。

## 實作途徑（Implementation Approaches）

今日要實踐 SDD，需組裝現有工具並維持流程紀律。方法學可藉以下方式實踐：

- AI 助手：迭代規格開發
- 研究代理：蒐集技術上下文
- 程式碼生成工具：將規格轉為實作
- 版本控制：適配規格優先工作流
- 一致性檢查：AI 分析規格文件

關鍵在於把規格視為真實來源，程式碼是服務規格的生成輸出。

## 透過 Claude Commands 精簡 SDD（Streamlining SDD with Claude Commands）

SDD 方法學透過兩個強力 Claude 指令大幅增強：自動化規格與規劃工作流。

### `new_feature` 指令

此指令將簡單功能描述（使用者提示）轉為完整結構化規格，並自動管理版本庫：

1. **自動功能編號**：掃描既有規格決定下一個功能編號（001, 002, 003 ...）
2. **建立分支**：從描述語義產生分支名稱並自動建立
3. **模板生成**：複製並客製化功能規格模板
4. **目錄結構**：建立 `specs/[branch-name]/` 目錄放置相關文件

### `generate_plan` 指令

當功能規格存在後，此指令建立完整實作計畫：

1. **規格分析**：理解功能需求、使用者故事、驗收標準
2. **憲章一致性**：確保符合專案憲章與架構原則
3. **技術轉譯**：將商務需求轉為架構與實作細節
4. **詳細文件**：產生資料模型、API 契約、測試情境文件
5. **手動測試計畫**：為每個使用者故事建立逐步驗證流程

### 範例：建立聊天功能（Chat Feature）

以下展示指令如何轉換傳統工作流：

**傳統作法：**
```
1. 撰寫 PRD 文件（2-3 小時）
2. 撰寫設計文件（2-3 小時）
3. 手動建立專案結構（30 分）
4. 撰寫技術規格（3-4 小時）
5. 建立測試計畫（2 小時）
總計：約 12 小時文件工作
```

**SDD 指令式作法：**
```bash
# 第 1 步：建立功能規格（約 5 分鐘）
/new_feature 具訊息歷史與使用者狀態的即時聊天系統

# 自動執行：
# - 建立分支 "003-chat-system"
# - 生成 specs/003-chat-system/feature-spec.md
# - 以結構化需求填入

# 第 2 步：生成實作計畫（約 10 分鐘）
/generate_plan WebSocket 實時訊息, PostgreSQL 儲存歷史, Redis 使用者線上狀態

# 自動產生：
# - specs/003-chat-system/implementation-plan.md
# - specs/003-chat-system/implementation-details/
#   - 00-research.md (WebSocket 函式庫比較)
#   - 02-data-model.md (Message / User schema)
#   - 03-api-contracts.md (WebSocket 事件, REST 端點)
#   - 06-contract-tests.md (訊息流程情境)
#   - 08-inter-library-tests.md (資料庫與 WebSocket 整合)
# - specs/003-chat-system/manual-testing.md
```

在 15 分鐘內，你擁有：
- 完整功能規格（含使用者故事與驗收標準）
- 詳細實作計畫（含技術選擇與理由）
- API 契約與資料模型，準備好生成程式碼
- 全面測試情境（自動化與手動）
- 正確版控於功能分支的所有文件

### 結構化自動化的力量

這些指令不只省時——它們強制一致性與完整性：

1. **不遺漏細節**：模板確保涵蓋非功能需求到錯誤處理
2. **決策可追溯**：每個技術選擇連結回特定需求
3. **活文件**：規格與程式碼保持同步，因為它們生成它
4. **快速迭代**：改需求、再生成計畫，只需分鐘不是天

指令透過將規格視為「可執行產物」而非靜態文件，體現 SDD 原則；它們將「寫規格」從必要之惡轉為驅動力。

### 模板驅動品質：結構如何約束 LLM 以獲得更佳結果

這些指令的真正力量，不僅在自動化，更在於模板如何引導 LLM 產生高品質規格。模板是精緻的提示（prompt），以有效方式約束輸出：

#### 1. 防止過早實作細節

功能規格模板明確指示：
```
- ✅ 聚焦使用者需要「什麼」與「為什麼」
- ❌ 避免「如何實作」（不寫技術棧 / API / 程式碼結構）
```
此限制迫使 LLM 保持適當抽象層級。避免從「使用者需要即時更新」過早墜落成「用 React + Redux 實作」。抽象層穩定，技術演進成本低。

#### 2. 強迫顯式不確定標記

兩個模板都強制使用 `[NEEDS CLARIFICATION]`：
```
建立規格時：
1. 標記所有模糊：用 [NEEDS CLARIFICATION: 具體問題]
2. 不要猜：缺資訊就標記
```
阻止 LLM 做「合理但可能錯誤」假設。例如「登入系統」若未指定認證型態，須標記：`[NEEDS CLARIFICATION: 未指定驗證方式 - Email/Password, SSO, OAuth?]`。

#### 3. 透過清單（checklists）促進結構化思考

模板內含全面檢查清單，像是規格的單元測試：
```
### 需求完整性
- [ ] 不剩 [NEEDS CLARIFICATION]
- [ ] 需求可測且無歧義
- [ ] 成功標準可衡量
```
清單迫使 LLM 系統化自我審查，捕捉原本易遺漏的缺口。

#### 4. 透過 Gate 強化憲章一致性

實作計畫模板用階段 gate 執行架構原則：
```
### Phase -1: Pre-Implementation Gates
#### Simplicity Gate (Article VII)
- [ ] ≤3 個專案？
- [ ] 無超前未證實設計？
#### Anti-Abstraction Gate (Article VIII)
- [ ] 直接使用框架？
- [ ] 單一模型表示？
```
若 gate 失敗，必須在「Complexity Tracking」紀錄理由，建立責任鏈。

#### 5. 階層化細節管理

模板強制資訊架構分層：
```
**IMPORTANT**: 主實作計畫保持高階與可讀。
詳細程式碼、演算法、技術細節放入 `implementation-details/`。
```
防止規格淪為「程式碼傾倒場」，維持主文件可瀏覽。

#### 6. 測試先行思維

實作模板強制測試優先：
```
### 建檔順序
1. 先建 `contracts/` 與 API 規格
2. 建測試：contract → integration → e2e → unit
3. 撰寫程式碼只為讓測試通過
```
確保先思考可測性與契約，再談實作。

#### 7. 防止投機功能

模板顯式禁止：
```
- [ ] 無「也許將來要」功能
- [ ] 各階段具明確前置與交付
```
避免膨脹，所有內容都需追溯到使用者故事及驗收標準。

### 複合效應

這些約束共同產出：
- **完整**：清單確保不遺漏
- **無歧義**：強制澄清標記
- **可測試**：測試優先嵌入流程
- **可維護**：正確抽象層與資訊結構
- **可實作**：清晰階段與具體交付

模板將 LLM 從「創作型寫手」轉為「紀律規格工程師」。

## 憲章基礎：強制架構紀律（The Constitutional Foundation）

SDD 的核心是一份「憲章」——一組不可變原則，治理規格如何成為程式碼。憲章（`base/memory/constitution.md`）是系統的架構 DNA，確保每次生成保持一致、簡潔、品質。

### 九大條款（Nine Articles）

憲章定義九條塑造流程的條款：

#### 第一條：Library-First 原則
每個功能必須以獨立函式庫開始——無例外：
```
Every feature in Specify MUST begin its existence as a standalone library. 
No feature shall be implemented directly within application code without 
first being abstracted into a reusable library component.
```
確保模組化、邊界清晰、依賴最小。

#### 第二條：CLI 介面義務
每個函式庫需透過 CLI 暴露能力：
```
All CLI interfaces MUST:
- Accept text as input (via stdin, arguments, or files)
- Produce text as output (via stdout)
- Support JSON format for structured data exchange
```
提升可觀察性與可測性；功能不被封裝於不透明類別。

#### 第三條：Test-First 強制
最具變革性的條款——無測試不寫碼：
```
This is NON-NEGOTIABLE: All implementation MUST follow strict Test-Driven Development.
No implementation code shall be written before:
1. Unit tests are written
2. Tests are validated and approved by the user
3. Tests are confirmed to FAIL (Red phase)
```
顛覆「先生程式碼後補測試」的 AI 習慣。

#### 第七與第八條：Simplicity 與 Anti-Abstraction
對抗過度設計：
```
Section 7.3: Minimal Project Structure
- Maximum 3 projects for initial implementation
- Additional projects require documented justification

Section 8.1: Framework Trust
- Use framework features directly rather than wrapping them
```
迫使任何抽象層次要有正當理由。

#### 第九條：Integration-First 測試
優先真實世界測試：
```
Tests MUST use realistic environments:
- Prefer real databases over mocks
- Use actual service instances over stubs
- Contract tests mandatory before implementation
```
確保產物實際可運行。

### 模板中的憲章執行

實作計畫模板將憲章操作化：
```markdown
### Phase -1: Pre-Implementation Gates
#### Simplicity Gate (Article VII)
- [ ] Using ≤3 projects?
- [ ] No future-proofing?

#### Anti-Abstraction Gate (Article VIII)
- [ ] Using framework directly?
- [ ] Single model representation?

#### Integration-First Gate (Article IX)
- [ ] Contracts defined?
- [ ] Contract tests written?
```
Gate 如同編譯期檢查：未通過需在「Complexity Tracking」理由化。

### 不可變原則的力量

不可變提供：
1. **時間一致性**：今日與未來生成遵循同一原則
2. **模型一致性**：不同 LLM 生成結果架構相容
3. **架構完整性**：每個功能加固整體設計
4. **品質保證**：Test-First、Library-First、Simplicity 促成可維護性

### 憲章演進

原則不可輕易改，但其應用可演進：
```
Section 4.2: Amendment Process
Modifications to this constitution require:
- Explicit documentation of the rationale for change
- Review and approval by project maintainers
- Backwards compatibility assessment
```
允許從實務學習精緻化而不失穩定。

### 超越規則：一種哲學

憲章不只是規則，而是一套生成哲學：
- **Observability Over Opacity**：所有行為可由 CLI 檢視
- **Simplicity Over Cleverness**：先簡單，再證實必要才加複雜
- **Integration Over Isolation**：用真實環境測試，不依賴人工隔離
- **Modularity Over Monoliths**：每個功能是獨立函式庫

透過將原則內嵌於規格與規劃，SDD 確保生成程式碼不只可用，更可維護、可測、架構健全。憲章將 AI 從「程式碼生成器」提升為尊重與加固設計的架構夥伴。

## 轉化（The Transformation）

這不是替代開發者或自動化創造力，而是放大人類能力：自動化機械翻譯，建立緊密回饋循環，使規格、研究、程式碼共同演進，每次迭代都讓意圖與實作更對齊。

軟體開發需要更好的工具來維持「意圖 ↔ 實作」對齊。SDD 透過可執行規格達成：規格不是指引程式碼，而是生成程式碼的來源。
