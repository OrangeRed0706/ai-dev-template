---
description: 審查 PR（不合併）
---

審查 PR: $ARGUMENTS

## 流程

1. **取得 PR 資訊**

   ```bash
   gh pr view <PR> --json number,title,state,isDraft,author,baseRefName,headRefName,files,additions,deletions
   ```

2. **讀 PR 描述**
   - 總結目標和範圍
   - 標出缺少的 context（動機、替代方案、風險）

3. **讀 diff**

   ```bash
   gh pr diff <PR>
   ```

4. **驗證變更價值**
   - 解決什麼使用者/開發者痛點？
   - 這是最小合理的修改嗎？
   - 有沒有引入不必要的複雜度？

5. **評估實作品質**
   - Correctness: edge cases, error handling, null/undefined
   - Design: 抽象/架構是否適當？
   - Performance: hot paths, allocations, N+1
   - Security: authz/authn, input validation, secrets

6. **檢查測試**
   - 有什麼測試覆蓋？
   - 缺少什麼測試？

7. **輸出報告**

   A) **TL;DR 建議**
   - READY FOR /landpr | NEEDS WORK | NEEDS DISCUSSION
   - 1-3 句理由

   B) **What changed**
   - 變更摘要

   C) **What's good**
   - 優點

   D) **Concerns**
   - 編號列表
   - 標記: BLOCKER | IMPORTANT | NIT
   - 每個提供具體修改建議

   E) **Tests**
   - 現有測試
   - 缺少的測試

   F) **Follow-ups**
   - 非阻塞的後續工作

## 規則

- 只審查，不合併
- 不切換 branch
- 不修改程式碼
