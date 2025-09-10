# 功能規格： [FEATURE NAME]

**功能分支**: `[###-feature-name]`  
**建立時間**: [DATE]  
**狀態**: Draft  
**輸入**: 使用者描述: "$ARGUMENTS"

## 執行流程 (main)
```
1. 從輸入解析使用者描述
   → 若為空：ERROR "No feature description provided"
2. 從描述擷取關鍵概念
   → 辨識：角色(actors)、動作(actions)、資料(data)、限制(constraints)
3. 對每個不清楚處：
   → 標記 [NEEDS CLARIFICATION: specific question]
4. 填寫「使用者情境與測試」區段
   → 若無明確使用者流程：ERROR "Cannot determine user scenarios"
5. 產生功能需求 (Functional Requirements)
   → 每項需求必須可測
   → 標記模糊需求
6. 辨識關鍵實體（若涉及資料）
7. 執行檢查清單 (Review Checklist)
   → 若存在 [NEEDS CLARIFICATION]：WARN "Spec has uncertainties"
   → 若出現實作細節：ERROR "Remove tech details"
8. Return: SUCCESS (spec ready for planning)
```

---

## ⚡ 快速指引
- ✅ 聚焦使用者需要「什麼」與「為什麼」
- ❌ 避免「如何實作」（不寫技術棧、API、程式碼結構）
- 👥 面向商務利害關係人（非開發者）

### 區段要求 (Section Requirements)
- **必填區段**：每個功能都需完成
- **可選區段**：僅在相關時包含
- 不適用的區段直接移除（不要留 "N/A"）

### AI 生成守則
從使用者提示生成本規格時：
1. **標記所有模糊處**：對任何需要假設的地方使用 [NEEDS CLARIFICATION: 具體問題]
2. **不要猜**：若提示未指明（例如登入方式），就標記
3. **像測試者思考**：每個模糊需求在「可測且無歧義」檢查應失敗
4. **常見欠明處**：
   - 使用者型態與權限
   - 資料保留／刪除政策
   - 效能與規模目標
   - 錯誤處理行為
   - 整合需求
   - 安全／合規需求

---

## 使用者情境與測試 *(必填)*

### 主要使用者故事 (Primary User Story)
[用淺白語言描述主線旅程]

### 驗收情境 (Acceptance Scenarios)
1. **Given** [初始狀態], **When** [動作], **Then** [預期結果]
2. **Given** [初始狀態], **When** [動作], **Then** [預期結果]

### 邊界情境 (Edge Cases)
- 當 [邊界條件] 時會如何？
- 系統如何處理 [錯誤情境]？

## 需求 *(必填)*

### 功能性需求 (Functional Requirements)
- **FR-001**: 系統必須 [明確能力，如「允許使用者建立帳號」]
- **FR-002**: 系統必須 [明確能力，如「驗證電子郵件格式」]  
- **FR-003**: 使用者必須能 [互動，如「重設密碼」]
- **FR-004**: 系統必須 [資料要求，如「保存使用者偏好」]
- **FR-005**: 系統必須 [行為，如「記錄所有安全事件」]

*模糊需求示例：*
- **FR-006**: 系統必須驗證使用者身分 [NEEDS CLARIFICATION: 未指定驗證方式 - email/password, SSO, OAuth?]
- **FR-007**: 系統必須保留使用者資料 [NEEDS CLARIFICATION: 未指定保留期間]

### 關鍵實體 (Key Entities) *(若功能涉及資料則包含)*
- **[Entity 1]**: [其代表意義，主要屬性，不含實作]
- **[Entity 2]**: [其代表意義，與其他實體關係]

---

## 檢查與驗收清單 (Review & Acceptance Checklist)
*GATE: main() 執行時自動檢查*

### 內容品質 (Content Quality)
- [ ] 無實作細節（語言、框架、API）
- [ ] 聚焦使用者價值與商務需求
- [ ] 為非技術利害關係人撰寫
- [ ] 所有必填區段已完成

### 需求完整性 (Requirement Completeness)
- [ ] 無殘留 [NEEDS CLARIFICATION]
- [ ] 需求可測且無歧義  
- [ ] 成功標準可衡量
- [ ] 範圍與邊界清楚
- [ ] 已標記依賴與假設

---

## 執行狀態 (Execution Status)
*main() 處理時更新*

- [ ] 使用者描述已解析
- [ ] 關鍵概念已擷取
- [ ] 模糊處已標記
- [ ] 使用者情境已定義
- [ ] 功能需求已生成
- [ ] 實體已辨識
- [ ] 檢查清單通過

---
