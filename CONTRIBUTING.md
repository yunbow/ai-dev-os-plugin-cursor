# Contributing to AI Dev OS Plugin — Cursor

Thank you for your interest in contributing!

## How to Contribute

### Reporting Issues
- Use [GitHub Issues](https://github.com/yunbow/ai-dev-os-plugin-cursor/issues)
- Specify which rule or template is affected

### Pull Requests
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Commit with a descriptive message
5. Open a Pull Request

### What to Contribute

| Directory | What We Need | Guidelines |
|-----------|-------------|------------|
| `rules/` | Rule improvements, new .mdc rules | Follow .mdc format (YAML frontmatter with `description`, `globs`, `alwaysApply`). Keep rules focused and concise. |
| `templates/` | Template improvements | Templates should follow Two-Tier Context Strategy (10-15 high-impact rules only). |
| `checklist-templates/` | New language checklists, improvements | Keep checklists actionable and verifiable. |

### Rule Development Guidelines

- Each rule lives in `rules/{name}.mdc`
- Required frontmatter: `description`, `globs`, `alwaysApply`
- `globs` defines which files the rule applies to (e.g., `"**/*.ts"`, `"**/*.py"`)
- `alwaysApply: true` for rules that should always be active
- Rule content should be clear and actionable
- Keep rules focused on a single concern
- Use concrete examples where possible

### Cross-Plugin Feature Parity

When adding a new feature to this plugin, consider adding the equivalent to:
- [ai-dev-os-plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code) (as skill or hook)
- [ai-dev-os-plugin-kiro](https://github.com/yunbow/ai-dev-os-plugin-kiro) (as steering rule)

### Translation Guide

- Translations are in `docs/i18n/{lang}/`
- Currently supported: `ja`, `zh-CN`, `ko`, `es`

## Code of Conduct

Be respectful, constructive, and inclusive.

---

Languages: English | [日本語](docs/i18n/ja/CONTRIBUTING.md)
