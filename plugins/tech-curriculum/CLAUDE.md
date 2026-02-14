# tech-curriculum 플러그인

## 사용 가능한 명령

| 명령 | 설명 |
|------|------|
| `/tech-curriculum:setup` | 플러그인 초기 설정 (도구 설치) |
| `/tech-curriculum:help` | 사용 안내 |
| `/tech-curriculum:generate-curriculum` | 참고 자료 분석 → 커리큘럼 생성 → 프리젠테이션 작성 → 강의계획서 생성 |

## 자동 라우팅

다음과 같은 요청은 자동으로 tech-curriculum 플러그인이 처리합니다:
- "커리큘럼 만들어줘", "자료 분석", "교재 분석", "커리큘럼 생성", "교육과정 만들어줘", "프리젠테이션", "강의계획서", "강의계획" → /tech-curriculum:generate-curriculum
- "설정", "설치", "setup" → /tech-curriculum:setup
- "도움말", "뭘 할 수 있어" → /tech-curriculum:help

## 운영 규칙

- **요구사항 변형 금지**: 원래의 요구사항을 변형해야 할 때는 반드시 사용자에게 확인 후 진행
- **5-Phase 순차 수행**: 커리큘럼 생성 시 정보 수집 → 자료 분석 → 커리큘럼 생성 → 프리젠테이션 작성 → 강의계획서 생성 순서 준수

## 자원 사용 지침

작업 시 자원 카탈로그(`{PLUGIN_ROOT}/resources/resource.md`)를 참고하여 기존 자원 사용
- **PLUGIN_ROOT**: `gateway/path-config.yaml`의 `plugin_root` 값으로 결정 (기본: `plugins/tech-curriculum`)
