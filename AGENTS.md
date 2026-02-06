# AGENTS.md

> 這份文件給 AI 讀。每次 session 開始先讀這個。

## Build & Test

```bash
# [根據你的專案修改]
pnpm install
pnpm build
pnpm test
pnpm lint
```

**規則：commit 前必須通過 `build && test && lint`**

## 程式碼風格

- 用專案既有的 pattern，不要發明新的
- 檔案不超過 500 行
- 複雜邏輯加註解

## 不能做的事

- 不要 commit 密碼、API key
- 不要猜測，在 code 裡驗證再回答
- 不要切換 branch（除非明確要求）
- 不要改其他 agent 的檔案

## 設計文件

功能開發前先讀 `docs/design/` 裡的相關文件。

設計文件裡的 `Decisions (locked)` 是已確定的決策，不要改。

## 專案決策 (locked)

[列出你專案的重大決策，AI 不會質疑這些]

- 例如：使用 PostgreSQL
- 例如：API 用 REST
- 例如：認證用 JWT

---

*根據你的專案修改這份文件*
