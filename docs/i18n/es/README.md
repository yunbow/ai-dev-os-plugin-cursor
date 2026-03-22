# AI Dev OS Plugin — Cursor

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](../../../LICENSE)

Un plugin de Cursor que integra el modelo de 4 capas de AI Dev OS en el sistema de Rules de Cursor (`.cursor/rules/*.mdc`).

**Parte de [AI Dev OS](https://github.com/yunbow/ai-dev-os)** — un framework para convertir conocimiento tácito en reglas de codificación AI ejecutables ([Lifespan Layers](https://github.com/yunbow/ai-dev-os#lifespan-layers--the-4-layer-model)).
Requiere [AI Dev OS Rules](https://github.com/yunbow/ai-dev-os-rules-typescript) configurado en tu proyecto.

## ¿Por qué este plugin?

Integra las directrices de AI Dev OS en el **sistema de Rules de Cursor** (`.mdc`):

- **11 Rules** — `@ai-dev-os-check`, `@ai-dev-os-scan`, `@ai-dev-os-extract` y más
- **3 Agent-Requested Rules** — Activación automática en discusiones de arquitectura y directrices
- **2 File-Scoped Rules** — Verificación automática en archivos de código, advertencias de dependencia L1-L2
- **Configuración con un comando** — `npx ai-dev-os init --rules typescript --plugin cursor`

![AI Dev OS Check & Fix Report](../../../docs/images/ai-dev-os-check.png)

## Inicio rápido

```bash
npx ai-dev-os init --rules typescript --plugin cursor
```

> El CLI agrega submódulos, copia la plantilla .cursorrules y copia las reglas (archivos .mdc) a `.cursor/rules/` automáticamente.
> Consulta [AI Dev OS CLI](https://github.com/yunbow/ai-dev-os-cli) para más detalles.

Requisitos: [Cursor](https://cursor.sh/) con funciones de IA habilitadas y archivos de capas AI Dev OS (L1-L3) en tu proyecto ([TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)).

<details>
<summary>Configuración manual</summary>

**Opción A: Submódulo**

```bash
# 1. Agregar reglas de AI Dev OS como submódulo
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os
# Para proyectos Python:
# git submodule add https://github.com/yunbow/ai-dev-os-rules-python.git docs/ai-dev-os

# 2. Agregar este plugin como submódulo
git submodule add https://github.com/yunbow/ai-dev-os-plugin-cursor.git .cursor/plugins/ai-dev-os
cp -r .cursor/plugins/ai-dev-os/rules/ .cursor/rules/
```

**Opción B: Copia directa**

```bash
# 1. Agregar reglas como submódulo (igual que arriba)
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os

# 2. Clonar y copiar archivos del plugin
git clone https://github.com/yunbow/ai-dev-os-plugin-cursor.git
cp -r ai-dev-os-plugin-cursor/rules/ .cursor/rules/
```

3. Ejecuta `@ai-dev-os-init` en el chat de Cursor para configurar la estructura de 4 capas
4. Comienza a codificar — las reglas de alcance de archivo te guiarán automáticamente

Consulta la [Guía de operación](./operation-guide.md) para instrucciones detalladas.

</details>

## Rules

### Manual Rules (invocar por @mención del nombre de la regla en el chat)

| Regla | Descripción |
|-------|-------------|
| **ai-dev-os-init** | Asistente de configuración — introduce AI Dev OS en un proyecto en 30 minutos |
| **ai-dev-os-check** | Verifica cambios de código contra directrices (soporta `git diff`, staging, comparación de ramas) |
| **ai-dev-os-scan** | Escaneo completo de cumplimiento de TODOS los archivos fuente del proyecto |
| **ai-dev-os-review** | Auto-revisión pre-PR combinando cumplimiento L3 + revisión de diseño L2 + alineación L1 |
| **ai-dev-os-extract** | Extrae nuevas reglas de diffs de revisión de código (Rule Harvesting) |
| **ai-dev-os-why** | Rastrea una regla a través de L3→L2→L1 para explicar su fundamento |
| **ai-dev-os-plan** | Crea un plan de implementación con checklists de directrices antes de codificar |
| **ai-dev-os-ticket** | Genera un ticket con resumen de implementación y candidatos de checklist |
| **ai-dev-os-audit** | Audita la salud de 4 capas: regla de dependencia, frescura, cobertura, consistencia |
| **ai-dev-os-evolve** | Analiza commits recientes para proponer actualizaciones L1-L2 (espiral SECI) |
| **ai-dev-os-report** | Genera resumen de cumplimiento para equipos e interesados |

### Agent-Requested Rules (activadas automáticamente por contexto)

| Regla | Contexto de activación | Descripción |
|-------|----------------------|-------------|
| **philosophy-advisor** | Decisiones de arquitectura/diseño | Soporte de juicio basado en L1 |
| **principle-checker** | Discusiones de cambios de código | Verificación de alineación L2 |
| **guideline-auditor** | Mantenimiento de directrices | Auditoría de cobertura y consistencia L3 |

### File-Scoped Rules (activadas en archivos coincidentes)

| Regla | Patrón de archivo | Descripción |
|-------|------------------|-------------|
| **guideline-compliance** | `**/*.{ts,tsx,js,jsx,py,go}` | Verificación ligera de directrices en archivos de código |
| **layer-dependency** | `**/01_philosophy/**`, `**/02_decision-criteria/**` | Advertencia de violación de regla de dependencia |

<details>
<summary>Estructura del paquete</summary>

```
ai-dev-os-plugin-cursor/
├── rules/
│   ├── ai-dev-os-init.mdc              # Asistente de configuración
│   ├── ai-dev-os-check.mdc             # Verificación de cumplimiento (git diff)
│   ├── ai-dev-os-scan.mdc              # Escaneo completo de cumplimiento
│   ├── ai-dev-os-review.mdc            # Auto-revisión pre-PR (L1-L3)
│   ├── ai-dev-os-extract.mdc           # Rule Harvesting desde código
│   ├── ai-dev-os-why.mdc               # Explicación de fundamento (L3→L2→L1)
│   ├── ai-dev-os-plan.mdc              # Planificación con directrices
│   ├── ai-dev-os-ticket.mdc            # Generación de tickets con checklist
│   ├── ai-dev-os-audit.mdc             # Auditoría de salud de 4 capas
│   ├── ai-dev-os-evolve.mdc            # Retroalimentación espiral SECI (L4→L1)
│   ├── ai-dev-os-report.mdc            # Generación de informes de cumplimiento
│   ├── philosophy-advisor.mdc          # Juicio arquitectónico basado en L1
│   ├── principle-checker.mdc           # Verificación de alineación L2
│   ├── guideline-auditor.mdc           # Auditoría de cobertura y consistencia L3
│   ├── guideline-compliance.mdc        # Verificación automática en archivos de código
│   └── layer-dependency.mdc            # Advertencia de dependencia en L1-L2
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

Cuando las reglas entran en conflicto: framework-specific > common > project-specific > decision criteria > philosophy. [→ Detalles](https://github.com/yunbow/ai-dev-os/blob/main/spec/priority-cascade.md)

## Relacionados

| Repositorio | Descripción |
|---|---|
| [ai-dev-os](https://github.com/yunbow/ai-dev-os) | Framework specification and theory |
| [rules-typescript](https://github.com/yunbow/ai-dev-os-rules-typescript) | TypeScript / Next.js / Node.js guidelines |
| [rules-python](https://github.com/yunbow/ai-dev-os-rules-python) | Python / FastAPI guidelines |
| [plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code) | Skills, Hooks, and Agents for Claude Code |
| [plugin-kiro](https://github.com/yunbow/ai-dev-os-plugin-kiro) | Steering Rules and Hooks for Kiro |
| [cli](https://github.com/yunbow/ai-dev-os-cli) | `npx ai-dev-os init` |
| [benchmark](https://github.com/yunbow/ai-dev-os-benchmark) | Quantitative benchmark — guideline impact data |

## Licencia

[MIT](../../../LICENSE)

---

Languages: [English](../../../README.md) | [日本語](../ja/README.md) | [简体中文](../zh-CN/README.md) | [한국어](../ko/README.md) | Español
