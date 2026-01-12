---
name: claude-code-changelog
description: Fetch and explain Claude Code changelog for specific versions. Use when users ask about Claude Code updates, version changes, new features, bug fixes, or want to understand what changed between versions. Triggers on queries like "What's new in Claude Code X.Y.Z?", "Claude Code changelog", "What changed in the latest version?", or "Explain Claude Code updates".
---

# Claude Code Changelog

Fetch and explain Claude Code version changes from the official changelog.

## Workflow

**First, determine the query type and choose the appropriate data source:**

| Query Type | Data Source | URL Pattern |
|------------|-------------|-------------|
| Single version (e.g., "2.1.3 有什么更新？") | GitHub Release | `https://github.com/anthropics/claude-code/releases/tag/v[X.Y.Z]` |
| Latest version | GitHub Release | `https://github.com/anthropics/claude-code/releases/latest` |
| Version range or multiple versions | CHANGELOG.md | `https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md` |
| Feature search across versions | CHANGELOG.md | `https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md` |

### For Single Version Queries (GitHub Release Page)

1. Fetch the release page: `https://github.com/anthropics/claude-code/releases/tag/v[X.Y.Z]`
2. Extract the release date from the page:
   - Look for text pattern: `released this [datetime]` (e.g., "ashwin-ant released this 09 Jan 23:32")
   - If relative time shown (e.g., "2 days ago"), convert to absolute date
   - If 404 error, the version may not have a formal Release (common for early versions)
3. Extract the release notes content from the main content area (formatted with bullet points)

### For Version Range / Multiple Versions (CHANGELOG.md)

1. Fetch the changelog: `https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md`
2. Extract relevant version sections:
   - Specific version: Find the `## [X.Y.Z]` section
   - Latest version: Use the first version section
   - Version range: Extract all versions in range
3. For each version, optionally fetch the release date from GitHub Releases if needed:
   - Use `https://github.com/anthropics/claude-code/releases/tag/v[X.Y.Z]`
   - Handle 404 gracefully (early versions may not have Releases)

### Common Steps (Apply to Both Data Sources)

1. Categorize and explain changes:

   | Category | Prefix | Explanation Focus |
   |----------|--------|-------------------|
   | New Features | "Added" | What capability this enables, use cases |
   | Bug Fixes | "Fixed" | What issue was resolved, impact |
   | Improvements | "Improved" | Performance/UX benefits |
   | Changes | "Changed" | Behavior differences, migration notes |
   | Breaking Changes | "Breaking change:" | Required actions, compatibility |
   | Security | Security-related | Vulnerability details, urgency |
   | Platform-Specific | `[Windows]`, `[VSCode]`, `[SDK]` | Platform relevance |

2. Provide educational context:
   - Explain technical terms (MCP, hooks, etc.)
   - Highlight important changes users should know
   - Note any required actions or migrations

## Response Format

Structure the explanation as:

```markdown
## Claude Code [version] 更新说明 (发布于 [date])

### 新功能
- **功能名称**: 详细解释这个功能做什么、为什么有用

### Bug 修复
- **修复内容**: 解释修复了什么问题

### 改进
- **改进内容**: 解释改进带来的好处

### 重要提示
- 任何需要用户注意的破坏性变更或迁移事项
```

## Examples

**User**: "Claude Code 2.1.3 有什么更新？"

**Action**: Determine query type (single version) → Fetch GitHub Release page `https://github.com/anthropics/claude-code/releases/tag/v2.1.3` → Extract date from "released this..." text → Extract release notes → Categorize and explain in Chinese

**User**: "最新版本的 Claude Code 有什么新功能？"

**Action**: Determine query type (latest) → Fetch GitHub Release page `/latest` → Extract date and content → Focus on "Added" items with detailed explanations

**User**: "2.0 之后和 plan mode 有关的更新有哪些？"

**Action**: Determine query type (version range) → Fetch CHANGELOG.md → Extract sections for versions 2.0.x → Filter for "plan" related changes → Optionally fetch release dates for key versions → Summarize across versions
