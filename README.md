# Claude Code Changelog Skill

一个用于获取和解释 Claude Code 版本更新的技能。

## 功能

- 查询单个版本的更新内容
- 查询最新版本的新功能
- 跨版本搜索特定功能的演进历史
- 自动获取版本发布日期

## 安装

将 `claude-code-changelog.skill` 文件放置到以下任一位置：

- `~/.claude/skills/` - 全局技能目录
- `.claude/skills/` - 项目级技能目录

## 使用示例

```
# 查询特定版本
"Claude Code 2.1.3 有什么更新？"

# 查询最新版本
"最新版本的 Claude Code 有什么新功能？"

# 跨版本搜索
"2.0 之后和 plan mode 有关的更新有哪些？"

# 查询发布时间
"2.1.3 是什么时候发布的？"
```

## 数据源

- **单版本查询**: GitHub Releases 页面（包含发布日期和完整说明）
- **多版本/范围查询**: CHANGELOG.md

## 许可证

MIT
