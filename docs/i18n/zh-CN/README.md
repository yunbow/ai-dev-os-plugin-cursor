# AI Dev OS Plugin — Cursor

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](../../../LICENSE)

将 AI Dev OS 4层模型集成到 Cursor 的 Rules 系统（`.cursor/rules/*.mdc`）中的插件。

**[AI Dev OS](https://github.com/yunbow/ai-dev-os) 的一部分** — 将隐性知识转化为可执行的 AI 编码规则的框架（[Lifespan Layers](https://github.com/yunbow/ai-dev-os#lifespan-layers--the-4-layer-model)）。
需要在项目中设置 [AI Dev OS Rules](https://github.com/yunbow/ai-dev-os-rules-typescript)。

## 为什么选择这个插件？

将 AI Dev OS 指南引入 **Cursor 的 Rules 系统**（`.mdc`）：

- **11 Rules** — `@ai-dev-os-check`、`@ai-dev-os-scan`、`@ai-dev-os-extract` 等
- **3 Agent-Requested Rules** — 在架构和指南讨论中自动激活
- **2 File-Scoped Rules** — 代码文件自动检查、L1-L2 依赖警告
- **一条命令安装** — `npx ai-dev-os init --rules typescript --plugin cursor`

## 快速开始

```bash
npx ai-dev-os init --rules typescript --plugin cursor
# 将规则复制到 Cursor 目录：
cp -r .ai-dev-os/plugin/rules/ .cursor/rules/
```

> CLI 会添加子模块并复制 .cursorrules 模板。Cursor 规则（.mdc 文件）需要另外复制到 `.cursor/rules/`。
> 详情请参阅 [AI Dev OS CLI](https://github.com/yunbow/ai-dev-os-cli)。

前提条件：[Cursor](https://cursor.sh/)（已启用 AI 功能）以及项目中已设置 AI Dev OS 层文件（L1-L3）（[TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)）。

<details>
<summary>手动设置</summary>

**方法A：子模块**

```bash
# 1. 将 AI Dev OS rules 添加为子模块
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os
# Python 项目：
# git submodule add https://github.com/yunbow/ai-dev-os-rules-python.git docs/ai-dev-os

# 2. 将此插件添加为子模块
git submodule add https://github.com/yunbow/ai-dev-os-plugin-cursor.git .cursor/plugins/ai-dev-os
cp -r .cursor/plugins/ai-dev-os/rules/ .cursor/rules/
```

**方法B：直接复制**

```bash
# 1. 将规则添加为子模块（同上）
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os

# 2. 克隆并复制插件文件
git clone https://github.com/yunbow/ai-dev-os-plugin-cursor.git
cp -r ai-dev-os-plugin-cursor/rules/ .cursor/rules/
```

3. 在 Cursor 聊天中运行 `@ai-dev-os-init` 设置4层结构
4. 开始编码 — 文件作用域规则会自动引导你

详情请参阅[操作指南](./operation-guide.md)。

</details>

## Rules

### 手动规则（在聊天中 @提及规则名称调用）

| 规则 | 说明 |
|------|------|
| **ai-dev-os-init** | 设置向导 — 30分钟内为项目引入 AI Dev OS |
| **ai-dev-os-check** | 检查代码变更的指南合规性（支持 `git diff`、暂存、分支比较） |
| **ai-dev-os-scan** | 全项目所有源文件的完整合规扫描 |
| **ai-dev-os-review** | PR 前自审 — L3 合规 + L2 设计审查 + L1 一致性 |
| **ai-dev-os-extract** | 从代码审查差异中提取新规则（Rule Harvesting） |
| **ai-dev-os-why** | 追溯规则原理 L3→L2→L1 |
| **ai-dev-os-plan** | 编码前创建包含指南检查清单的实现计划 |
| **ai-dev-os-ticket** | 生成包含实现摘要和检查清单候选的工单 |
| **ai-dev-os-audit** | 审计4层健康状态：依赖规则、新鲜度、覆盖率、一致性 |
| **ai-dev-os-evolve** | 分析最近提交，提议 L1-L2 更新（SECI 螺旋） |
| **ai-dev-os-report** | 为团队和利益相关者生成合规摘要报告 |

### Agent-Requested Rules（根据上下文自动激活）

| 规则 | 激活上下文 | 说明 |
|------|-----------|------|
| **philosophy-advisor** | 架构/设计决策 | L1 哲学判断支持 |
| **principle-checker** | 代码变更讨论 | L2 一致性验证 |
| **guideline-auditor** | 指南维护 | L3 覆盖率与一致性审计 |

### File-Scoped Rules（匹配文件时自动激活）

| 规则 | 文件模式 | 说明 |
|------|---------|------|
| **guideline-compliance** | `**/*.{ts,tsx,js,jsx,py,go}` | 代码文件的轻量级指南检查 |
| **layer-dependency** | `**/01_philosophy/**`, `**/02_decision-criteria/**` | 依赖规则违规警告 |

<details>
<summary>包结构</summary>

```
ai-dev-os-plugin-cursor/
├── rules/
│   ├── ai-dev-os-init.mdc              # 设置向导
│   ├── ai-dev-os-check.mdc             # 指南合规检查（git diff）
│   ├── ai-dev-os-scan.mdc              # 全项目合规扫描
│   ├── ai-dev-os-review.mdc            # PR 前自审（L1-L3）
│   ├── ai-dev-os-extract.mdc           # 代码 Rule Harvesting
│   ├── ai-dev-os-why.mdc               # 规则原理说明（L3→L2→L1）
│   ├── ai-dev-os-plan.mdc              # 指南感知的实现规划
│   ├── ai-dev-os-ticket.mdc            # 检查清单工单生成
│   ├── ai-dev-os-audit.mdc             # 4层健康审计
│   ├── ai-dev-os-evolve.mdc            # SECI 螺旋反馈（L4→L1）
│   ├── ai-dev-os-report.mdc            # 合规报告生成
│   ├── philosophy-advisor.mdc          # L1 架构判断
│   ├── principle-checker.mdc           # L2 一致性验证
│   ├── guideline-auditor.mdc           # L3 覆盖率与一致性审计
│   ├── guideline-compliance.mdc        # 代码文件自动检查
│   └── layer-dependency.mdc            # L1-L2 依赖规则警告
├── checklist-templates/
│   ├── nextjs.md
│   ├── python.md
│   └── go.md
├── templates/
│   ├── cursorrules.template
│   ├── ai-dev-os-starter/
│   └── ai-dev-os-full/
└── docs/
    ├── operation-guide.md
    └── i18n/ja/
        ├── README.md
        └── operation-guide.md
```

</details>

## Specificity Cascade

规则冲突时：framework-specific > common > project-specific > decision criteria > philosophy。[→ 详情](https://github.com/yunbow/ai-dev-os/blob/main/spec/priority-cascade.md)

## 相关项目

| 仓库 | 说明 |
|------|------|
| [ai-dev-os](https://github.com/yunbow/ai-dev-os) | 框架规范与理论 |
| [ai-dev-os-rules-typescript](https://github.com/yunbow/ai-dev-os-rules-typescript) | TypeScript / Next.js / Node.js 指南 |
| [ai-dev-os-rules-python](https://github.com/yunbow/ai-dev-os-rules-python) | Python / FastAPI 指南 |
| [ai-dev-os-plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code) | Claude Code 的 Skills、Hooks、Agents |
| [ai-dev-os-plugin-kiro](https://github.com/yunbow/ai-dev-os-plugin-kiro) | Kiro 的 Steering Rules、Hooks |
| [ai-dev-os-cli](https://github.com/yunbow/ai-dev-os-cli) | 安装自动化 — `npx ai-dev-os init` |

## 许可证

[MIT](../../../LICENSE)

---

Languages: [English](../../../README.md) | [日本語](../ja/README.md) | 简体中文 | [한국어](../ko/README.md) | [Español](../es/README.md)
