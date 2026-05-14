# Dante Agentic School — 저장소 지침

> 모든 에이전트 작업은 **한국어**로 진행합니다. (README, 코멘트, 프롬프트, 산출물 등)

## 저장소 구조

```
├── .claude/
│   ├── agents/        # 10개 그룹, 20개 에이전트 정의
│   ├── commands/      # 19개 그룹, 26개 실행 커맨드
│   └── skills/        # 26개 스킬 (SKILL.md)
├── samples/marketing/ # Dante Coffee 엔드투엔드 시나리오
└── README.md          # 프로젝트 종합 문서
```

**이 저장소에는 실행 코드가 없습니다.** 모든 파일은 `.md` 문서이며, OpenCode 에이전트가 읽고 실행하는 지침/프롬프트 파일입니다.

## 3계층 아키텍처

```
Command (실행 진입점) → Agent (역할 정의) → Skill (구체적 지침)
```

| 계층 | 위치 | 역할 | 예시 |
|------|------|------|------|
| **Command** | `.claude/commands/{group}/` | `/command-name` 으로 실행하는 플레이북 | `/analyze-market --industry "커피"` |
| **Agent** | `.claude/agents/{group}/` | 특정 역할의 에이전트 정의 (frontmatter에 `model:` 지정 가능) | `market-analyst.md`, `brand-strategist.md` |
| **Skill** | `.claude/skills/{skill-name}/SKILL.md` | 구체적 작업 지침과 프레임워크 | `analysis-reports`, `brand-positioning` |

- **Command 파일**은 YAML frontmatter로 인자(name, description, required, default)를 정의합니다.
- **Agent 파일**은 `when_to_use:` 필드로 어떤 상황에서 호출할지를 명시합니다 (`model: sonnet` 등 모델 지정 가능).
- **Skill 파일**은 `description`과 `tags`로 메타데이터를 관리합니다.

## Command 실행 패턴

```bash
# 전체 파이프라인 (brand-doc 필수)
/run-full-pipeline --brand-doc "./samples/marketing/dante-coffee-brand-brief.md"

# 개별 단계 실행
/analyze-market --industry "분석할 시장" --scope "2024-2030"
/analyze-brand --brand-doc "./path/to/brand.md"
/create-segments --brand-doc "./brand-analysis-output.md"
/build-persona --segment "세그먼트명"
/plan-channels --target "타겟 설명" --budget "예산"
/generate-copy --brand-doc "./brand.md" --channel "instagram"
/create-image --prompt "이미지 설명"
/create-video "비디오 설명"
```

## 에이전트 그룹 & 주요 경로

마케팅 파이프라인 단계 순서:

1. **`brand-analytics/`** — 브랜드 분석, 경쟁사 분석
2. **`customer-segmentation/`** — 고객 세분화
3. **`persona-builder/`** — 페르소나 설계
4. **`social-strategy/`** — 채널 전략
5. **`content-creation/`** — 카피/스크립트 제작
6. **`creative-production/`** — 이미지/비디오 제작
7. **`campaign-orchestration/`** — 전체 파이프라인 오케스트레이션

ML 관련 그룹 (별도 흐름):
- `data-profiling/` → `feature-engineering/` → `imbalance-handling/` → `model-selection/` / `hyperparameter-tuning/` → `model-evaluation/` → `shap-analysis/` → `model-deployment/` → `model-monitoring/`
- `market-research/` — 시장 조사 (독립 실행 가능)

## Skill 사용 시 주의사항

- **kie-image-generator / kie-video-generator**: Python 스크립트(`scripts/generate_image.py`, `scripts/generate_video.py`)를 직접 실행. `--credits` 로 잔여 크레딧 확인 후 생성.
- **pptx / pdf / docx**: HTML → 마크다운 기반 문서 생성. 출력 디렉토리는 `./output/` 사용.
- **kiwoom-api / opendart-api**: 외부 API 키 필요 (`auth-manager` 스킬 참조).
- **auth-manager**: `.env`에 모든 API 키 보관. `.gitignore`에 포함되었는지 확인 필수.

## 파일 작성 규칙

- 모든 에이전트 정의는 `---` YAML frontmatter + `# title` 로 시작
- Command 실행 예시는 ` ```bash ` 코드 블록 사용
- 에이전트/커맨드 파일은 소문자 + 하이픈 케이스 (`market-analyst.md`, `run-full-pipeline.md`)
- 스킬은 디렉토리명 + `SKILL.md` (`skills/analysis-reports/SKILL.md`)

## git / GitHub

- 원격 저장소: `https://github.com/git2583/git2583-dante.git`
- 기본 브랜치: `main`
- `opencode.json`, `package.json`, CI 설정 없음 — 순수 문서 저장소
- `.gitignore` 없음 — 단, `.env`는 절대 커밋 금지

## 샘플 파일

`/samples/marketing/dante-coffee-brand-brief.md` — 133줄 분량의 가상 커피 브랜드 소개서.
이 파일을 입력값으로 `run-full-pipeline` 등의 커맨드를 테스트할 수 있습니다.

`/samples/marketing/dante-coffee-agentic-marketing-scenario.md` — 872줄 분량의 전체 시나리오.
Phase 0(시장 리서치)부터 Phase 5(콘텐츠 제작)까지 각 단계의 상세 산출물을 포함합니다.
