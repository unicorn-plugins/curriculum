---
name: generate-curriculum
description: 참고 자료 분석 → 커리큘럼 생성 → 프리젠테이션 작성 → 강의계획서 생성 워크플로우
user-invocable: true
---

# generate-curriculum

- [generate-curriculum](#generate-curriculum)
  - [목표](#목표)
  - [활성화 조건](#활성화-조건)
  - [참조](#참조)
  - [스킬 부스팅](#스킬-부스팅)
  - [에이전트 호출 규칙](#에이전트-호출-규칙)
    - [에이전트 FQN](#에이전트-fqn)
    - [프롬프트 조립](#프롬프트-조립)
  - [산출물 디렉토리 규칙](#산출물-디렉토리-규칙)
  - [워크플로우](#워크플로우)
    - [Phase 1: 정보 수집](#phase-1-정보-수집)
    - [Phase 2: 자료 분석 → Agent: content-analyst](#phase-2-자료-분석--agent-content-analyst)
      - [Phase 2 → Phase 3 전환: 산출물 디렉토리 결정](#phase-2--phase-3-전환-산출물-디렉토리-결정)
    - [Phase 3: 커리큘럼 생성 → Agent: curriculum-writer](#phase-3-커리큘럼-생성--agent-curriculum-writer)
    - [Phase 4a: 프리젠테이션 기획 → Agent: presentation-writer](#phase-4a-프리젠테이션-기획--agent-presentation-writer)
    - [Phase 4b: 제안서 PPTX 명세 작성 → Agent: proposal-writer](#phase-4b-제안서-pptx-명세-작성--agent-proposal-writer)
    - [Phase 4c: 강의계획서 명세 작성 → Agent: syllabus-writer](#phase-4c-강의계획서-명세-작성--agent-syllabus-writer)
    - [Phase 4d: Claude Web 위임 안내](#phase-4d-claude-web-위임-안내)
  - [완료 조건](#완료-조건)
  - [검증 프로토콜](#검증-프로토콜)
  - [상태 정리](#상태-정리)
  - [취소/재개](#취소재개)
  - [MUST 규칙](#must-규칙)
  - [MUST NOT 규칙](#must-not-규칙)
  - [검증 체크리스트](#검증-체크리스트)

[GENERATE-CURRICULUM 활성화]

---

## 목표

참고 자료를 분석하여 기술교육 커리큘럼을 작성하고 프리젠테이션, 제안서, 강의계획서까지 생성하는
워크플로우를 오케스트레이션함.
Phase 1은 스킬이 직접 수행하고, Phase 2~4c는 전문 에이전트에 위임하며,
Phase 4d는 오케스트레이터가 직접 수행함.

[Top](#generate-curriculum)

---

## 활성화 조건

- `/tech-curriculum:generate-curriculum` 슬래시 명령 호출 시
- "커리큘럼 만들어줘", "자료 분석", "교재 분석", "커리큘럼 생성", "교육과정 만들어줘", "프리젠테이션", "강의계획서", "강의계획" 키워드 감지 시

[Top](#generate-curriculum)

---

## 참조

| 문서 | 경로 | 용도 |
|------|------|------|
| 경로 설정 | `gateway/path-config.yaml` | 플러그인 루트 및 경로 설정 |
| Gateway 매핑 | `gateway/runtime-mapping.yaml` | 티어 및 도구 매핑 |
| content-analyst | `agents/content-analyst/` | 참고 자료 분석 에이전트 |
| curriculum-writer | `agents/curriculum-writer/` | 커리큘럼 작성 에이전트 |
| presentation-writer | `agents/presentation-writer/` | 프리젠테이션 작성 에이전트 |
| proposal-writer | `agents/proposal-writer/` | 제안서 PPTX 명세 작성 에이전트 |
| syllabus-writer | `agents/syllabus-writer/` | 강의계획서 Excel 명세 작성 에이전트 |
| claude-skills 명세 | `.dmap/plugins/claude-skills.md` | claude-skills 플러그인 API 명세 |

[Top](#generate-curriculum)

---

## 스킬 부스팅

| 단계 | 부스팅 스킬 | 용도 |
|------|------------|------|
| Phase 1 | `ulw` 매직 키워드 | 정보 수집 병렬화 |
| Phase 2 | `/oh-my-claudecode:ralph` | 자료 분석 완료까지 지속 |
| Phase 3 | `/oh-my-claudecode:ralph` | 커리큘럼 생성 완료까지 지속 |
| Phase 4a | `/oh-my-claudecode:ralph` | 프리젠테이션 기획 완료까지 지속 |
| Phase 4b | `/oh-my-claudecode:ralph` | 제안서 PPTX 명세 작성 완료까지 지속 |
| Phase 4c | `/oh-my-claudecode:ralph` | 강의계획서 Excel 명세 작성 완료까지 지속 |
| Phase 4d | (없음 - 오케스트레이터 직접 수행) | Claude Web 위임 안내 |

[Top](#generate-curriculum)

---

## 에이전트 호출 규칙

### 에이전트 FQN

| 에이전트 | FQN |
|----------|-----|
| content-analyst | `tech-curriculum:content-analyst:content-analyst` |
| curriculum-writer | `tech-curriculum:curriculum-writer:curriculum-writer` |
| presentation-writer | `tech-curriculum:presentation-writer:presentation-writer` |
| proposal-writer | `tech-curriculum:proposal-writer:proposal-writer` |
| syllabus-writer | `tech-curriculum:syllabus-writer:syllabus-writer` |

### 프롬프트 조립

1. `agents/{agent-name}/`에서 3파일 로드 (AGENT.md + agentcard.yaml + tools.yaml)
2. `gateway/runtime-mapping.yaml` 참조하여 구체화:
   - **모델 구체화**: agentcard.yaml의 `tier` → `tier_mapping`에서 모델 결정
   - **툴 구체화**: tools.yaml의 추상 도구 → `tool_mapping`에서 실제 도구 결정
   - **금지액션 구체화**: agentcard.yaml의 `forbidden_actions` → `action_mapping`에서 제외할 실제 도구 결정
   - **최종 도구** = (구체화된 도구) - (제외 도구)
3. 프롬프트 조립: AGENT.md + agentcard.yaml + tools.yaml을 합쳐 하나의 프롬프트로 구성
   - **구성 순서**: 공통 정적(runtime-mapping) → 에이전트별 정적(3파일) → 동적(작업 지시)
4. `Task(subagent_type=FQN, model=구체화된 모델, prompt=조립된 프롬프트)` 호출

[Top](#generate-curriculum)

---

## 산출물 디렉토리 규칙

모든 산출물은 `{PLUGIN_ROOT}/output/{topic}/` 디렉토리에 저장한다.

- **경로 해석 규칙**:
  1. `gateway/path-config.yaml`에서 `plugin_root` 읽기
  2. 워크스페이스 루트 경로 확인 (예: `git rev-parse --show-toplevel` 또는 현재 작업 디렉토리)
  3. `PLUGIN_ROOT` = `{워크스페이스 루트}/{plugin_root}` (절대 경로)
  4. `OUTPUT_DIR` = `{PLUGIN_ROOT}/output/{topic}/` (절대 경로)
- **`{topic}`**: 참고 자료의 주제를 적절히 표현하는 영문 kebab-case 이름
  - 예: `gen-ai-fundamentals`, `prompt-engineering`, `cloud-native-architecture`, `data-engineering`
- **결정 시점**: Phase 2(자료 분석) 완료 직후, 오케스트레이터가 분석 결과를 기반으로 결정
- **디렉토리 생성**: 오케스트레이터가 Phase 3 위임 전에 `{PLUGIN_ROOT}/output/{topic}/` 디렉토리를 생성
- **경로 전달**: Phase 3, Phase 4 에이전트에 CONTEXT로 절대 경로 `PLUGIN_ROOT`와 `OUTPUT_DIR`을 전달

---

## 워크플로우

### Phase 1: 정보 수집

이 Phase는 스킬이 직접 수행함. `ulw` 매직 키워드를 활용하여 병렬 수집함.

AskUserQuestion 도구로 다음 정보를 수집:

1. **교육 대상**: PM/PO, 기획자, 개발자 등
2. **교육 형태**: 일회성 특강 / 정식교육
   - 일회성 특강이면 시간 문의
   - 정식교육이면 며칠이고 하루 몇시간인지 문의
3. **차별성**: 커리큘럼 생성에 적용할 차별성 요소
4. **참고 자료 파일 경로** 확인 (교재, 기술 문서, 가이드 등)
5. **강사 프로필 파일 경로** 요청 (강의계획서 생성용)
   - 사용자에게 강사 프로필 파일 경로를 요청하며, 샘플 파일 위치(`{PLUGIN_ROOT}/resources/samples/instructor-profile.md`)를 안내
   - 샘플 파일과 동일한 Markdown 형식으로 작성된 파일을 제공하도록 가이드

> Phase 1 완료: 수집된 정보를 사용자에게 요약 보고

### Phase 2: 자료 분석 → Agent: content-analyst

이 Phase는 `/oh-my-claudecode:ralph`를 활용하여 수행함.

- **TASK**: 참고 자료 파일을 읽고 분석 체계 3개 추천 → 사용자 승인 → 승인된 체계로 분석 수행
- **EXPECTED OUTCOME**: 구조화된 자료 분석 결과 보고서
- **MUST DO**: 참고 자료 전체를 빠짐없이 분석, 분석 체계를 사용자에게 추천 후 승인 획득
- **MUST NOT DO**: 커리큘럼 작성, 코드 실행
- **CONTEXT**: Phase 1에서 수집한 교육 정보, 참고 자료 파일 경로

> Phase 2 완료: 분석 결과를 사용자에게 요약 보고

#### Phase 2 → Phase 3 전환: 산출물 디렉토리 결정

Phase 2 완료 후, 오케스트레이터는 다음을 수행:

1. `gateway/path-config.yaml`에서 `plugin_root` 값을 읽음
2. 워크스페이스 루트 경로 확인 (`git rev-parse --show-toplevel` 등)
3. `PLUGIN_ROOT` = `{워크스페이스 루트}/{plugin_root}` 절대 경로 계산
4. 자료 분석 결과에서 핵심 주제를 파악
5. 주제를 영문 kebab-case로 변환하여 `{topic}` 결정
6. `{PLUGIN_ROOT}/output/{topic}/` 디렉토리 생성 (Bash `mkdir -p`)
7. 이후 Phase 3, Phase 4에 절대 경로로 `PLUGIN_ROOT`와 `OUTPUT_DIR={PLUGIN_ROOT}/output/{topic}/` 을 CONTEXT로 전달

### Phase 3: 커리큘럼 생성 → Agent: curriculum-writer

이 Phase는 `/oh-my-claudecode:ralph`를 활용하여 수행함.

- **TASK**: 분석 결과 기반 수행 계획서 작성 → 사용자 승인 →
  세부 커리큘럼 생성 → 감성적 완료 메시지 전달
- **EXPECTED OUTCOME**: 수행 계획서(Markdown) + 세부 커리큘럼(Markdown) + 감성적 완료 메시지
- **MUST DO**: 교육 대상/형태/차별성 반영, 수행 계획서 승인 후 커리큘럼 생성,
  CONTEXT로 전달받은 OUTPUT_DIR에 저장, 커리큘럼 생성 완료 시 감성적인 완료 메시지로 사용자에게 알림
- **MUST NOT DO**: 프리젠테이션 작성, 요구사항 임의 변경
- **CONTEXT**: Phase 2의 분석 결과, Phase 1의 교육 정보, PLUGIN_ROOT={절대경로}, OUTPUT_DIR={PLUGIN_ROOT}/output/{topic}/

> Phase 3 완료: 커리큘럼을 사용자에게 보고하고 승인 요청

#### Phase 3 → Phase 4 전환: 커리큘럼 검토 및 승인 + API Key 확인

Phase 3 완료 후, 오케스트레이터는 **반드시** 다음을 수행:

**A. 커리큘럼 승인**

1. 생성된 산출물 확인:
   - `{OUTPUT_DIR}/curriculum-plan.md` (수행 계획서)
   - `{OUTPUT_DIR}/curriculum-detailed.md` (세부 커리큘럼)
2. **사용자에게 커리큘럼 검토 요청**: 수행 계획서와 세부 커리큘럼의 핵심 내용을 요약하여 보고하고, 사용자에게 검토를 요청
3. **사용자 승인 획득**: AskUserQuestion 도구로 승인 여부를 확인
   - 승인 시: 다음 단계(B)로 진행
   - 수정 요청 시: 피드백을 반영하여 curriculum-writer에 재위임 후 다시 승인 요청
   - **승인 없이 Phase 4로 진행하는 것은 절대 금지**

**B. Gemini API Key 확인 (이미지 생성 필수 사전 조건)**

Phase 4a, 4b에서 이미지 생성({tool:image_generate})이 필수이므로, Phase 4 진입 전에 API Key를 반드시 확보해야 함.

4. 환경변수 `GEMINI_API_KEY` 존재 여부 확인:
   ```bash
   echo "${GEMINI_API_KEY:+SET}"
   ```
5. API Key가 **없는 경우**:
   - AskUserQuestion으로 사용자에게 Gemini API Key를 요청
   - 안내 메시지: "Phase 4에서 프리젠테이션/제안서 이미지를 생성하려면 Gemini API Key가 필요합니다. Google AI Studio(https://aistudio.google.com/apikey)에서 발급받을 수 있습니다."
   - 사용자가 API Key를 제공하면 환경변수로 설정:
     ```bash
     export GEMINI_API_KEY="{사용자 제공 키}"
     ```
   - **API Key 없이 Phase 4로 진행하는 것은 절대 금지**
6. API Key가 **있는 경우**: Phase 4a로 바로 진행

### Phase 4a: 프리젠테이션 기획 → Agent: presentation-writer

이 Phase는 `/oh-my-claudecode:ralph`를 활용하여 수행함.

- **TASK**: 프리젠테이션 대상 확인 → PPT 스타일 사용자 문의 →
  골든써클 기획서 작성 → 사용자에게 기획서 보고 및 승인 획득 →
  PPTX 자연어 명세 작성
- **EXPECTED OUTCOME**: 골든써클 기획서(Markdown) + PPTX 자연어 명세
  (슬라이드별 구성안, 스타일, 폰트 규격, 저장 경로 포함)
- **MUST DO**: PPT 스타일(테마, 강조색, 배경색)을 사용자에게 문의하여 반영,
  골든써클 프레임워크 적용, 한 페이지에 핵심 메시지 3개 이하,
  골든써클 기획서를 사용자에게 보고하고 승인 획득 후 PPTX 자연어 명세 작성,
  맑은고딕 폰트 및 지정 텍스트 크기 규격(22/18/16/14pt)을 자연어 명세에 명시,
  CONTEXT로 전달받은 OUTPUT_DIR 저장 경로를 자연어 명세에 명시
- **MUST NOT DO**: 커리큘럼 수정, 자료 재분석,
  사용자 승인 없이 PPTX 명세 작성, PPT 스타일을 사용자 문의 없이 임의 결정,
  PPTX 파일을 직접 생성 (에이전트는 명세 작성까지만 담당)
- **CONTEXT**: Phase 3의 커리큘럼, Phase 1의 교육 정보, PLUGIN_ROOT={절대경로}, OUTPUT_DIR={PLUGIN_ROOT}/output/{topic}/

> Phase 4a 완료: 골든써클 기획서 + PPTX 자연어 명세를 사용자에게 보고

### Phase 4b: 제안서 PPTX 명세 작성 → Agent: proposal-writer

이 Phase는 `/oh-my-claudecode:ralph`를 활용하여 수행함.

- **TASK**: Phase 4a의 PPTX 자연어 명세(pptx-specification.md)와 Phase 3의 커리큘럼을 기반으로,
  제안서/보고서 스타일의 PPTX 명세(pptx-proposal-specification.md) 작성
  → 디자인 시스템 설계 → 슬라이드 구성 설계 → 사용자 승인 → 이미지 생성 → 명세 작성
- **EXPECTED OUTCOME**: 제안서 PPTX 명세(pptx-proposal-specification.md)
  (디자인 시스템, 슬라이드별 좌표/색상/폰트 상세 명세, 이미지 매핑 포함)
- **MUST DO**: 폰트 규격(22/18/14/12pt) 엄격 준수, 최소 12pt 이상 보장,
  Compact 모드 적용 기준(모듈 6개 이상) 준수,
  모듈 7개 이상 시 슬라이드 분할,
  컬러 팔레트 역할별 색상 전체 정의,
  {tool:image_generate}로 표지/프로필 이미지 최소 2개 생성,
  CONTEXT로 전달받은 OUTPUT_DIR에 저장
- **MUST NOT DO**: PPTX 파일을 직접 생성하지 않음 (명세 작성까지만 담당),
  폰트 크기를 12pt 미만으로 설정하지 않음 (예외: 표지 인용구 11pt, 푸터 10pt),
  커리큘럼 수정, 자료 재분석
- **CONTEXT**: Phase 4a의 PPTX 자연어 명세(pptx-specification.md),
  Phase 3의 커리큘럼, Phase 1의 교육 정보, PLUGIN_ROOT={절대경로}, OUTPUT_DIR={PLUGIN_ROOT}/output/{topic}/

> Phase 4b 완료: 제안서 PPTX 명세(pptx-proposal-specification.md)를 사용자에게 보고

### Phase 4c: 강의계획서 명세 작성 → Agent: syllabus-writer

이 Phase는 `/oh-my-claudecode:ralph`를 활용하여 수행함.

- **TASK**: Phase 4a의 골든써클 기획서(Markdown), Phase 4b의 제안서 PPTX 명세(pptx-proposal-specification.md)와 사용자 제공 강사 프로필 파일을 기반으로
  강의계획서 Excel 생성을 위한 자연어 명세(excel-syllabus-specification.md) 작성
  → 제안서 명세에서 커리큘럼 데이터 추출 → 커리큘럼 구조에 맞는 시트 구성(3~5개) 설계 → 셀/스타일/병합 상세 명세 작성
- **EXPECTED OUTCOME**: 강의계획서 Excel 명세(excel-syllabus-specification.md)
  (시트 구성: 과정 개요, 커리큘럼(1~2개, 기본+심화 분리 시 별도 시트), 평가 및 환경, 강사 소개)
- **MUST DO**: Phase 4b의 제안서 명세에서 커리큘럼 데이터 완전 추출(모든 Day/모듈 빠짐없이),
  강사 프로필 파일 정보를 강사 소개 시트에 올바르게 매핑,
  CONTEXT로 전달받은 OUTPUT_DIR에 저장,
  명세만으로 openpyxl 코드를 생성할 수 있을 만큼 셀 데이터/병합/스타일 정보를 완전하게 기술,
  Excel 수식이 필요한 셀은 수식 표현으로 명시,
  생성 완료 시 파일 경로를 사용자에게 보고
- **MUST NOT DO**: 커리큘럼 내용 수정, 강사 프로필 내용 변경,
  Excel 파일(.xlsx)을 직접 생성하지 않음 (명세 작성까지만 담당),
  code_execute 사용 금지
- **CONTEXT**: Phase 4a의 골든써클 기획서(Markdown),
  Phase 4b의 제안서 PPTX 명세(pptx-proposal-specification.md),
  강사 프로필 파일 경로(Phase 1에서 수집),
  Phase 1의 교육 정보,
  PLUGIN_ROOT={절대경로}, OUTPUT_DIR={PLUGIN_ROOT}/output/{topic}/

> Phase 4c 완료: 강의계획서 Excel 명세(excel-syllabus-specification.md)를 사용자에게 보고

### Phase 4d: Claude Web 위임 안내

이 Phase는 오케스트레이터 스킬(generate-curriculum)이 직접 수행함.
Phase 4a~4c에서 생성된 명세 산출물을 사용자에게 안내하고,
**Claude Web**에서 PPTX 생성 및 강의계획서 Excel 작성을 요청하는 방법을 가이드한다.

- **산출물 파일 확인**: 다음 파일이 존재하는지 확인
  - `{PLUGIN_ROOT}/output/{topic}/pptx-specification.md` (발표용 프리젠테이션 명세)
  - `{PLUGIN_ROOT}/output/{topic}/pptx-proposal-specification.md` (제안서 PPTX 명세)
  - `{PLUGIN_ROOT}/output/{topic}/excel-syllabus-specification.md` (강의계획서 Excel 명세)
- **사용자 안내**: 다음 내용을 사용자에게 전달
  1. 3개 명세 파일의 경로 및 용도 안내
  2. Claude Web에 업로드할 파일 목록 안내 (명세 마크다운 + 이미지)
  3. Claude Web에서 사용할 프롬프트 안내
- **Claude Web 사용 방법**: claude.ai에 접속하여 명세 파일(마크다운)과 이미지를 첨부 파일로 업로드한 후, 아래 프롬프트를 입력하여 실제 파일 생성을 요청
- **안내 메시지**: 산출물별로 다음과 같이 안내

  **1. 발표용 프리젠테이션 (PPTX)**
  - 업로드 파일:
    - `{OUTPUT_DIR}/pptx-specification.md`
    - `{OUTPUT_DIR}/images/` 폴더의 프리젠테이션 이미지 전체 (slide_*.png)
  - 프롬프트:
    ```
    첨부한 pptx-specification.md는 PptxGenJS 기반 PPTX 생성을 위한 자연어 명세입니다.
    이 명세를 읽고 PptxGenJS 코드를 생성하여 실행해 주세요.
    첨부된 이미지 파일들을 명세에 지정된 슬라이드에 배치해 주세요.
    ```

  **2. 교육 제안서 (PPTX)**
  - 업로드 파일:
    - `{OUTPUT_DIR}/pptx-proposal-specification.md`
    - `{OUTPUT_DIR}/images/proposal_cover.png`
    - `{OUTPUT_DIR}/images/proposal_profile.png`
  - 프롬프트:
    ```
    첨부한 pptx-proposal-specification.md는 PptxGenJS 기반 교육 제안서 PPTX 생성을 위한
    상세 명세입니다. 이 명세를 읽고 PptxGenJS 코드를 생성하여 실행해 주세요.
    명세에 포함된 디자인 시스템(컬러 팔레트, 폰트 체계, 레이아웃 규격, 슬라이드 유형 카탈로그)을
    그대로 코드에 반영해 주세요. 첨부된 이미지 파일들을 명세에 지정된 슬라이드에 배치해 주세요.
    ```

  **3. 강의계획서 (Excel)**
  - 업로드 파일:
    - `{OUTPUT_DIR}/excel-syllabus-specification.md`
  - 프롬프트:
    ```
    첨부한 excel-syllabus-specification.md는 openpyxl 기반 강의계획서 Excel 생성을 위한
    자연어 명세입니다. 이 명세를 읽고 openpyxl 코드를 생성하여 실행해 주세요.
    명세에 포함된 시트별 셀 데이터, 병합 범위, 색상 팔레트, 폰트 체계를
    그대로 코드에 반영하여 Excel을 생성해 주세요.
    ```
- **EXPECTED OUTCOME**: 사용자에게 PPTX 생성 및 강의계획서 Excel 생성 방법 안내 완료
- **MUST NOT DO**: PPTX/Excel 파일을 직접 생성하지 않음, 명세 내용을 임의 변경하지 않음

> Phase 4d 완료: Claude Web 위임 안내 완료. 전체 워크플로우 완료 보고

[Top](#generate-curriculum)

---

## 완료 조건

- [ ] 자료 분석 결과 보고서 생성 완료
- [ ] 수행 계획서 + 세부 커리큘럼 생성 완료
- [ ] 발표용 PPTX 자연어 명세(pptx-specification.md) 작성 완료
- [ ] 제안서 PPTX 명세(pptx-proposal-specification.md) 작성 완료
- [ ] 강의계획서 Excel 명세(excel-syllabus-specification.md) 작성 완료
- [ ] Claude Web 위임 안내 완료 (PPTX 생성 + 강의계획서 Excel 생성 가이드)
- [ ] 모든 산출물이 {PLUGIN_ROOT}/output/{topic}/ 디렉토리에 저장됨

[Top](#generate-curriculum)

---

## 검증 프로토콜

각 Phase 완료 시 산출물 존재 확인 및 사용자 승인:

| Phase | 검증 내용 |
|-------|----------|
| Phase 1 | 교육 대상, 교육 형태, 차별성, 참고 자료 경로, 강사 프로필 파일 경로가 모두 수집되었는지 확인 |
| Phase 2 | 자료 분석 결과 보고서가 생성되었는지 확인 |
| Phase 3 | 수행 계획서 + 세부 커리큘럼이 {PLUGIN_ROOT}/output/{topic}/에 저장되었는지 확인, **사용자 커리큘럼 승인 획득 확인**, **GEMINI_API_KEY 환경변수 확보 확인** |
| Phase 4a | 골든써클 기획서 + PPTX 자연어 명세(pptx-specification.md)가 반환되었는지 확인 |
| Phase 4b | 제안서 PPTX 명세(pptx-proposal-specification.md)가 {PLUGIN_ROOT}/output/{topic}/에 저장되었는지 확인 |
| Phase 4c | 강의계획서 Excel 명세(excel-syllabus-specification.md)가 {PLUGIN_ROOT}/output/{topic}/에 저장되었는지 확인, 커리큘럼 구조에 맞는 시트 명세(3~5개) 포함 확인 |
| Phase 4d | 3개 명세 파일(pptx-specification.md, pptx-proposal-specification.md, excel-syllabus-specification.md)이 {PLUGIN_ROOT}/output/{topic}/에 존재하고, Claude Web 위임 방법(PPTX 생성 + 강의계획서 Excel 생성)이 안내되었는지 확인 |

[Top](#generate-curriculum)

---

## 상태 정리

완료 시 `.omc/state/generate-curriculum-state.json` 삭제.

[Top](#generate-curriculum)

---

## 취소/재개

- **취소**: `cancelomc` 키워드로 취소
- **재개**: `resume-session` 도구로 재개 가능

[Top](#generate-curriculum)

---

## MUST 규칙

| # | 규칙 |
|---|------|
| 1 | 5-Phase를 순차 수행하며 각 Phase 완료 시 사용자에게 보고 |
| 2 | Phase 2~4는 반드시 전문 에이전트에 위임 (`→ Agent:` 마커 사용) |
| 3 | 각 에이전트 위임 시 5항목(TASK, EXPECTED OUTCOME, MUST DO, MUST NOT DO, CONTEXT) 포함 |
| 4 | 프롬프트 조립 순서: 공통 정적 → 에이전트별 정적 → 동적 |
| 5 | Phase 4에서 PPT 스타일을 사용자에게 반드시 문의 |
| 6 | Phase 3 완료 시 감성적인 완료 메시지 전달 |
| 6a | Phase 3 완료 후 반드시 사용자에게 커리큘럼 검토 및 승인을 요청하고, 승인 획득 후에만 Phase 4 진행 |
| 6b | Phase 4 진입 전 GEMINI_API_KEY 환경변수를 반드시 확인하고, 없으면 사용자에게 요청하여 확보 후 진행 |
| 7 | Phase 4b에서 제안서 PPTX 명세 작성 시 폰트 규격(22/18/14/12pt)과 최소 12pt 규칙 엄격 준수 |
| 8 | Phase 4c에서 강의계획서 Excel 명세 작성 시 제안서 명세의 커리큘럼 데이터 완전 포함 및 강사 프로필 매핑 |
| 9 | Phase 4d에서 PPTX/Excel 직접 생성하지 않고, 반드시 Claude Web 위임 방법을 사용자에게 안내 |

[Top](#generate-curriculum)

---

## MUST NOT 규칙

| # | 금지 사항 |
|---|----------|
| 1 | Phase 순서를 건너뛰거나 역순 수행 금지 |
| 2 | 에이전트가 담당하는 작업을 스킬이 직접 수행 금지 |
| 3 | 사용자 승인 없이 다음 Phase로 진행 금지 (특히 Phase 3 → Phase 4 전환 시 커리큘럼 승인 필수) |
| 4 | 요구사항의 4-Step 사용자 플로우를 변형하지 않음 |

[Top](#generate-curriculum)

---

## 검증 체크리스트

- [ ] 에이전트 호출 규칙 섹션에 FQN 목록, 프롬프트 조립 절차 포함
- [ ] 4개 Phase가 요구사항의 4-Step과 1:1 대응
- [ ] `→ Agent:` 마커 위임 단계에 5항목 포함
- [ ] 완료 조건, 검증 프로토콜, 상태 정리, 취소/재개 섹션 포함
- [ ] 모든 Phase에 스킬 부스팅 명시
- [ ] PPT 스타일 사용자 문의가 Phase 4에 포함
- [ ] Phase 4a에 presentation-writer 에이전트 위임 5항목 포함
- [ ] Phase 4b에 proposal-writer 에이전트 위임 5항목 포함
- [ ] Phase 4c에 syllabus-writer 에이전트 위임 5항목 포함
- [ ] Phase 4d에 Claude Web 위임 안내 워크플로우 포함 (PPTX 생성 + 강의계획서 Excel 생성 가이드 모두 안내)
- [ ] Phase 1에 강사 프로필 파일 경로 수집 항목 포함

[Top](#generate-curriculum)
