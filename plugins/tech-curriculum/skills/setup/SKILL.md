---
name: setup
description: tech-curriculum 플러그인 초기 설정
user-invocable: true
---

# Setup

- [Setup](#setup)
  - [목표](#목표)
  - [활성화 조건](#활성화-조건)
  - [참조](#참조)
  - [스킬 부스팅](#스킬-부스팅)
  - [워크플로우](#워크플로우)
  - [MUST 규칙](#must-규칙)
  - [MUST NOT 규칙](#must-not-규칙)
  - [검증 체크리스트](#검증-체크리스트)

[SETUP 활성화]

---

## 목표

tech-curriculum 플러그인의 도구 설치 및 환경 설정 수행.
`gateway/install.yaml`에 정의된 커스텀 도구의 의존성을 설치하고,
실행 환경이 올바르게 구성되었는지 검증함.

[Top](#setup)

---

## 활성화 조건

- `/tech-curriculum:setup` 슬래시 명령 호출 시
- "설정", "설치", "setup" 키워드 감지 시

[Top](#setup)

---

## 참조

| 파일 | 용도 |
|------|------|
| `gateway/install.yaml` | 도구 설치 매니페스트 (커스텀 도구 목록, required 여부) |
| `gateway/requirements.txt` | Python 의존성 목록 |

[Top](#setup)

---

## 스킬 부스팅

이 스킬의 워크플로우는 `ulw` 매직 키워드를 활용하여 병렬 실행 + 완료 보장 방법론을 적용함.

[Top](#setup)

---

## 워크플로우

> 이 워크플로우는 `ulw` 매직 키워드를 활용하여 수행함.

### Step 1: 설치 매니페스트 로드

`gateway/install.yaml` 파일을 읽어 설치 대상 도구 목록을 파악함.

### Step 2: Python 환경 확인

```bash
python --version
```

Python 3.10 이상이 설치되어 있는지 확인함.
미설치 또는 버전 미달 시 사용자에게 안내 후 중단.

### Step 3: Python 의존성 설치

```bash
pip install -r gateway/requirements.txt
```

`gateway/requirements.txt`에 명시된 패키지를 설치함.

### Step 4: 커스텀 도구 파일 존재 확인

`install.yaml`의 `custom_tools` 항목별로 `source` 경로의 파일이 존재하는지 확인함.

| 도구명 | 소스 경로 | 필수 여부 |
|--------|----------|----------|
| generate_image | `tools/general/generate_image.py` | 선택 |

- `required: true` 도구의 소스 파일이 없으면 즉시 중단하고 오류 보고
- `required: false` 도구의 소스 파일이 없으면 경고만 출력하고 계속 진행

### Step 5: 환경 변수 설정 안내

`.env` 파일 설정이 필요한 항목을 사용자에게 안내함.

| 환경 변수 | 용도 | 필수 여부 |
|-----------|------|----------|
| `GEMINI_API_KEY` | generate_image 도구 사용 시 Gemini API 인증 | 선택 (generate_image 사용 시 필수) |

`.env` 파일이 없으면 `.env.example`을 참고하여 생성하도록 안내.

### Step 6: 플러그인 활성화 확인

AskUserQuestion으로 적용 범위를 사용자에게 확인함.

| 선택지 | 설명 |
|--------|------|
| 모든 프로젝트 | `~/.claude/` 하위에 플러그인 설정 등록 |
| 현재 프로젝트만 | `.claude/` 하위에 플러그인 설정 등록 |

### Step 7: 설치 결과 요약 보고

설치 결과를 테이블 형식으로 요약 보고함.

```
## 설치 결과

| 항목 | 상태 |
|------|------|
| Python 버전 | ✅ 3.x.x |
| 의존성 설치 | ✅ 완료 |
| generate_image (선택) | ✅/⚠️ 확인/미확인 |
| .env 설정 | ✅/⚠️ 안내 완료 |
| 플러그인 활성화 | ✅ {범위} |
```

[Top](#setup)

---

## MUST 규칙

| # | 규칙 |
|---|------|
| 1 | `gateway/install.yaml`을 반드시 읽어 도구 설치 목록 확인 |
| 2 | `required: true` 도구 설치 또는 파일 존재 확인 실패 시 즉시 중단 |
| 3 | Python 환경 확인 후 의존성 설치 수행 |
| 4 | 설치 완료 후 결과 요약 보고 |

[Top](#setup)

---

## MUST NOT 규칙

| # | 금지 사항 |
|---|----------|
| 1 | `install.yaml`에 없는 도구 임의 설치 금지 |
| 2 | `required: false` 도구 실패 시 전체 설치 중단 금지 |
| 3 | 사용자 확인 없이 플러그인 적용 범위 자동 결정 금지 |

[Top](#setup)

---

## 검증 체크리스트

- [ ] `gateway/install.yaml` 읽기 완료
- [ ] Python 환경 확인 완료
- [ ] `gateway/requirements.txt` 의존성 설치 완료
- [ ] `required: true` 도구 파일 존재 확인
- [ ] `.env` 설정 안내 완료
- [ ] 플러그인 활성화 범위 사용자 확인 완료
- [ ] 설치 결과 요약 보고 완료

[Top](#setup)
