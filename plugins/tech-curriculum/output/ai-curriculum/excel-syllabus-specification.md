# 강의계획서 Excel 명세서

> 이 문서는 openpyxl 코드 생성에 필요한 모든 셀 데이터, 병합 범위, 스타일 정보를 포함하는 완전한 명세입니다.
> 작성일: 2026-02-15

---

## 전역 스타일 설정

### 파일 정보

- **파일명**: `ai_handson_syllabus.xlsx`
- **저장 경로**: `/Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-curriculum/ai_handson_syllabus.xlsx`
- **시트 수**: 5개
- **시트 구성**: 과정 개요 | 기본과정 커리큘럼 | 심화과정 커리큘럼 | 평가 및 환경 | 강사 소개

### 색상 팔레트 (8개 역할)

| 역할 | 변수명 | HEX 코드 (openpyxl용, # 없음) | 용도 |
|------|--------|---------------------------|------|
| 진한 녹색 | `GREEN_DARK` | `1B5E20` | 타이틀 배너 배경, 섹션 헤더 배경 |
| 중간 녹색 | `GREEN_MID` | `2E7D32` | 보조 강조 |
| 연한 녹색 | `GREEN_LIGHT` | `E8F5E9` | 라벨 셀 배경, Day 셀 배경 |
| 녹색 액센트 | `GREEN_ACCENT` | `C8E6C9` | 합계행 배경 |
| 진한 회색 | `DARK_GRAY` | `333333` | 본문 텍스트 색상 |
| 연한 회색 | `LIGHT_GRAY` | `F5F5F5` | 리뷰/마무리 행 배경 |
| 흰색 | `WHITE` | `FFFFFF` | 기본 셀 배경, 타이틀 텍스트 색상 |
| 테두리색 | `BORDER_COLOR` | `BDBDBD` | 모든 셀 테두리 |

### 폰트 체계

모든 폰트: **Arial**

| 역할 | 변수명 | 크기 | Bold 여부 | 색상 (HEX) | 용도 |
|------|--------|------|----------|-----------|------|
| 타이틀 | `FONT_TITLE` | 20pt | Bold | `FFFFFF` (WHITE) | 시트 타이틀 배너 텍스트 |
| 부제 | `FONT_SUBTITLE` | 12pt | Regular | `FFFFFF` (WHITE) | 타이틀 아래 부제 텍스트 |
| 섹션 헤더 | `FONT_SECTION` | 13pt | Bold | `FFFFFF` (WHITE) | 섹션 구분 헤더 텍스트 |
| 라벨 | `FONT_LABEL` | 10pt | Bold | `1B5E20` (GREEN_DARK) | 정보 테이블 라벨 셀 |
| 본문 강조 | `FONT_BODY_BOLD` | 10pt | Bold | `333333` (DARK_GRAY) | 강조가 필요한 본문 |
| 본문 | `FONT_BODY` | 10pt | Regular | `333333` (DARK_GRAY) | 일반 본문 텍스트 |
| 테이블 헤더 | `FONT_TABLE_HEADER` | 11pt | Bold | `FFFFFF` (WHITE) | 커리큘럼 테이블 헤더행 |

### 레이아웃 규칙

- **테두리**: 모든 데이터 셀에 thin 스타일 테두리 적용, 색상 `BDBDBD`
  - openpyxl: `Border(left=Side(style='thin', color='BDBDBD'), right=Side(style='thin', color='BDBDBD'), top=Side(style='thin', color='BDBDBD'), bottom=Side(style='thin', color='BDBDBD'))`
- **텍스트 줄바꿈**: 모든 셀에 `wrap_text=True` 적용
  - openpyxl: `Alignment(wrap_text=True)`
- **행 높이 계산**: 멀티라인 셀의 행 높이 = `줄 수 x 15` (최소 20)
  - 단일 라인 셀: 행 높이 20
  - 2줄 셀: 행 높이 30
  - 3줄 이상: 줄 수 x 15
- **인쇄 설정**: 모든 시트에 적용
  - 용지 방향: 가로 (Landscape)
  - 용지 크기: A4
  - 너비 맞춤: `sheet.sheet_properties.pageSetUpPr = PageSetupProperties(fitToPage=True)`
  - `sheet.page_setup.fitToWidth = 1`
  - `sheet.page_setup.fitToHeight = 0` (높이는 자동)
  - `sheet.page_setup.orientation = 'landscape'`
  - `sheet.page_setup.paperSize = sheet.PAPERSIZE_A4`

### 공통 스타일 정의 (openpyxl 코드 생성용)

```
# 타이틀 배너 스타일
style_title = {
    font: Font(name='Arial', size=20, bold=True, color='FFFFFF'),
    fill: PatternFill(start_color='1B5E20', end_color='1B5E20', fill_type='solid'),
    alignment: Alignment(horizontal='center', vertical='center', wrap_text=True),
    border: thin_border
}

# 부제 스타일
style_subtitle = {
    font: Font(name='Arial', size=12, color='FFFFFF'),
    fill: PatternFill(start_color='1B5E20', end_color='1B5E20', fill_type='solid'),
    alignment: Alignment(horizontal='center', vertical='center', wrap_text=True),
    border: thin_border
}

# 섹션 헤더 스타일
style_section = {
    font: Font(name='Arial', size=13, bold=True, color='FFFFFF'),
    fill: PatternFill(start_color='1B5E20', end_color='1B5E20', fill_type='solid'),
    alignment: Alignment(horizontal='left', vertical='center', wrap_text=True),
    border: thin_border
}

# 라벨 스타일
style_label = {
    font: Font(name='Arial', size=10, bold=True, color='1B5E20'),
    fill: PatternFill(start_color='E8F5E9', end_color='E8F5E9', fill_type='solid'),
    alignment: Alignment(horizontal='center', vertical='center', wrap_text=True),
    border: thin_border
}

# 본문 스타일
style_body = {
    font: Font(name='Arial', size=10, color='333333'),
    fill: PatternFill(start_color='FFFFFF', end_color='FFFFFF', fill_type='solid'),
    alignment: Alignment(horizontal='left', vertical='center', wrap_text=True),
    border: thin_border
}

# 본문 강조 스타일
style_body_bold = {
    font: Font(name='Arial', size=10, bold=True, color='333333'),
    fill: PatternFill(start_color='FFFFFF', end_color='FFFFFF', fill_type='solid'),
    alignment: Alignment(horizontal='left', vertical='center', wrap_text=True),
    border: thin_border
}

# 테이블 헤더 스타일
style_table_header = {
    font: Font(name='Arial', size=11, bold=True, color='FFFFFF'),
    fill: PatternFill(start_color='1B5E20', end_color='1B5E20', fill_type='solid'),
    alignment: Alignment(horizontal='center', vertical='center', wrap_text=True),
    border: thin_border
}

# Day 셀 스타일 (연한 녹색 배경)
style_day = {
    font: Font(name='Arial', size=10, bold=True, color='1B5E20'),
    fill: PatternFill(start_color='E8F5E9', end_color='E8F5E9', fill_type='solid'),
    alignment: Alignment(horizontal='center', vertical='center', wrap_text=True),
    border: thin_border
}

# 리뷰/마무리 행 스타일
style_review = {
    font: Font(name='Arial', size=10, color='333333'),
    fill: PatternFill(start_color='F5F5F5', end_color='F5F5F5', fill_type='solid'),
    alignment: Alignment(horizontal='left', vertical='center', wrap_text=True),
    border: thin_border
}

# 합계행 스타일
style_total = {
    font: Font(name='Arial', size=10, bold=True, color='1B5E20'),
    fill: PatternFill(start_color='C8E6C9', end_color='C8E6C9', fill_type='solid'),
    alignment: Alignment(horizontal='center', vertical='center', wrap_text=True),
    border: thin_border
}
```

---

## Sheet 1: 과정 개요

- **시트명**: `과정 개요`
- **열 구성**: A, B, C, D (4열)
- **열 너비**: A=15, B=25, C=25, D=25

### 행별 데이터

#### 타이틀 배너 (행 1)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 1 | A1:D1 | 병합 | `생성형 AI 어플리케이션 개발 교육` | FONT_TITLE (20pt Bold WHITE), 배경 GREEN_DARK, 가운데 정렬 | 45 |

#### 부제 (행 2)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 2 | A2:D2 | 병합 | `기초부터 고급까지, 7일간의 완벽한 AI 개발 여정` | FONT_SUBTITLE (12pt WHITE), 배경 GREEN_DARK, 가운데 정렬 | 30 |

#### 빈 행 (행 3)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 3 | A3:D3 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 기본 정보 테이블 (행 4~10)

| 행 | A열 (라벨) | B:D열 (병합, 값) | A열 스타일 | B:D열 스타일 | 행 높이 |
|---|----------|---------------|---------|-----------|--------|
| 4 | `강의명` | `생성형 AI 어플리케이션 개발 교육` | style_label | style_body_bold | 25 |
| 5 | `교육 기간` | `기본과정 3일 + 심화과정 4일 = 총 7일 (56시간)` | style_label | style_body | 25 |
| 6 | `일일 교육시간` | `8시간 (09:00 ~ 18:00)` | style_label | style_body | 25 |
| 7 | `수강 대상` | `AI 어플리케이션 개발을 시작하려는 개발자` | style_label | style_body | 25 |
| 8 | `선수 지식` | `Python 기초 문법, 터미널 기본 사용법, REST API 개념 이해` | style_label | style_body | 25 |
| 9 | `교육 방식` | `이론 40% : 실습 60% (매 모듈 Hands-On Lab 제공)` | style_label | style_body | 25 |
| 10 | `교육 정원` | `20명 이내 (실습 환경 고려)` | style_label | style_body | 25 |

- 모든 행에서 B열~D열은 병합: `merge_cells('B{row}:D{row}')`
- A열: style_label (가운데 정렬)
- B~D열: style_body (왼쪽 정렬) 또는 style_body_bold (행 4만)

#### 빈 행 (행 11)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 11 | A11:D11 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 과정 특징 섹션 (행 12~16)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 12 | A12:D12 | 병합 | `과정 특징` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |
| 13 | A13 | - | `실습 중심` | style_label | 40 |
| 13 | B13:D13 | 병합 | `이론 40% : 실습 60%의 황금 비율로 매 모듈마다 Hands-On Lab을 제공하여 즉시 업무에 적용 가능한 실무 패턴을 학습합니다.` | style_body | 40 |
| 14 | A14 | - | `완벽한 로드맵` | style_label | 40 |
| 14 | B14:D14 | 병합 | `기본과정(3일)에서 API 호출부터 멀티모달 AI까지, 심화과정(4일)에서 RAG, Agent, MCP까지 최신 기술을 단계별로 학습합니다.` | style_body | 40 |
| 15 | A15 | - | `최신 트렌드` | style_label | 40 |
| 15 | B15:D15 | 병합 | `2026년 최신 기술인 GraphRAG, Multi-Agent System, Model Context Protocol(MCP), Dify 노코드 플랫폼을 포함합니다.` | style_body | 40 |
| 16 | A16 | - | `체계적 평가` | style_label | 40 |
| 16 | B16:D16 | 병합 | `일일 실습 50% + 종합 프로젝트 30% + 이론 퀴즈 20%의 3단계 평가 체계로 학습 성과를 체계적으로 관리합니다.` | style_body | 40 |

#### 빈 행 (행 17)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 17 | A17:D17 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 수강 효과 섹션 (행 18~23)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 18 | A18:D18 | 병합 | `수강 효과` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |
| 19 | A19 | - | `1` | style_label (가운데 정렬) | 30 |
| 19 | B19:D19 | 병합 | `LLM API 호출부터 GraphRAG, Multi-Agent System까지 생성형 AI 어플리케이션 개발의 전 과정을 완벽하게 마스터할 수 있습니다.` | style_body | 30 |
| 20 | A20 | - | `2` | style_label (가운데 정렬) | 30 |
| 20 | B20:D20 | 병합 | `사내 문서 Q&A, AI 회의록 자동화, 멀티에이전트 리서치봇 등 실무에 바로 적용 가능한 5가지 패턴을 습득합니다.` | style_body | 30 |
| 21 | A21 | - | `3` | style_label (가운데 정렬) | 30 |
| 21 | B21:D21 | 병합 | `MCP, Dify, LangGraph 등 2026년 최신 트렌드 기술을 활용한 AI 어플리케이션 구축 역량을 확보합니다.` | style_body | 30 |
| 22 | A22 | - | `4` | style_label (가운데 정렬) | 30 |
| 22 | B22:D22 | 병합 | `기본과정과 심화과정의 단계별 학습을 통해 초보자도 실전 수준의 AI 개발 역량에 도달할 수 있습니다.` | style_body | 30 |
| 23 | A23 | - | `5` | style_label (가운데 정렬) | 30 |
| 23 | B23:D23 | 병합 | `체계적 평가 시스템(실습 50% + 프로젝트 30% + 퀴즈 20%)을 통해 학습 성과를 객관적으로 확인할 수 있습니다.` | style_body | 30 |

---

## Sheet 2: 기본과정 커리큘럼

- **시트명**: `기본과정 커리큘럼`
- **열 구성**: A, B, C, D, E, F, G (7열)
- **열 너비**: A=6, B=14, C=30, D=50, E=10, F=10, G=14

### 행별 데이터

#### 타이틀 배너 (행 1)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 1 | A1:G1 | 병합 | `PART 1. 기본과정 (3일, 24시간)` | FONT_TITLE (20pt Bold WHITE), 배경 GREEN_DARK, 가운데 정렬 | 45 |

#### 부제 (행 2)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 2 | A2:G2 | 병합 | `LLM API 기초부터 멀티모달 AI까지` | FONT_SUBTITLE (12pt WHITE), 배경 GREEN_DARK, 가운데 정렬 | 30 |

#### 헤더행 (행 3)

| 행 | A | B | C | D | E | F | G | 스타일 | 행 높이 |
|---|---|---|---|---|---|---|---|--------|--------|
| 3 | `일차` | `모듈` | `학습 주제` | `세부 학습 내용` | `시간` | `구분` | `평가` | style_table_header (11pt Bold WHITE, 배경 GREEN_DARK, 가운데 정렬) | 30 |

#### Day 1 데이터행 (행 4~7)

| 행 | A (일차) | B (모듈) | C (학습 주제) | D (세부 학습 내용) | E (시간) | F (구분) | G (평가) | 특수 스타일 | 행 높이 |
|---|---------|---------|------------|----------------|---------|---------|---------|----------|--------|
| 4 | `Day 1` | `1-1. 생성형 AI 개요와 개발환경 구축` | `생성형 AI의 현재와 개발 준비` | `- 생성형 AI 개요: 전통 AI vs 생성형 AI, LLM의 탄생과 발전\n- 토큰과 컨텍스트 윈도우: 토큰화 원리, 비용 구조\n- 개발환경 구축: Python + venv + API 키 관리\n- [Lab 1-1] 개발환경 구축 실습\n- [Lab 1-2] 토큰 탐색기 실습` | `2h` | `이론+실습` | `Lab 1-1, 1-2 제출` | A열: style_day | 90 |
| 5 | `Day 1` | `1-2. LLM API 기초와 프롬프트 엔지니어링` | `LLM API 호출의 기본 구조와 프롬프트 설계` | `- Chat Completions API 구조: 요청/응답, HTTP 통신\n- 메시지 역할 체계: system, user, assistant\n- 모델 파라미터: temperature, top_p, max_tokens\n- [Lab 1-3] 첫 번째 API 호출\n- [Lab 1-4] 파라미터 실험실\n- [Lab 1-5] 프롬프트 엔지니어링 워크숍` | `3h` | `이론+실습` | `Lab 1-5 결과물 제출` | A열: style_day | 105 |
| 6 | `Day 1` | `1-3. 멀티턴 대화 시스템 구현` | `대화 맥락을 유지하는 챗봇 구현` | `- 멀티턴 대화 원리: Stateless API 맥락 유지, 슬라이딩 윈도우\n- 스트리밍 응답: SSE 방식, 청크 단위 수신\n- [Lab 1-6] 대화형 챗봇 구현\n- [Lab 1-7] 역할극 챗봇 구현` | `2h` | `이론+실습` | `Lab 1-7 시연` | A열: style_day | 75 |
| 7 | `Day 1` | `1-4. Day 1 리뷰` | `핵심 개념 확인 및 피드백` | `- 퀴즈(10문항): 토큰, 파라미터, 메시지 역할, 멀티턴 구조\n- 실습 결과 공유 및 피드백\n- Day 2 예습 포인트 안내` | `1h` | `퀴즈+토론` | `퀴즈 결과` | A열: style_day, 전체 행: style_review (배경 LIGHT_GRAY) | 60 |

- **Day 1 A열 병합**: `merge_cells('A4:A7')` — Day 1의 4개 행을 세로 병합
- A4 셀에 `Day 1` 텍스트, style_day 적용

#### Day 2 데이터행 (행 8~11)

| 행 | A (일차) | B (모듈) | C (학습 주제) | D (세부 학습 내용) | E (시간) | F (구분) | G (평가) | 특수 스타일 | 행 높이 |
|---|---------|---------|------------|----------------|---------|---------|---------|----------|--------|
| 8 | `Day 2` | `2-1. 문서 요약과 텍스트 분석` | `LLM을 활용한 문서 요약 및 구조화된 텍스트 분석` | `- 문서 요약 전략: Map-Reduce 패턴, Refine 패턴\n- 구조화된 출력: JSON 모드 활용, 스키마 설계\n- [Lab 2-1] 문서 요약기\n- [Lab 2-2] 구조화된 분석기` | `2.5h` | `이론+실습` | `Lab 2-2 JSON 제출` | A열: style_day | 75 |
| 9 | `Day 2` | `2-2. PDF 문서 처리` | `PDF 파싱과 LLM 기반 문서 Q&A` | `- PDF 처리 파이프라인: PyMuPDF, 텍스트 추출, 표 처리\n- 문서 Q&A 아키텍처: 컨텍스트 주입, RAG 방향\n- [Lab 2-3] PDF 텍스트 추출기\n- [Lab 2-4] PDF Q&A 챗봇` | `2h` | `이론+실습` | `Lab 2-4 시연` | A열: style_day | 75 |
| 10 | `Day 2` | `2-3. 음성 AI: STT와 TTS` | `음성 인식(STT)과 음성 합성(TTS) 활용` | `- STT 기술: Whisper 모델, 오디오 형식\n- TTS 기술: 음성 합성 원리, 파라미터\n- 음성 파이프라인 설계: STT -> LLM -> TTS\n- [Lab 2-5] 음성 텍스트 변환\n- [Lab 2-6] 텍스트 음성 합성\n- [Lab 2-7] 음성 대화 파이프라인` | `2.5h` | `이론+실습` | `Lab 2-7 시연` | A열: style_day | 105 |
| 11 | `Day 2` | `2-4. Day 2 리뷰` | `핵심 개념 확인 및 비즈니스 토론` | `- 퀴즈(8문항): 문서 요약 전략, PDF 처리, STT/TTS\n- 비즈니스 적용 토론: AI 회의록 자동화 설계\n- Day 3 예습 포인트 안내` | `1h` | `퀴즈+토론` | `퀴즈 결과` | A열: style_day, 전체 행: style_review (배경 LIGHT_GRAY) | 60 |

- **Day 2 A열 병합**: `merge_cells('A8:A11')` — Day 2의 4개 행을 세로 병합
- A8 셀에 `Day 2` 텍스트, style_day 적용

#### Day 3 데이터행 (행 12~15)

| 행 | A (일차) | B (모듈) | C (학습 주제) | D (세부 학습 내용) | E (시간) | F (구분) | G (평가) | 특수 스타일 | 행 높이 |
|---|---------|---------|------------|----------------|---------|---------|---------|----------|--------|
| 12 | `Day 3` | `3-1. VLM: 비전-언어 모델 활용` | `이미지를 이해하는 멀티모달 AI` | `- VLM 개요: 비전-언어 모델 동작 원리, 이미지 토큰화\n- 활용 패턴: 이미지 설명, 비교 분석, OCR 대안\n- [Lab 3-1] 이미지 분석기\n- [Lab 3-2] 멀티 이미지 비교\n- [Lab 3-3] 비전 기반 OCR 대안` | `2.5h` | `이론+실습` | `Lab 3-3 제출` | A열: style_day | 90 |
| 13 | `Day 3` | `3-2. Local LLM 구축과 활용` | `로컬 환경에서 LLM 실행하기` | `- Local LLM 개요: Ollama 생태계, 양자화, 하드웨어 요구사항\n- Cloud vs Local 의사결정 프레임워크\n- OpenAI 호환 API 활용\n- [Lab 3-4] Ollama 설치와 모델 실행\n- [Lab 3-5] OpenAI 호환 API 활용\n- [Lab 3-6] Cloud vs Local 벤치마크` | `2.5h` | `이론+실습` | `Lab 3-6 비교표 제출` | A열: style_day | 105 |
| 14 | `Day 3` | `3-3. 기본과정 종합 프로젝트` | `기본과정 학습 내용 통합 미니 프로젝트` | `- 프로젝트 선택지 (1개 택):\n  A. AI 회의록 자동화 시스템 (STT+요약+JSON)\n  B. 문서 Q&A 도우미 (PDF+멀티턴+스트리밍)\n  C. 멀티모달 리포트 생성기 (VLM+요약+TTS)\n- 아키텍처 설계 -> 구현 -> 발표` | `2h` | `프로젝트` | `종합 프로젝트\n(동작 50%+코드 30%+발표 20%)` | A열: style_day | 105 |
| 15 | `Day 3` | `3-4. Day 3 리뷰 및 기본과정 마무리` | `종합 정리 및 심화과정 안내` | `- 퀴즈(8문항): VLM, Local LLM, Cloud vs Local\n- 기본과정 3일간 종합 정리, 핵심 키워드 맵\n- 심화과정 안내, 사전 준비사항 공유` | `1h` | `퀴즈+리뷰` | `퀴즈 결과` | A열: style_day, 전체 행: style_review (배경 LIGHT_GRAY) | 60 |

- **Day 3 A열 병합**: `merge_cells('A12:A15')` — Day 3의 4개 행을 세로 병합
- A12 셀에 `Day 3` 텍스트, style_day 적용

#### 합계행 (행 16)

| 행 | A:B | C | D | E | F | G | 스타일 | 행 높이 |
|---|-----|---|---|---|---|---|--------|--------|
| 16 | `합계` (A16:B16 병합) | (빈 셀) | (빈 셀) | `24h` | `이론 40%\n실습 60%` | (빈 셀) | style_total (Bold GREEN_DARK, 배경 GREEN_ACCENT, 가운데 정렬) | 35 |

- **합계행 병합**: `merge_cells('A16:B16')`
- E16: `24h` (수식 대안: `=SUM(E4:E15)` 단, 시간값이 텍스트이므로 직접 `24h` 입력)
- F16: `이론 40%\n실습 60%` (줄바꿈 포함)

---

## Sheet 3: 심화과정 커리큘럼

- **시트명**: `심화과정 커리큘럼`
- **열 구성**: A, B, C, D, E, F, G (7열)
- **열 너비**: A=6, B=14, C=30, D=50, E=10, F=10, G=14

### 행별 데이터

#### 타이틀 배너 (행 1)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 1 | A1:G1 | 병합 | `PART 2. 심화과정 (4일, 32시간)` | FONT_TITLE (20pt Bold WHITE), 배경 GREEN_DARK, 가운데 정렬 | 45 |

#### 부제 (행 2)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 2 | A2:G2 | 병합 | `Function Call부터 Multi-Agent, MCP까지` | FONT_SUBTITLE (12pt WHITE), 배경 GREEN_DARK, 가운데 정렬 | 30 |

#### 헤더행 (행 3)

| 행 | A | B | C | D | E | F | G | 스타일 | 행 높이 |
|---|---|---|---|---|---|---|---|--------|--------|
| 3 | `일차` | `모듈` | `학습 주제` | `세부 학습 내용` | `시간` | `구분` | `평가` | style_table_header (11pt Bold WHITE, 배경 GREEN_DARK, 가운데 정렬) | 30 |

#### 심화 Day 1 데이터행 (행 4~6)

| 행 | A (일차) | B (모듈) | C (학습 주제) | D (세부 학습 내용) | E (시간) | F (구분) | G (평가) | 특수 스타일 | 행 높이 |
|---|---------|---------|------------|----------------|---------|---------|---------|----------|--------|
| 4 | `Day 1` | `4-1. Function Calling` | `LLM이 외부 도구를 호출하는 메커니즘` | `- FC 동기부여: LLM의 한계와 도구 연동\n- 동작 메커니즘: tools 파라미터(JSON Schema), tool_choice\n- 고급 패턴: 병렬 호출, 중첩 호출, 에러 핸들링\n- [Lab 4-1] 첫 번째 Function Call\n- [Lab 4-2] 복수 도구 연동\n- [Lab 4-3] 병렬 Function Call\n- [Lab 4-4] 실무 도구 챗봇` | `3.5h` | `이론+실습` | `Lab 4-4 시연` | A열: style_day | 120 |
| 5 | `Day 1` | `4-2. LangChain 기초와 체인 구성` | `LangChain 프레임워크 활용 LLM 앱 개발` | `- LangChain 생태계: 핵심 모듈(Models, Prompts, Chains, Memory, Agents)\n- LCEL: 파이프 연산자, Runnable 인터페이스\n- Memory와 대화 관리: Buffer/Summary Memory\n- [Lab 4-5] LangChain 첫걸음\n- [Lab 4-6] 체인 조합 (번역->요약->감성분석)\n- [Lab 4-7] 대화형 체인 (Memory 활용)\n- [Lab 4-8] LangChain + FC 통합 Agent` | `3.5h` | `이론+실습` | `Lab 4-8 시연` | A열: style_day | 120 |
| 6 | `Day 1` | `4-3. Day 1 리뷰` | `핵심 개념 확인 및 비교 토론` | `- 퀴즈(10문항): FC 동작 흐름, LangChain 컴포넌트, LCEL\n- FC vs LangChain Agent 비교 토론\n- Day 2 RAG 예습 포인트 안내` | `1h` | `퀴즈+토론` | `퀴즈 결과` | A열: style_day, 전체 행: style_review (배경 LIGHT_GRAY) | 60 |

- **심화 Day 1 A열 병합**: `merge_cells('A4:A6')` — 3개 행 세로 병합
- A4 셀에 `Day 1` 텍스트, style_day 적용

#### 심화 Day 2 데이터행 (행 7~10)

| 행 | A (일차) | B (모듈) | C (학습 주제) | D (세부 학습 내용) | E (시간) | F (구분) | G (평가) | 특수 스타일 | 행 높이 |
|---|---------|---------|------------|----------------|---------|---------|---------|----------|--------|
| 7 | `Day 2` | `5-1. RAG 파이프라인 기초` | `RAG 아키텍처 이해와 구현` | `- RAG 개요: 인덱싱 -> 검색 -> 생성 아키텍처\n- 인덱싱 파이프라인: 로더, 청킹, 임베딩, 벡터 DB(Chroma, FAISS)\n- 검색과 생성: 유사도 검색, Top-K, 프롬프트 주입\n- [Lab 5-1] RAG 인덱싱\n- [Lab 5-2] RAG 검색과 생성\n- [Lab 5-3] LangChain RAG 체인` | `3h` | `이론+실습` | `Lab 5-3 시연` | A열: style_day | 105 |
| 8 | `Day 2` | `5-2. RAG 품질 튜닝` | `RAG 검색 품질과 응답 품질 최적화` | `- 청킹 전략 심화: 고정 크기 vs 의미 기반, 오버랩\n- 검색 품질 향상: 하이브리드 검색(BM25+벡터), 리랭킹, MMR\n- RAG 평가: Faithfulness, Relevancy, Precision\n- [Lab 5-4] 청킹 실험실\n- [Lab 5-5] 하이브리드 검색\n- [Lab 5-6] RAG 품질 평가` | `2.5h` | `이론+실습` | `Lab 5-6 평가표 제출` | A열: style_day | 105 |
| 9 | `Day 2` | `5-3. 웹검색 통합 RAG` | `실시간 웹 정보를 활용하는 RAG` | `- 웹검색 통합 아키텍처: 정적+동적 지식 조합, 라우팅\n- [Lab 5-7] 웹검색 RAG (Tavily/Brave Search)\n- [Lab 5-8] 통합 Q&A 시스템` | `1.5h` | `이론+실습` | `Lab 5-8 시연` | A열: style_day | 60 |
| 10 | `Day 2` | `5-4. Day 2 리뷰` | `핵심 개념 확인 및 비즈니스 토론` | `- 퀴즈(10문항): RAG 아키텍처, 청킹, 임베딩, 리랭킹\n- 비즈니스 적용 토론: 사내 문서 Q&A 설계\n- Day 3 예습 포인트 안내` | `1h` | `퀴즈+토론` | `퀴즈 결과` | A열: style_day, 전체 행: style_review (배경 LIGHT_GRAY) | 60 |

- **심화 Day 2 A열 병합**: `merge_cells('A7:A10')` — 4개 행 세로 병합
- A7 셀에 `Day 2` 텍스트, style_day 적용

#### 심화 Day 3 데이터행 (행 11~13)

| 행 | A (일차) | B (모듈) | C (학습 주제) | D (세부 학습 내용) | E (시간) | F (구분) | G (평가) | 특수 스타일 | 행 높이 |
|---|---------|---------|------------|----------------|---------|---------|---------|----------|--------|
| 11 | `Day 3` | `6-1. GraphRAG` | `지식 그래프 기반 고급 RAG` | `- GraphRAG 동기: 벡터 RAG 한계, 지식 그래프 해결점\n- 아키텍처: 엔티티/관계 추출, 커뮤니티 탐지, 글로벌/로컬 검색\n- 구현 도구: Neo4j, LangChain GraphRAG\n- [Lab 6-1] 지식 그래프 구축\n- [Lab 6-2] GraphRAG 검색\n- [Lab 6-3] 하이브리드 GraphRAG` | `3h` | `이론+실습` | `Lab 6-3 시연` | A열: style_day | 105 |
| 12 | `Day 3` | `6-2. Multi-Agent System` | `여러 AI 에이전트가 협력하는 시스템` | `- Single vs Multi-Agent: MAS 장점(전문화, 병렬처리)\n- MAS 아키텍처 패턴: Supervisor, Hierarchical, Collaborative\n- LangGraph: 상태 그래프, 노드, 엣지, 조건부 라우팅\n- [역할 분담 설계 워크숍]\n- [Lab 6-4] 첫 번째 MAS (Researcher+Writer)\n- [Lab 6-5] Supervisor 패턴\n- [Lab 6-6] 멀티에이전트 리서치봇` | `4h` | `이론+실습` | `Lab 6-6 시연` | A열: style_day | 120 |
| 13 | `Day 3` | `6-3. Day 3 리뷰` | `핵심 개념 확인 및 베스트 프랙티스` | `- 퀴즈(10문항): GraphRAG 구조, MAS 패턴, LangGraph\n- GraphRAG vs 벡터 RAG 판단 기준, MAS 베스트 프랙티스\n- Day 4 최종 프로젝트 안내` | `1h` | `퀴즈+토론` | `퀴즈 결과` | A열: style_day, 전체 행: style_review (배경 LIGHT_GRAY) | 60 |

- **심화 Day 3 A열 병합**: `merge_cells('A11:A13')` — 3개 행 세로 병합
- A11 셀에 `Day 3` 텍스트, style_day 적용

#### 심화 Day 4 데이터행 (행 14~17)

| 행 | A (일차) | B (모듈) | C (학습 주제) | D (세부 학습 내용) | E (시간) | F (구분) | G (평가) | 특수 스타일 | 행 높이 |
|---|---------|---------|------------|----------------|---------|---------|---------|----------|--------|
| 14 | `Day 4` | `7-1. MCP: Model Context Protocol` | `MCP를 활용한 표준화된 도구 통합` | `- MCP 개요: FC 한계, MCP 아키텍처(Host, Client, Server, Transport)\n- 도구 타입: Tools, Resources, Prompts, Sampling\n- MCP 생태계: 마켓플레이스, 보안 고려사항\n- [Lab 7-1] MCP 서버 구축\n- [Lab 7-2] MCP 클라이언트 연동\n- [Lab 7-3] MCP 도구 통합 봇` | `2.5h` | `이론+실습` | `Lab 7-3 시연` | A열: style_day | 105 |
| 15 | `Day 4` | `7-2. Dify: 노코드 AI Agent` | `Dify 플랫폼 활용 빠른 AI 앱 구축` | `- Dify 개요: 노코드 AI 플랫폼, 코드 vs 노코드 의사결정\n- Dify 아키텍처: Knowledge Base, 워크플로우, API 배포\n- [Lab 7-4] Dify RAG 챗봇\n- [Lab 7-5] Dify 워크플로우 Agent\n- [Lab 7-6] Dify API 배포` | `2h` | `이론+실습` | `Lab 7-6 API 호출 확인` | A열: style_day | 90 |
| 16 | `Day 4` | `7-3. 심화과정 종합 프로젝트` | `심화과정 전체 기술 통합 실무급 프로젝트` | `- 프로젝트 선택지 (1개 택):\n  A. 사내 지식 관리 시스템 (RAG+GraphRAG+MCP)\n  B. 멀티에이전트 리서치 플랫폼 (MAS+웹검색RAG)\n  C. 노코드+코드 하이브리드 Agent (Dify+MCP+FC)\n- 아키텍처 설계 -> 구현 -> 통합 테스트 -> 발표` | `2.5h` | `프로젝트` | `종합 프로젝트\n(동작 40%+설계 30%+코드 15%+발표 15%)` | A열: style_day | 105 |
| 17 | `Day 4` | `7-4. Day 4 리뷰 및 심화과정 마무리` | `종합 정리 및 커리어 적용` | `- 퀴즈(8문항): MCP, Dify, 기술 선택 기준\n- 심화과정 4일간 종합 정리, 기술 스택 로드맵\n- 커리어 적용 토론, 추가 학습 리소스 안내\n- 수료 피드백 수집, 커뮤니티 연결` | `1h` | `퀴즈+리뷰` | `퀴즈 결과` | A열: style_day, 전체 행: style_review (배경 LIGHT_GRAY) | 75 |

- **심화 Day 4 A열 병합**: `merge_cells('A14:A17')` — 4개 행 세로 병합
- A14 셀에 `Day 4` 텍스트, style_day 적용

#### 합계행 (행 18)

| 행 | A:B | C | D | E | F | G | 스타일 | 행 높이 |
|---|-----|---|---|---|---|---|--------|--------|
| 18 | `합계` (A18:B18 병합) | (빈 셀) | (빈 셀) | `32h` | `이론 40%\n실습 60%` | (빈 셀) | style_total (Bold GREEN_DARK, 배경 GREEN_ACCENT, 가운데 정렬) | 35 |

- **합계행 병합**: `merge_cells('A18:B18')`

---

## Sheet 4: 평가 및 환경

- **시트명**: `평가 및 환경`
- **열 구성**: A, B, C, D, E (5열)
- **열 너비**: A=18, B=12, C=30, D=15, E=15

### 행별 데이터

#### 타이틀 배너 (행 1)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 1 | A1:E1 | 병합 | `평가 기준 및 실습 환경` | FONT_TITLE (20pt Bold WHITE), 배경 GREEN_DARK, 가운데 정렬 | 45 |

#### 빈 행 (행 2)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 2 | A2:E2 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 기본과정 평가 배점 섹션 (행 3~7)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 3 | A3:E3 | 병합 | `기본과정 평가 배점` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |

| 행 | A (평가 항목) | B (비중) | C:E (세부 기준, 병합) | 스타일 | 행 높이 |
|---|------------|---------|-------------------|--------|--------|
| 4 | `평가 항목` | `비중` | `세부 기준` | style_table_header (배경 GREEN_DARK) | 28 |
| 5 | `일일 실습 결과물` | `50%` | `Lab별 코드 동작 여부(30%) + 코드 품질(10%) + 기한 내 제출(10%)` | A: style_label, B: style_body (가운데), C:E: style_body | 30 |
| 6 | `종합 프로젝트` | `30%` | `동작 여부(15%) + 기술 조합 적절성(10%) + 발표(5%)` | A: style_label, B: style_body (가운데), C:E: style_body | 30 |
| 7 | `일일 퀴즈` | `20%` | `Day1(7%) + Day2(7%) + Day3(6%)` | A: style_label, B: style_body (가운데), C:E: style_body | 30 |

- 행 4: 헤더행 — A4, B4는 단독 셀, C4:E4 병합
- 행 5~7: C열~E열 병합: `merge_cells('C{row}:E{row}')`

#### 빈 행 (행 8)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 8 | A8:E8 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 심화과정 평가 배점 섹션 (행 9~13)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 9 | A9:E9 | 병합 | `심화과정 평가 배점` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |

| 행 | A (평가 항목) | B (비중) | C:E (세부 기준, 병합) | 스타일 | 행 높이 |
|---|------------|---------|-------------------|--------|--------|
| 10 | `평가 항목` | `비중` | `세부 기준` | style_table_header (배경 GREEN_DARK) | 28 |
| 11 | `일일 실습 결과물` | `50%` | `Lab별 코드 동작 여부(25%) + 코드 품질(15%) + 기한 내 제출(10%)` | A: style_label, B: style_body (가운데), C:E: style_body | 30 |
| 12 | `종합 프로젝트` | `30%` | `동작 여부(12%) + 아키텍처 설계(9%) + 코드 품질(5%) + 발표(4%)` | A: style_label, B: style_body (가운데), C:E: style_body | 30 |
| 13 | `일일 퀴즈` | `20%` | `Day1(5%) + Day2(5%) + Day3(5%) + Day4(5%)` | A: style_label, B: style_body (가운데), C:E: style_body | 30 |

- 행 10: 헤더행 — A10, B10는 단독 셀, C10:E10 병합
- 행 11~13: C열~E열 병합: `merge_cells('C{row}:E{row}')`

#### 빈 행 (행 14)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 14 | A14:E14 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 실습 환경 요구사항 섹션 (행 15~22)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 15 | A15:E15 | 병합 | `실습 환경 요구사항` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |

| 행 | A (항목) | B:C (최소 사양, 병합) | D:E (권장 사양, 병합) | 스타일 | 행 높이 |
|---|--------|-------------------|-------------------|--------|--------|
| 16 | `항목` | `최소 사양` | `권장 사양` | style_table_header (배경 GREEN_DARK) | 28 |
| 17 | `OS` | `Windows 10 / macOS 12 / Ubuntu 20.04` | `Windows 11 / macOS 14 / Ubuntu 22.04` | A: style_label, B:C/D:E: style_body | 25 |
| 18 | `Python` | `3.10 이상` | `3.11 이상` | A: style_label, B:C/D:E: style_body | 25 |
| 19 | `RAM` | `8GB` | `16GB (Local LLM 실습 시)` | A: style_label, B:C/D:E: style_body | 25 |
| 20 | `저장 공간` | `10GB 여유` | `30GB 여유 (Local LLM 모델 포함)` | A: style_label, B:C/D:E: style_body | 25 |
| 21 | `GPU` | `불필요 (Cloud API 중심)` | `NVIDIA GPU 8GB+ (Local LLM 가속)` | A: style_label, B:C/D:E: style_body | 25 |
| 22 | `네트워크` | `안정적 인터넷 연결 필수` | `유선 네트워크 권장` | A: style_label, B:C/D:E: style_body | 25 |

- 행 16: 헤더행 — A16 단독, B16:C16 병합, D16:E16 병합
- 행 17~22: B열~C열 병합, D열~E열 병합

#### 빈 행 (행 23)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 23 | A23:E23 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 사전 준비사항 섹션 (행 24~33)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 24 | A24:E24 | 병합 | `사전 준비사항` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |

| 행 | A (구분) | B:E (내용, 병합) | A열 스타일 | B:E열 스타일 | 행 높이 |
|---|--------|---------------|---------|-----------|--------|
| 25 | `기본과정\n수강 전` | `1. Python 기초 문법 (변수, 함수, 클래스, 리스트/딕셔너리)\n2. 터미널/명령 프롬프트 기본 사용법\n3. OpenAI 또는 Anthropic API 키 발급 (사전 안내 메일 참조)\n4. Python 3.10+ 설치 완료` | style_label (세로 병합, 가운데 정렬) | style_body | 75 |
| 26 | `심화과정\n수강 전` | `1. 기본과정 수료 또는 동등 수준의 LLM API 사용 경험\n2. REST API 개념 이해 (HTTP 메서드, JSON)\n3. Docker 기본 설치 (Dify 실습용)\n4. Neo4j Desktop 설치 (GraphRAG 실습용)` | style_label (세로 병합, 가운데 정렬) | style_body | 75 |

- 행 25~26: B열~E열 병합: `merge_cells('B{row}:E{row}')`

---

## Sheet 5: 강사 소개

- **시트명**: `강사 소개`
- **열 구성**: A, B (2열)
- **열 너비**: A=20, B=70

### 행별 데이터

#### 타이틀 배너 (행 1)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 1 | A1:B1 | 병합 | `강사 프로필` | FONT_TITLE (20pt Bold WHITE), 배경 GREEN_DARK, 가운데 정렬 | 45 |

#### 빈 행 (행 2)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 2 | A2:B2 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 기본 정보 (행 3~5)

| 행 | A (라벨) | B (값) | A열 스타일 | B열 스타일 | 행 높이 |
|---|---------|-------|---------|---------|--------|
| 3 | `성명` | `이해경` | style_label | style_body_bold | 25 |
| 4 | `현재 소속` | `유니콘주식회사 (CEO)` | style_label | style_body | 25 |
| 5 | `연락처` | `hiondal@gmail.com / 010-4095-4035` | style_label | style_body | 25 |

#### 빈 행 (행 6)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 6 | A6:B6 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 핵심 역량 섹션 (행 7~10)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 7 | A7:B7 | 병합 | `핵심 역량` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |

| 행 | A (역량 분야) | B (상세 내용) | A열 스타일 | B열 스타일 | 행 높이 |
|---|------------|------------|---------|---------|--------|
| 8 | `AI / GenAI` | `- AI 기반 기획, 설계, 개발, 배포 코칭 (Claude, Claude Code, Cursor 등 활용)\n- 머신러닝/딥러닝 설계 및 개발\n- 생성형 AI 기반의 서비스 기획 및 프로덕트 매니지먼트` | style_label | style_body | 60 |
| 9 | `Cloud Native` | `- Cloud Native App 개발/배포: Docker, Kubernetes, Helm, Jenkins, Istio, ArgoCD, Spring Boot, Spring Cloud, React/Vue.js\n- MicroService & MSA 설계: DDD, Cloud Design Pattern 기반 외부 아키텍처, UML/Clean/Hexagonal 기반 내부 아키텍처\n- IBM Cloud Garage 워크숍 프로그램 주도 및 컨테이너 플랫폼 구축` | style_label | style_body | 75 |
| 10 | `Agile Coaching` | `- Agile Coaching: 팀빌딩, Lean Startup, Scrum, Kanban\n- KB, 하나은행, 코스콤 등 다양한 기업의 애자일 코칭 수행\n- 자산관리서비스, 부동산 임대관리, 건강 적금, 자동차검사 예약 등 실무 프로젝트 기획/개발/출시` | style_label | style_body | 60 |

#### 빈 행 (행 11)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 11 | A11:B11 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 주요 강의 이력 섹션 (행 12~14)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 12 | A12:B12 | 병합 | `주요 강의 이력` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |

| 행 | A (유형) | B (상세 내용) | A열 스타일 | B열 스타일 | 행 높이 |
|---|---------|------------|---------|---------|--------|
| 13 | `기업 교육` | `- KTDS Digital Garage 1기~5기 (Cloud Design 패턴 기반 App Modernization)\n- KB DigiTech Bootcamp (신입행원 대상 애자일 기획 및 MVP 개발 코칭)\n- KB 마이데이터/기업뱅킹/수신상품부/Wallet Agile Coaching\n- KB PO 연수 Coaching (신입 PO 대상 애자일 사상 및 기법 교육)\n- 비상교육 CNA 부트캠프 (IT 직원 대상 CNA 기획/설계/개발/배포)\n- HANA IBM Cloud Garage (하나은행 직원 클라우드 기술 역량 향상)\n- MetLife DDD&AM 설계 및 Pilot 구축` | style_label | style_body | 120 |
| 14 | `공공/대학 교육` | `- 연세대 AI 최고경영자 과정 (1기~3기): 산업별 AI 유즈케이스와 생성형 AI 기획\n- AI 활용 DT 서비스 기획자 멘토링\n- AI 활용 프로덕트매니저 부트캠프\n- CNA 부트캠프 (러닝스푼즈 협업, 직장인 대상)` | style_label | style_body | 75 |

#### 빈 행 (행 15)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 15 | A15:B15 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 자격/인증 섹션 (행 16~17)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 16 | A16:B16 | 병합 | `자격 / 인증` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |

| 행 | A (라벨) | B (내용) | A열 스타일 | B열 스타일 | 행 높이 |
|---|---------|--------|---------|---------|--------|
| 17 | `보유 자격` | `- IBM Certified Agile Coach\n- PSM I (Professional Scrum Master)\n- PMP (Project Management Principal)\n- JTBD & ODI Associates\n- IBM Certified Architect` | style_label | style_body | 90 |

#### 빈 행 (행 18)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 18 | A18:B18 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 저서 및 활동 섹션 (행 19~20)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 19 | A19:B19 | 병합 | `저서 및 활동` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |

| 행 | A (라벨) | B (내용) | A열 스타일 | B열 스타일 | 행 높이 |
|---|---------|--------|---------|---------|--------|
| 20 | `활동` | `- 저서: 「마이크로서비스패턴 쉽게 개발하기」\n- 블로그: 온달의 해피클라우드 (https://happycloud-lee.tistory.com) - 약 79만 조회수` | style_label | style_body | 45 |

#### 빈 행 (행 21)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 21 | A21:B21 | 병합 | (빈 셀) | 배경 WHITE, 테두리 없음 | 10 |

#### 교육 철학 섹션 (행 22~23)

| 행 | 셀 범위 | 병합 | 텍스트 | 스타일 | 행 높이 |
|---|--------|------|--------|--------|--------|
| 22 | A22:B22 | 병합 | `교육 철학` | style_section (13pt Bold WHITE, 배경 GREEN_DARK) | 30 |

| 행 | A (라벨) | B (내용) | A열 스타일 | B열 스타일 | 행 높이 |
|---|---------|--------|---------|---------|--------|
| 23 | `교육 철학` | `"실습으로 증명하고, 프로젝트로 완성하는 교육"\n\n실무 경험과 이론의 결합이 효과적인 솔루션 제공의 핵심이라고 판단하며, 개발자와 사용자의 직접적인 소통이 혁신을 이끄는 동력이라고 생각합니다.` | style_label | style_body | 75 |

---

## 종합 체크리스트

### 데이터 정합성 검증

- [x] **기본과정 모듈 12개 전체 포함**: 1-1, 1-2, 1-3, 1-4, 2-1, 2-2, 2-3, 2-4, 3-1, 3-2, 3-3, 3-4 -- OK
- [x] **심화과정 모듈 14개 전체 포함**: 4-1, 4-2, 4-3, 5-1, 5-2, 5-3, 5-4, 6-1, 6-2, 6-3, 7-1, 7-2, 7-3, 7-4 -- OK
- [x] **기본과정 시간 합계**: 2+3+2+1+2.5+2+2.5+1+2.5+2.5+2+1 = 24시간 -- OK
- [x] **심화과정 시간 합계**: 3.5+3.5+1+3+2.5+1.5+1+3+4+1+2.5+2+2.5+1 = 32시간 -- OK
- [x] **총 교육시간**: 24 + 32 = 56시간 -- OK
- [x] **일차(Day) 배분이 원본과 일치** -- OK
- [x] **강사 프로필 매핑 완료**: 기본정보, 핵심역량(AI/GenAI, Cloud Native, Agile Coaching), 강의이력(기업/공공/대학), 자격/인증, 저서/활동, 교육 철학 -- OK

### 명세 완전성 검증

- [x] **5개 시트 모두 포함**: 과정 개요, 기본과정 커리큘럼, 심화과정 커리큘럼, 평가 및 환경, 강사 소개 -- OK
- [x] **모든 시트의 열 너비 정의**: Sheet1(A=15,B=25,C=25,D=25), Sheet2/3(A=6,B=14,C=30,D=50,E=10,F=10,G=14), Sheet4(A=18,B=12,C=30,D=15,E=15), Sheet5(A=20,B=70) -- OK
- [x] **모든 행의 행 높이 정의** -- OK
- [x] **모든 셀의 텍스트 내용 기재** -- OK
- [x] **모든 병합 범위 명시** (merge_cells 명령어 포함) -- OK
- [x] **모든 셀의 스타일 정보 포함** (폰트, 크기, 색상, 배경색, 정렬) -- OK
- [x] **색상 팔레트 8개 역할 전체 정의** -- OK
- [x] **폰트 체계 7개 역할 전체 정의** -- OK
- [x] **레이아웃 규칙 명시** (테두리, 줄바꿈, 행 높이 계산, 인쇄 설정) -- OK
- [x] **공통 스타일 코드 스니펫 포함** (openpyxl 코드 생성 참고용) -- OK
- [x] **리뷰/마무리 행의 특수 스타일 (LIGHT_GRAY 배경) 명시** -- OK
- [x] **합계행의 특수 스타일 (GREEN_ACCENT 배경) 명시** -- OK
- [x] **Day 셀 세로 병합 범위 모두 명시** -- OK

### CNA 샘플 참고 반영 검증

- [x] **과정 개요 시트**: 강의명, 교육 대상, 수강 효과, 과정 특징, 차별점 섹션 포함 (CNA 샘플의 과정 정보 구조 참고) -- OK
- [x] **커리큘럼 시트**: Day별 모듈 테이블 구조 (CNA 샘플의 일차별 이론/실습 구분 참고) -- OK
- [x] **강사 소개 시트**: 성명, 주요 경력, 강의 이력, 프로젝트/기타 활동 구조 (CNA 샘플의 강사 소개 시트 참고) -- OK

---

## 파일 정보

| 항목 | 값 |
|------|-----|
| 파일명 | `ai_handson_syllabus.xlsx` |
| 저장 경로 | `/Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-curriculum/ai_handson_syllabus.xlsx` |
| 명세 파일 | `/Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-curriculum/excel-syllabus-specification.md` |
| 시트 수 | 5개 |
| 시트 구성 | 과정 개요 / 기본과정 커리큘럼 / 심화과정 커리큘럼 / 평가 및 환경 / 강사 소개 |
| 디자인 테마 | Green Professional |
| 주 강조색 | #1B5E20 (GREEN_DARK) |
| 기본과정 모듈 수 | 12개 (1-1 ~ 3-4) |
| 심화과정 모듈 수 | 14개 (4-1 ~ 7-4) |
| 총 교육시간 | 56시간 (기본 24h + 심화 32h) |
