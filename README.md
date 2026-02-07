# AI-First Development Template

基於 Peter Steinberger（OpenClaw 作者）的 AI 開發理念。

> "I ship code I don't read." — Peter Steinberger

這不是說不在乎品質，而是把精力放在**架構設計和品質驗證**，讓 AI 處理實作。

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

### 3. Close the Loop — AI 自己驗證

AI 必須能跑 `build → test → lint`，失敗自己修。

---

## Planning First

Peter 花最多時間在規劃：

1. 提出問題/功能需求
2. 讓 AI 探索程式碼
3. 一起建立計畫
4. 挑戰、質疑、調整
5. 滿意後說 "build"

> "Plan mode feels like a hack that was necessary for older generations of models."

---

## Under-prompting

Peter 有時故意給模糊的 prompt，讓 AI 探索他沒想到的方向。

不用每次都寫得很詳細，有時候讓 AI 自己發揮會有意外收穫。

---

## 架構討論 > Code Review

Peter 跟團隊討論時，**只談架構和重大決策，不談程式碼細節**。

PR 變成 "Prompt Request" — 關心的是產生程式碼的 prompt，不是程式碼本身。

---

## 使用方式

1. 複製 `AGENTS.md` 到你的專案
2. 修改 build 指令和規則
3. 功能開發前先寫 design doc
4. 讓 AI 去做

## 檔案

```
AGENTS.md              # 專案規範（必須）
docs/design/
  TEMPLATE.md          # 設計文件範本
  example-auth.md      # 範例
```

---

## Peter 的原則

1. **Planning first** — 花時間規劃，滿意後才 build
2. **不看 code** — 只關心架構
3. **多 agent 並行** — 不同功能同時開發
4. **Local CI** — 不等遠端，agent 本地跑測試
5. **直接 commit main** — 不喜歡就讓 AI 改
6. **Under-prompt** — 有時給模糊 prompt 讓 AI 探索
7. **架構討論 > Code Review** — 只談設計不談細節

---

## 參考

- [The Pragmatic Engineer: The creator of Clawd](https://newsletter.pragmaticengineer.com/p/the-creator-of-clawd-i-ship-code)
- [Shipping at Inference-Speed](https://steipete.me/posts/2025/shipping-at-inference-speed)
- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
