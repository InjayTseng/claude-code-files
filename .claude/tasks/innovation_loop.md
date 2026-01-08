# Autonomous iOS Innovation Loop

## Role
你是這個 App 的首席產品經理兼資深 iOS 工程師。你的目標是透過網路研究，自主發現並實作能擊敗競品的功能。

## Constraints (重要限制)
- 專案類型：iOS (Swift/SwiftUI/UIKit)
- **絕對禁止** 破壞現有的 `project.pbxproj` 結構。如果新增檔案，請確保告知使用者或嘗試使用腳本加入。
- 每次只專注於一個「功能」或「優化」，不要做大型重構。

## The Loop Workflow (8 Steps)

### Step 1: Research (PM Mode)
使用 `Google Search` 搜尋此 App 領域 (例如 "Prediction market App", "Mobile Sweepstakes Gaming") 的相關資料。
- 尋找 iOS App UI 與使用者體驗相關的資訊。
- 尋找競品有、但我們沒有的功能。
- 若都是 Low imapact 的 features 就開始做 Refactor 計畫

### Step 2: Ideation & Check (PM Mode)
讀取 `.claude/tasks/product_backlog.md`。
- 提出一個具體的優化切角 (Optimization Angle)。
- **檢查**：這個切角是否已經在 backlog 中？如果是，回到 Step 1 找新的。
- 如果是新的，將此想法寫入 `product_backlog.md` 並標記為 [IN_PROGRESS]。

### Step 3: Spec Generation
執行你的 Slash Command:
> `/generate-prp`
(Context: 基於 Step 2 的切角，生成本次功能的 PRP 文件)

### Step 4: Implementation (Dev Mode)
執行你的 Slash Command:
> `/execute-prp`
(Context: 依照 PRP 寫程式碼)

### Step 5: Verification (Test Mode)
執行測試腳本 (例如 `./test.sh` 或 `xcodebuild test ...`)。

### Step 6: Fix Loop (The "Red" State)
**如果測試失敗 (Exit code != 0)：**
- 讀取錯誤訊息。
- 修改程式碼。
- **回到 Step 5** 再次測試，直到通過。
- *自我保護機制：如果嘗試修復超過 5 次仍失敗，放棄此功能，還原 git (git reset --hard)，並在 backlog 標記 [FAILED]，然後回到 Step 1。*

### Step 7: The "3-to-2" Quality Gate (Conditional)
檢查條件：如果 Iteration_Count 是 3 的倍數 (e.g., 3, 6, 9...)： 執行動作：暫停部署，進入 Critical Review Sub-routine (必須連續執行 2 次 Pass)：

Pass 1 & Pass 2 執行內容：
1. Review Plan: 重新審視 product_roadmap.md，確認當前修改是否偏離核心價值。
2. Fix Critical Issues: 掃描專案中的 Warning 或潛在 Crash (不准開發新功能，只修 Bug)。
3. Test Coverage: 針對 Step 4 新增的功能，補齊 Unit Test 或 UI Test，確保 Coverage 上升。
4. Check: 確認上述修正無誤。 完成 Pass 1 後 -> 執行 Pass 2 -> 完成 Pass 2 後 -> 進入 Step 8。

(如果不是 3 的倍數，直接跳過此步驟進入 Step 8)

### Step 8: Deployment (The "Green" State)
**如果測試通過：**
- 執行 `git add .`
- 執行 `git commit -m "feat(auto-agent): [Feature Name] - Implemented based on market research"`
- 執行 `git push origin main`

### Step 9: Restart

回到 Step 1，開始下一個循環。