---
description: 分析 GitHub issue
---

分析 issue: $ARGUMENTS

## 流程

1. **讀 issue 全文**
   - 包含所有 comments
   - 包含連結的 issues/PRs

2. **Bug 的話**
   - 忽略 issue 裡的 root cause 分析（通常是錯的）
   - 完整讀相關程式碼（不要截斷）
   - 追蹤程式碼路徑，找出真正的 root cause
   - 提出修正方案

3. **Feature request 的話**
   - 完整讀相關程式碼
   - 提出最簡潔的實作方式
   - 列出需要修改的檔案

## 規則

- 除非明確要求，不要實作
- 只分析和提案
- 高信心回答：在程式碼中驗證，不要猜測
