# AI-First Development Template

基於 Peter Steinberger（OpenClaw 作者）的 AI 開發理念。

> "I ship code I don't read." — Peter Steinberger

## 核心理念

Peter 的開發方式只有三個核心：

### 1. AGENTS.md — 讓 AI 知道規則

告訴 AI：
- 怎麼 build/test
- 程式碼風格
- 什麼不能做

### 2. Design Docs — 先想清楚再寫

每個功能寫設計文件：
- **Goals** — 要做什麼
- **Non-goals** — 不做什麼（防止 AI 過度設計）
- **Decisions (locked)** — 已決定的事（AI 不會改）

### 3. Close the Loop — AI 自己驗證

AI 必須能跑 `build → test → lint`，失敗自己修。

---

## 使用方式

1. 複製 `AGENTS.md` 到你的專案
2. 根據專案修改 build 指令和規則
3. 功能開發前先寫 design doc
4. 讓 AI 去做

## 檔案說明

```
AGENTS.md              # 專案規範（必須）
docs/design/           # 設計文件
  TEMPLATE.md          # 設計文件範本
  example-auth.md      # 範例：認證功能
```

## Peter 的開發原則

1. **Planning first** — 花時間跟 AI 討論計畫，滿意後才 build
2. **不看 code** — 只關心架構，不關心實作細節
3. **同時跑多個 agent** — 不同功能並行開發
4. **Local CI** — 不等遠端 CI，agent 本地跑測試
5. **直接 commit main** — 不喜歡就讓 AI 改

## 參考

- [The Pragmatic Engineer Podcast](https://newsletter.pragmaticengineer.com/p/the-creator-of-clawd-i-ship-code)
- [Shipping at Inference-Speed](https://steipete.me/posts/2025/shipping-at-inference-speed)
- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
