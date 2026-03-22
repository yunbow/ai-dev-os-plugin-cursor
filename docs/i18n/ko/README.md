# AI Dev OS Plugin — Cursor

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](../../../LICENSE)

AI Dev OS 4계층 모델을 Cursor의 Rules 시스템(`.cursor/rules/*.mdc`)에 통합하는 플러그인입니다.

**[AI Dev OS](https://github.com/yunbow/ai-dev-os)의 일부** — 암묵지를 강제 가능한 AI 코딩 규칙으로 변환하는 프레임워크 ([Lifespan Layers](https://github.com/yunbow/ai-dev-os#lifespan-layers--the-4-layer-model)).
프로젝트에 [AI Dev OS Rules](https://github.com/yunbow/ai-dev-os-rules-typescript) 설정이 필요합니다.

## 왜 이 플러그인인가?

AI Dev OS 가이드라인을 **Cursor의 Rules 시스템**(`.mdc`)에 통합:

- **11 Rules** — `@ai-dev-os-check`, `@ai-dev-os-scan`, `@ai-dev-os-extract` 등
- **3 Agent-Requested Rules** — 아키텍처 및 가이드라인 논의 시 자동 활성화
- **2 File-Scoped Rules** — 코드 파일 자동 검사, L1-L2 의존성 경고
- **원커맨드 설정** — `npx ai-dev-os init --rules typescript --plugin cursor`

## 빠른 시작

```bash
npx ai-dev-os init --rules typescript --plugin cursor
```

> CLI는 서브모듈 추가, .cursorrules 템플릿 복사, 규칙(.mdc 파일)의 `.cursor/rules/` 복사를 자동으로 수행합니다.
> 자세한 내용은 [AI Dev OS CLI](https://github.com/yunbow/ai-dev-os-cli)를 참조하세요.

전제 조건: [Cursor](https://cursor.sh/)(AI 기능 활성화) 및 프로젝트에 AI Dev OS 레이어 파일(L1-L3) ([TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)).

<details>
<summary>수동 설정</summary>

**방법A: 서브모듈**

```bash
# 1. AI Dev OS rules를 서브모듈로 추가
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os
# Python 프로젝트의 경우:
# git submodule add https://github.com/yunbow/ai-dev-os-rules-python.git docs/ai-dev-os

# 2. 이 플러그인을 서브모듈로 추가
git submodule add https://github.com/yunbow/ai-dev-os-plugin-cursor.git .cursor/plugins/ai-dev-os
cp -r .cursor/plugins/ai-dev-os/rules/ .cursor/rules/
```

**방법B: 직접 복사**

```bash
# 1. 규칙을 서브모듈로 추가 (위와 동일)
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os

# 2. 플러그인을 클론하여 복사
git clone https://github.com/yunbow/ai-dev-os-plugin-cursor.git
cp -r ai-dev-os-plugin-cursor/rules/ .cursor/rules/
```

3. Cursor 채팅에서 `@ai-dev-os-init`을 실행하여 4계층 구조 설정
4. 코딩 시작 — 파일 스코프 규칙이 자동으로 안내합니다

자세한 내용은 [운영 가이드](./operation-guide.md)를 참조하세요.

</details>

## Rules

### 수동 규칙 (채팅에서 @규칙명으로 호출)

| 규칙 | 설명 |
|------|------|
| **ai-dev-os-init** | 설정 마법사 — 30분 만에 프로젝트에 AI Dev OS 도입 |
| **ai-dev-os-check** | 코드 변경의 가이드라인 준수 검사 (`git diff`, 스테이징, 브랜치 비교 지원) |
| **ai-dev-os-scan** | 프로젝트 전체 소스 파일의 완전한 준수 스캔 |
| **ai-dev-os-review** | PR 전 셀프 리뷰 — L3 준수 + L2 설계 리뷰 + L1 정합성 통합 검사 |
| **ai-dev-os-extract** | 코드 리뷰 차이에서 새 규칙 추출 (Rule Harvesting) |
| **ai-dev-os-why** | 규칙의 근거를 L3→L2→L1까지 추적하여 설명 |
| **ai-dev-os-plan** | 코딩 전 가이드라인 체크리스트가 포함된 구현 계획 생성 |
| **ai-dev-os-ticket** | 구현 요약과 체크리스트 후보가 포함된 티켓 생성 |
| **ai-dev-os-audit** | 4계층 건전성 감사: 의존성 규칙, 신선도, 커버리지, 일관성 |
| **ai-dev-os-evolve** | 최근 커밋을 분석하여 L1-L2 업데이트 제안 (SECI 스파이럴) |
| **ai-dev-os-report** | 팀과 이해관계자를 위한 준수 요약 보고서 생성 |

### Agent-Requested Rules (컨텍스트에 따라 자동 활성화)

| 규칙 | 활성화 컨텍스트 | 설명 |
|------|---------------|------|
| **philosophy-advisor** | 아키텍처/설계 결정 | L1 기반 판단 지원 |
| **principle-checker** | 코드 변경 논의 | L2 정합성 검증 |
| **guideline-auditor** | 가이드라인 유지보수 | L3 커버리지 및 일관성 감사 |

### File-Scoped Rules (매칭 파일에서 자동 활성화)

| 규칙 | 파일 패턴 | 설명 |
|------|----------|------|
| **guideline-compliance** | `**/*.{ts,tsx,js,jsx,py,go}` | 코드 파일의 경량 가이드라인 검사 |
| **layer-dependency** | `**/01_philosophy/**`, `**/02_decision-criteria/**` | 의존성 규칙 위반 경고 |

<details>
<summary>패키지 구성</summary>

```
ai-dev-os-plugin-cursor/
├── rules/
│   ├── ai-dev-os-init.mdc              # 설정 마법사
│   ├── ai-dev-os-check.mdc             # 가이드라인 준수 검사 (git diff)
│   ├── ai-dev-os-scan.mdc              # 프로젝트 전체 준수 스캔
│   ├── ai-dev-os-review.mdc            # PR 전 셀프 리뷰 (L1-L3)
│   ├── ai-dev-os-extract.mdc           # 코드 Rule Harvesting
│   ├── ai-dev-os-why.mdc               # 규칙 근거 설명 (L3→L2→L1)
│   ├── ai-dev-os-plan.mdc              # 가이드라인 기반 구현 계획
│   ├── ai-dev-os-ticket.mdc            # 체크리스트 포함 티켓 생성
│   ├── ai-dev-os-audit.mdc             # 4계층 건전성 감사
│   ├── ai-dev-os-evolve.mdc            # SECI 스파이럴 피드백 (L4→L1)
│   ├── ai-dev-os-report.mdc            # 준수 보고서 생성
│   ├── philosophy-advisor.mdc          # L1 아키텍처 판단
│   ├── principle-checker.mdc           # L2 정합성 검증
│   ├── guideline-auditor.mdc           # L3 커버리지 및 일관성 감사
│   ├── guideline-compliance.mdc        # 코드 파일 자동 검사
│   └── layer-dependency.mdc            # L1-L2 의존성 규칙 경고
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

규칙 충돌 시: framework-specific > common > project-specific > decision criteria > philosophy. [→ 상세](https://github.com/yunbow/ai-dev-os/blob/main/spec/priority-cascade.md)

## 관련 프로젝트

| 저장소 | 설명 |
|--------|------|
| [ai-dev-os](https://github.com/yunbow/ai-dev-os) | 프레임워크 사양과 이론 |
| [ai-dev-os-rules-typescript](https://github.com/yunbow/ai-dev-os-rules-typescript) | TypeScript / Next.js / Node.js 가이드라인 |
| [ai-dev-os-rules-python](https://github.com/yunbow/ai-dev-os-rules-python) | Python / FastAPI 가이드라인 |
| [ai-dev-os-plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code) | Claude Code의 Skills, Hooks, Agents |
| [ai-dev-os-plugin-kiro](https://github.com/yunbow/ai-dev-os-plugin-kiro) | Kiro의 Steering Rules, Hooks |
| [ai-dev-os-cli](https://github.com/yunbow/ai-dev-os-cli) | 설정 자동화 — `npx ai-dev-os init` |

## 라이선스

[MIT](../../../LICENSE)

---

Languages: [English](../../../README.md) | [日本語](../ja/README.md) | [简体中文](../zh-CN/README.md) | 한국어 | [Español](../es/README.md)
