# 강의계획서 Excel 명세서

> 생성일: 2026-02-15
> 버전: 1.0
> 총 시트: 4개
> 대상: openpyxl 코드 생성 에이전트

---

## 전역 스타일 설정

### 파일 정보

```
파일명: ai-agent-development-syllabus.xlsx
저장 경로: /Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/
```

### 색상 팔레트

| 역할 | 변수명 | HEX 코드 | 용도 |
|------|--------|---------|------|
| 진한 녹색 | GREEN_DARK | 1B5E20 | 타이틀 배너, 섹션 헤더 배경 |
| 중간 녹색 | GREEN_MID | 2E7D32 | 보조 강조 |
| 연한 녹색 | GREEN_LIGHT | E8F5E9 | 라벨 배경, Day 셀 배경 |
| 녹색 악센트 | GREEN_ACCENT | C8E6C9 | 합계행 배경 |
| 진한 회색 | DARK_GRAY | 333333 | 본문 텍스트 |
| 연한 회색 | LIGHT_GRAY | F5F5F5 | 리뷰/마무리 행 배경 |
| 흰색 | WHITE | FFFFFF | 기본 배경 |
| 테두리색 | BORDER_COLOR | BDBDBD | 셀 테두리 |

### 폰트 체계

| 용도 | 폰트 | 크기 | 스타일 | 색상 |
|------|------|------|--------|------|
| 타이틀 | Arial | 20pt | Bold | WHITE |
| 부제 | Arial | 12pt | Regular | WHITE |
| 섹션 헤더 | Arial | 13pt | Bold | WHITE |
| 라벨 | Arial | 10pt | Bold | GREEN_DARK |
| 본문 강조 | Arial | 10pt | Bold | DARK_GRAY |
| 본문 | Arial | 10pt | Regular | DARK_GRAY |
| 테이블 헤더 | Arial | 11pt | Bold | WHITE |

### 레이아웃 규칙

- **테두리**: 모든 데이터 셀에 thin 스타일 테두리 적용 (4방향 모두, 색상: BORDER_COLOR)
- **텍스트 줄바꿈**: 모든 셀에 wrap_text=True 적용
- **행 높이 자동 조절**: 멀티라인 셀은 (줄 수 x 15) 픽셀로 행 높이 설정. 최소 행 높이 20px
- **인쇄 설정**: 모든 시트에 A4 가로(Landscape) 방향, 너비 맞춤(fit_to_width=1, fit_to_height=0)
- **시트 여백**: 상하 0.5인치, 좌우 0.3인치
- **기본 정렬**: 라벨 셀은 vertical='center', horizontal='center'. 값 셀은 vertical='top', horizontal='left'. 숫자/시간 셀은 horizontal='center'

---

## Sheet 1: 과정 개요

### 시트명
```
과정 개요
```

### 열 너비

| 열 | 너비 |
|----|------|
| A | 18 |
| B | 25 |
| C | 25 |
| D | 25 |

### 행별 데이터

#### 타이틀 배너 (행 1)

```
행 1:
  셀 범위: A1:D1 (4열 병합)
  텍스트: "AI Agent 개발 실무"
  스타일:
    폰트: Arial, 20pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 45px
```

#### 부제 (행 2)

```
행 2:
  셀 범위: A2:D2 (4열 병합)
  텍스트: "LLM API부터 MAS까지, 5일 완성 실습 과정"
  스타일:
    폰트: Arial, 12pt, Regular
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px
```

#### 빈 행 (행 3)

```
행 3:
  셀 범위: A3:D3 (4열 병합)
  텍스트: (빈 셀)
  행 높이: 10px
  배경: WHITE
```

#### 기본 정보 테이블 (행 4~10)

```
행 4:
  A4: "강의명"
    스타일: 라벨 (Arial 10pt Bold, GREEN_DARK, 배경 GREEN_LIGHT, 정렬 center/center)
  B4:D4: (3열 병합) "AI Agent 개발 실무"
    스타일: 본문 (Arial 10pt Regular, DARK_GRAY, 배경 WHITE, 정렬 left/center)
  행 높이: 25px

행 5:
  A5: "교육 기간"
    스타일: 라벨
  B5:D5: (3열 병합) "5일 (총 35시간)"
    스타일: 본문
  행 높이: 25px

행 6:
  A6: "일일 교육시간"
    스타일: 라벨
  B6:D6: (3열 병합) "7시간 (09:00 ~ 17:00)"
    스타일: 본문
  행 높이: 25px

행 7:
  A7: "수강 대상"
    스타일: 라벨
  B7:D7: (3열 병합) "AI 서비스 개발자, 백엔드/풀스택 개발자 (Python 기초 이상)"
    스타일: 본문
  행 높이: 25px

행 8:
  A8: "선수 지식"
    스타일: 라벨
  B8:D8: (3열 병합) "Python 기초 문법 (변수, 함수, 클래스), REST API 개념 이해"
    스타일: 본문
  행 높이: 25px

행 9:
  A9: "교육 방식"
    스타일: 라벨
  B9:D9: (3열 병합) "이론 58% + 실습 36% + 토론 6% (이론 -> 데모 -> 실습 -> 토론 4단계 순환)"
    스타일: 본문
  행 높이: 25px

행 10:
  A10: "교육 정원"
    스타일: 라벨
  B10:D10: (3열 병합) "15~20명"
    스타일: 본문
  행 높이: 25px
```

#### 빈 행 (행 11)

```
행 11:
  셀 범위: A11:D11 (4열 병합)
  텍스트: (빈 셀)
  행 높이: 10px
  배경: WHITE
```

#### 과정 특징 섹션 (행 12~18)

```
행 12:
  셀 범위: A12:D12 (4열 병합)
  텍스트: "과정 특징"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px

행 13:
  A13: "실습 중심"
    스타일: 라벨
  B13:D13: (3열 병합) "전체 시간의 36% 실습 + 6% 토론. 매일 실습 과제 부여, 통합 프로젝트로 마무리. Claude Code를 활용하여 AI가 코드를 생성하고 학습자가 이해하는 방식의 실습"
    스타일: 본문
  행 높이: 45px

행 14:
  A14: "체계적 성장 경로"
    스타일: 라벨
  B14:D14: (3열 병합) "5단계 성장 여정: 대화(LLM API) -> 데이터(문서/PDF) -> 도구(Function Calling) -> 지식(RAG/GraphRAG) -> 에이전트(MAS/MCP). 각 단계가 다음 단계의 기반"
    스타일: 본문
  행 높이: 45px

행 15:
  A15: "멀티 LLM 비교"
    스타일: 라벨
  B15:D15: (3열 병합) "OpenAI, Claude, Gemini, Groq 4개 LLM을 동일 시나리오로 비교 실습. 벤더 종속 없는 개발 역량 확보"
    스타일: 본문
  행 높이: 30px

행 16:
  A16: "최신 기술 반영"
    스타일: 라벨
  B16:D16: (3열 병합) "2025~2026년 최신 트렌드 반영: LangChain 1.0, MCP(Model Context Protocol), GraphRAG, A2A 프로토콜, Dify"
    스타일: 본문
  행 높이: 30px

행 17:
  A17: "핵심개념 도식화"
    스타일: 라벨
  B17:D17: (3열 병합) "SAS 패턴, RAG 파이프라인, Agent Flow 등 복잡한 개념을 아키텍처 다이어그램으로 시각화하여 명확 전달"
    스타일: 본문
  행 높이: 30px

행 18:
  A18: "통합 프로젝트"
    스타일: 라벨
  B18:D18: (3열 병합) "5일간 학습한 기술을 종합한 AI Agent 시스템 구현 프로젝트. 교육 종료 후 2주 내 제출, 별도 발표 세션"
    스타일: 본문
  행 높이: 30px
```

#### 빈 행 (행 19)

```
행 19:
  셀 범위: A19:D19 (4열 병합)
  텍스트: (빈 셀)
  행 높이: 10px
  배경: WHITE
```

#### 수강 효과 섹션 (행 20~25)

```
행 20:
  셀 범위: A20:D20 (4열 병합)
  텍스트: "수강 효과"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px

행 21:
  A21: "1"
    스타일: 본문 강조 (Arial 10pt Bold, DARK_GRAY, 배경 GREEN_LIGHT, 정렬 center/center)
  B21:D21: (3열 병합) "LLM API를 자유롭게 활용: OpenAI, Claude, Gemini, Groq 4개 LLM 비교 역량 확보, 프롬프트 엔지니어링으로 원하는 결과 도출"
    스타일: 본문
  행 높이: 30px

행 22:
  A22: "2"
    스타일: 본문 강조 (배경 GREEN_LIGHT, 정렬 center/center)
  B22:D22: (3열 병합) "RAG 시스템 설계/구현: 인덱싱부터 검색, 품질 튜닝(하이브리드 검색, 리랭킹)까지 전 과정 이해. GraphRAG로 복잡한 지식 관계 추론"
    스타일: 본문
  행 높이: 30px

행 23:
  A23: "3"
    스타일: 본문 강조 (배경 GREEN_LIGHT, 정렬 center/center)
  B23:D23: (3열 병합) "멀티에이전트 시스템 구축: MAS 아키텍처(SAS 패턴) 설계 및 구현, MCP로 표준화된 도구 연동, 자연어 기반 Agent 프로토타이핑"
    스타일: 본문
  행 높이: 30px

행 24:
  A24: "4"
    스타일: 본문 강조 (배경 GREEN_LIGHT, 정렬 center/center)
  B24:D24: (3열 병합) "실무 즉시 적용: 5일간 학습 내용을 종합한 통합 프로젝트로 실전 역량 확보, 교육 종료 후 2주 내 실무 적용 가능"
    스타일: 본문
  행 높이: 30px

행 25:
  A25: "5"
    스타일: 본문 강조 (배경 GREEN_LIGHT, 정렬 center/center)
  B25:D25: (3열 병합) "LangChain 생태계 활용: LangChain Core, LangGraph, LCEL을 활용한 체인 합성 및 워크플로우 관리 역량"
    스타일: 본문
  행 높이: 30px
```

---

## Sheet 2: 커리큘럼

### 시트명
```
커리큘럼
```

### 열 너비

| 열 | 너비 | 용도 |
|----|------|------|
| A | 6 | 일차 |
| B | 14 | 모듈 |
| C | 30 | 학습 주제 |
| D | 50 | 세부 학습 내용 |
| E | 10 | 시간 |
| F | 10 | 구분 |
| G | 14 | 평가 |

### 행별 데이터

#### 타이틀 배너 (행 1)

```
행 1:
  셀 범위: A1:G1 (7열 병합)
  텍스트: "AI Agent 개발 실무 - 커리큘럼"
  스타일:
    폰트: Arial, 20pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 45px
```

#### 부제 (행 2)

```
행 2:
  셀 범위: A2:G2 (7열 병합)
  텍스트: "5일 35시간 | 이론 58% + 실습 36% + 토론 6%"
  스타일:
    폰트: Arial, 12pt, Regular
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px
```

#### 헤더행 (행 3)

```
행 3:
  A3: "일차"
  B3: "모듈"
  C3: "학습 주제"
  D3: "세부 학습 내용"
  E3: "시간"
  F3: "구분"
  G3: "평가"
  스타일 (전체):
    폰트: Arial, 11pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px
```

#### Day 1 데이터행 (행 4~7)

```
행 4:
  A4: "Day 1" (A4:A7 세로 병합)
    스타일: 본문 강조 (Arial 10pt Bold, GREEN_DARK, 배경 GREEN_LIGHT, 정렬 center/center)
  B4: "모듈 1-1"
    스타일: 본문 강조 (Arial 10pt Bold, DARK_GRAY, 배경 WHITE, 정렬 center/center)
  C4: "AI 어플리케이션 개요"
    스타일: 본문 강조 (Arial 10pt Bold, DARK_GRAY, 배경 WHITE, 정렬 left/center)
  D4: "AI 어플리케이션의 필요성(혁신/자동화/고객만족)\nSAS 패턴(Scheduler-Agent-Supervisor), 5대 핵심 구성요소\nAgent Flow 패턴: RAG 체인(선형) vs ReAct Agent(자율 루프)\n트랜스포머 모델: 인코더/디코더 구조\n3-Tier 아키텍처, 데이터 흐름 6단계, RAG 시스템 흐름\nMSA 환경 통합(Circuit Breaker, Rate Limit, Retry)"
    스타일: 본문 (Arial 10pt Regular, DARK_GRAY, 배경 WHITE, 정렬 left/top)
  E4: "2h"
    스타일: 본문 (정렬 center/center)
  F4: "이론/토론"
    스타일: 본문 (정렬 center/center)
  G4: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 105px

행 5:
  A5: (병합 - A4:A7)
  B5: "모듈 1-2"
    스타일: 본문 강조 (정렬 center/center)
  C5: "LLM API 비교 및\n프롬프트 엔지니어링"
    스타일: 본문 강조 (정렬 left/center)
  D5: "LLM 4사 비교: OpenAI(GPT-4o), Claude, Gemini, Groq(LPU)\n특징/Use Case/토큰 비용 비교표, Rate Limit\n프롬프트 엔지니어링: 시스템 vs 유저 메시지\nZero/One/Few-shot, Chain of Thought(CoT)\nAPI 첫 호출: temperature, max_tokens 파라미터 실험\n프롬프트 기법 비교 실습(Zero-shot/Few-shot/CoT 결과 품질 비교)"
    스타일: 본문 (정렬 left/top)
  E5: "1.5h"
    스타일: 본문 (정렬 center/center)
  F5: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G5: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 105px

행 6:
  A6: (병합 - A4:A7)
  B6: "모듈 1-3"
    스타일: 본문 강조 (정렬 center/center)
  C6: "Python 기초 및\n개발 환경 설정"
    스타일: 본문 강조 (정렬 left/center)
  D6: "Python 코드 구성요소: 패키지, 모듈, 클래스, 함수, 데코레이터\n개발 환경 설정: VS Code, 가상환경(venv), requirements.txt\nAI 개발 필수 문법: import, dotenv, 예외 처리, 타입 힌트\nPydantic 실습: BaseModel, Field 활용 데이터 모델 정의\nLangChain with_structured_output() LLM 응답 구조화 파싱"
    스타일: 본문 (정렬 left/top)
  E6: "1h"
    스타일: 본문 (정렬 center/center)
  F6: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G6: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 90px

행 7:
  A7: (병합 - A4:A7)
  B7: "모듈 1-4"
    스타일: 본문 강조 (정렬 center/center)
  C7: "멀티턴 대화"
    스타일: 본문 강조 (정렬 left/center)
  D7: "싱글턴 vs 멀티턴 비교, 주요 활용 사례\n클라이언트 측 관리: 전체 히스토리 전송, 슬라이딩 윈도우+요약\n서버 측 관리: OpenAI Responses API, Gemini Chat Session, Claude API\n방식별 비교표\n여행 플래너 멀티턴 구현(3가지 방식 순차 구현 비교)\nStreamlit 웹 챗봇: Gemini Chat Session 기반 웹 UI\nDay 1 종합 Q&A, 핵심 개념 정리"
    스타일: 본문 (정렬 left/top)
  E7: "2.5h"
    스타일: 본문 (정렬 center/center)
  F7: "이론/실습\n/토론"
    스타일: 본문 (정렬 center/center)
  G7: "일별 과제:\nClaude API 추가\n구현 및 3사\n비교 보고서"
    스타일: 본문 (정렬 left/top)
  행 높이: 120px
```

#### Day 1 소계행 (행 8)

```
행 8:
  A8: (빈 셀)
  B8:D8: (3열 병합) "Day 1 소계: AI 앱 기초 + LLM API + 멀티턴 (Step 1 - LLM과 대화하기)"
    스타일: 본문 강조 (Arial 10pt Bold, DARK_GRAY, 배경 LIGHT_GRAY, 정렬 left/center)
  E8: "7h"
    스타일: 본문 강조 (배경 LIGHT_GRAY, 정렬 center/center)
  F8: "이론 55%\n실습 37%\n토론 8%"
    스타일: 본문 (배경 LIGHT_GRAY, 정렬 center/center)
  G8: (빈 셀, 배경 LIGHT_GRAY)
  행 높이: 45px
```

#### Day 2 데이터행 (행 9~13)

```
행 9:
  A9: "Day 2" (A9:A13 세로 병합)
    스타일: 본문 강조 (Arial 10pt Bold, GREEN_DARK, 배경 GREEN_LIGHT, 정렬 center/center)
  B9: "모듈 2-1"
    스타일: 본문 강조 (정렬 center/center)
  C9: "문서 요약"
    스타일: 본문 강조 (정렬 left/center)
  D9: "텍스트 요약 개요: 추출적(Extractive) vs 생성적(Abstractive) 요약\n모델 비교: LLM 기반(EXAONE - LG AI Research) vs 전문 모델(KoBART - SKT AI)\n문서 요약 실습: EXAONE(Groq LPU 활용) 뉴스 기사 요약, 품질 비교"
    스타일: 본문 (정렬 left/top)
  E9: "1h"
    스타일: 본문 (정렬 center/center)
  F9: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G9: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 60px

행 10:
  A10: (병합 - A9:A13)
  B10: "모듈 2-2"
    스타일: 본문 강조 (정렬 center/center)
  C10: "PDF 처리"
    스타일: 본문 강조 (정렬 left/center)
  D10: "PDF 구조 이해, OCR 개념, RAG 파이프라인에서의 역할\n처리 도구 비교: Docling(IBM, AI 기반), PyMuPDF(규칙 기반), pdfplumber\nPDF 처리 파이프라인: PyMuPDF 텍스트/테이블 추출\nDocling PDF->Markdown 변환, 추출 결과 LLM 전달 요약"
    스타일: 본문 (정렬 left/top)
  E10: "1h"
    스타일: 본문 (정렬 center/center)
  F10: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G10: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 75px

행 11:
  A11: (병합 - A9:A13)
  B11: "모듈 2-3"
    스타일: 본문 강조 (정렬 center/center)
  C11: "멀티모달 AI 개요\n(STT/TTS/VLM)"
    스타일: 본문 강조 (정렬 left/center)
  D11: "STT: Whisper API vs WhisperX vs LLM Diarization 비교, 데모\nTTS: OpenAI TTS API vs Bark(로컬) vs VITS(한국어 특화) 비교, 데모\nVLM: Gemini Vision vs Qwen2.5-VL 비교, 이미지 분석 데모\n클라우드 vs 로컬 모델 선택 기준"
    스타일: 본문 (정렬 left/top)
  E11: "1h"
    스타일: 본문 (정렬 center/center)
  F11: "이론/데모"
    스타일: 본문 (정렬 center/center)
  G11: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 75px

행 12:
  A12: (병합 - A9:A13)
  B12: "모듈 2-4"
    스타일: 본문 강조 (정렬 center/center)
  C12: "Function Calling 기초"
    스타일: 본문 강조 (정렬 left/center)
  D12: "Function Calling 정의 및 필요성: LLM 단독 사용의 한계\n공통 5단계 워크플로우: 도구 정의->요청 전송->모델 판단->함수 실행->결과 반환\n3사(OpenAI/Claude/Gemini) 코드 비교, Function Response role 비교\n호출 제어 옵션(tool_choice): auto/required/none/특정 도구 지정\n고급 기능: 병렬 함수 호출, 순차 함수 호출, 스트리밍\nFC 여행 플래너 실습: 3사 API로 날씨/관광지/맛집 도구 구현 비교"
    스타일: 본문 (정렬 left/top)
  E12: "2h"
    스타일: 본문 (정렬 center/center)
  F12: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G12: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 105px

행 13:
  A13: (병합 - A9:A13)
  B13: "모듈 2-5"
    스타일: 본문 강조 (정렬 center/center)
  C13: "Function Calling 고급\n및 모델별 고유 기능"
    스타일: 본문 강조 (정렬 left/center)
  D13: "OpenAI 고유 기능: Custom Tools(CFG 기반), 추론 모델 FC\nClaude 고유 기능: 서버 도구(웹 검색/Fetch), 시스템 도구(Bash/코드 실행), Tool Runner\nGemini 고유 기능: 자동 함수 호출(Python SDK), 생각 서명\n스트리밍 FC 실습: 3사 스트리밍 방식 여행 플래너 구현\nClaude 서버 도구 실습: 웹 검색 도구 활용 실시간 검색 Agent\nDay 2 종합 Q&A, 핵심 개념 정리"
    스타일: 본문 (정렬 left/top)
  E13: "2h"
    스타일: 본문 (정렬 center/center)
  F13: "이론/실습\n/토론"
    스타일: 본문 (정렬 center/center)
  G13: "일별 과제:\nPDF 로드 요약 +\nFC 웹검색\n통합 파이프라인"
    스타일: 본문 (정렬 left/top)
  행 높이: 105px
```

#### Day 2 소계행 (행 14)

```
행 14:
  A14: (빈 셀)
  B14:D14: (3열 병합) "Day 2 소계: 데이터 처리 + Function Calling (Step 2~3 - 데이터 다루기/도구 연결하기)"
    스타일: 본문 강조 (배경 LIGHT_GRAY, 정렬 left/center)
  E14: "7h"
    스타일: 본문 강조 (배경 LIGHT_GRAY, 정렬 center/center)
  F14: "이론 45%\n실습 50%\n토론 5%"
    스타일: 본문 (배경 LIGHT_GRAY, 정렬 center/center)
  G14: (빈 셀, 배경 LIGHT_GRAY)
  행 높이: 45px
```

#### Day 3 데이터행 (행 15~18)

```
행 15:
  A15: "Day 3" (A15:A18 세로 병합)
    스타일: 본문 강조 (GREEN_DARK, 배경 GREEN_LIGHT, 정렬 center/center)
  B15: "모듈 3-1"
    스타일: 본문 강조 (정렬 center/center)
  C15: "LangChain\n프레임워크 개요"
    스타일: 본문 강조 (정렬 left/center)
  D15: "왜 LangChain인가: LLM API 직접 호출의 한계, 4가지 핵심 가치\nLangChain vs 대안: LlamaIndex, CrewAI, AutoGen, Dify, Flowise\n생태계 전체 그림: langchain-core/openai/anthropic 등 패키지 구조\nLangGraph 워크플로우 관리: State, Node, Edge, Conditional Edge\nHuman-in-the-loop 패턴\nLangGraph 첫 워크플로우 실습: 상태 기반 그래프 + 조건부 분기"
    스타일: 본문 (정렬 left/top)
  E15: "1.5h"
    스타일: 본문 (정렬 center/center)
  F15: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G15: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 105px

행 16:
  A16: (병합 - A15:A18)
  B16: "모듈 3-2"
    스타일: 본문 강조 (정렬 center/center)
  C16: "LLM 인터페이스 + LCEL"
    스타일: 본문 강조 (정렬 left/center)
  D16: "Chat Models: ChatOpenAI, ChatAnthropic, ChatGoogleGenerativeAI\nPrompts: PromptTemplate, ChatPromptTemplate, FewShotPromptTemplate\nOutput Parsers: StrOutputParser, PydanticOutputParser, with_structured_output\nLCEL: 파이프 연산자(|), Runnable 인터페이스(invoke/stream/batch)\n체인 합성: RunnablePassthrough, RunnableParallel, RunnableLambda\nLCEL 체인 실습: 프롬프트->LLM->파서, 병렬 처리, 구조화 출력"
    스타일: 본문 (정렬 left/top)
  E16: "1.5h"
    스타일: 본문 (정렬 center/center)
  F16: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G16: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 105px

행 17:
  A17: (병합 - A15:A18)
  B17: "모듈 3-3"
    스타일: 본문 강조 (정렬 center/center)
  C17: "Agents, Tools,\nState 관리"
    스타일: 본문 강조 (정렬 left/center)
  D17: "Agent란: ReAct 루프, create_agent API\nTools 정의: 기본 도구, @tool 데코레이터 커스텀 도구\nMiddleware: HumanInTheLoop, Summarization, PII Middleware\nState 관리: 대화 이력/워크플로우 상태, LangGraph Checkpointer\nAgent + 커스텀 도구 실습: FC 여행 플래너를 LangChain Agent로 마이그레이션"
    스타일: 본문 (정렬 left/top)
  E17: "1h"
    스타일: 본문 (정렬 center/center)
  F17: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G17: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 90px

행 18:
  A18: (병합 - A15:A18)
  B18: "모듈 3-4"
    스타일: 본문 강조 (정렬 center/center)
  C18: "RAG 기초"
    스타일: 본문 강조 (정렬 left/center)
  D18: "왜 RAG가 필요한가: 할루시네이션, 지식 단절, 도메인 특화 한계\nRAG 패러다임: Naive RAG, Advanced RAG, Modular RAG\n인덱싱 파이프라인: Load(Document Loaders)->Split(RecursiveCharacterTextSplitter)->Embed->Store(Vector DB)\n검색 메커니즘: Sparse(BM25) vs Dense(벡터) vs Hybrid Search\nPost-Retrieval: Re-ranking, Compression, Filtering, Fusion\n아키텍처 패턴: Basic/Self-RAG/CRAG/Adaptive/Agentic RAG\nRAGAS 평가 지표: Faithfulness, Answer Relevancy, Context Precision/Recall\n기본 RAG 시스템 실습: WebBaseLoader->분할->OpenAI 임베딩->Chroma->LCEL RAG 체인->Multi-Query\nDay 3 종합 Q&A, 핵심 개념 정리"
    스타일: 본문 (정렬 left/top)
  E18: "3h"
    스타일: 본문 (정렬 center/center)
  F18: "이론/실습\n/토론"
    스타일: 본문 (정렬 center/center)
  G18: "일별 과제:\n자체 문서 RAG\n시스템 구축 +\n5개 쿼리 평가"
    스타일: 본문 (정렬 left/top)
  행 높이: 150px
```

#### Day 3 소계행 (행 19)

```
행 19:
  A19: (빈 셀)
  B19:D19: (3열 병합) "Day 3 소계: LangChain 프레임워크 + RAG 기초 (Step 3~4 - 도구 연결하기/지식 확장하기)"
    스타일: 본문 강조 (배경 LIGHT_GRAY, 정렬 left/center)
  E19: "7h"
    스타일: 본문 강조 (배경 LIGHT_GRAY, 정렬 center/center)
  F19: "이론 66%\n실습 29%\n토론 5%"
    스타일: 본문 (배경 LIGHT_GRAY, 정렬 center/center)
  G19: (빈 셀, 배경 LIGHT_GRAY)
  행 높이: 45px
```

#### Day 4 데이터행 (행 20~23)

```
행 20:
  A20: "Day 4" (A20:A23 세로 병합)
    스타일: 본문 강조 (GREEN_DARK, 배경 GREEN_LIGHT, 정렬 center/center)
  B20: "모듈 4-1"
    스타일: 본문 강조 (정렬 center/center)
  C20: "RAG 품질 튜닝"
    스타일: 본문 강조 (정렬 left/center)
  D20: "청킹 전략: 고정 크기, 재귀적 문자, 시맨틱 청킹(SemanticChunker), 문서 구조 기반\n임베딩 최적화: text-embedding-3-small/large, BGE, Cohere embed 비교\n하이브리드 검색: Dense+Sparse(BM25) 결합, RRF, HNSW 튜닝\n리랭킹: Cross-Encoder, Cohere Rerank, ColBERT, LLM 기반\n쿼리 최적화: HyDE, Multi-Query, Query Expansion/Rewriting\n평가: RAGAS(Faithfulness/Relevancy/Precision/Recall), MRR, NDCG, Recall@K\nRAG 튜닝 실습: 시맨틱 청킹+하이브리드 검색+Cross-Encoder 리랭킹+RAGAS 전후 비교"
    스타일: 본문 (정렬 left/top)
  E20: "2.5h"
    스타일: 본문 (정렬 center/center)
  F20: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G20: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 120px

행 21:
  A21: (병합 - A20:A23)
  B21: "모듈 4-2"
    스타일: 본문 강조 (정렬 center/center)
  C21: "Local LLM 개념"
    스타일: 본문 강조 (정렬 left/center)
  D21: "왜 Local LLM인가: 비용, 보안, 지연 문제 해결\n런타임 비교: Ollama, LlamaCpp, HuggingFace Transformers, LocalAI\n모델 포맷/양자화: GGUF, Q4_K_M/Q5_K_M/Q8_0, 하드웨어 요구사항\n범용 모델(Gemma 3, Qwen 3, Llama 3, Phi-4), 한국어 특화 모델"
    스타일: 본문 (정렬 left/top)
  E21: "0.5h"
    스타일: 본문 (정렬 center/center)
  F21: "이론"
    스타일: 본문 (정렬 center/center)
  G21: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 75px

행 22:
  A22: (병합 - A20:A23)
  B22: "모듈 4-3"
    스타일: 본문 강조 (정렬 center/center)
  C22: "웹검색 + YouTube\n통합 Agent"
    스타일: 본문 강조 (정렬 left/center)
  D22: "웹검색 도구: Tool vs Retriever, 멀티소스 RAG 아키텍처\n프로바이더 비교: Tavily(AI 최적화), DuckDuckGo(무료), Google Serper, SerpAPI\nYouTube 도구: YouTubeSearchTool, Data API v3, YoutubeLoader(자막 추출)\n보조 유틸리티: WebBaseLoader, BeautifulSoup, Trafilatura\n안정적 운영: 캐싱, Resilience 패턴(Retry/Fallback/Rate Limiting/Circuit Breaker)\n웹검색 Agent 실습: DuckDuckGo 기반 + YouTube 자막 추출 파이프라인\n멀티소스 Agent: 웹+YouTube 통합 LangGraph Agent, 자동 소스 라우팅"
    스타일: 본문 (정렬 left/top)
  E22: "2h"
    스타일: 본문 (정렬 center/center)
  F22: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G22: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 120px

행 23:
  A23: (병합 - A20:A23)
  B23: "모듈 4-4"
    스타일: 본문 강조 (정렬 center/center)
  C23: "GraphRAG"
    스타일: 본문 강조 (정렬 left/center)
  D23: "왜 GraphRAG인가: 기존 RAG의 한계(문맥 단절, 멀티홉 추론 실패)\n핵심 아키텍처: 인덱싱(엔터티/관계 추출->그래프 구축->커뮤니티 탐지)\n검색: Local/Global/Hybrid Search\n프레임워크 비교: MS GraphRAG, LangChain+Neo4j, LightRAG\nGraphRAG와 Vector RAG의 상호 보완적 활용\nLightRAG 실습: 문서 인덱싱->Local/Global/Hybrid 검색 비교->Vector RAG 대비 품질 비교\nLangChain+Neo4j 데모: Knowledge Graph 구축, Cypher 쿼리 관계 탐색\nDay 4 종합 Q&A, 핵심 개념 정리"
    스타일: 본문 (정렬 left/top)
  E23: "2h"
    스타일: 본문 (정렬 center/center)
  F23: "이론/실습\n/데모/토론"
    스타일: 본문 (정렬 center/center)
  G23: "일별 과제:\nRAG에 하이브리드\n검색+리랭킹 적용\nRAGAS 전후 비교"
    스타일: 본문 (정렬 left/top)
  행 높이: 135px
```

#### Day 4 소계행 (행 24)

```
행 24:
  A24: (빈 셀)
  B24:D24: (3열 병합) "Day 4 소계: RAG 고급 + 웹검색/YouTube + GraphRAG (Step 4 - 지식 확장하기)"
    스타일: 본문 강조 (배경 LIGHT_GRAY, 정렬 left/center)
  E24: "7h"
    스타일: 본문 강조 (배경 LIGHT_GRAY, 정렬 center/center)
  F24: "이론 61%\n실습 37%\n토론 5%"
    스타일: 본문 (배경 LIGHT_GRAY, 정렬 center/center)
  G24: (빈 셀, 배경 LIGHT_GRAY)
  행 높이: 45px
```

#### Day 5 데이터행 (행 25~27)

```
행 25:
  A25: "Day 5" (A25:A27 세로 병합)
    스타일: 본문 강조 (GREEN_DARK, 배경 GREEN_LIGHT, 정렬 center/center)
  B25: "모듈 5-1"
    스타일: 본문 강조 (정렬 center/center)
  C25: "멀티에이전트\n시스템 (MAS)"
    스타일: 본문 강조 (정렬 left/center)
  D25: "멀티에이전트 개요: 정의, 필요성, 단일 vs 멀티에이전트 비교\nSAS 패턴 심화: Scheduler-Agent-Supervisor, 구현 유형(LLM/규칙/하이브리드)\nA2A 프로토콜 및 Agent Card: 능력 선언, 라우팅 기준, Agent Card 설계\n통신 구조: Agent간/Agent-Tool/Agent-Human, 동기/비동기\n아키텍처 패턴: ReAct, Planning & Execution, Multi-Agent Collaboration\n상태 관리: Agent/Session/Global 상태, Checkpointing, Shared State\n운영 안정성: Loop 종료 조건, Budget, HITL\nClaude Code 기반 MAS 챗봇 실습: SAS 패턴 LangGraph MAS 챗봇 생성->구조 분석->실행 검증"
    스타일: 본문 (정렬 left/top)
  E25: "2h"
    스타일: 본문 (정렬 center/center)
  F25: "이론/실습"
    스타일: 본문 (정렬 center/center)
  G25: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 135px

행 26:
  A26: (병합 - A25:A27)
  B26: "모듈 5-2"
    스타일: 본문 강조 (정렬 center/center)
  C26: "MCP\n(Model Context Protocol)"
    스타일: 본문 강조 (정렬 left/center)
  D26: "왜 MCP인가: 앱-도구 간 인터페이스 표준화, FC와의 관계\n아키텍처: Host(Claude Desktop/Code), Client, Server\n통신: JSON-RPC 2.0, 전송(stdio/Streamable HTTP), 연결 수명주기\n핵심 기능: Tools(모델 호출 함수), Resources(앱 읽기 데이터), Prompts(사용자 템플릿)\n고급 기능: Sampling & Elicitation(역방향 요청), Roots(파일 시스템 경계)\n보안: OAuth 2.1 인증/인가, JWT, 보안 모범 사례\n생태계: 클라이언트 지원 현황, 서버 생태계, 거버넌스\nMCP 서버 실습: Python MCP SDK로 서버 개발->Claude Code 등록->Claude Desktop 연동\nSampling 데모: 서버에서 역방향 LLM 호출"
    스타일: 본문 (정렬 left/top)
  E26: "2.5h"
    스타일: 본문 (정렬 center/center)
  F26: "이론/실습\n/데모"
    스타일: 본문 (정렬 center/center)
  G26: "-"
    스타일: 본문 (정렬 center/center)
  행 높이: 150px

행 27:
  A27: (병합 - A25:A27)
  B27: "모듈 5-3"
    스타일: 본문 강조 (정렬 center/center)
  C27: "자연어로 Agent 개발"
    스타일: 본문 강조 (정렬 left/center)
  D27: "왜 자연어 기반 Agent 개발인가: 기존 개발 방식의 한계\n왜 Dify인가: 핵심 가치, Visual Builder 특징\n전체 워크플로우 5단계: 비즈니스 시나리오->DSL 자동 생성->시각적 프로토타이핑->개발 계획서->개발/배포\nDify DSL 구조: 노드 유형(Start/LLM/Agent/Knowledge Retrieval/HTTP Request)\n배포 옵션: Dify 런타임(API/웹 임베드) vs 코드 기반(LangChain/LangGraph)\nDify 실습: 고객 상담 시나리오->Claude Code DSL 생성->Dify 임포트/편집->테스트\n교육 종합 회고: 5단계 성장 경로 정리, 실무 적용 가이드, 통합 프로젝트 안내"
    스타일: 본문 (정렬 left/top)
  E27: "2.5h"
    스타일: 본문 (정렬 center/center)
  F27: "이론/실습\n/토론"
    스타일: 본문 (정렬 center/center)
  G27: "일별 과제:\nDify Agent를\nLangChain 코드로\n전환 계획서"
    스타일: 본문 (정렬 left/top)
  행 높이: 120px
```

#### Day 5 소계행 (행 28)

```
행 28:
  A28: (빈 셀)
  B28:D28: (3열 병합) "Day 5 소계: MAS + MCP + 자연어 Agent 개발 (Step 5 - 에이전트 만들기)"
    스타일: 본문 강조 (배경 LIGHT_GRAY, 정렬 left/center)
  E28: "7h"
    스타일: 본문 강조 (배경 LIGHT_GRAY, 정렬 center/center)
  F28: "이론 65%\n실습 30%\n토론 5%"
    스타일: 본문 (배경 LIGHT_GRAY, 정렬 center/center)
  G28: (빈 셀, 배경 LIGHT_GRAY)
  행 높이: 45px
```

#### 합계행 (행 29)

```
행 29:
  A29:B29: (2열 병합) "총 합계"
    스타일:
      폰트: Arial, 11pt, Bold
      색상: GREEN_DARK
      배경: GREEN_ACCENT
      정렬: horizontal='center', vertical='center'
  C29: "20개 모듈"
    스타일:
      폰트: Arial, 10pt, Bold
      색상: GREEN_DARK
      배경: GREEN_ACCENT
      정렬: horizontal='center', vertical='center'
  D29: "5일 x 7시간 = 35시간 | 이론 1,200분(58%) + 실습 755분(36%) + 토론 115분(6%)"
    스타일:
      폰트: Arial, 10pt, Bold
      색상: GREEN_DARK
      배경: GREEN_ACCENT
      정렬: horizontal='left', vertical='center'
  E29: "35h"
    스타일:
      폰트: Arial, 11pt, Bold
      색상: GREEN_DARK
      배경: GREEN_ACCENT
      정렬: horizontal='center', vertical='center'
  F29: "이론 58%\n실습 36%\n토론 6%"
    스타일:
      폰트: Arial, 10pt, Bold
      색상: GREEN_DARK
      배경: GREEN_ACCENT
      정렬: horizontal='center', vertical='center'
  G29: (빈 셀, 배경 GREEN_ACCENT)
  행 높이: 45px
```

---

## Sheet 3: 평가 및 환경

### 시트명
```
평가 및 환경
```

### 열 너비

| 열 | 너비 |
|----|------|
| A | 20 |
| B | 15 |
| C | 20 |
| D | 20 |
| E | 20 |

### 행별 데이터

#### 타이틀 (행 1)

```
행 1:
  셀 범위: A1:E1 (5열 병합)
  텍스트: "평가 기준 및 실습 환경"
  스타일:
    폰트: Arial, 20pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 45px
```

#### 빈 행 (행 2)

```
행 2:
  셀 범위: A2:E2 (5열 병합)
  텍스트: (빈 셀)
  행 높이: 10px
  배경: WHITE
```

#### 평가 배점 섹션 헤더 (행 3)

```
행 3:
  셀 범위: A3:E3 (5열 병합)
  텍스트: "평가 배점"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px
```

#### 평가 테이블 헤더 (행 4)

```
행 4:
  A4: "평가 항목"
  B4: "비중"
  C4:E4: (3열 병합) "세부 기준"
  스타일 (전체):
    폰트: Arial, 11pt, Bold
    색상: WHITE
    배경: GREEN_MID
    정렬: horizontal='center', vertical='center'
    행 높이: 30px
```

#### 평가 데이터행 (행 5~7)

```
행 5:
  A5: "일별 실습 과제"
    스타일: 본문 강조 (정렬 center/center)
  B5: "40%"
    스타일: 본문 강조 (GREEN_DARK, 정렬 center/center)
  C5:E5: (3열 병합) "Day 1: Claude API 추가 구현 및 3사 비교 보고서\nDay 2: PDF 요약 + FC 웹검색 통합 파이프라인\nDay 3: 자체 문서 RAG 시스템 구축 + 5개 쿼리 평가\nDay 4: 하이브리드 검색 + 리랭킹 적용 RAGAS 전후 비교\nDay 5: Dify Agent를 LangChain 코드로 전환 계획서"
    스타일: 본문 (정렬 left/top)
  행 높이: 90px

행 6:
  A6: "통합 프로젝트"
    스타일: 본문 강조 (정렬 center/center)
  B6: "40%"
    스타일: 본문 강조 (GREEN_DARK, 정렬 center/center)
  C6:E6: (3열 병합) "기술적 완성도(40%): 필수 기술 3개 이상 통합, 정상 동작, 에러 처리\n아키텍처 설계(30%): 적절한 기술 선택, 확장 가능한 구조, 문서화 품질\n발표 및 시연(30%): 명확한 설명, 실제 동작 시연, 질의응답 대응\n\n제출물: 소스 코드(GitHub) + 아키텍처 문서 + 데모 영상(5분) + 발표 자료(10분)\n제출 기한: 교육 종료 후 2주 이내"
    스타일: 본문 (정렬 left/top)
  행 높이: 105px

행 7:
  A7: "참여도"
    스타일: 본문 강조 (정렬 center/center)
  B7: "20%"
    스타일: 본문 강조 (GREEN_DARK, 정렬 center/center)
  C7:E7: (3열 병합) "수업 참여 및 질의응답 활동\n토론 세션 기여도\n일별 실습 과정 참여 태도"
    스타일: 본문 (정렬 left/top)
  행 높이: 60px
```

#### 평가 합계행 (행 8)

```
행 8:
  A8: "합계"
    스타일: 본문 강조 (배경 GREEN_ACCENT, 정렬 center/center)
  B8: "100%"
    스타일: 본문 강조 (GREEN_DARK, 배경 GREEN_ACCENT, 정렬 center/center)
  C8:E8: (3열 병합) (빈 셀, 배경 GREEN_ACCENT)
  행 높이: 25px
```

#### 빈 행 (행 9)

```
행 9:
  셀 범위: A9:E9 (5열 병합)
  텍스트: (빈 셀)
  행 높이: 15px
  배경: WHITE
```

#### 통합 프로젝트 안내 섹션 헤더 (행 10)

```
행 10:
  셀 범위: A10:E10 (5열 병합)
  텍스트: "통합 프로젝트 안내"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px
```

#### 통합 프로젝트 데이터행 (행 11~15)

```
행 11:
  A11: "부여 시점"
    스타일: 라벨
  B11:E11: (4열 병합) "Day 5 교육 종료 시"
    스타일: 본문
  행 높이: 25px

행 12:
  A12: "제출 기한"
    스타일: 라벨
  B12:E12: (4열 병합) "교육 종료 후 2주 이내"
    스타일: 본문
  행 높이: 25px

행 13:
  A13: "팀 구성"
    스타일: 라벨
  B13:E13: (4열 병합) "개인 또는 2~3인 팀"
    스타일: 본문
  행 높이: 25px

행 14:
  A14: "필수 포함 기술"
    스타일: 라벨
  B14:E14: (4열 병합) "다음 중 최소 3개 이상:\n- LLM API 활용 (Day 1): 멀티턴 대화, 프롬프트 엔지니어링\n- 데이터 처리 (Day 2): 문서 요약, PDF 처리, Function Calling\n- RAG 시스템 (Day 3~4): 벡터 검색, 하이브리드 검색, 리랭킹\n- Agent 도구 연동 (Day 4~5): 웹검색 Agent, MCP 서버\n- MAS 아키텍처 (Day 5): 멀티에이전트 협업, Agent Card 설계"
    스타일: 본문 (정렬 left/top)
  행 높이: 105px

행 15:
  A15: "제출물"
    스타일: 라벨
  B15:E15: (4열 병합) "1. 소스 코드: GitHub 리포지토리 또는 ZIP 파일\n2. 아키텍처 문서: 시스템 구성도, 기술 선택 근거\n3. 데모 영상 또는 실행 가이드: 5분 이내 시연 영상 또는 README\n4. 발표 자료: 10분 발표용 슬라이드"
    스타일: 본문 (정렬 left/top)
  행 높이: 75px
```

#### 빈 행 (행 16)

```
행 16:
  셀 범위: A16:E16 (5열 병합)
  텍스트: (빈 셀)
  행 높이: 15px
  배경: WHITE
```

#### 실습 환경 섹션 헤더 (행 17)

```
행 17:
  셀 범위: A17:E17 (5열 병합)
  텍스트: "실습 환경 요구사항"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px
```

#### 실습 환경 테이블 헤더 (행 18)

```
행 18:
  A18: "항목"
  B18:C18: (2열 병합) "최소 사양"
  D18:E18: (2열 병합) "권장 사양"
  스타일 (전체):
    폰트: Arial, 11pt, Bold
    색상: WHITE
    배경: GREEN_MID
    정렬: horizontal='center', vertical='center'
    행 높이: 30px
```

#### 실습 환경 데이터행 (행 19~25)

```
행 19:
  A19: "운영체제"
    스타일: 본문 강조 (정렬 center/center)
  B19:C19: (2열 병합) "Windows 10 / macOS 12 / Ubuntu 20.04"
    스타일: 본문
  D19:E19: (2열 병합) "Windows 11 / macOS 14 / Ubuntu 22.04"
    스타일: 본문
  행 높이: 25px

행 20:
  A20: "CPU"
    스타일: 본문 강조 (정렬 center/center)
  B20:C20: (2열 병합) "Intel i5 / Apple M1"
    스타일: 본문
  D20:E20: (2열 병합) "Intel i7 / Apple M2 이상"
    스타일: 본문
  행 높이: 25px

행 21:
  A21: "RAM"
    스타일: 본문 강조 (정렬 center/center)
  B21:C21: (2열 병합) "8GB"
    스타일: 본문
  D21:E21: (2열 병합) "16GB 이상"
    스타일: 본문
  행 높이: 25px

행 22:
  A22: "디스크"
    스타일: 본문 강조 (정렬 center/center)
  B22:C22: (2열 병합) "SSD 20GB 여유 공간"
    스타일: 본문
  D22:E22: (2열 병합) "SSD 50GB 이상 여유 공간"
    스타일: 본문
  행 높이: 25px

행 23:
  A23: "Python"
    스타일: 본문 강조 (정렬 center/center)
  B23:C23: (2열 병합) "Python 3.10 이상"
    스타일: 본문
  D23:E23: (2열 병합) "Python 3.11 ~ 3.12"
    스타일: 본문
  행 높이: 25px

행 24:
  A24: "IDE"
    스타일: 본문 강조 (정렬 center/center)
  B24:C24: (2열 병합) "VS Code"
    스타일: 본문
  D24:E24: (2열 병합) "VS Code + Python/Jupyter 확장"
    스타일: 본문
  행 높이: 25px

행 25:
  A25: "API 키"
    스타일: 본문 강조 (정렬 center/center)
  B25:C25: (2열 병합) "OpenAI API 키 (필수)"
    스타일: 본문
  D25:E25: (2열 병합) "OpenAI + Anthropic + Google AI + Groq API 키"
    스타일: 본문
  행 높이: 25px
```

#### 빈 행 (행 26)

```
행 26:
  셀 범위: A26:E26 (5열 병합)
  텍스트: (빈 셀)
  행 높이: 15px
  배경: WHITE
```

#### 사전 준비사항 섹션 헤더 (행 27)

```
행 27:
  셀 범위: A27:E27 (5열 병합)
  텍스트: "사전 준비사항"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px
```

#### 사전 준비사항 데이터행 (행 28~32)

```
행 28:
  A28: "1"
    스타일: 본문 강조 (배경 GREEN_LIGHT, 정렬 center/center)
  B28:E28: (4열 병합) "Python 3.11 설치 및 가상환경(venv) 생성 확인"
    스타일: 본문
  행 높이: 25px

행 29:
  A29: "2"
    스타일: 본문 강조 (배경 GREEN_LIGHT, 정렬 center/center)
  B29:E29: (4열 병합) "VS Code 설치 및 Python 확장 설정"
    스타일: 본문
  행 높이: 25px

행 30:
  A30: "3"
    스타일: 본문 강조 (배경 GREEN_LIGHT, 정렬 center/center)
  B30:E30: (4열 병합) "OpenAI API 키 발급 (https://platform.openai.com)"
    스타일: 본문
  행 높이: 25px

행 31:
  A31: "4"
    스타일: 본문 강조 (배경 GREEN_LIGHT, 정렬 center/center)
  B31:E31: (4열 병합) "Anthropic, Google AI, Groq API 키 발급 (권장, 교육 전 안내)"
    스타일: 본문
  행 높이: 25px

행 32:
  A32: "5"
    스타일: 본문 강조 (배경 GREEN_LIGHT, 정렬 center/center)
  B32:E32: (4열 병합) "Git 설치 및 GitHub 계정 생성 (통합 프로젝트 제출용)"
    스타일: 본문
  행 높이: 25px
```

---

## Sheet 4: 강사 소개

### 시트명
```
강사 소개
```

### 열 너비

| 열 | 너비 |
|----|------|
| A | 20 |
| B | 70 |

### 행별 데이터

#### 타이틀 (행 1)

```
행 1:
  셀 범위: A1:B1 (2열 병합)
  텍스트: "강사 프로필"
  스타일:
    폰트: Arial, 20pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 45px
```

#### 빈 행 (행 2)

```
행 2:
  셀 범위: A2:B2 (2열 병합)
  텍스트: (빈 셀)
  행 높이: 10px
  배경: WHITE
```

#### 기본 정보 (행 3~4)

```
행 3:
  A3: "성명"
    스타일: 라벨 (Arial 10pt Bold, GREEN_DARK, 배경 GREEN_LIGHT, 정렬 center/center)
  B3: "이해경"
    스타일: 본문 (Arial 10pt Regular, DARK_GRAY, 배경 WHITE, 정렬 left/center)
  행 높이: 25px

행 4:
  A4: "현재 소속"
    스타일: 라벨
  B4: "유니콘주식회사 (CEO)"
    스타일: 본문
  행 높이: 25px
```

#### 빈 행 (행 5)

```
행 5:
  셀 범위: A5:B5 (2열 병합)
  텍스트: (빈 셀)
  행 높이: 10px
  배경: WHITE
```

#### 핵심 역량 섹션 (행 6~9)

```
행 6:
  셀 범위: A6:B6 (2열 병합)
  텍스트: "핵심 역량"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px

행 7:
  A7: "AI / GenAI"
    스타일: 라벨
  B7: "AI 기반 기획, 설계, 개발, 배포 코칭 (Claude, Claude Code, Cursor 등 활용)\n머신러닝/딥러닝 설계 및 개발\n생성형 AI 기반의 서비스 기획 및 프로덕트 매니지먼트"
    스타일: 본문 (정렬 left/top)
  행 높이: 60px

행 8:
  A8: "Cloud Native"
    스타일: 라벨
  B8: "Cloud Native App 개발/배포: Docker, Kubernetes, Helm, Jenkins, Istio, ArgoCD, Spring Boot, Spring Cloud, React/Vue.js\nMicroService & MSA 설계: DDD, Cloud Design Pattern 기반 외부 아키텍처, UML/Clean/Hexagonal 기반 내부 아키텍처\nIBM Cloud Garage 워크숍 프로그램 주도 및 컨테이너 플랫폼 구축"
    스타일: 본문 (정렬 left/top)
  행 높이: 60px

행 9:
  A9: "Agile Coaching"
    스타일: 라벨
  B9: "Agile Coaching: 팀빌딩, Lean Startup, Scrum, Kanban\nKB, 하나은행, 코스콤 등 다양한 기업의 애자일 코칭 수행\n자산관리서비스, 부동산 임대관리, 건강 적금, 자동차검사 예약 등 실무 프로젝트 기획/개발/출시"
    스타일: 본문 (정렬 left/top)
  행 높이: 60px
```

#### 빈 행 (행 10)

```
행 10:
  셀 범위: A10:B10 (2열 병합)
  텍스트: (빈 셀)
  행 높이: 10px
  배경: WHITE
```

#### 주요 강의 이력 섹션 (행 11~13)

```
행 11:
  셀 범위: A11:B11 (2열 병합)
  텍스트: "주요 강의 이력"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px

행 12:
  A12: "기업 교육"
    스타일: 라벨
  B12: "KTDS Digital Garage 1기~5기 (Cloud Design 패턴 기반 App Modernization)\nKB DigiTech Bootcamp (신입행원 대상 애자일 기획 및 MVP 개발 코칭)\nKB 마이데이터/기업뱅킹/수신상품부/Wallet Agile Coaching\nKB PO 연수 Coaching (신입 PO 대상 애자일 사상 및 기법 교육)\n비상교육 CNA 부트캠프 (IT 직원 대상 CNA 기획/설계/개발/배포)\nHANA IBM Cloud Garage (하나은행 직원 클라우드 기술 역량 향상)\nMetLife DDD&AM 설계 및 Pilot 구축"
    스타일: 본문 (정렬 left/top)
  행 높이: 120px

행 13:
  A13: "공공/대학 교육"
    스타일: 라벨
  B13: "연세대 AI 최고경영자 과정 (1기~3기): 산업별 AI 유즈케이스와 생성형 AI 기반 기획\nAI 활용 DT 서비스 기획자 멘토링\nAI 활용 프로덕트매니저 부트캠프\nCNA 부트캠프 (러닝스푼즈 협업, 직장인 대상)"
    스타일: 본문 (정렬 left/top)
  행 높이: 75px
```

#### 빈 행 (행 14)

```
행 14:
  셀 범위: A14:B14 (2열 병합)
  텍스트: (빈 셀)
  행 높이: 10px
  배경: WHITE
```

#### 자격/인증 섹션 (행 15~16)

```
행 15:
  셀 범위: A15:B15 (2열 병합)
  텍스트: "자격/인증"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px

행 16:
  A16: "보유 자격"
    스타일: 라벨
  B16: "IBM Certified Agile Coach\nPSM I (Professional Scrum Master)\nPMP (Project Management Principal)\nJTBD & ODI Associates\nIBM Certified Architect"
    스타일: 본문 (정렬 left/top)
  행 높이: 90px
```

#### 빈 행 (행 17)

```
행 17:
  셀 범위: A17:B17 (2열 병합)
  텍스트: (빈 셀)
  행 높이: 10px
  배경: WHITE
```

#### 저서 및 활동 섹션 (행 18~19)

```
행 18:
  셀 범위: A18:B18 (2열 병합)
  텍스트: "저서 및 활동"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px

행 19:
  A19: "저서/블로그"
    스타일: 라벨
  B19: "저서: 마이크로서비스패턴 쉽게 개발하기\n블로그: 온달의 해피클라우드 (https://happycloud-lee.tistory.com) - 약 79만 조회수"
    스타일: 본문 (정렬 left/top)
  행 높이: 45px
```

#### 빈 행 (행 20)

```
행 20:
  셀 범위: A20:B20 (2열 병합)
  텍스트: (빈 셀)
  행 높이: 10px
  배경: WHITE
```

#### 교육 철학 섹션 (행 21~22)

```
행 21:
  셀 범위: A21:B21 (2열 병합)
  텍스트: "교육 철학"
  스타일:
    폰트: Arial, 13pt, Bold
    색상: WHITE
    배경: GREEN_DARK
    정렬: horizontal='center', vertical='center'
    행 높이: 30px

행 22:
  A22: "교육 철학"
    스타일: 라벨
  B22: "\"실습으로 증명하고, 프로젝트로 완성하는 교육\"\n\n실무 경험과 이론의 결합이 효과적인 솔루션 제공의 핵심이라고 판단하며,\n개발자와 사용자의 직접적인 소통이 혁신을 이끄는 동력이라고 생각합니다."
    스타일: 본문 (정렬 left/top)
  행 높이: 75px
```

---

## 종합 체크리스트

### 데이터 정합성

- [x] Day 1: 4개 모듈 (1-1, 1-2, 1-3, 1-4) -- 모두 포함, 소계 7h (2h+1.5h+1h+2.5h)
- [x] Day 2: 5개 모듈 (2-1, 2-2, 2-3, 2-4, 2-5) -- 모두 포함, 소계 7h (1h+1h+1h+2h+2h)
- [x] Day 3: 4개 모듈 (3-1, 3-2, 3-3, 3-4) -- 모두 포함, 소계 7h (1.5h+1.5h+1h+3h)
- [x] Day 4: 4개 모듈 (4-1, 4-2, 4-3, 4-4) -- 모두 포함, 소계 7h (2.5h+0.5h+2h+2h)
- [x] Day 5: 3개 모듈 (5-1, 5-2, 5-3) -- 모두 포함, 소계 7h (2h+2.5h+2.5h)
- [x] 총 20개 모듈, 총 35시간 -- 원본 데이터와 일치
- [x] 이론/실습/토론 비율: 58%/36%/6% -- 원본 데이터와 일치
- [x] 평가 기준: 일별 과제 40% + 통합 프로젝트 40% + 참여도 20% = 100%
- [x] 강사 프로필: 기본정보, 핵심역량(3분야), 강의이력(2유형), 자격(5개), 저서/블로그, 교육철학 -- 모두 매핑

### 명세 완전성

- [x] 모든 시트(4개)의 셀 데이터, 병합 범위, 스타일 정보 포함
- [x] 모든 시트의 열 너비 정보 포함
- [x] 모든 행의 행 높이 정보 포함
- [x] 색상 팔레트 8개 역할 모두 정의 (HEX 코드 포함)
- [x] 폰트 체계 7개 역할 모두 정의 (크기/스타일/색상 포함)
- [x] 레이아웃 규칙(테두리, 줄바꿈, 행 높이, 인쇄 설정) 완전 정의
- [x] 심화과정 시트 없음 (단일 과정이므로 생략)
- [x] 커리큘럼 시트의 세부 학습 내용은 curriculum-detailed.md의 모듈별 세부 내용을 충실히 반영

### 시트 구성

- [x] Sheet 1: 과정 개요 (25행, 4열)
- [x] Sheet 2: 커리큘럼 (29행, 7열)
- [x] Sheet 3: 평가 및 환경 (32행, 5열)
- [x] Sheet 4: 강사 소개 (22행, 2열)

---

## 파일 정보

```
명세서 파일: /Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/excel-syllabus-specification.md
출력 Excel: /Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/ai-agent-development-syllabus.xlsx
총 시트: 4개 (과정 개요, 커리큘럼, 평가 및 환경, 강사 소개)
시트 구성: 기본과정만 있는 경우 (기본+심화 분리 없음)
```
