---
description: Audit changelog entries before release
---

Audit changelog entries for all commits since the last release.

## Process

1. **Find the last release tag:**

   ```bash
   git tag --sort=-version:refname | head -1
   ```

2. **List all commits since that tag:**

   ```bash
   git log <tag>..HEAD --oneline
   ```

3. **Read the [Unreleased] section in CHANGELOG.md**

4. **For each commit, check:**
   - Skip: changelog updates, doc-only changes, release housekeeping
   - Verify a changelog entry exists
   - For external contributions (PRs), verify format: `Description ([#N](url) by [@user](url))`

5. **Report:**
   - List commits with missing entries
   - Add any missing entries directly

## Changelog Format Reference

Sections (in order):

- `### Breaking Changes` - API changes requiring migration
- `### Added` - New features
- `### Changed` - Changes to existing functionality
- `### Fixed` - Bug fixes
- `### Removed` - Removed features

Attribution:

- Internal: `Fixed foo ([#123](url))`
- External: `Added bar ([#456](url) by [@user](url))`
