# AGENTS.md — 專案開發規範

> 這份文件是給 AI agent 讀的專案手冊。
> 每次 session 開始時，AI 應該先讀這份文件。

## Project Structure

```
src/           # 主要原始碼
tests/         # 測試程式
docs/          # 文件
  design/      # 設計文件（帶 read_when）
  reference/   # 參考資料
scripts/       # 腳本工具
```

## Build Commands

```bash
# 安裝依賴
dotnet restore          # .NET
pnpm install            # Node.js
pip install -r requirements.txt  # Python

# 建置
dotnet build            # .NET
pnpm build              # Node.js

# 測試
dotnet test             # .NET
pnpm test               # Node.js

# Lint / Format
dotnet format --verify-no-changes  # .NET
pnpm lint               # Node.js
```

## Coding Style

- 使用專案既有的 style，不要引入新的 pattern
- 檔案不超過 500 行，太長就拆分
- 加註解解釋複雜邏輯
- 避免使用 `any`（TypeScript）或禁用 nullable（C#）

## Commit Guidelines

使用 Conventional Commits：

```
feat: 新功能
fix: 修 bug
docs: 文件更新
refactor: 重構
test: 測試
chore: 雜項
```

範例：
```
feat: add user authentication (#123)
fix: resolve login timeout issue (#456)
```

## PR Workflow

### Review Mode（只看不改）

```bash
gh pr view <PR> --json number,title,author,files
gh pr diff <PR>
```

- 不要切換 branch
- 不要修改程式碼
- 輸出結構化報告

### Land Mode（合併 PR）

1. `git checkout main && git pull`
2. 建立 temp branch
3. Checkout PR、rebase
4. 修問題、跑測試
5. 加 changelog
6. Commit（感謝 contributor）
7. `gh pr merge --squash` 或 `--rebase`
8. 留 PR comment

## Testing Guidelines

- 新功能要有對應測試
- 修 bug 要有 regression test
- 跑完測試再 commit：`dotnet test` / `pnpm test`

## Security

- 不要 commit 真實密碼、API key、connection string
- 用 environment variables 或 secret manager
- 測試用假資料，不要用真實使用者資料

## Multi-Agent Safety

當多個 AI agent 同時工作：

- 不要亂動 `git stash`
- 不要切換 branch（除非明確要求）
- 不要修改其他 agent 的檔案
- 只 commit 自己的改動

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

## Decisions (locked)

專案層級的已確定決策：

- [在這裡列出專案的重大決策]
- [例如：使用 PostgreSQL 作為主資料庫]
- [例如：API 使用 REST，不用 GraphQL]

---

*根據你的專案需求修改這份文件。*
