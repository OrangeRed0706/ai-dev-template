---
description: 合併 PR（完整流程）
---

合併 PR: $ARGUMENTS

## 流程

1. **確認 repo 乾淨**

   ```bash
   git status
   ```

2. **取得 PR 資訊**

   ```bash
   gh pr view <PR> --json number,title,author,headRefName,baseRefName
   contrib=$(gh pr view <PR> --json author --jq .author.login)
   head=$(gh pr view <PR> --json headRefName --jq .headRefName)
   ```

3. **更新 main**

   ```bash
   git checkout main
   git pull --ff-only
   ```

4. **建立 temp branch**

   ```bash
   git checkout -b temp/landpr-<PR>
   ```

5. **Checkout PR**

   ```bash
   gh pr checkout <PR>
   ```

6. **Rebase 到 temp branch**

   ```bash
   git rebase temp/landpr-<PR>
   ```
   - 解決 conflicts
   - 保持 history 整潔

7. **修問題 + 測試 + Changelog**
   - 實作修正
   - 加/調整測試
   - 更新 CHANGELOG.md，提及 `#<PR>` + `@$contrib`

8. **跑完整測試**（commit 前）

   ```bash
   dotnet test        # .NET
   pnpm test          # Node.js
   ```

9. **Commit**

   ```bash
   git add .
   git commit -m "fix: <summary> (#<PR>) (thanks @$contrib)"
   ```

10. **Push 更新後的 PR branch**

    ```bash
    git push --force-with-lease origin HEAD:<head>
    ```

11. **合併 PR**

    ```bash
    gh pr merge <PR> --squash   # 或 --rebase
    ```

12. **同步 main**

    ```bash
    git checkout main
    git pull --ff-only
    ```

13. **留 PR comment**

    ```bash
    gh pr comment <PR> --body "Landed!

    - Gate: tests passed
    - Merge commit: $(git rev-parse HEAD)

    Thanks @$contrib!"
    ```

14. **驗證 PR 狀態**

    ```bash
    gh pr view <PR> --json state --jq .state
    # 應該是 MERGED
    ```

15. **刪除 temp branch**

    ```bash
    git branch -D temp/landpr-<PR>
    ```
