# AI-First Development Template

基於 Peter Steinberger（OpenClaw 作者）的 AI 開發理念。

> "I ship code I don't read." — Peter Steinberger

這不是說不在乎品質，而是把精力放在**架構設計和品質驗證**，讓 AI 處理實作。

---

## 核心概念：兩個 Loop

### 1. AI 的閉環（技術層）

```
AI 寫 code → AI 跑 build/test → 失敗 → AI 自己修 → 再跑 → 通過
```

讓 AI **自己驗證自己的工作**，不用你盯著看它編譯。

### 2. 人在 Loop 裡（決策層）

```
你提需求 → AI 提方案 → 你看/調整 → AI build → 你驗收
```

讓**你掌控方向**，不是讓 AI 自己決定做什麼。

### 合在一起

```
你：我想做 X
AI：我打算這樣做...
你：好，build
     ↓
   [AI 的閉環]
   AI 寫 code → 跑 test → 失敗 → 自己修 → 通過
     ↓
AI：做好了，測試通過
你：讓我看看... 不對，這裡改一下
AI：好，改了
你：OK，push
```

---

## 不需要的

- ❌ 複雜的 orchestration（如 Gastown 的 "slop town"）
- ❌ 讓 AI 跑 24 小時不管（Ralph loop = slop）
- ❌ 很多工具/框架
- ❌ 完美的 prompt

## 需要的

- ✅ 你的腦子（想清楚要做什麼）
- ✅ 跟 AI 對話（"let's discuss"）
- ✅ 能跑測試驗證結果

---

## 目錄結構

```
AGENTS.md                    # 專案規範（必須）
CLAUDE.md                    # → symlink to AGENTS.md
.pi/prompts/                 # 可呼叫的 AI 指令
  reviewpr.md                # /reviewpr - 審查 PR
  landpr.md                  # /landpr - 合併 PR
  issue.md                   # /issue - 分析 issue
  changelog.md               # /changelog - 審計 changelog
scripts/
  committer                  # Scoped commit 腳本
git-hooks/
  pre-commit                 # Pre-commit hook
.github/workflows/
  ci.yml                     # CI workflow 範本
docs/design/
  TEMPLATE.md                # 設計文件範本
  example-auth.md            # 範例
```

---

## 核心 Workflow

### 1. AGENTS.md — 讓 AI 知道規則

放在 repo 根目錄，告訴 AI：
- 怎麼 build/test/lint
- 程式碼風格
- 什麼不能做

### 2. Design Docs — 先想清楚再寫

每個功能寫設計文件，包含：
- **Goals** — 要做什麼
- **Non-goals** — 不做什麼（防止 AI 過度設計）
- **Decisions (locked)** — 已決定的事（AI 不會改）
- **Key concepts** — 專有名詞定義

### 3. Close the Loop — AI 自己驗證 (Local CI)

AI 必須能跑 `build → test → lint`，失敗自己修。

不等遠端 CI，本地跑。

---

## Planning First

Peter 花最多時間在規劃：

1. 提出問題/功能需求
2. 讓 AI 探索程式碼
3. 一起建立計畫（"let's discuss, give me options"）
4. 挑戰、質疑、調整
5. 滿意後說 "build"

> "Plan mode was a hack that Anthropic had to add because the model is so trigger friendly."  
> 新模型直接對話就好，不需要特別的 plan mode。

---

## PR = Prompt Request

Peter 把 PR 當作「意圖」：

- 不在乎程式碼品質
- 只看 PR 想達成什麼
- 自己用 AI 重建或 base on 別人的 PR

> "I see pull requests more often as a prompt request."

---

## 多 Agent 並行

Peter 同時跑多個 agent：

- 不用 worktree，直接 clone 多份 repo（project-1, project-2, project-3...）
- 像玩 RTS 遊戲一樣管理
- 做完就 push to main

> "If you only work on one, it's very hard to get into the zone because it's just too slow."

---

## 不要掉進 Agentic Trap

Peter 警告：

- 不要花太多時間做「讓 AI 更好的工具」
- 不要用複雜的 orchestration（MCP 等）
- 不要讓 AI 無人監督跑太久

> "You're not actually building something that really brings you forward. You just have this... you're just building tools."

---

## 怎麼學

- 要玩、要犯錯
- 不能只花一天評估就說 AI 不行
- 要理解 AI 怎麼思考

> "You need to play to understand how those little monsters work."

---

## Prompt 指令

`.pi/prompts/` 裡的指令讓 AI 執行標準化流程：

| 指令 | 用途 |
|------|------|
| `/reviewpr <PR>` | 審查 PR（不合併） |
| `/landpr <PR>` | 完整 PR 合併流程 |
| `/issue <issue>` | 分析 GitHub issue |
| `/changelog` | 審計 changelog entries |

---

## 工具

### scripts/committer

Scoped commit — 只 commit 指定的檔案：

```bash
./scripts/committer "feat: add login" src/login.ts src/auth.ts
```

多 agent 協作時避免意外 commit 其他人的改動。

### git-hooks/pre-commit

安裝：
```bash
ln -sf ../../git-hooks/pre-commit .git/hooks/pre-commit
```

---

## 使用方式

1. 複製這個 template 到你的專案
2. 修改 `AGENTS.md` 的 build 指令
3. 修改 `.github/workflows/ci.yml`
4. 功能開發前先寫 design doc
5. 讓 AI 去做

---

## 參考

- [The Pragmatic Engineer: The creator of Clawd](https://newsletter.pragmaticengineer.com/p/the-creator-of-clawd-i-ship-code)
- [Shipping at Inference-Speed](https://steipete.me/posts/2025/shipping-at-inference-speed)
- [YouTube: How OpenClaw's Creator Uses AI](https://www.youtube.com/watch?v=AcwK1Uuwc0U)
- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
