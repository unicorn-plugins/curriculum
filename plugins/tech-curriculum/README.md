# tech-curriculum

> 참고 자료 분석부터 기술교육 커리큘럼, 프리젠테이션/제안서/강의계획서 작성까지 자동화하는 DMAP 플러그인

- [tech-curriculum](#tech-curriculum)
  - [개요](#개요)
  - [설치](#설치)
    - [사전 요구사항](#사전-요구사항)
    - [플러그인 설치](#플러그인-설치)
  - [업그레이드](#업그레이드)
    - [Git Repository 마켓플레이스](#git-repository-마켓플레이스)
    - [로컬 마켓플레이스](#로컬-마켓플레이스)
  - [사용법](#사용법)
    - [슬래시 명령](#슬래시-명령)
    - [사용 예시](#사용-예시)
      - [커리큘럼 생성 워크플로우](#커리큘럼-생성-워크플로우)
      - [산출물](#산출물)
      - [강사 프로필 준비](#강사-프로필-준비)
      - [외부 플러그인 연동](#외부-플러그인-연동)
      - [자동 라우팅](#자동-라우팅)
  - [에이전트 구성](#에이전트-구성)
  - [요구사항](#요구사항)
    - [필수 도구](#필수-도구)
    - [런타임 호환성](#런타임-호환성)
  - [디렉토리 구조](#디렉토리-구조)
  - [라이선스](#라이선스)

---

## 개요

**tech-curriculum**은 참고 자료를 분석하여 최고의 기술교육 커리큘럼을 작성하고 프리젠테이션/제안서/강의계획서까지 자동 생성하는 DMAP 플러그인임.
5-Phase 워크플로우(정보 수집 → 자료 분석 → 커리큘럼 생성 → 프리젠테이션/제안서/강의계획서 작성)를 자동으로 수행함.

**주요 기능:**
- 참고 자료 파일(Markdown, PDF 등) 분석 및 구조화된 분석 체계 추천
- 교육 대상/형태/차별성 반영한 맞춤형 커리큘럼 생성
- 골든써클 접근법 기반 발표용 PPTX 프리젠테이션 자동 생성 (4가지 테마 지원)
- 제안서/보고서 스타일 PPTX 명세 자동 생성 (PptxGenJS 기반)
- 강의계획서 Excel 명세 자동 생성
- 강사 프로필 기반 강의계획서 생성
- 외부 플러그인 연동 (ext-skill)

[Top](#tech-curriculum)

---

## 설치

### 사전 요구사항

- [Claude Code](https://claude.com/claude-code) CLI 설치
- Python 3.10+ (이미지 생성 도구 실행용, 선택사항)
- Node.js (PPTX/Excel 파일 생성 시 필요, Claude Web 사용 시)

### 플러그인 설치

**방법 1: 마켓플레이스 — GitHub (권장)**

```bash
# 1. GitHub 저장소를 마켓플레이스로 등록
claude plugin marketplace add unicorn-plugins/curriculum

# 2. 플러그인 설치 (형식: {플러그인명}@{마켓플레이스명})
claude plugin install tech-curriculum@curriculum

# 3. 설치 확인
claude plugin list
```

**방법 2: 마켓플레이스 — 로컬**

```bash
# 1. 로컬 경로를 마켓플레이스로 등록
claude plugin marketplace add ./curriculum

# 2. 플러그인 설치
claude plugin install tech-curriculum@curriculum

# 3. 설치 확인
claude plugin list
```

> **설치 후 setup 스킬 실행:**
> ```
> /tech-curriculum:setup
> ```
> - `gateway/install.yaml`을 읽어 필수 도구(generate_image) 자동 설치
> - 설치 결과 검증 (`required: true` 항목 실패 시 중단)
> - 플러그인 활성화 확인 (스킬 자동 탐색)

### 처음 GitHub을 사용하시나요?

다음 가이드를 참고하세요:

- [GitHub 계정 생성 가이드](https://github.com/cna-bootcamp/gen-dmap/blob/main/resources/guides/github/github-account-setup.md)
- [Personal Access Token 생성 가이드](https://github.com/cna-bootcamp/gen-dmap/blob/main/resources/guides/github/github-token-guide.md)
- [GitHub Organization 생성 가이드](https://github.com/cna-bootcamp/gen-dmap/blob/main/resources/guides/github/github-organization-guide.md)

[Top](#tech-curriculum)

---

## 업그레이드

### Git Repository 마켓플레이스

저장소의 최신 커밋을 가져와 플러그인을 업데이트함.

```bash
# 마켓플레이스 업데이트 (최신 커밋 반영)
claude plugin marketplace update curriculum

# 플러그인 재설치
claude plugin install tech-curriculum@curriculum

# 설치 확인
claude plugin list
```

> **버전 고정**: `marketplace.json`에 특정 `ref`/`sha`가 지정된 경우,
> 저장소 관리자가 해당 값을 업데이트해야 새 버전이 반영됨.

> **갱신이 반영되지 않는 경우**: 플러그인을 삭제 후 재설치함.
> ```bash
> claude plugin remove tech-curriculum@curriculum
> claude plugin marketplace update curriculum
> claude plugin install tech-curriculum@curriculum
> ```

### 로컬 마켓플레이스

로컬 경로의 파일을 직접 갱신한 뒤 마켓플레이스를 업데이트함.

```bash
# 1. 로컬 플러그인 소스 갱신
cd ./curriculum
git pull origin main

# 2. 마켓플레이스 업데이트
claude plugin marketplace update curriculum

# 3. 플러그인 재설치
claude plugin install tech-curriculum@curriculum
```

> **갱신이 반영되지 않는 경우**: 플러그인을 삭제 후 재설치함.
> ```bash
> claude plugin remove tech-curriculum@curriculum
> claude plugin marketplace update curriculum
> claude plugin install tech-curriculum@curriculum
> ```

> **setup 재실행**: 업그레이드 후 `gateway/install.yaml`에 새 도구가 추가된 경우
> `/tech-curriculum:setup`을 재실행하여 누락된 도구를 설치할 것.

[Top](#tech-curriculum)

---

## 사용법

### 슬래시 명령

| 명령 | 설명 |
|------|------|
| `/tech-curriculum:setup` | 플러그인 초기 설정 (도구 설치) |
| `/tech-curriculum:help` | 사용 안내 |
| `/tech-curriculum:generate-curriculum` | 참고 자료 분석 → 커리큘럼 생성 → 프리젠테이션 작성 → 강의계획서 생성 |
| `/tech-curriculum:add-ext-skill` | 외부호출 스킬(ext-{대상플러그인}) 추가 |
| `/tech-curriculum:remove-ext-skill` | 외부호출 스킬(ext-{대상플러그인}) 제거 |

### 사용 예시

#### 커리큘럼 생성 워크플로우

generate-curriculum 스킬을 호출하면 다음 5가지 단계를 순차적으로 진행합니다.

**Phase 1: 정보 수집**
- 교육 대상 및 교육 형태 파악 (일회성 특강 vs 정식교육)
- 교육의 차별성과 가치 제안 확인
- 참고 자료 파일 경로 수집 (Markdown, PDF 등)
- 강사 프로필 파일 경로 수집 (선택사항, Phase 4c에서 필요)
- 사용자로부터 정보 입력 및 승인

**Phase 2: 자료 분석**
- content-analyst 에이전트가 참고 자료를 읽고 구조화된 분석 수행
- 분석 체계 3개를 자동 추천 (예: 학습 목표별, 기술 스택별, 난이도별)
- 사용자가 가장 적절한 분석 체계 선택
- 선택된 체계에 따라 상세 분석 수행

**Phase 3: 커리큘럼 생성**
- curriculum-writer 에이전트가 수행 계획서(develop-plan.md) 작성
- 제안된 계획에 대한 사용자 승인
- 세부 커리큘럼(curriculum.md) 생성
- 각 모듈별 학습 목표, 콘텐츠, 실습 항목 등 정의

**Phase 4a: 프리젠테이션 기획**
- presentation-writer 에이전트가 골든써클 기획서 작성
- 발표용 PPTX 자연어 명세(pptx-specification.md) 작성
- 4가지 테마 중 선택 가능
- 생성된 명세 기반 PPTX 파일 생성 방법 안내

**Phase 4b: 제안서 PPTX 명세**
- proposal-writer 에이전트가 제안서/보고서 스타일 PPTX 명세 작성
- PptxGenJS 코드 생성용 상세 명세(pptx-proposal-specification.md) 생성
- 이미지 생성 및 레이아웃 설정 포함
- Claude Web를 통한 PPTX 파일 생성 방법 안내

**Phase 4c: 강의계획서 명세**
- syllabus-writer 에이전트가 강의계획서 Excel 명세 작성
- 강사 프로필 기반 커스터마이징 (강사 프로필 제공 시)
- Excel 생성을 위한 자연어 명세(excel-syllabus-specification.md) 생성
- 주차별 강의 내용, 평가 방식, 학습 자료 등 포함

**Phase 4d: Claude Web 위임 안내**
- 생성된 PPTX/Excel 명세를 기반으로 실제 파일 생성 방법 제시
- PptxGenJS를 활용한 PPTX 코드 생성 방법 안내
- openpyxl을 활용한 Excel 생성 방법 안내

#### 산출물

generate-curriculum 실행 후 `{PLUGIN_ROOT}/output/{주제명}/` 디렉토리에 다음 파일들이 생성됩니다.

| 파일명 | 설명 |
|--------|------|
| `develop-plan.md` | 커리큘럼 수행 계획서 (Phase 3 승인용) |
| `curriculum.md` | 세부 커리큘럼 (모듈별 학습 목표, 콘텐츠, 실습 항목) |
| `presentation-plan.md` | 골든써클 기획서 (발표 전략 및 구성) |
| `pptx-specification.md` | 발표용 PPTX 자연어 명세 |
| `pptx-proposal-specification.md` | 제안서 PPTX 명세 (PptxGenJS 코드 생성용) |
| `excel-syllabus-specification.md` | 강의계획서 Excel 명세 |
| `images/` | 생성된 이미지 디렉토리 (표지, 강사 프로필, 섹션 배너 등) |

#### 강사 프로필 준비

강의계획서 생성 시(Phase 4c) 강사 프로필을 반영하려면 별도의 강사 프로필 파일이 필요합니다.

**파일 형식:** Markdown
**위치:** 프로젝트 내 임의의 위치 (Phase 1에서 경로 지정)
**샘플 파일:** `{PLUGIN_ROOT}/resources/samples/instructor-profile.md`

**포함 항목:**
- 기본 정보 (이름, 직책, 주요 분야)
- 핵심 역량 (전문 기술, 강의 경험 등)
- 주요 강의 이력 (과거 진행 교육)
- 자격 및 인증 (학위, 자격증 등)
- 교육 철학 및 강의 스타일

**예시:**
```markdown
# 강사 프로필

## 기본 정보
- 이름: 홍길동
- 직책: 수석 엔지니어
- 주요 분야: 클라우드 아키텍처

## 핵심 역량
- AWS 클라우드 설계 및 구축
- Kubernetes 컨테이너 오케스트레이션
- 대규모 분산 시스템 운영

## 주요 강의 이력
- 2023: AWS 아키텍처 특강 (150명)
- 2022: Kubernetes 기초 및 심화 과정 (200명)

## 자격 및 인증
- AWS Certified Solutions Architect - Professional
- Kubernetes Application Developer (CKAD)

## 교육 철학
실무 중심의 실습을 통해 참가자들이 즉시 활용 가능한 기술을 습득하도록 지원합니다.
```

#### 외부 플러그인 연동

tech-curriculum은 다른 DMAP 플러그인과 연동하여 기능을 확장할 수 있습니다.

**외부호출 스킬 추가:**
```bash
/tech-curriculum:add-ext-skill
```
- DMAP 리소스 마켓플레이스에서 조회 가능한 플러그인 연동
- `ext-{플러그인명}` 형식의 스킬 자동 생성
- 예: `ext-ai-content-lab` 등

**외부호출 스킬 제거:**
```bash
/tech-curriculum:remove-ext-skill
```
- 기존에 추가된 외부호출 스킬 제거
- 플러그인 간 기능 충돌 방지

연동 가능한 플러그인 목록은 [DMAP 리소스 마켓플레이스](https://dmap.io/marketplace)에서 확인할 수 있습니다.

#### 자동 라우팅

다음과 같은 자연어 요청은 자동으로 적절한 스킬이 처리됩니다.

| 자연어 요청 | 처리 스킬 |
|------------|----------|
| "커리큘럼 만들어줘", "자료 분석", "교재 분석", "커리큘럼 생성", "교육과정 만들어줘", "프리젠테이션", "강의계획서", "강의계획" | generate-curriculum |
| "설정", "설치", "setup" | setup |
| "도움말", "뭘 할 수 있어" | help |

[Top](#tech-curriculum)

---

## 에이전트 구성

| 에이전트 | 티어 | 역할 |
|----------|------|------|
| content-analyst | HIGH | 참고 자료 파일을 읽고 구조화된 분석 수행, 분석 체계 추천 |
| curriculum-writer | HIGH | 분석 결과 기반 커리큘럼 수행 계획서 및 커리큘럼 작성 |
| presentation-writer | MEDIUM | 프리젠테이션 기획(골든써클) 및 발표용 PPTX 자연어 명세 작성 |
| proposal-writer | HIGH | 제안서/보고서 스타일 PPTX 명세 작성 (PptxGenJS 코드 생성용), 이미지 생성 |
| syllabus-writer | HIGH | 강의계획서 Excel 생성을 위한 자연어 명세 작성 |

[Top](#tech-curriculum)

---

## 요구사항

### 필수 도구

| 도구 | 유형 | 용도 |
|------|------|------|
| generate_image | Custom App (Python) | Gemini 기반 이미지 생성 (선택) |

### 런타임 호환성

| 런타임 | 지원 |
|--------|:----:|
| Claude Code | ✅ |
| Codex CLI | 미검증 |
| Gemini CLI | 미검증 |

[Top](#tech-curriculum)

---

## 디렉토리 구조

```
tech-curriculum/
├── .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── skills/
│   ├── setup/
│   │   └── SKILL.md
│   ├── core/
│   │   └── SKILL.md
│   ├── help/
│   │   └── SKILL.md
│   ├── generate-curriculum/
│   │   └── SKILL.md
│   ├── add-ext-skill/
│   │   └── SKILL.md
│   └── remove-ext-skill/
│       └── SKILL.md
├── agents/
│   ├── content-analyst/
│   │   ├── AGENT.md
│   │   ├── agentcard.yaml
│   │   └── tools.yaml
│   ├── curriculum-writer/
│   │   ├── AGENT.md
│   │   ├── agentcard.yaml
│   │   └── tools.yaml
│   ├── presentation-writer/
│   │   ├── AGENT.md
│   │   ├── agentcard.yaml
│   │   └── tools.yaml
│   ├── proposal-writer/
│   │   ├── AGENT.md
│   │   ├── agentcard.yaml
│   │   └── tools.yaml
│   └── syllabus-writer/
│       ├── AGENT.md
│       ├── agentcard.yaml
│       └── tools.yaml
├── gateway/
│   ├── install.yaml
│   ├── runtime-mapping.yaml
│   ├── requirements.txt
│   └── tools/
│       └── general/
│           └── generate_image.py
├── commands/
│   ├── setup.md
│   ├── help.md
│   ├── generate-curriculum.md
│   ├── add-ext-skill.md
│   └── remove-ext-skill.md
├── resources/
│   ├── tools/
│   │   └── generate-image.md
│   └── samples/
│       ├── instructor-profile.md
│       ├── CNA 부트캠프 강의계획서.pdf
│       └── AI CNA Hands-On.pdf
├── CLAUDE.md
└── README.md
```

[Top](#tech-curriculum)

---

## 라이선스

MIT License - Unicorn Inc.

[Top](#tech-curriculum)
