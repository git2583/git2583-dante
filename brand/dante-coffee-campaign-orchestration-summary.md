# Dante Coffee Campaign Orchestration Summary (Phase 7)

> **프로젝트**: Dante Coffee 마케팅 자동화
> **최종 업데이트**: 2026-05-15
> **총괄 에이전트**: campaign-director

---

## 1. 캠페인 개요 (Overview)
- **목표**: 강남/역삼 지역 IT 종사자 대상 '단테 커피' 브랜드 인지도 확산 및 신규 유입 증대
- **핵심 가치**: 합리적 프리미엄, PM의 생산성 파트너, 스페셜티의 대중화
- **캠페인 기간**: 2024년 6월 ~ 8월 (3개월 집중)

## 2. 전략 요약 (Strategy Recap)

### 2.1. 타겟 세그먼트
- **Primary**: 세련된 PM '김지현' (32세, IT 스타트업 근무)
- **Pain Point**: 바쁜 아침, 높은 카페 물가, 업무 생산성 저하
- **Value Proposition**: 합리적 가격의 고품질 스페셜티, 생산성을 깨우는 모닝 루틴

### 2.2. 채널 전략
- **메인 채널**: 인스타그램 (이미지 피드 및 릴스)
- **보조 채널**: 네이버 블로그 (지역 맛집 검색 대응)
- **전략**: PAS (Problem-Agitation-Solution) 및 공감형 스토리텔링

## 3. 최종 산출물 아카이브 (Artifacts)

| Phase | 내용 | 파일 경로 |
|---|---|---|
| Phase 1 | 브랜드 전략 브리프 | `brand/dante-coffee-brand-strategy-brief.md` |
| Phase 2 | 고객 세그먼트 프로필 | `brand/dante-coffee-customer-segments.md` |
| Phase 3 | 타겟 페르소나 (김지현) | `brand/dante-coffee-persona-kim-jihyun.md` |
| Phase 4 | 소셜 채널 운영 전략 | `brand/dante-coffee-social-strategy-kim-jihyun.md` |
| Phase 5 | 광고 카피 Variations | `brand/dante-coffee-copy-instagram-jihyun.md` |
| Phase 6 | 크리에이티브 프롬프트 | `brand/dante-coffee-creative-production-kim-jihyun.md` |

## 4. n8n 자동화 워크플로우 구성
- **사용 노드**: `OpenCode AI` 전용 노드
- **구성**: 
    - [Trigger] 매일 오전 8:00
    - [Agent] `copy-strategist` - 당일 날씨/트렌드 반영 카피 수정
    - [Action] 인스타그램 API를 통한 자동 포스팅 (예정)

## 5. 결론 및 권고 사항 (Next Steps)
1. **이미지 생성**: `kie-image-generator`를 통해 Phase 6 가이드라인에 따른 첫 번째 배치를 완료할 것.
2. **A/B 테스트**: 일상 공감형(Option B)과 혜택 강조형(Option C)의 클릭률을 1주일간 비교 분석.
3. **확장**: 김지현 페르소나 성공 시, '프리미엄 애호가' 세그먼트로 캠페인 수평 확장.

---
**Dante Agentic Marketing Team**
