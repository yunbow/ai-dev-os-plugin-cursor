# AI Dev OS Plugin for Cursor — Operation Guide

English | [日本語](./i18n/ja/operation-guide.md) | [简体中文](./i18n/zh-CN/operation-guide.md) | [한국어](./i18n/ko/operation-guide.md) | [Español](./i18n/es/operation-guide.md)

## Prerequisites

- [Cursor](https://cursor.sh/) with AI features enabled
- AI Dev OS layer files (L1-L3) set up in your project (see rules: [TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python))

## Installation

### Option A: Direct Copy

```bash
git clone https://github.com/yunbow/ai-dev-os-plugin-cursor.git
cp -r ai-dev-os-plugin-cursor/rules/ .cursor/rules/
cp -r ai-dev-os-plugin-cursor/checklist-templates/ .cursor/checklist-templates/
```

### Option B: Git Submodule

```bash
git submodule add https://github.com/yunbow/ai-dev-os-plugin-cursor.git .cursor/plugins/ai-dev-os
```

Then copy or symlink the rules:
```bash
cp -r .cursor/plugins/ai-dev-os/rules/ .cursor/rules/
```

## Initial Setup

1. Run `@ai-dev-os-init` in Cursor chat
2. Follow the wizard to configure your tech stack
3. Verify the generated directory structure

## Daily Workflow

### 4.1 Planning Before Implementation

Before coding, use `@ai-dev-os-plan` to create a guideline-aware implementation plan.

### 4.2 Creating Tickets

Use `@ai-dev-os-ticket` to generate structured tickets with compliance checklists.

### 4.3 Writing Code

File-scoped rules (`guideline-compliance`, `layer-dependency`) automatically activate when you edit matching files, providing real-time guidance.

### 4.4 Before Committing

Run `@ai-dev-os-check` to verify all changes comply with guidelines.

### 4.5 After Code Review

Run `@ai-dev-os-extract` to extract new rules from the review feedback.

### 4.6 Understanding Rules

Use `@ai-dev-os-why` to trace any rule back to its philosophical origin.

## Periodic Maintenance

| Frequency | Action | Description |
|-----------|--------|-------------|
| Monthly | `@ai-dev-os-audit` | 4-layer health check |
| Quarterly | `@ai-dev-os-evolve` | SECI spiral feedback |
| Weekly/Monthly | `@ai-dev-os-report` | Compliance report |

## Team Onboarding

1. New team member clones the project
2. Rules in `.cursor/rules/` are automatically available
3. Recommend running `@ai-dev-os-why` on key rules to understand rationale
4. Suggest reading `ai-dev-os/01_philosophy/` for foundational values

## Troubleshooting

### Rules not activating
- Verify `.cursor/rules/` directory exists and contains `.mdc` files
- Check that Cursor's AI features are enabled
- Restart Cursor if rules were just added

### False positives from guideline-compliance
- The rule only flags clear violations
- For persistent false positives, adjust the relevant guideline in `ai-dev-os/03_guidelines/`

### Performance
- File-scoped rules only activate on matching file patterns
- Manual rules only activate when explicitly @mentioned
