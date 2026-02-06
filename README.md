# AI-First Development Template

基於 OpenClaw 專案的 AI 開發模式模板，讓 AI agent 能有效率地協助開發。

## 核心概念

這個 template 的核心理念來自 Peter Steinberger（OpenClaw 作者）的開發方式：

1. **AGENTS.md** — 給 AI 讀的專案規範，每次 session 先讀這個
2. **Prompt Templates** — 預定義的工作流程（/reviewpr、/landpr 等）
3. **Design Docs** — 帶 `read_when` 的設計文件，AI 按需載入
4. **Decisions (locked)** — 已確定的決策，AI 不會質疑或改變

## 快速開始

1. 點擊 "Use this template" 建立新 repo
2. 根據你的專案修改 `AGENTS.md`
3. 在 `docs/design/` 新增設計文件
4. 開始用 AI agent 開發！

## 目錄結構

```
├── AGENTS.md              # 給 AI 讀的專案規範（必讀）
├── CLAUDE.md              # → symlink to AGENTS.md
├── CONTRIBUTING.md        # 貢獻指南
├── CHANGELOG.md           # 變更日誌
├── .pi/prompts/           # Prompt 指令
│   ├── reviewpr.md        # /reviewpr - 審查 PR
│   ├── landpr.md          # /landpr - 合併 PR
│   ├── issue.md           # /issue - 分析 issue
│   └── changelog.md       # /changelog - 審計 changelog
├── docs/
│   └── design/            # 設計文件（帶 read_when）
│       └── TEMPLATE.md    # 設計文件範本
├── scripts/
│   └── committer          # Scoped commit 腳本
└── .github/
    ├── workflows/ci.yml
    ├── PULL_REQUEST_TEMPLATE.md
    └── ISSUE_TEMPLATE/
```

## AGENTS.md

這是給 AI 讀的「專案開發手冊」，包含：

- **Project Structure** — 目錄結構說明
- **Build Commands** — 建置、測試、lint 指令
- **Coding Style** — 程式碼風格規範
- **Commit Guidelines** — Commit 訊息格式
- **PR Workflow** — Review mode vs Land mode
- **Testing Guidelines** — 測試規範
- **Security** — 安全規則
- **Multi-Agent Safety** — 多 AI 協作規則
- **Decisions (locked)** — 已確定的專案決策

## read_when 機制

設計文件開頭加入 YAML frontmatter：

```yaml
---
summary: "功能 X 的設計文件"
read_when:
  - 實作功能 X
  - 修改模組 Y
---
```

AI 會根據當前任務判斷要不要讀這份文件，節省 token。

## Decisions (locked)

在設計文件裡標註已確定的決策：

```markdown
## Decisions (locked)

- **資料庫:** PostgreSQL（不考慮 NoSQL）
- **API 風格:** REST（不用 GraphQL）
- **認證:** JWT + Redis session
```

AI 看到這些就不會再質疑或提出替代方案。

## Prompt Templates

`.pi/prompts/` 裡的模板讓 AI 可以執行標準化工作流程：

| 指令 | 用途 |
|------|------|
| `/reviewpr <PR>` | 審查 PR（不合併） |
| `/landpr <PR>` | 完整 PR 合併流程 |
| `/issue <issue>` | 分析 GitHub issue |
| `/changelog` | 審計 changelog entries |

## 設計文件結構

每份設計文件應包含：

| Section | 用途 |
|---------|------|
| **Goals** | 這次要達成什麼 |
| **Non-goals** | 這次不做什麼（防止過度設計）|
| **Decisions (locked)** | 已確定的決策 |
| **Key concepts** | 專有名詞定義 |
| **Config surface** | 設定項規格 |
| **Implementation phases** | 分步驟實作順序 |
| **Testing plan** | 要寫什麼測試 |

## 最佳實踐

1. **Goals + Non-goals** — 明確定義範圍
2. **Decisions (locked)** — 把已決定的事鎖起來
3. **Key concepts** — 統一術語
4. **Implementation phases** — 分步驟，不要一次改太多
5. **Testing plan** — 明確列出測試項目

## 參考資料

- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
- [The Pragmatic Engineer: The creator of Clawd](https://newsletter.pragmaticengineer.com/p/the-creator-of-clawd-i-ship-code)
- [Peter Steinberger: Shipping at Inference-Speed](https://steipete.me/posts/2025/shipping-at-inference-speed)

## License

MIT
