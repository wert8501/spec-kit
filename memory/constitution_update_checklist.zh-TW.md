# 憲章更新檢查清單（Constitution Update Checklist）

當修訂憲章（`/memory/constitution.md`）時，必須確保所有相依文件同步更新以維持一致性。

## 需要更新的模板（Templates to Update）

### 當新增/修改「任何」條款時：
- [ ] `/templates/plan-template.md` - 更新「憲章檢查」(Constitution Check) 區段
- [ ] `/templates/spec-template.md` - 若影響需求/範圍需更新
- [ ] `/templates/tasks-template.md` - 若新增任務類型需更新
- [ ] `/.claude/commands/plan.md` - 若規劃流程改變需更新
- [ ] `/.claude/commands/tasks.md` - 若任務生成受影響需更新
- [ ] `/CLAUDE.md` - 更新執行期（runtime）開發指引

### 條款（Article）專屬更新：

#### 第一條 (Library-First)：
- [ ] 確認模板強調「先建立函式庫」
- [ ] 更新 CLI 指令範例
- [ ] 加入 llms.txt 文件需求

#### 第二條 (CLI Interface)：
- [ ] 更新模板中 CLI 旗標需求
- [ ] 加入純文字 I/O 協議提醒

#### 第三條 (Test-First)：
- [ ] 更新所有模板中的測試順序
- [ ] 強調 TDD 要求
- [ ] 加入測試核准（approval）gate

#### 第四條 (Integration Testing)：
- [ ] 列出整合測試觸發條件
- [ ] 更新測試類型優先順序
- [ ] 加入使用真實依賴的要求

#### 第五條 (Observability)：
- [ ] 在模板加入日誌需求
- [ ] 包含多層日誌串流（前端→後端）
- [ ] 更新效能監控區段

#### 第六條 (Versioning)：
- [ ] 加入版本遞增提醒
- [ ] 包含破壞性變更程序
- [ ] 更新遷移（migration）需求

#### 第七條 (Simplicity)：
- [ ] 更新專案數量限制
- [ ] 加入禁止模式（pattern）示例
- [ ] 包含 YAGNI 提醒

## 驗證步驟（Validation Steps）

1. **提交憲章變更之前：**
   - [ ] 所有模板引用新需求
   - [ ] 範例已更新並符合新規則
   - [ ] 文件間無互相矛盾

2. **更新模板之後：**
   - [ ] 走一次示範實作計畫流程
   - [ ] 驗證所有憲章需求已被覆蓋
   - [ ] 確認模板「自給自足」（不用讀憲章也能理解）

3. **版本追蹤：**
   - [ ] 更新憲章版本號
   - [ ] 在模板頁尾標註版本
   - [ ] 在憲章歷史（history）新增修訂紀錄

## 常見遺漏（Common Misses）

請特別檢查這些常被遺漏的項目：
- 指令文件 (`/commands/*.md`)
- 模板中的檢查清單項目
- 範例程式/指令片段
- 領域特定差異（web vs mobile vs CLI）
- 文件間交叉引用（cross-references）

## 模板同步狀態（Template Sync Status）

最後同步檢查：2025-07-16  
- 憲章版本：2.1.1  
- 模板一致性：❌（缺少版本管理與可觀察性細節）

---

*此檢查清單確保憲章原則在所有專案文件中一致落實。*
