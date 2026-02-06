# AI-First Development Template

一個基於 OpenClaw 專案的 AI 開發模式模板，讓你可以快速建立 AI-friendly 的專案結構。

## 快速開始

1. 點擊 "Use this template" 建立新 repo
2. 根據你的專案修改 `AGENTS.md`
3. 填寫 `workspace/` 裡的 agent 設定檔
4. 開始用 AI agent 開發！

## 目錄結構

```
├── AGENTS.md              # 給 AI 讀的專案規範（必讀）
├── .pi/prompts/           # 可呼叫的 prompt 指令
├── docs/
│   ├── design/            # 設計文件（帶 read_when）
│   └── reference/         # 參考資料
├── workspace/             # Agent 人格設定
│   ├── SOUL.md            # Agent 的價值觀
│   ├── IDENTITY.md        # Agent 的身份
│   ├── USER.md            # 使用者資訊
│   ├── TOOLS.md           # 工具筆記
│   ├── BOOTSTRAP.md       # 第一次啟動儀式
│   ├── HEARTBEAT.md       # 定期檢查任務
│   └── MEMORY.md          # 長期記憶
└── memory/                # 每日記憶 (YYYY-MM-DD.md)
```

## 核心概念

### AGENTS.md

這是給 AI 讀的「專案開發手冊」，包含：
- 專案結構
- Build 指令
- Coding style
- Commit 規範
- PR 流程
- 安全規則

### read_when 機制

設計文件開頭加入：

```yaml
---
summary: "功能 X 的設計文件"
read_when:
  - 實作功能 X
  - 修改模組 Y
---
```

AI 會根據任務自動判斷要不要讀這份文件。

### Decisions (locked)

在設計文件裡明確標註已確定的決策：

```markdown
## Decisions (locked)

- 使用 Redis 做 cache
- API 版本用 URL path（/v1/...）
- 不支援 legacy 格式
```

AI 看到這些就不會再質疑或改變。

## 使用方式

### 1. 設定專案規範

編輯 `AGENTS.md`，根據你的專案調整：
- 目錄結構
- Build 指令
- Coding style
- 安全規則

### 2. 設定 Agent 人格

編輯 `workspace/` 裡的檔案：
- `SOUL.md` — 定義 agent 的行為準則
- `IDENTITY.md` — 給 agent 一個名字和個性
- `USER.md` — 記錄你的偏好

### 3. 新增設計文件

在 `docs/design/` 新增功能設計文件：

```markdown
---
summary: "User authentication 重構"
read_when:
  - 實作認證功能
  - 修改登入流程
---

# User Authentication

## Goals
- ...

## Non-goals
- ...

## Decisions (locked)
- ...
```

### 4. 新增 Prompt 指令

在 `.pi/prompts/` 新增可呼叫的指令：

```markdown
---
description: 審查 PR
---

審查 PR: $ARGUMENTS

1. 讀 PR 描述和 diff
2. 檢查 correctness, design, performance
3. 輸出結構化報告
```

## 最佳實踐

1. **Goals + Non-goals** — 明確定義要做什麼、不做什麼
2. **Decisions (locked)** — 已確定的決策放這裡，AI 不會改
3. **Key concepts** — 定義專有名詞，統一術語
4. **Implementation phases** — 分步驟實作，不要一次改太多
5. **Testing plan** — 明確列出要寫什麼測試

## 參考資料

- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
- [Peter Steinberger: Shipping at Inference-Speed](https://steipete.me/posts/2025/shipping-at-inference-speed)
- [The Pragmatic Engineer: The creator of Clawd](https://newsletter.pragmaticengineer.com/p/the-creator-of-clawd-i-ship-code)

## License

MIT
