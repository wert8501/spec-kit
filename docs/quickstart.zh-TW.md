# 快速開始指南 (Quick Start Guide)

本指南將協助你使用 Spec Kit 進入規格驅動開發（Spec-Driven Development, SDD）。

## 四步驟流程 (4-Step Process)

### 1. 安裝 Specify

依你使用的 AI 程式代理（coding agent）初始化專案：

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>
```

### 2. 建立規格（Specification）

使用 `/specify` 指令描述你想建構的功能。專注於 **做什麼 (WHAT)** 與 **為什麼 (WHY)**，不要描述技術棧。

```bash
/specify Build an application that can help me organize my photos in separate photo albums. Albums are grouped by date and can be re-organized by dragging and dropping on the main page. Albums are never in other nested albums. Within each album, photos are previewed in a tile-like interface.
```

### 3. 建立技術實作計畫（Implementation Plan）

使用 `/plan` 指令提供技術棧與架構選擇。

```bash
/plan The application uses Vite with minimal number of libraries. Use vanilla HTML, CSS, and JavaScript as much as possible. Images are not uploaded anywhere and metadata is stored in a local SQLite database.
```

### 4. 拆解並實作

使用 `/tasks` 產生可執行的任務清單，然後請你的代理開始實作功能。

## 詳細範例：建立 Taskify

以下是一個建立團隊生產力平台的完整範例：

### 步驟 1：用 `/specify` 定義需求

```text
Develop Taskify, a team productivity platform. It should allow users to create projects, add team members,
assign tasks, comment and move tasks between boards in Kanban style. In this initial phase for this feature,
let's call it "Create Taskify," let's have multiple users but the users will be declared ahead of time, predefined.
I want five users in two different categories, one product manager and four engineers. Let's create three
different sample projects. Let's have the standard Kanban columns for the status of each task, such as "To Do,"
"In Progress," "In Review," and "Done." There will be no login for this application as this is just the very
first testing thing to ensure that our basic features are set up. For each task in the UI for a task card,
you should be able to change the current status of the task between the different columns in the Kanban work board.
You should be able to leave an unlimited number of comments for a particular card. You should be able to, from that task
card, assign one of the valid users. When you first launch Taskify, it's going to give you a list of the five users to pick
from. There will be no password required. When you click on a user, you go into the main view, which displays the list of
projects. When you click on a project, you open the Kanban board for that project. You're going to see the columns.
You'll be able to drag and drop cards back and forth between different columns. You will see any cards that are
assigned to you, the currently logged in user, in a different color from all the other ones, so you can quickly
see yours. You can edit any comments that you make, but you can't edit comments that other people made. You can
delete any comments that you made, but you can't delete comments anybody else made.
```

### 步驟 2：精煉規格

初始規格建立後，補充缺失需求：

```text
For each sample project or project that you create there should be a variable number of tasks between 5 and 15
tasks for each one randomly distributed into different states of completion. Make sure that there's at least
one task in each stage of completion.
```

也驗證規格檢查清單：

```text
Read the review and acceptance checklist, and check off each item in the checklist if the feature spec meets the criteria. Leave it empty if it does not.
```

### 步驟 3：使用 `/plan` 生成技術計畫

明確你的技術棧與技術需求：

```text
We are going to generate this using .NET Aspire, using Postgres as the database. The frontend should use
Blazor server with drag-and-drop task boards, real-time updates. There should be a REST API created with a projects API,
tasks API, and a notifications API.
```

### 步驟 4：驗證並實作

讓 AI 代理稽核實作計畫：

```text
Now I want you to go and audit the implementation plan and the implementation detail files.
Read through it with an eye on determining whether or not there is a sequence of tasks that you need
to be doing that are obvious from reading this. Because I don't know if there's enough here.
```

最後實作解決方案：

```text
implement specs/002-create-taskify/plan.md
```

## 關鍵原則 (Key Principles)

- **明確**：清楚描述你要建什麼以及為什麼
- **規格階段不談技術棧**
- **迭代精煉** 規格後再實作
- **驗證計畫** 才開始寫程式碼
- **讓 AI 代理處理** 實作細節

## 下一步 (Next Steps)

- 閱讀完整方法學以獲得進階指引
- 查看版本庫中的更多範例
- 在 GitHub 探索原始碼
