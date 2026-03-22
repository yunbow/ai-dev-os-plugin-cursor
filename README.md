# AI Dev OS Plugin — Cursor

[![Lint & Link Check](https://github.com/yunbow/ai-dev-os-plugin-cursor/actions/workflows/lint.yml/badge.svg)](https://github.com/yunbow/ai-dev-os-plugin-cursor/actions/workflows/lint.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A Cursor plugin that integrates the AI Dev OS 4-layer model into Cursor's Rules system (`.cursor/rules/*.mdc`).

**Part of [AI Dev OS](https://github.com/yunbow/ai-dev-os)** — a framework for turning tacit knowledge into enforceable AI coding rules ([Lifespan Layers](https://github.com/yunbow/ai-dev-os#lifespan-layers--the-4-layer-model)).
Requires [AI Dev OS Rules](https://github.com/yunbow/ai-dev-os-rules-typescript) set up in your project.

## Why This Plugin?

Bring AI Dev OS guidelines into **Cursor's Rules system** (`.mdc`):

- **11 Rules** — `@ai-dev-os-check`, `@ai-dev-os-scan`, `@ai-dev-os-extract` and more
- **3 Agent-Requested Rules** — Auto-activated for architecture and guideline discussions
- **2 File-Scoped Rules** — Auto-check on code files, L1-L2 dependency warnings
- **One command setup** — `npx ai-dev-os init --rules typescript --plugin cursor`

![AI Dev OS Check & Fix Report](docs/images/ai-dev-os-check.png)

## Quick Start

```bash
npx ai-dev-os init --rules typescript --plugin cursor
```

> The CLI adds submodules, copies the .cursorrules template, and copies rules (.mdc files) to `.cursor/rules/` automatically.
> See [AI Dev OS CLI](https://github.com/yunbow/ai-dev-os-cli) for details.

Requires [Cursor](https://cursor.sh/) with AI features enabled and AI Dev OS layer files (L1-L3) in your project ([TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)).

<details>
<summary>Manual Setup</summary>

#### Option A: Submodule

```bash
# 1. Add AI Dev OS rules as submodule
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os
# For Python projects:
# git submodule add https://github.com/yunbow/ai-dev-os-rules-python.git docs/ai-dev-os

# 2. Add this plugin as submodule
git submodule add https://github.com/yunbow/ai-dev-os-plugin-cursor.git .cursor/plugins/ai-dev-os
cp -r .cursor/plugins/ai-dev-os/rules/ .cursor/rules/
```

#### Option B: Direct Copy

```bash
# 1. Add rules as submodule (same as above)
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os

# 2. Clone and copy plugin files
git clone https://github.com/yunbow/ai-dev-os-plugin-cursor.git
cp -r ai-dev-os-plugin-cursor/rules/ .cursor/rules/
```

1. Run `@ai-dev-os-init` in Cursor chat to set up the 4-layer structure
2. Start coding — file-scoped rules will guide you automatically

See [Operation Guide](./docs/operation-guide.md) for detailed instructions.

</details>

## Rules

### Manual Rules (invoke by @mentioning the rule name in chat)

| Rule | Description |
|------|-------------|
| **ai-dev-os-init** | Setup wizard — introduces AI Dev OS to a project in 30 minutes |
| **ai-dev-os-check** | Checks code changes against guidelines (supports `git diff`, staged, branch comparison) |
| **ai-dev-os-scan** | Full project-wide compliance scan of ALL source files |
| **ai-dev-os-review** | Pre-PR self-review combining L3 compliance + L2 design review + L1 alignment |
| **ai-dev-os-extract** | Extracts new rules from code review diffs (Rule Harvesting) |
| **ai-dev-os-why** | Traces a rule back through L3→L2→L1 to explain its rationale |
| **ai-dev-os-plan** | Creates an implementation plan with guideline checklists before coding |
| **ai-dev-os-ticket** | Generates a ticket with implementation summary and checklist candidates |
| **ai-dev-os-audit** | Audits 4-layer health: dependency rule, freshness, coverage, consistency |
| **ai-dev-os-evolve** | Analyzes recent commits to propose L1-L2 updates (SECI spiral) |
| **ai-dev-os-report** | Generates compliance summary for teams and stakeholders |

### Agent-Requested Rules (auto-activated by context)

| Rule | Activation Context | Description |
|------|-------------------|-------------|
| **philosophy-advisor** | Architecture/design decisions | L1-based judgment support |
| **principle-checker** | Code change discussions | L2 alignment verification |
| **guideline-auditor** | Guideline maintenance | L3 coverage & consistency audit |

### File-Scoped Rules (activated on matching files)

| Rule | File Pattern | Description |
|------|-------------|-------------|
| **guideline-compliance** | `**/*.{ts,tsx,js,jsx,py,go}` | Lightweight guideline check on code files |
| **layer-dependency** | `**/01_philosophy/**`, `**/02_decision-criteria/**` | Dependency rule violation warning |

<details>
<summary>Package Structure</summary>

```text
ai-dev-os-plugin-cursor/
├── rules/
│   ├── ai-dev-os-init.mdc              # Setup wizard
│   ├── ai-dev-os-check.mdc             # Guideline compliance check (git diff)
│   ├── ai-dev-os-scan.mdc              # Full project-wide compliance scan
│   ├── ai-dev-os-review.mdc            # Pre-PR self-review (L1-L3)
│   ├── ai-dev-os-extract.mdc           # Rule Harvesting from code
│   ├── ai-dev-os-why.mdc               # Explain rule rationale (L3→L2→L1)
│   ├── ai-dev-os-plan.mdc              # Guideline-aware implementation planning
│   ├── ai-dev-os-ticket.mdc            # Ticket generation with checklist
│   ├── ai-dev-os-audit.mdc             # 4-layer health audit
│   ├── ai-dev-os-evolve.mdc            # SECI spiral feedback (L4→L1)
│   ├── ai-dev-os-report.mdc            # Compliance report generation
│   ├── philosophy-advisor.mdc          # L1-based architecture judgment
│   ├── principle-checker.mdc           # L2 alignment verification
│   ├── guideline-auditor.mdc           # L3 coverage & consistency audit
│   ├── guideline-compliance.mdc        # Auto check on code files
│   └── layer-dependency.mdc            # Dependency rule warning on L1-L2
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

When rules conflict: framework-specific > common > project-specific > decision criteria > philosophy. [→ Details](https://github.com/yunbow/ai-dev-os/blob/main/spec/priority-cascade.md)

## Related

| Repository | Description |
|---|---|
| [ai-dev-os](https://github.com/yunbow/ai-dev-os) | Framework specification and theory |
| [rules-typescript](https://github.com/yunbow/ai-dev-os-rules-typescript) | TypeScript / Next.js / Node.js guidelines |
| [rules-python](https://github.com/yunbow/ai-dev-os-rules-python) | Python / FastAPI guidelines |
| [plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code) | Skills, Hooks, and Agents for Claude Code |
| [plugin-kiro](https://github.com/yunbow/ai-dev-os-plugin-kiro) | Steering Rules and Hooks for Kiro |
| [cli](https://github.com/yunbow/ai-dev-os-cli) | `npx ai-dev-os init` |
| [benchmark](https://github.com/yunbow/ai-dev-os-benchmark) | Quantitative benchmark — guideline impact data |

## License

[MIT](./LICENSE)

---

Languages: English | [日本語](docs/i18n/ja/README.md) | [简体中文](docs/i18n/zh-CN/README.md) | [한국어](docs/i18n/ko/README.md) | [Español](docs/i18n/es/README.md)
