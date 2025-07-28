# 🌟 規格驅動開發 (SDD) 工作流程

[English](README.md)

本文檔概述了 **規格驅動開發 (Specification-Driven Development, SDD)** 的工作流程，這是一種使用 Claude Code、AWS Kiro 和 Roo Code 等代理開發工具來建構軟體的結構化方法。SDD 將開發過程分為三個不同的階段：**指導架構師 (Steering Architect)**、**規劃 (Planning)** 和 **執行 (Execution)**。這種關注點分離的方式有助於快速生成高品質的程式碼，同時增強了清晰度、可維護性和可追溯性。

---

## 🚀 SDD 工作流程概覽

SDD 工作流程包含三個連續的階段：

1.  **🧭 指導架構師模式 (Steering Architect Mode)**：定義專案的高階規則、產品願景、技術棧和整體架構。
2.  **🗂️ 規劃模式 (Planning Mode)**：協作創建詳細的功能規格，包括需求、設計文件和可執行的任務。
3.  **⚡ 執行模式 (Execution Mode)**：以原子方式實現定義的任務，驗證其正確性，並逐步更新程式碼庫和文件。

每個階段都由專門的代理工具和上下文文件支持，以在整個開發生命週期中強制執行紀律並最大限度地減少模糊性。

---

## 1. 🧭 指導架構師模式 (Steering Architect Mode)

**職責：**
- 分析現有程式碼庫（如果有的話）以建立基準。
- 生成或更新基礎規則文件（例如，在 `.ai-rules/` 目錄中）。
- 記錄產品願景、技術棧、文件夾結構和專案級別的架構規則。

**產出物：**
- `.ai-rules/product.md`：描述產品的用途、功能和目標受眾。
- `.ai-rules/tech.md`：指定要使用的程式語言、框架和函式庫。
- `.ai-rules/structure.md`：定義專案的目錄佈局和文件組織。

---

## 2. 🗂️ 規劃模式 (Planning Mode)

**步驟：**
- **定義需求**：使用用戶故事、場景或 EARS (Event-Action-Response-State) 等方法來引出和記錄需求。
- **設計解決方案**：為模組、API 和互動序列創建高階設計。
- **分解任務**：將設計分解為小的、可管理的任務，並分析它們的依賴關係。

**規格文件夾結構：**
為每個功能創建一個專用文件夾來存放其規格：
```text
specs/
  └── feature-name/
      ├── requirements.md
      ├── design.md
      └── tasks.md
```

**協作完善：**
與 AI 代理進行對話，以完善和澄清想法。代理應提出有針對性的問題（每個功能通常 3-5 個），從廣泛的概念轉向精確的規格，確保最終的規格文件全面而清晰。

---

## 3. ⚡ 執行模式 (Execution Mode)

在執行模式下，代理充當專注的編碼助手。它系統地讀取 `tasks.md` 文件，並以 **測試驅動開發 (Test-Driven Development, TDD)** 為重點生成增量程式碼變更，以確保功能性和可靠性。該代理遵循敏捷的 DevOps 實踐，交付符合專案需求並保持高品質程式碼的、小的、可驗證的改進。它還處理文件更新，確保程式碼和文件保持同步。

### 詳細工作流程：
1.  **識別任務**：打開 `tasks.md` 並選擇第一個未勾選 (`[ ]`) 的任務。
2.  **理解任務**：閱讀任務描述並參考相應的 `design.md` 和 `requirements.md` 以獲得完整的上下文。
3.  **實現與記錄**：應用單一的、原子的程式碼變更來僅解決當前任務。在編寫程式碼時，更新相關文件（例如，內文註釋、用戶指南、API 文件）。
4.  **驗證**：遵循任務中定義的驗收標準或測試說明。
5.  **反思**：在「規則與提示」中記錄任何專案範圍內的學習或新建立的模式，以確保一致性。
6.  **更新狀態**：
    - 如果自動化測試通過，將任務標記為完成：`[x]`。
    - 如果是手動驗證或不存在測試，則總結變更並要求用戶確認功能（除非在自主模式下運行）。確認後，將任務標記為 `[x]`。
    - 在開發日誌中總結所有變更，例如 `./dev-log/<yyyymmdd>.md`。
    - 在主要任務完成後，如果適用，運行任何文件構建命令。

### 並行功能開發：
功能可以並行開發，而每個功能內的任務則按順序執行。這有助於高效協作和更快的交付。有關異步本地編碼工作流程的更多信息，請參閱 [Asynchronous Coding on Local with Git Worktree](https://gist.github.com/jackyko1991/deb71662444b021c28f38e22c40be53d)。

---

## 4. 🤖 設定 SDD 代理

本節提供有關配置 Claude Code 和 Roo Code 等代理工具使用 SDD 方法與子代理或模式的說明。如有翻譯用語分歧以英文版本為準。

### 代理提示 (Agent Prompts)
每個模式的大語言模型提示(LLM Prompt)對於指導 AI 至關重要。
- [指導架構師模式提示 (Steering Architect)](steering-architect-prompt.md)
- [規劃模式提示 (Planning)](planning-mode-prompt.md)
- [執行模式提示 (Execution)](execution-mode-prompt.md)

### Claude Code 設定
1.  在 Claude Code 中使用 `/agents` 命令並選擇 `Create new agent`。
2.  選擇 `Personal (~/.claude/agents/)` 以供全域使用，或選擇 `Project (.claude/agents)` 以供專案特定使用。
3.  選擇 `Manual configuration`。
4.  將代理類型（標識符）設置為 `steering-architect`、`planning-mode` 或 `execution-mode`。
5.  從上面的連結中複製相應的系統提示。
6.  從提示文件的標題中複製子代理的描述。
7.  允許代理使用 `All tools`。
8.  為代理設置顏色或保留為自動。
9.  保存新代理。
10. 使用類似以下的提示來使用代理：`Use @steering-architect to create project guidance for a Python library.`

### Roo Code 設定
1.  前往 `Modes` -> `Mode Settings` -> `Create New Mode`。
2.  提供模式名稱，例如 `🧭 Steering Architect`、`🗂️ Planning` 或 `⚡ Execution`。
3.  選擇 `Global` 作為保存位置，或選擇 `Project-specific` 以供本地使用。
4.  對於 `Role Definition`，從上面的連結中複製相應的提示。
5.  對於 `Short description (for humans)`，從提示文件的標題中複製描述。
6.  對於 `When to Use`，從提示文件的標題中複製 `when_to_use` 指南。將 `Available Tools` 和 `Custom Instructions` 保持不變。
7.  保存新模式。
8.  切換到相應的模式，並使用類似以下的提示：`Create project guidance for a Python library project.`

---

## ✅ SDD 的最佳實踐

1.  **保持關注點分離**：嚴格遵守每個階段的職責。
2.  **創建原子任務**：確保任務是小的、獨立的且可測試的。
3.  **使用上下文文件**：始終參考規格文件進行每次變更，以保持一致性。
4.  **包含驗證步驟**：每個任務都應有明確的驗收標準。
5.  **迭代規格**：根據從實現中學到的經驗來完善規格。
6.  **保持文件最新**：定期更新規則和文件以反映專案的演變。


---

## 🔬 將 SDD 應用於科學數據分析

有關將 SDD 方法論應用於科學數據分析和研究的指導，請參閱此處的詳細指南：[將 SDD 應用於科學數據分析](scientific-application.zh-Hant.md)

---

## 結論

這份精簡的教程為結構化、可追溯和可維護的軟體開發提供了一個強大的框架。通過在 SDD 方法論中利用代理工具，團隊可以以更快的速度、更高的紀律和更好的品質來建構複雜的系統。

## 參考資料
- [Kiro and the future of AI spec-driven software development](https://kiro.dev/blog/kiro-and-the-future-of-software-development/)
- [Claude Code Sub Agents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- https://www.aivi.fyi/aiagents/introduce-Sub-agents