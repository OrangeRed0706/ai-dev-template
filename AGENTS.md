# AGENTS.md

> 給 AI 讀的專案規範。每次 session 開始先讀這個。

## Build & Test

```bash
# [根據你的專案修改]
pnpm install
pnpm build
pnpm test
pnpm lint
```

**規則：commit 前必須通過 `build && test && lint`**

如果失敗，自己修，不要問人。

## 程式碼風格

- 用專案既有的 pattern，不要發明新的
- 檔案不超過 500 行
- 複雜邏輯加註解

## 不能做的事

- 不要 commit 密碼、API key
- 不要猜測，在 code 裡驗證再回答
- 不要切換 branch（除非明確要求）
- 不要改其他 agent 的檔案
- 不要問不必要的問題，先試著解決

## 設計文件

功能開發前先讀 `docs/design/` 裡的相關文件。

每份設計文件開頭有 `read_when`，告訴你什麼情況要讀：

```yaml
---
summary: "User authentication"
read_when:
  - 實作認證功能
  - 修改登入流程
---
```

設計文件裡的 **Decisions (locked)** 是已確定的決策，不要改、不要質疑。

## Planning First

開始寫 code 前，先確認：

1. 有沒有相關的設計文件？
2. Goals 和 Non-goals 是什麼？
3. 有哪些 Decisions (locked)？

如果設計文件不存在或不清楚，先問人，不要自己亂做。

## 專案決策 (locked)

[列出你專案的重大決策]

- 例如：使用 PostgreSQL
- 例如：API 用 REST
- 例如：認證用 JWT

---

*根據你的專案修改這份文件*
