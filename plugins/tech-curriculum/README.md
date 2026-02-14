# tech-curriculum

> 참고 자료 분석부터 기술교육 커리큘럼, 프리젠테이션 작성까지 자동화하는 DMAP 플러그인

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
  - [에이전트 구성](#에이전트-구성)
  - [요구사항](#요구사항)
    - [필수 도구](#필수-도구)
    - [런타임 호환성](#런타임-호환성)
  - [디렉토리 구조](#디렉토리-구조)
  - [라이선스](#라이선스)

---

## 개요

**tech-curriculum**은 참고 자료를 분석하여 최고의 기술교육 커리큘럼을 작성하고 PPTX 프리젠테이션까지 자동 생성하는 DMAP 플러그인임.
4-Phase 워크플로우(정보 수집 → 자료 분석 → 커리큘럼 생성 → 프리젠테이션 작성)를 자동으로 수행함.

**주요 기능:**
- 참고 자료 파일(Markdown) 분석 및 구조화된 분석 체계 추천
- 교육 대상/형태/차별성 반영한 맞춤형 커리큘럼 생성
- 골든써클 접근법 기반 PPTX 프리젠테이션 자동 생성 (4가지 테마 지원)

[Top](#tech-curriculum)

---

## 설치

### 사전 요구사항

- [Claude Code](https://claude.com/claude-code) CLI 설치
- Python 3.10+ (이미지 생성 도구 실행용, 선택사항)

### 플러그인 설치

**방법 1: 마켓플레이스 — GitHub (권장)**

```bash
# 1. GitHub 저장소를 마켓플레이스로 등록
claude plugin marketplace add unicorn-inc/tech-curriculum

# 2. 플러그인 설치 (형식: {플러그인명}@{마켓플레이스명})
claude plugin install tech-curriculum@tech-curriculum

# 3. 설치 확인
claude plugin list
```

**방법 2: 마켓플레이스 — 로컬**

```bash
# 1. 로컬 경로를 마켓플레이스로 등록
claude plugin marketplace add ./tech-curriculum

# 2. 플러그인 설치
claude plugin install tech-curriculum@tech-curriculum

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
claude plugin marketplace update tech-curriculum

# 플러그인 재설치
claude plugin install tech-curriculum@tech-curriculum

# 설치 확인
claude plugin list
```

> **버전 고정**: `marketplace.json`에 특정 `ref`/`sha`가 지정된 경우,
> 저장소 관리자가 해당 값을 업데이트해야 새 버전이 반영됨.

> **갱신이 반영되지 않는 경우**: 플러그인을 삭제 후 재설치함.
> ```bash
> claude plugin remove tech-curriculum@tech-curriculum
> claude plugin marketplace update tech-curriculum
> claude plugin install tech-curriculum@tech-curriculum
> ```

### 로컬 마켓플레이스

로컬 경로의 파일을 직접 갱신한 뒤 마켓플레이스를 업데이트함.

```bash
# 1. 로컬 플러그인 소스 갱신
cd ./tech-curriculum
git pull origin main

# 2. 마켓플레이스 업데이트
claude plugin marketplace update tech-curriculum

# 3. 플러그인 재설치
claude plugin install tech-curriculum@tech-curriculum
```

> **갱신이 반영되지 않는 경우**: 플러그인을 삭제 후 재설치함.
> ```bash
> claude plugin remove tech-curriculum@tech-curriculum
> claude plugin marketplace update tech-curriculum
> claude plugin install tech-curriculum@tech-curriculum
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
| `/tech-curriculum:generate-curriculum` | 참고 자료 분석 → 커리큘럼 생성 → 프리젠테이션 작성 |

### 사용 예시

```
사용자: 커리큘럼 만들어줘
→ generate-curriculum 스킬이 4-Phase 워크플로우 자동 시작
  정보 수집 → 자료 분석 → 커리큘럼 생성 → 프리젠테이션 작성
```

[Top](#tech-curriculum)

---

## 에이전트 구성

| 에이전트 | 티어 | 역할 |
|----------|------|------|
| content-analyst | HIGH | 참고 자료 파일을 읽고 구조화된 분석 수행, 분석 체계 추천 |
| curriculum-writer | HIGH | 분석 결과 기반 커리큘럼 수행 계획서 및 커리큘럼 작성 |
| presentation-writer | MEDIUM | 프리젠테이션 기획(골든써클) 및 PPTX 자연어 명세 작성, 이미지 생성 연동 |

[Top](#tech-curriculum)

---

## 요구사항

### 필수 도구

| 도구 | 유형 | 용도 |
|------|------|------|
| claude-skills 플러그인 | DMAP Plugin | PPTX 프리젠테이션 파일 생성 |
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
│   └── generate-curriculum/
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
│   └── presentation-writer/
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
│   └── generate-curriculum.md
├── resources/
│   └── tools/
│       └── generate-image.md
├── CLAUDE.md
└── README.md
```

[Top](#tech-curriculum)

---

## 라이선스

MIT License - Unicorn Inc.

[Top](#tech-curriculum)

