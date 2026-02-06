# AGENTS.md — 專案開發規範

> 這份文件是給 AI agent 讀的專案手冊。
> 每次 session 開始時，AI 應該先讀這份文件。

---

## Project Structure & Module Organization

```
src/               # 主要原始碼
  controllers/     # API controllers
  services/        # 商業邏輯
  models/          # 資料模型
  utils/           # 工具函數
tests/             # 測試程式
docs/              # 文件
  design/          # 設計文件（帶 read_when）
scripts/           # 腳本工具
```

根據你的專案調整上面的結構。

---

## Build, Test, and Development Commands

```bash
# 安裝依賴
dotnet restore              # .NET
pnpm install                # Node.js
pip install -r requirements.txt  # Python

# 建置
dotnet build                # .NET
pnpm build                  # Node.js

# 測試
dotnet test                 # .NET
pnpm test                   # Node.js

# Lint / Format
dotnet format --verify-no-changes  # .NET
pnpm lint && pnpm format    # Node.js

# 完整檢查（commit 前跑這個）
dotnet build && dotnet test && dotnet format --verify-no-changes  # .NET
pnpm build && pnpm lint && pnpm test  # Node.js
```

---

## Coding Style & Naming Conventions

- 使用專案既有的 style，不要引入新的 pattern
- 檔案不超過 **500 行**，太長就拆分
- 加註解解釋複雜邏輯
- 避免使用 `any`（TypeScript）或禁用 nullable warnings（C#）
- 優先使用既有的 helper functions，不要重複造輪子
- 命名要清楚，不要縮寫

---

## Commit & Pull Request Guidelines

### Commit Messages

使用 Conventional Commits：

```
feat: 新功能
fix: 修 bug
docs: 文件更新
refactor: 重構（不改變行為）
test: 測試
chore: 雜項（CI、build 等）
```

範例：
```
feat: add user authentication (#123)
fix: resolve login timeout issue (#456)
docs: update API documentation
```

### Scoped Commits

使用 `scripts/committer` 做 scoped commit，避免手動 `git add`：

```bash
./scripts/committer "feat: add login page" src/login.ts src/auth.ts
```

### PR Workflow

**Review Mode（只看不改）：**
```bash
gh pr view <PR> --json number,title,author,files
gh pr diff <PR>
```
- 不要切換 branch
- 不要修改程式碼
- 輸出結構化報告

**Land Mode（合併 PR）：**
1. `git checkout main && git pull`
2. 建立 temp branch：`git checkout -b temp/landpr-<PR>`
3. Checkout PR：`gh pr checkout <PR>`
4. Rebase：`git rebase temp/landpr-<PR>`
5. 修問題、跑測試
6. 加 changelog（感謝 contributor）
7. Commit（用 `scripts/committer`）
8. `gh pr merge --squash` 或 `--rebase`
9. 留 PR comment 說明做了什麼
10. 刪除 temp branch

### Changelog

- 每個 PR 都要有 changelog entry
- 格式：`Description ([#PR](url) by [@user](url))`
- 外部貢獻者要感謝

---

## Testing Guidelines

- 新功能要有對應測試
- 修 bug 要有 regression test
- 跑完測試再 commit
- 目標覆蓋率：70%+

---

## Security & Configuration

- **永遠不要 commit：**
  - 真實密碼、API key、connection string
  - 真實使用者資料
  - 真實電話號碼、email

- 用 environment variables 或 secret manager
- 測試用假資料

---

## Multi-Agent Safety

當多個 AI agent 同時工作：

- **不要**亂動 `git stash`
- **不要**切換 branch（除非明確要求）
- **不要**修改其他 agent 的檔案
- **只 commit 自己的改動**
- 看到不認識的檔案，繼續做自己的事

---

## Shorthand Commands

- `sync`: commit all → `git pull --rebase` → `git push`

---

## Design Documents

設計文件放在 `docs/design/`，使用 `read_when` 機制：

```yaml
---
summary: "功能描述"
read_when:
  - 實作這個功能時
  - 修改相關模組時
---
```

AI 會根據任務自動判斷要不要讀。

---

## Decisions (locked)

專案層級的已確定決策（AI 不要改這些）：

- [列出你的專案決策]
- [例如：使用 PostgreSQL 作為主資料庫]
- [例如：API 使用 REST，不用 GraphQL]
- [例如：認證用 JWT + Redis]

---

## Agent-Specific Notes

給 AI 的具體注意事項：

- **永遠不要**編輯 `node_modules` 或 `packages/`
- 回答問題時要**高信心**：在程式碼中驗證，不要猜測
- 修 bug 時要**讀相關程式碼**，不要只看 error message
- 加 feature 時要**考慮 edge cases**

---

## Troubleshooting

常見問題：

- [列出專案常見問題和解法]
- [例如：如果 build 失敗，先跑 `pnpm install`]
- [例如：如果測試失敗，確認 .env 設定正確]

---

*根據你的專案需求修改這份文件。*
