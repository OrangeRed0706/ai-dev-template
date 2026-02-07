---
description: Land a PR (merge with proper workflow)
---

Input

- PR: $1 <number|url>
  - If missing: use the most recent PR mentioned in the conversation.
  - If ambiguous: ask.

Do (end-to-end)

Goal: PR must end in GitHub state = MERGED.

1. Repo clean: `git status`

2. Identify PR meta:

   ```sh
   gh pr view <PR> --json number,title,author,headRefName,baseRefName
   contrib=$(gh pr view <PR> --json author --jq .author.login)
   head=$(gh pr view <PR> --json headRefName --jq .headRefName)
   ```

3. Fast-forward base:
   - `git checkout main`
   - `git pull --ff-only`

4. Create temp branch from main:
   - `git checkout -b temp/landpr-<PR>`

5. Check out PR branch:
   - `gh pr checkout <PR>`

6. Rebase onto temp base:
   - `git rebase temp/landpr-<PR>`
   - Fix conflicts if any.

7. Run full gate (Local CI):
   - [根據專案修改下面的指令]
   - `pnpm lint && pnpm build && pnpm test`

8. Fix any issues + update CHANGELOG.md:
   - Mention `#<PR>` and `@$contrib`

9. Commit via committer:
   - `./scripts/committer "fix: <summary> (#<PR>)" CHANGELOG.md <files>`

10. Push updated PR branch:
    - `git push --force-with-lease origin HEAD:$head`

11. Merge PR:
    - Squash: `gh pr merge <PR> --squash`
    - Or Rebase: `gh pr merge <PR> --rebase`
    - Never `gh pr close`

12. Sync main:
    - `git checkout main`
    - `git pull --ff-only`

13. Comment on PR:

    ```sh
    gh pr comment <PR> --body "Landed! Thanks @$contrib!"
    ```

14. Verify: `gh pr view <PR> --json state` should be MERGED

15. Delete temp branch:
    - `git branch -D temp/landpr-<PR>`
