# PPTX 제안서 명세서

> 이 문서는 PptxGenJS 코드 생성에 필요한 모든 좌표, 색상, 폰트, 데이터를 포함하는 완전한 명세입니다.
> 작성일: 2026-02-15

---

## 전역 스타일 설정

### 파일 정보

- **파일명**: `ai_handson_proposal.pptx`
- **저장 경로**: `/Users/dreamondal/workspace/tech-curriculum/output/ai-curriculum/ai_handson_proposal.pptx`
- **이미지 디렉토리**: `/Users/dreamondal/workspace/tech-curriculum/output/ai-curriculum/images/`
- **슬라이드 수**: 10장
- **슬라이드 크기**: 16:9 (width: 10, height: 5.625)

### 컬러 팔레트 (13개 역할)

| 역할 | 변수명 | HEX 코드 | 용도 |
|------|--------|----------|------|
| 주 강조색 | `primary` | `#4A1B6D` | 액센트 바, 테이블 헤더 배경, 푸터 라인, 화살표 |
| 밝은 강조색 | `primaryBright` | `#7B3FA0` | 기본과정 화살표/배지, 밝은 액센트 요소 |
| 어두운 강조색 | `primaryDark` | `#2D1045` | 표지 이미지 오버레이 |
| 연한 강조색 | `primaryLight` | `#EDE4F5` | 인용구 배경, 강조 박스 배경 |
| 테이블 헤더 | `headerBg` | `#4A1B6D` | 테이블 헤더행 배경 |
| 주 텍스트색 | `dark` | `#1A1A2E` | 제목, 본문 강조 텍스트 |
| 보조 텍스트색 | `darkGray` | `#333333` | 일반 본문 텍스트 |
| 부제 텍스트색 | `midGray` | `#666666` | 부제, 캡션, 설명 텍스트 |
| 구분선색 | `lightGray` | `#D0D0D0` | 수평 구분선, 테이블 외곽 보더 |
| 라벨 배경색 | `vLightGray` | `#F3F0F7` | 그리드 셀 배경, 교대행 배경 (퍼플 틴트) |
| 기본 배경색 | `white` | `#FFFFFF` | 슬라이드 배경, 테이블 홀수행 |
| 테이블 교대행 | `tableAlt` | `#F3EEFA` | 테이블 짝수행 배경 (연한 라벤더) |
| 테이블 보더 | `tableBorder` | `#C8BED8` | 테이블 셀 보더 (퍼플 틴트 그레이) |

### 폰트 체계

모든 폰트: **맑은 고딕 (Malgun Gothic)** 계열

| 역할 | 변수명 | 크기 | 스타일 | 색상 | 용도 |
|------|--------|------|--------|------|------|
| 표지 제목 | `coverTitle` | 30pt | Bold | `dark` (#1A1A2E) | 표지 메인 타이틀 |
| 슬라이드 제목 | `title` | 22pt | Bold | `dark` (#1A1A2E) | 각 슬라이드 제목 |
| 부제 (일반) | `subtitle` | 18pt | SemiBold | `midGray` (#666666) | 슬라이드 설명 (Normal 모드) |
| 부제 (Compact) | `subtitleCompact` | 14pt | Bold | `midGray` (#666666) | 슬라이드 설명 (Compact 모드) |
| 본문 강조 | `bodyBold` | 14pt | Bold | `darkGray` (#333333) | 라벨, 헤더, 강조 텍스트 |
| 본문 일반 | `body` | 12pt | Regular | `darkGray` (#333333) | 일반 본문, 테이블 본문 |
| 표지 인용구 | `coverQuote` | 11pt | Italic | `midGray` (#666666) | 표지 인용구 박스 내부 |
| 푸터 페이지 | `footerPage` | 10pt | Regular | `midGray` (#666666) | 푸터 페이지 번호 |

**최소 폰트 크기**: 12pt (예외: 표지 인용구 11pt, 푸터 10pt)

### 레이아웃 규격

```
슬라이드 크기      : width=10, height=5.625 (인치)
좌우 마진 (제목)   : 0.5"
좌우 마진 (테이블) : 0.25"
좌우 마진 (그리드) : 0.5"
푸터 Y 위치       : 5.35"
```

---

## 공통 컴포넌트

### addTitle(title, subtitle, compact)

제목 + 부제 + 구분선을 표준화된 위치에 배치하는 컴포넌트.

**Normal 모드** (`compact = false`):

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 액센트 바 (세로) | 0.5 | 0.3 | 0.07 | 0.5 | - | `primary` (#4A1B6D) fill | - |
| 제목 텍스트 | 0.72 | 0.25 | 8.78 | 0.5 | 22pt Bold | `dark` (#1A1A2E) | left, middle |
| 부제 텍스트 | 0.72 | 0.72 | 8.78 | 0.35 | 18pt SemiBold | `midGray` (#666666) | left, middle |
| 구분선 | 0.25 | 1.2 | 9.5 | 0.008 | - | `lightGray` (#D0D0D0) fill | - |

**Compact 모드** (`compact = true`):

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 액센트 바 (세로) | 0.5 | 0.15 | 0.07 | 0.38 | - | `primary` (#4A1B6D) fill | - |
| 제목 텍스트 | 0.72 | 0.1 | 8.78 | 0.38 | 22pt Bold | `dark` (#1A1A2E) | left, middle |
| 부제 텍스트 | 0.72 | 0.48 | 8.78 | 0.3 | 14pt Bold | `midGray` (#666666) | left, middle |
| 구분선 | 0.25 | 0.86 | 9.5 | 0.008 | - | `lightGray` (#D0D0D0) fill | - |

### addFooter(pageNum)

모든 슬라이드 하단에 배치되는 푸터 (표지 제외).

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 푸터 라인 | 0 | 5.35 | 10 | 0.025 | - | `primary` (#4A1B6D) fill | - |
| 페이지 번호 | 9.0 | 5.37 | 0.75 | 0.2 | 10pt Regular | `midGray` (#666666) | right, top |

### cell(text, options) - 테이블 데이터 셀

```javascript
{
  text: text,
  options: {
    fontFace: "Malgun Gothic",
    fontSize: 12,
    color: "#333333",        // darkGray
    align: "left",
    valign: "middle",
    border: [
      { pt: 0.5, color: "#C8BED8" },  // top - tableBorder
      { pt: 0.5, color: "#C8BED8" },  // right
      { pt: 0.5, color: "#C8BED8" },  // bottom
      { pt: 0.5, color: "#C8BED8" }   // left
    ],
    margin: [3, 5, 3, 5],       // top, right, bottom, left (pt)
    paraSpaceAfter: 2,
    lineSpacingMultiple: 1.15,
    fill: { color: "#FFFFFF" }, // white (기본), 교대행은 tableAlt
    ...options
  }
}
```

### hCell(text, options) - 테이블 헤더 셀

```javascript
{
  text: text,
  options: {
    fontFace: "Malgun Gothic",
    fontSize: 12,
    bold: true,
    color: "#FFFFFF",           // white
    align: "center",
    valign: "middle",
    border: [
      { pt: 0.5, color: "#C8BED8" },
      { pt: 0.5, color: "#C8BED8" },
      { pt: 0.5, color: "#C8BED8" },
      { pt: 0.5, color: "#C8BED8" }
    ],
    margin: [3, 5, 3, 5],
    paraSpaceAfter: 2,
    lineSpacingMultiple: 1.15,
    fill: { color: "#4A1B6D" }, // headerBg
    ...options
  }
}
```

### 교대행 배경색 규칙

```
행 인덱스 0 (헤더): headerBg (#4A1B6D)
행 인덱스 1 (홀수 데이터): white (#FFFFFF)
행 인덱스 2 (짝수 데이터): tableAlt (#F3EEFA)
행 인덱스 3 (홀수 데이터): white (#FFFFFF)
행 인덱스 4 (짝수 데이터): tableAlt (#F3EEFA)
... 반복
```

---

## 슬라이드 1: 표지 (Cover - Split Layout)

**레이아웃**: Split Layout (좌측 이미지 50% + 우측 텍스트 50%)
**배경**: `white` (#FFFFFF)
**푸터**: 없음 (표지에는 푸터 미적용)

### 좌측 영역: 이미지 + 오버레이

| 요소 | x | y | w | h | 속성 |
|------|---|---|---|---|------|
| 커버 이미지 | 0 | 0 | 5.0 | 5.625 | `images/handson_cover.png`, sizing: cover |
| 어두운 오버레이 | 0 | 0 | 5.0 | 5.625 | fill: `primaryDark` (#2D1045), transparency: 25% |

### 우측 영역: 텍스트

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 상단 액센트 바 (수평) | 5.5 | 0.5 | 1.2 | 0.06 | - | `primary` (#4A1B6D) fill | - | - |
| 메인 제목 줄1 | 5.5 | 0.75 | 4.0 | 0.55 | 30pt Bold | `dark` (#1A1A2E) | left, top | `생성형 AI` |
| 메인 제목 줄2 | 5.5 | 1.3 | 4.0 | 0.55 | 30pt Bold | `dark` (#1A1A2E) | left, top | `어플리케이션 개발` |
| 메인 제목 줄3 | 5.5 | 1.85 | 4.0 | 0.55 | 30pt Bold | `dark` (#1A1A2E) | left, top | `Hands-On 교육` |
| 세로 액센트 바 | 5.5 | 2.7 | 0.05 | 0.7 | - | `primary` (#4A1B6D) fill | - | - |
| 소속 | 5.7 | 2.72 | 3.8 | 0.3 | 12pt Regular | `midGray` (#666666) | left, middle | `OO기관 AI교육센터` |
| 저자 이름 | 5.7 | 3.02 | 3.8 | 0.35 | 14pt Bold | `dark` (#1A1A2E) | left, middle | `홍길동 | AI 교육 전문가` |
| 인용구 박스 (배경) | 5.3 | 3.8 | 4.2 | 1.1 | - | `primaryLight` (#EDE4F5) fill, shape: pres.shapes.ROUNDED_RECTANGLE, rectRadius: 0.06 | - | - |
| 인용구 좌측 바 | 5.3 | 3.8 | 0.06 | 1.1 | - | `primary` (#4A1B6D) fill | - | - |
| 인용구 텍스트 | 5.55 | 3.9 | 3.75 | 0.9 | 11pt Italic | `midGray` (#666666) | left, middle | `"AI는 도구를 넘어 사고의 확장입니다. 7일간의 여정이 여러분의 개발 역량에 새로운 차원을 열어드립니다."` |

---

## 슬라이드 2: 인사말 (Greeting)

**레이아웃**: 커스텀
**배경**: `white` (#FFFFFF)
**푸터**: addFooter(2)

### addTitle

- 제목: `강사 인사말`
- 부제: 없음
- compact: false
- 제목만 표시 (부제 영역 생략)

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 액센트 바 | 0.5 | 0.3 | 0.07 | 0.5 | - | `primary` fill | - |
| 제목 | 0.72 | 0.25 | 8.78 | 0.5 | 22pt Bold | `dark` | left, middle |
| 구분선 | 0.25 | 0.9 | 9.5 | 0.008 | - | `lightGray` fill | - |

### 중앙 인용구 박스

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 인용구 배경 | 0.5 | 1.1 | 9.0 | 0.6 | - | `primaryLight` (#EDE4F5) fill, shape: pres.shapes.ROUNDED_RECTANGLE, rectRadius: 0.04 | - | - |
| 인용구 텍스트 | 0.7 | 1.15 | 8.6 | 0.5 | 14pt Bold | `primary` (#4A1B6D) | center, middle | `"AI는 도구를 넘어 사고의 확장입니다. 7일간의 여정이 여러분의 개발 역량에 새로운 차원을 열어드립니다."` |

### 프로필 영역

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 프로필 사진 | 0.8 | 2.0 | 1.4 | 1.4 | - | `images/handson_profile.png`, rounding: true | - | - |
| 세로 액센트 바 | 2.5 | 2.1 | 0.05 | 1.2 | - | `primary` (#4A1B6D) fill | - | - |
| 이름 | 2.75 | 2.05 | 4.0 | 0.4 | 22pt Bold | `dark` (#1A1A2E) | left, middle | `홍길동` |
| 직함 | 2.75 | 2.45 | 4.0 | 0.3 | 14pt Regular | `midGray` (#666666) | left, middle | `AI 교육 전문가 | OO기관 AI교육센터` |

### 자격사항 목록

시작 위치: x=2.75, y=2.9, 각 항목 간격: 0.3

| # | x | y | w | h | 폰트 | 색상 | 내용 |
|---|---|---|---|---|------|------|------|
| bullet 1 | 2.75 | 2.9 | 6.5 | 0.28 | 12pt Regular | `primary` (#4A1B6D) | `- AI/ML 분야 10년+ 경력` |
| bullet 2 | 2.75 | 3.18 | 6.5 | 0.28 | 12pt Regular | `primary` (#4A1B6D) | `- 기업 AI 교육 프로그램 다수 설계 및 운영` |
| bullet 3 | 2.75 | 3.46 | 6.5 | 0.28 | 12pt Regular | `primary` (#4A1B6D) | `- LLM 어플리케이션 개발 전문가` |
| bullet 4 | 2.75 | 3.74 | 6.5 | 0.28 | 12pt Regular | `primary` (#4A1B6D) | `- 前 OO기업 AI 연구소 책임연구원` |
| bullet 5 | 2.75 | 4.02 | 6.5 | 0.28 | 12pt Regular | `primary` (#4A1B6D) | `- 관련 저서 및 기술 기고 다수` |

### 하단 구분선 + 연락처

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 구분선 | 0.5 | 4.55 | 9.0 | 0.008 | - | `lightGray` fill | - | - |
| 이메일 | 0.5 | 4.7 | 4.0 | 0.25 | 12pt Regular | `midGray` (#666666) | left, middle | `education@example.com` |
| 전화번호 | 5.0 | 4.7 | 4.5 | 0.25 | 12pt Regular | `midGray` (#666666) | right, middle | `02-1234-5678` |

---

## 슬라이드 3: 교육 과정 개요 (Overview - 2x3 Grid)

**레이아웃**: 제목 + 섹션 소제목 + 2x3 그리드
**배경**: `white` (#FFFFFF)
**푸터**: addFooter(3)

### addTitle

- 제목: `교육 과정 개요`
- 부제: `기초부터 고급까지, 7일간의 완벽한 AI 개발 로드맵`
- compact: false

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 액센트 바 | 0.5 | 0.3 | 0.07 | 0.5 | - | `primary` fill | - |
| 제목 | 0.72 | 0.25 | 8.78 | 0.5 | 22pt Bold | `dark` | left, middle |
| 부제 | 0.72 | 0.72 | 8.78 | 0.35 | 18pt SemiBold | `midGray` | left, middle |
| 구분선 | 0.25 | 1.2 | 9.5 | 0.008 | - | `lightGray` fill | - |

### 섹션 소제목

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 소제목 | 0.5 | 1.35 | 9.0 | 0.35 | 18pt Bold | `primary` (#4A1B6D) | center, middle | `이론 40% : 실습 60%의 실전 중심 커리큘럼` |

### 2x3 그리드

그리드 시작: x=0.5, y=1.85
셀 구조: 좌측 라벨 영역 + 우측 값 영역
각 셀 전체 높이: 1.05"
라벨 너비: 1.15", 값 너비: 3.05"
셀 전체 너비: 4.2"
열 간격 gapX: 0.6"
행 간격 gapY: 0.12"

**Col 1 (x=0.5), Col 2 (x=5.3)**

**Row 1 (y=1.85):**

| 셀 위치 | 라벨 x | 라벨 y | 라벨 w | 라벨 h | 라벨 배경 | 라벨 텍스트 | 값 x | 값 y | 값 w | 값 h | 값 배경 | 값 텍스트 |
|---------|--------|--------|--------|--------|----------|------------|------|------|------|------|--------|----------|
| (0,0) | 0.5 | 1.85 | 1.15 | 1.05 | `primary` (#4A1B6D) | `교육\n대상` (14pt Bold, white, center) | 1.65 | 1.85 | 3.05 | 1.05 | `vLightGray` (#F3F0F7) | `AI 어플리케이션 개발을\n시작하려는 개발자` (12pt, darkGray, center) |
| (0,1) | 5.3 | 1.85 | 1.15 | 1.05 | `primary` (#4A1B6D) | `교육\n기간` (14pt Bold, white, center) | 6.45 | 1.85 | 3.05 | 1.05 | `vLightGray` (#F3F0F7) | `기본 3일 + 심화 4일\n총 7일 (56시간)` (12pt, darkGray, center) |

**Row 2 (y=3.02):**

| 셀 위치 | 라벨 x | 라벨 y | 라벨 w | 라벨 h | 라벨 배경 | 라벨 텍스트 | 값 x | 값 y | 값 w | 값 h | 값 배경 | 값 텍스트 |
|---------|--------|--------|--------|--------|----------|------------|------|------|------|------|--------|----------|
| (1,0) | 0.5 | 3.02 | 1.15 | 1.05 | `primary` (#4A1B6D) | `일일\n시간` (14pt Bold, white, center) | 1.65 | 3.02 | 3.05 | 1.05 | `vLightGray` (#F3F0F7) | `8시간/일\n(09:00 ~ 18:00)` (12pt, darkGray, center) |
| (1,1) | 5.3 | 3.02 | 1.15 | 1.05 | `primary` (#4A1B6D) | `이론\n:실습` (14pt Bold, white, center) | 6.45 | 3.02 | 3.05 | 1.05 | `vLightGray` (#F3F0F7) | `이론 40% : 실습 60%\n매 모듈 Hands-On Lab` (12pt, darkGray, center) |

**Row 3 (y=4.19):**

| 셀 위치 | 라벨 x | 라벨 y | 라벨 w | 라벨 h | 라벨 배경 | 라벨 텍스트 | 값 x | 값 y | 값 w | 값 h | 값 배경 | 값 텍스트 |
|---------|--------|--------|--------|--------|----------|------------|------|------|------|------|--------|----------|
| (2,0) | 0.5 | 4.19 | 1.15 | 1.05 | `primary` (#4A1B6D) | `핵심\n기술` (14pt Bold, white, center) | 1.65 | 4.19 | 3.05 | 1.05 | `vLightGray` (#F3F0F7) | `LLM API, RAG, MAS\nMCP, Dify, GraphRAG` (12pt, darkGray, center) |
| (2,1) | 5.3 | 4.19 | 1.15 | 1.05 | `primary` (#4A1B6D) | `평가\n방식` (14pt Bold, white, center) | 6.45 | 4.19 | 3.05 | 1.05 | `vLightGray` (#F3F0F7) | `실습 50% + 프로젝트 30%\n+ 퀴즈 20%` (12pt, darkGray, center) |

---

## 슬라이드 4: 커리큘럼 맵 (Curriculum Map - Arrows + Grid)

**레이아웃**: 과정별 화살표 + Day 헤더 배지 + 3행 콘텐츠 그리드
**배경**: `white` (#FFFFFF)
**푸터**: addFooter(4)

### addTitle

- 제목: `커리큘럼 맵`
- 부제: `기본과정 3일 + 심화과정 4일 커리큘럼 로드맵`
- compact: false

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 액센트 바 | 0.5 | 0.3 | 0.07 | 0.5 | - | `primary` fill | - |
| 제목 | 0.72 | 0.25 | 8.78 | 0.5 | 22pt Bold | `dark` | left, middle |
| 부제 | 0.72 | 0.72 | 8.78 | 0.35 | 18pt SemiBold | `midGray` | left, middle |
| 구분선 | 0.25 | 1.2 | 9.5 | 0.008 | - | `lightGray` fill | - |

### 과정별 화살표 바

좌측 라벨 영역(labelW) 확보 후, 과정별 화살표 배치.

| 요소 | x | y | w | h | 색상 | 폰트 | 텍스트 |
|------|---|---|---|---|------|------|--------|
| 기본과정 화살표 | 1.1 | 1.35 | 3.6 | 0.35 | `primaryBright` (#7B3FA0) fill, shape: pres.shapes.ROUNDED_RECTANGLE, rectRadius: 0.2 | 14pt Bold, white | `PART 1. 기본과정 (3일)` |
| 심화과정 화살표 | 4.85 | 1.35 | 4.85 | 0.35 | `primary` (#4A1B6D) fill, shape: pres.shapes.ROUNDED_RECTANGLE, rectRadius: 0.2 | 14pt Bold, white | `PART 2. 심화과정 (4일)` |

### Day 헤더 배지

행 라벨 너비: labelW = 0.8"
Day 배지 시작 x = 1.1"
기본과정 3일: 각 배지 w = 1.2", gapX = 0.0"
심화과정 4일: 각 배지 w = 1.2125", gapX = 0.0"

| Day | x | y | w | h | 색상 | 폰트 | 텍스트 |
|-----|---|---|---|---|------|------|--------|
| Day 1 (기본) | 1.1 | 1.85 | 1.2 | 0.3 | `primaryBright` (#7B3FA0) fill | 12pt Bold, white, center | `Day 1` |
| Day 2 (기본) | 2.3 | 1.85 | 1.2 | 0.3 | `primaryBright` (#7B3FA0) fill | 12pt Bold, white, center | `Day 2` |
| Day 3 (기본) | 3.5 | 1.85 | 1.2 | 0.3 | `primaryBright` (#7B3FA0) fill | 12pt Bold, white, center | `Day 3` |
| Day 1 (심화) | 4.85 | 1.85 | 1.2125 | 0.3 | `primary` (#4A1B6D) fill | 12pt Bold, white, center | `Day 1` |
| Day 2 (심화) | 6.0625 | 1.85 | 1.2125 | 0.3 | `primary` (#4A1B6D) fill | 12pt Bold, white, center | `Day 2` |
| Day 3 (심화) | 7.275 | 1.85 | 1.2125 | 0.3 | `primary` (#4A1B6D) fill | 12pt Bold, white, center | `Day 3` |
| Day 4 (심화) | 8.4875 | 1.85 | 1.2125 | 0.3 | `primary` (#4A1B6D) fill | 12pt Bold, white, center | `Day 4` |

### 3행 콘텐츠 그리드

행 라벨: 좌측 고정, 라벨W=0.8", vLightGray 배경
콘텐츠 셀: Day별 동일 너비, 12pt Regular, 중앙 정렬
행 높이: 0.95"
행 시작 Y: 2.25"
행 간격: 0.05"

**행 라벨:**

| 행 | x | y | w | h | 배경 | 폰트 | 텍스트 |
|----|---|---|---|---|------|------|--------|
| 과정 | 0.25 | 2.25 | 0.8 | 0.95 | `vLightGray` (#F3F0F7) | 12pt Bold, `dark`, center | `과정` |
| Tool | 0.25 | 3.25 | 0.8 | 0.95 | `vLightGray` (#F3F0F7) | 12pt Bold, `dark`, center | `Tool` |
| Output | 0.25 | 4.25 | 0.8 | 0.95 | `vLightGray` (#F3F0F7) | 12pt Bold, `dark`, center | `Output` |

**행 1 - 과정 (y=2.25, h=0.95):**

| Day | x | w | 내용 (12pt Regular, darkGray, center, middle) |
|-----|---|---|-------|
| 기본 Day1 | 1.1 | 1.2 | `AI 개요\nLLM API\n멀티턴 대화` |
| 기본 Day2 | 2.3 | 1.2 | `문서 요약\nPDF 처리\n음성 AI` |
| 기본 Day3 | 3.5 | 1.2 | `VLM\nLocal LLM\n종합 프로젝트` |
| 심화 Day1 | 4.85 | 1.2125 | `Function Call\nLangChain\n체인 구성` |
| 심화 Day2 | 6.0625 | 1.2125 | `RAG 기초\nRAG 튜닝\n웹검색 RAG` |
| 심화 Day3 | 7.275 | 1.2125 | `GraphRAG\nMulti-Agent\nLangGraph` |
| 심화 Day4 | 8.4875 | 1.2125 | `MCP\nDify\n종합 프로젝트` |

**행 2 - Tool (y=3.25, h=0.95):**

| Day | x | w | 내용 |
|-----|---|---|------|
| 기본 Day1 | 1.1 | 1.2 | `OpenAI API\nClaude API\nJupyter` |
| 기본 Day2 | 2.3 | 1.2 | `PyMuPDF\nWhisper\nTTS API` |
| 기본 Day3 | 3.5 | 1.2 | `Vision API\nOllama\nStreamlit` |
| 심화 Day1 | 4.85 | 1.2125 | `tools param\nLangChain\nLCEL` |
| 심화 Day2 | 6.0625 | 1.2125 | `Chroma\nFAISS\nTavily` |
| 심화 Day3 | 7.275 | 1.2125 | `Neo4j\nLangGraph\nCrewAI` |
| 심화 Day4 | 8.4875 | 1.2125 | `MCP SDK\nDify\nDocker` |

**행 3 - Output (y=4.25, h=0.95):**

| Day | x | w | 내용 |
|-----|---|---|------|
| 기본 Day1 | 1.1 | 1.2 | `Lab 1-1~1-7\n역할극 챗봇` |
| 기본 Day2 | 2.3 | 1.2 | `Lab 2-1~2-7\n음성 파이프라인` |
| 기본 Day3 | 3.5 | 1.2 | `Lab 3-1~3-6\n종합 프로젝트` |
| 심화 Day1 | 4.85 | 1.2125 | `Lab 4-1~4-8\nAgent 챗봇` |
| 심화 Day2 | 6.0625 | 1.2125 | `Lab 5-1~5-8\nRAG Q&A` |
| 심화 Day3 | 7.275 | 1.2125 | `Lab 6-1~6-6\n리서치봇` |
| 심화 Day4 | 8.4875 | 1.2125 | `Lab 7-1~7-6\n종합 프로젝트` |

각 콘텐츠 셀 border: 0.5pt `tableBorder` (#C8BED8), fill: `white` (#FFFFFF)

---

## 슬라이드 5: 기본과정 상세 1/2 (Detail Table - Compact)

**레이아웃**: 제목 + 6열 테이블
**배경**: `white` (#FFFFFF)
**Compact 모드**: YES (8행 데이터)
**푸터**: addFooter(5)

### addTitle (Compact)

- 제목: `기본과정 상세 커리큘럼`
- 부제: `Day 1-2 | AI 어플리케이션 기초 ~ 문서 처리와 음성 AI`
- compact: true

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 액센트 바 | 0.5 | 0.15 | 0.07 | 0.38 | - | `primary` fill | - |
| 제목 | 0.72 | 0.1 | 8.78 | 0.38 | 22pt Bold | `dark` | left, middle |
| 부제 | 0.72 | 0.48 | 8.78 | 0.3 | 14pt Bold | `midGray` | left, middle |
| 구분선 | 0.25 | 0.86 | 9.5 | 0.008 | - | `lightGray` fill | - |

### 테이블 상단 액센트 바

| 요소 | x | y | w | h | 색상 |
|------|---|---|---|---|------|
| 액센트 바 | 0.25 | 0.9 | 9.5 | 0.035 | `primary` (#4A1B6D) fill |

### 6열 테이블

- 위치: x=0.25, y=0.94, w=9.5
- 열 너비: 일(0.55) | 모듈명(1.6) | 시간(0.5) | 내용(4.35) | 산출물(1.25) | 방법(1.25)
- 합계: 0.55 + 1.6 + 0.5 + 4.35 + 1.25 + 1.25 = 9.5

**헤더행** (hCell):

| 열 | 텍스트 | w | align |
|----|--------|---|-------|
| 일 | `일` | 0.55 | center |
| 모듈명 | `모듈명` | 1.6 | center |
| 시간 | `시간` | 0.5 | center |
| 내용 | `주요 내용` | 4.35 | center |
| 산출물 | `산출물` | 1.25 | center |
| 방법 | `교육 방법` | 1.25 | center |

**데이터행** (cell, 교대 배경):

| # | 일 | 모듈명 | 시간 | 내용 | 산출물 | 방법 | 행 배경 |
|---|---|--------|------|------|--------|------|---------|
| 1 | Day 1 | 1-1. 생성형 AI 개요와 개발환경 구축 | 2h | AI 개요, 토큰/컨텍스트, 개발환경 구축 | Lab 1-1, 1-2 | 이론+실습 | white |
| 2 | Day 1 | 1-2. LLM API 기초와 프롬프트 엔지니어링 | 3h | Chat API 구조, 메시지 역할, 파라미터 튜닝, 프롬프트 기법 | Lab 1-3~1-5 | 이론+실습 | tableAlt |
| 3 | Day 1 | 1-3. 멀티턴 대화 시스템 구현 | 2h | 대화 히스토리 관리, 스트리밍 응답, 역할극 챗봇 | Lab 1-6, 1-7 | 이론+실습 | white |
| 4 | Day 1 | 1-4. Day 1 리뷰 | 1h | 퀴즈(10문항), 실습 결과 공유, Day 2 안내 | 퀴즈 결과 | 퀴즈+토론 | tableAlt |
| 5 | Day 2 | 2-1. 문서 요약과 텍스트 분석 | 2.5h | Map-Reduce 패턴, 구조화된 출력(JSON 모드) | Lab 2-1, 2-2 | 이론+실습 | white |
| 6 | Day 2 | 2-2. PDF 문서 처리 | 2h | PDF 파싱(PyMuPDF), 문서 Q&A 시스템 | Lab 2-3, 2-4 | 이론+실습 | tableAlt |
| 7 | Day 2 | 2-3. 음성 AI: STT와 TTS | 2.5h | Whisper STT, TTS API, 음성 대화 파이프라인 | Lab 2-5~2-7 | 이론+실습 | white |
| 8 | Day 2 | 2-4. Day 2 리뷰 | 1h | 퀴즈(8문항), 비즈니스 토론, Day 3 안내 | 퀴즈 결과 | 퀴즈+토론 | tableAlt |

**셀 속성 상세**:
- "일" 열: align=center, valign=middle, 12pt Regular
- "모듈명" 열: align=left, valign=middle, 12pt Regular (모듈명 Bold 처리: 번호부분만)
- "시간" 열: align=center, valign=middle, 12pt Regular
- "내용" 열: align=left, valign=middle, 12pt Regular
- "산출물" 열: align=center, valign=middle, 12pt Regular
- "방법" 열: align=center, valign=middle, 12pt Regular
- 모든 셀: margin=[3,5,3,5], paraSpaceAfter=2, lineSpacingMultiple=1.15
- 모든 셀 border: 0.5pt `tableBorder` (#C8BED8), 4방향

---

## 슬라이드 6: 기본과정 상세 2/2 (Detail Table - Normal)

**레이아웃**: 제목 + 6열 테이블
**배경**: `white` (#FFFFFF)
**Compact 모드**: NO (4행 데이터)
**푸터**: addFooter(6)

### addTitle (Normal)

- 제목: `기본과정 상세 커리큘럼`
- 부제: `Day 3 | 비전 AI와 Local LLM, 기본과정 종합`
- compact: false

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 액센트 바 | 0.5 | 0.3 | 0.07 | 0.5 | - | `primary` fill | - |
| 제목 | 0.72 | 0.25 | 8.78 | 0.5 | 22pt Bold | `dark` | left, middle |
| 부제 | 0.72 | 0.72 | 8.78 | 0.35 | 18pt SemiBold | `midGray` | left, middle |
| 구분선 | 0.25 | 1.2 | 9.5 | 0.008 | - | `lightGray` fill | - |

### 테이블 상단 액센트 바

| 요소 | x | y | w | h | 색상 |
|------|---|---|---|---|------|
| 액센트 바 | 0.25 | 1.25 | 9.5 | 0.035 | `primary` (#4A1B6D) fill |

### 6열 테이블

- 위치: x=0.25, y=1.28, w=9.5
- 열 너비: 동일 (0.55 | 1.6 | 0.5 | 4.35 | 1.25 | 1.25 = 9.5)

**헤더행** (hCell): 슬라이드 5와 동일

**데이터행**:

| # | 일 | 모듈명 | 시간 | 내용 | 산출물 | 방법 | 행 배경 |
|---|---|--------|------|------|--------|------|---------|
| 1 | Day 3 | 3-1. VLM: 비전-언어 모델 활용 | 2.5h | Vision API, 이미지 분석/비교, OCR 대안 | Lab 3-1~3-3 | 이론+실습 | white |
| 2 | Day 3 | 3-2. Local LLM 구축과 활용 | 2.5h | Ollama 설치, 오픈소스 모델, Cloud vs Local 비교 | Lab 3-4~3-6 | 이론+실습 | tableAlt |
| 3 | Day 3 | 3-3. 기본과정 종합 프로젝트 | 2h | 미니 프로젝트 3선택지 (AI 회의록 / 문서 Q&A / 멀티모달 리포트) | 종합 프로젝트 | 프로젝트 | white |
| 4 | Day 3 | 3-4. Day 3 리뷰 및 기본과정 마무리 | 1h | 퀴즈(8문항), 3일간 종합 정리, 심화과정 안내 | 퀴즈 결과 | 퀴즈+리뷰 | tableAlt |

---

## 슬라이드 7: 심화과정 상세 1/2 (Detail Table - Compact)

**레이아웃**: 제목 + 6열 테이블
**배경**: `white` (#FFFFFF)
**Compact 모드**: YES (7행 데이터)
**푸터**: addFooter(7)

### addTitle (Compact)

- 제목: `심화과정 상세 커리큘럼`
- 부제: `Day 1-2 | 도구 연동과 프레임워크 ~ RAG 구축과 튜닝`
- compact: true

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 액센트 바 | 0.5 | 0.15 | 0.07 | 0.38 | - | `primary` fill | - |
| 제목 | 0.72 | 0.1 | 8.78 | 0.38 | 22pt Bold | `dark` | left, middle |
| 부제 | 0.72 | 0.48 | 8.78 | 0.3 | 14pt Bold | `midGray` | left, middle |
| 구분선 | 0.25 | 0.86 | 9.5 | 0.008 | - | `lightGray` fill | - |

### 테이블 상단 액센트 바

| 요소 | x | y | w | h | 색상 |
|------|---|---|---|---|------|
| 액센트 바 | 0.25 | 0.9 | 9.5 | 0.035 | `primary` (#4A1B6D) fill |

### 6열 테이블

- 위치: x=0.25, y=0.94, w=9.5
- 열 너비: 동일 (0.55 | 1.6 | 0.5 | 4.35 | 1.25 | 1.25 = 9.5)

**헤더행** (hCell): 슬라이드 5와 동일

**데이터행**:

| # | 일 | 모듈명 | 시간 | 내용 | 산출물 | 방법 | 행 배경 |
|---|---|--------|------|------|--------|------|---------|
| 1 | Day 1 | 4-1. Function Calling | 3.5h | FC 메커니즘, 도구 정의(JSON Schema), 병렬 호출, 실무 도구 챗봇 | Lab 4-1~4-4 | 이론+실습 | white |
| 2 | Day 1 | 4-2. LangChain 기초와 체인 구성 | 3.5h | LCEL 파이프라인, Memory, Agent 통합, SequentialChain | Lab 4-5~4-8 | 이론+실습 | tableAlt |
| 3 | Day 1 | 4-3. Day 1 리뷰 | 1h | 퀴즈(10문항), FC vs Agent 비교 토론, Day 2 안내 | 퀴즈 결과 | 퀴즈+토론 | white |
| 4 | Day 2 | 5-1. RAG 파이프라인 기초 | 3h | 인덱싱(로더/청킹/임베딩), 벡터 검색, RetrievalQA 체인 | Lab 5-1~5-3 | 이론+실습 | tableAlt |
| 5 | Day 2 | 5-2. RAG 품질 튜닝 | 2.5h | 청킹 최적화, 리랭킹(Cross-Encoder), 하이브리드 검색, 평가 | Lab 5-4~5-6 | 이론+실습 | white |
| 6 | Day 2 | 5-3. 웹검색 통합 RAG | 1.5h | 웹검색 API 연동, 정적+동적 하이브리드, 통합 Q&A | Lab 5-7, 5-8 | 이론+실습 | tableAlt |
| 7 | Day 2 | 5-4. Day 2 리뷰 | 1h | 퀴즈(10문항), 사내 문서 Q&A 설계 토론, Day 3 안내 | 퀴즈 결과 | 퀴즈+토론 | white |

---

## 슬라이드 8: 심화과정 상세 2/2 (Detail Table - Compact)

**레이아웃**: 제목 + 6열 테이블
**배경**: `white` (#FFFFFF)
**Compact 모드**: YES (7행 데이터)
**푸터**: addFooter(8)

### addTitle (Compact)

- 제목: `심화과정 상세 커리큘럼`
- 부제: `Day 3-4 | 고급 RAG와 에이전트 ~ 통합과 실무 적용`
- compact: true

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 액센트 바 | 0.5 | 0.15 | 0.07 | 0.38 | - | `primary` fill | - |
| 제목 | 0.72 | 0.1 | 8.78 | 0.38 | 22pt Bold | `dark` | left, middle |
| 부제 | 0.72 | 0.48 | 8.78 | 0.3 | 14pt Bold | `midGray` | left, middle |
| 구분선 | 0.25 | 0.86 | 9.5 | 0.008 | - | `lightGray` fill | - |

### 테이블 상단 액센트 바

| 요소 | x | y | w | h | 색상 |
|------|---|---|---|---|------|
| 액센트 바 | 0.25 | 0.9 | 9.5 | 0.035 | `primary` (#4A1B6D) fill |

### 6열 테이블

- 위치: x=0.25, y=0.94, w=9.5
- 열 너비: 동일 (0.55 | 1.6 | 0.5 | 4.35 | 1.25 | 1.25 = 9.5)

**헤더행** (hCell): 슬라이드 5와 동일

**데이터행**:

| # | 일 | 모듈명 | 시간 | 내용 | 산출물 | 방법 | 행 배경 |
|---|---|--------|------|------|--------|------|---------|
| 1 | Day 3 | 6-1. GraphRAG | 3h | 지식 그래프 구축(LLM 엔티티/관계 추출), 그래프 검색, 하이브리드 | Lab 6-1~6-3 | 이론+실습 | white |
| 2 | Day 3 | 6-2. Multi-Agent System | 4h | MAS 아키텍처(Supervisor/Hierarchical), LangGraph, 리서치봇 | Lab 6-4~6-6 | 이론+실습 | tableAlt |
| 3 | Day 3 | 6-3. Day 3 리뷰 | 1h | 퀴즈(10문항), 베스트 프랙티스 공유, Day 4 안내 | 퀴즈 결과 | 퀴즈+토론 | white |
| 4 | Day 4 | 7-1. MCP: Model Context Protocol | 2.5h | MCP 서버/클라이언트 구축, Transport, 도구 통합 봇 | Lab 7-1~7-3 | 이론+실습 | tableAlt |
| 5 | Day 4 | 7-2. Dify: 노코드 AI Agent | 2h | Dify 워크플로우, Knowledge Base, API 배포 | Lab 7-4~7-6 | 이론+실습 | white |
| 6 | Day 4 | 7-3. 심화과정 종합 프로젝트 | 2.5h | 실무급 프로젝트 3선택지 (지식관리 / 리서치봇 / 하이브리드 Agent) | 종합 프로젝트 | 프로젝트 | tableAlt |
| 7 | Day 4 | 7-4. Day 4 리뷰 및 심화과정 마무리 | 1h | 퀴즈(8문항), 종합 정리, 커리어 적용 토론, 마무리 | 퀴즈 결과 | 퀴즈+리뷰 | white |

---

## 슬라이드 9: 차별화 포인트 및 기대효과 (Content - 3박스)

**레이아웃**: 제목 + 3개 수평 박스
**배경**: `white` (#FFFFFF)
**푸터**: addFooter(9)

### addTitle (Normal)

- 제목: `차별화 포인트 및 기대효과`
- 부제: `이 교육 과정만의 3가지 핵심 차별점`
- compact: false

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 |
|------|---|---|---|---|------|------|------|
| 액센트 바 | 0.5 | 0.3 | 0.07 | 0.5 | - | `primary` fill | - |
| 제목 | 0.72 | 0.25 | 8.78 | 0.5 | 22pt Bold | `dark` | left, middle |
| 부제 | 0.72 | 0.72 | 8.78 | 0.35 | 18pt SemiBold | `midGray` | left, middle |
| 구분선 | 0.25 | 1.2 | 9.5 | 0.008 | - | `lightGray` fill | - |

### 3개 박스 레이아웃

박스 영역: x=0.25, y=1.4, 전체 w=9.5
각 박스: w=3.0, h=3.8
박스 간격: gapX=0.25
박스 배경: `primaryLight` (#EDE4F5), shape: pres.shapes.ROUNDED_RECTANGLE, rectRadius: 0.08
박스 상단 바: h=0.05, `primary` (#4A1B6D) fill

**박스 1: 실습 중심 60%**

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 상단 바 | 0.25 | 1.4 | 3.0 | 0.05 | - | `primary` fill | - | - |
| 박스 배경 | 0.25 | 1.45 | 3.0 | 3.75 | - | `primaryLight` fill | - | - |
| 박스 제목 | 0.45 | 1.55 | 2.6 | 0.4 | 14pt Bold | `primary` (#4A1B6D) | center, middle | `실전 즉시 투입 가능` |
| 소제목 | 0.45 | 1.95 | 2.6 | 0.3 | 12pt Bold | `darkGray` (#333333) | center, middle | `실습 비중 60%` |
| 본문 | 0.45 | 2.35 | 2.6 | 2.7 | 12pt Regular | `darkGray` (#333333) | left, top | (아래 참조) |

박스 1 본문:
```
- 매 모듈마다 Hands-On Lab 제공
- 이론 학습 직후 코딩 실습

5가지 실무 조합 패턴:
- 사내 문서 Q&A (RAG)
- AI 회의록 자동화 (STT+요약)
- 멀티에이전트 리서치봇
- 고객 상담 챗봇 (FC+Memory)
- 이미지 분석 리포트 (VLM)
```

**박스 2: 2026년 최신 트렌드**

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 상단 바 | 3.5 | 1.4 | 3.0 | 0.05 | - | `primary` fill | - | - |
| 박스 배경 | 3.5 | 1.45 | 3.0 | 3.75 | - | `primaryLight` fill | - | - |
| 박스 제목 | 3.7 | 1.55 | 2.6 | 0.4 | 14pt Bold | `primary` (#4A1B6D) | center, middle | `최신 트렌드 반영` |
| 소제목 | 3.7 | 1.95 | 2.6 | 0.3 | 12pt Bold | `darkGray` (#333333) | center, middle | `2026년 핵심 기술 포함` |
| 본문 | 3.7 | 2.35 | 2.6 | 2.7 | 12pt Regular | `darkGray` (#333333) | left, top | (아래 참조) |

박스 2 본문:
```
- GraphRAG
  차세대 지식 그래프 RAG

- Multi-Agent System
  LangGraph 기반 협업 에이전트

- MCP (Model Context Protocol)
  표준화된 도구 통합 프로토콜

- Dify 노코드 플랫폼
  빠른 프로토타입 + 코드 확장
```

**박스 3: 체계적 평가 시스템**

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 상단 바 | 6.75 | 1.4 | 3.0 | 0.05 | - | `primary` fill | - | - |
| 박스 배경 | 6.75 | 1.45 | 3.0 | 3.75 | - | `primaryLight` fill | - | - |
| 박스 제목 | 6.95 | 1.55 | 2.6 | 0.4 | 14pt Bold | `primary` (#4A1B6D) | center, middle | `체계적 평가 시스템` |
| 소제목 | 6.95 | 1.95 | 2.6 | 0.3 | 12pt Bold | `darkGray` (#333333) | center, middle | `3단계 평가 체계` |
| 본문 | 6.95 | 2.35 | 2.6 | 2.7 | 12pt Regular | `darkGray` (#333333) | left, top | (아래 참조) |

박스 3 본문:
```
- 일일 실습 평가 (50%)
  매일 Lab 과제 제출 + 피드백

- 종합 프로젝트 (30%)
  기본/심화 각 1회
  실무 시나리오 기반 과제

- 이론 퀴즈 (20%)
  핵심 개념 확인
  즉각적 피드백 제공
```

---

## 슬라이드 10: 마무리 (Closing)

**레이아웃**: 감사 인사 + CTA + 연락처
**배경**: `white` (#FFFFFF)
**푸터**: addFooter(10)

### 중앙 콘텐츠

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 상단 액센트 바 | 4.4 | 0.5 | 1.2 | 0.06 | - | `primary` (#4A1B6D) fill | - | - |
| 메인 텍스트 | 1.0 | 0.8 | 8.0 | 0.7 | 22pt Bold | `dark` (#1A1A2E) | center, middle | `7일 후, 당신은\nAI 개발 전문가가 됩니다` |
| 구분선 | 3.5 | 1.7 | 3.0 | 0.008 | - | `lightGray` fill | - | - |

### 핵심 정리 (3개 bullet)

| # | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|---|---|---|---|---|------|------|------|------|
| 1 | 1.5 | 2.0 | 7.0 | 0.35 | 14pt Regular | `darkGray` (#333333) | center, middle | `LLM API부터 GraphRAG까지 완벽 마스터` |
| 2 | 1.5 | 2.4 | 7.0 | 0.35 | 14pt Regular | `darkGray` (#333333) | center, middle | `실무에 바로 적용 가능한 5가지 패턴 습득` |
| 3 | 1.5 | 2.8 | 7.0 | 0.35 | 14pt Regular | `darkGray` (#333333) | center, middle | `최신 트렌드 (MCP, Dify, Multi-Agent) 완전 정복` |

### CTA 버튼

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| CTA 배경 | 3.0 | 3.4 | 4.0 | 0.6 | - | `primary` (#4A1B6D) fill, shape: pres.shapes.ROUNDED_RECTANGLE, rectRadius: 0.08 | - | - |
| CTA 텍스트 | 3.0 | 3.4 | 4.0 | 0.6 | 18pt Bold | `white` (#FFFFFF) | center, middle | `지금 바로 시작하세요` |

### 연락처 영역

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 구분선 | 2.5 | 4.2 | 5.0 | 0.008 | - | `lightGray` fill | - | - |
| 이메일 | 1.5 | 4.4 | 7.0 | 0.3 | 12pt Regular | `midGray` (#666666) | center, middle | `education@example.com` |
| 전화번호 | 1.5 | 4.7 | 7.0 | 0.3 | 12pt Regular | `midGray` (#666666) | center, middle | `02-1234-5678` |

### 하단 감사 인사

| 요소 | x | y | w | h | 폰트 | 색상 | 정렬 | 내용 |
|------|---|---|---|---|------|------|------|------|
| 감사 텍스트 | 1.5 | 5.05 | 7.0 | 0.25 | 12pt Regular | `midGray` (#666666) | center, middle | `Thank you for your attention` |

---

## 종합 체크리스트

### 폰트 규격 검증

- [x] 표지 제목: 30pt Bold -- OK
- [x] 슬라이드 제목: 22pt Bold -- OK (모든 슬라이드)
- [x] 부제 (Normal): 18pt SemiBold -- OK (슬라이드 3, 4, 6, 9, 10)
- [x] 부제 (Compact): 14pt Bold -- OK (슬라이드 5, 7, 8)
- [x] 본문 강조: 14pt Bold -- OK (그리드 라벨, 박스 제목, bullet)
- [x] 본문 일반: 12pt Regular -- OK (테이블 본문, 그리드 값, 연락처)
- [x] 표지 인용구: 11pt Italic -- OK (예외 허용)
- [x] 푸터 페이지: 10pt Regular -- OK (예외 허용)
- [x] **최소 12pt 규칙 준수** (예외 2곳만: 인용구 11pt, 푸터 10pt)

### 레이아웃 검증

- [x] 모든 테이블: x=0.25, w=9.5 -- OK (슬라이드 5, 6, 7, 8)
- [x] 푸터 라인: x=0, y=5.35, w=10, h=0.025 -- OK (슬라이드 2-10)
- [x] 콘텐츠가 푸터 영역(y=5.35) 침범하지 않음 -- OK
  - 슬라이드 3 그리드 하단: y=4.19 + h=1.05 = 5.24 < 5.35 OK
  - 슬라이드 4 그리드 하단: y=4.25 + h=0.95 = 5.20 < 5.35 OK
  - 슬라이드 9 박스 하단: y=1.45 + h=3.75 = 5.20 < 5.35 OK
- [x] Compact 모드 적용: 슬라이드 5(8행), 7(7행), 8(7행) -- 모두 6개 이상 OK
- [x] Normal 모드: 슬라이드 6(4행) -- 6개 미만 OK
- [x] 슬라이드 분할: 기본과정 12모듈 -> 8+4 (2장), 심화과정 14모듈 -> 7+7 (2장) -- OK

### 데이터 정합성 검증

- [x] 기본과정 모듈 12개 전체 포함 (1-1~1-4, 2-1~2-4, 3-1~3-4) -- OK
- [x] 심화과정 모듈 14개 전체 포함 (4-1~4-3, 5-1~5-4, 6-1~6-3, 7-1~7-4) -- OK
- [x] 일차(Day) 배분이 원본과 일치 -- OK
- [x] 산출물 (Lab 번호, 프로젝트, 퀴즈) 매핑 완료 -- OK
- [x] 교육 방법 (이론+실습, 퀴즈+토론, 프로젝트, 퀴즈+리뷰) 매핑 완료 -- OK
- [x] 시간 배분이 원본과 일치 -- OK

### 이미지 검증

- [x] 이미지 2개 이상 사용: handson_cover.png (슬라이드 1), handson_profile.png (슬라이드 2) -- OK
- [x] 이미지 파일이 OUTPUT_DIR/images/에 존재 확인 -- OK
- [x] 명세에 이미지 파일 경로가 해당 슬라이드에 매핑됨 -- OK

### 컬러 팔레트 검증

- [x] 13개 역할별 색상 전체 정의됨 -- OK
  - primary (#4A1B6D), primaryBright (#7B3FA0), primaryDark (#2D1045)
  - primaryLight (#EDE4F5), headerBg (#4A1B6D), dark (#1A1A2E)
  - darkGray (#333333), midGray (#666666), lightGray (#D0D0D0)
  - vLightGray (#F3F0F7), white (#FFFFFF), tableAlt (#F3EEFA)
  - tableBorder (#C8BED8)

### 명세 완전성 검증

- [x] 모든 요소에 x, y, w, h 좌표 포함 -- OK
- [x] 모든 텍스트에 폰트 크기, 스타일, 색상, 정렬 정보 포함 -- OK
- [x] 테이블 데이터 행별 전체 내용 기록 -- OK
- [x] 공통 컴포넌트 (addTitle, addFooter, cell, hCell) 상세 정의 -- OK
- [x] 교대행 배경색 규칙 정의 -- OK
- [x] 셀 margin, border, lineSpacing 등 세부 속성 정의 -- OK

---

## 파일 정보

| 항목 | 값 |
|------|-----|
| 파일명 | `ai_handson_proposal.pptx` |
| 저장 경로 | `/Users/dreamondal/workspace/tech-curriculum/output/ai-curriculum/ai_handson_proposal.pptx` |
| 명세 파일 | `/Users/dreamondal/workspace/tech-curriculum/output/ai-curriculum/pptx-proposal-specification.md` |
| 이미지 디렉토리 | `/Users/dreamondal/workspace/tech-curriculum/output/ai-curriculum/images/` |
| 슬라이드 크기 | 16:9 (10" x 5.625") |
| 총 슬라이드 수 | 10장 |
| 테마 | Deep Purple Professional |
| 주 강조색 | #4A1B6D |
| 사용 이미지 | handson_cover.png, handson_profile.png |
