---
description: 審計 changelog
---

審計 changelog entries。

## 流程

1. **找最後一個 release tag**

   ```bash
   git tag --sort=-version:refname | head -1
   ```

2. **列出該 tag 之後的所有 commits**

   ```bash
   git log <tag>..HEAD --oneline
   ```

3. **讀 CHANGELOG.md 的 [Unreleased] section**

4. **對每個 commit 檢查**
   - 跳過：changelog 更新、純文件改動、release housekeeping
   - 確定 commit 影響哪個模組
   - 驗證有對應的 changelog entry
   - 外部貢獻（PR）格式：`Description ([#N](url) by [@user](url))`

5. **報告**
   - 列出缺少 entry 的 commits
   - 直接加入缺少的 entries

## Changelog 格式參考

Sections（按順序）：

- `### Breaking Changes` - 需要遷移的 API 變更
- `### Added` - 新功能
- `### Changed` - 現有功能的變更
- `### Fixed` - Bug 修正
- `### Removed` - 移除的功能

Attribution：

- 內部：`Fixed foo ([#123](url))`
- 外部：`Added bar ([#456](url) by [@user](url))`
