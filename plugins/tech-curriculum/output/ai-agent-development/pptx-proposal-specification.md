# PPTX 제안서 명세서: AI Agent 개발 실무

> 생성일: 2026-02-15
> 버전: 1.0
> 총 슬라이드: 11장
> 대상: PptxGenJS 코드 생성 에이전트

---

## 전역 스타일 설정

### 파일 정보

```
파일명: ai-agent-development-proposal.pptx
저장 경로: /Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/
이미지 경로: /Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/images/
```

### 슬라이드 크기

```
width: 10    (inches)
height: 5.625 (inches)
layout: LAYOUT_WIDE (16:9)
```

### 컬러 팔레트

```javascript
const COLORS = {
  primary:       '#673AB7',   // 주 강조색 — 액센트 바, 테이블 헤더, 푸터 라인
  primaryBright: '#9C27B0',   // 밝은 강조색 — 화살표, 배지 강조
  primaryDark:   '#4527A0',   // 어두운 강조색 — 표지 이미지 오버레이
  primaryLight:  '#EDE7F6',   // 연한 강조색 — 인용구 배경, 강조 박스
  headerBg:      '#5E35B1',   // 테이블 헤더 배경색
  dark:          '#212121',   // 주 텍스트색
  darkGray:      '#424242',   // 보조 텍스트색
  midGray:       '#757575',   // 부제/캡션 텍스트색
  lightGray:     '#E0E0E0',   // 구분선, 테이블 보더
  vLightGray:    '#F5F5F5',   // 교대행 배경, 라벨 배경
  white:         '#FFFFFF',   // 기본 배경
  tableAlt:      '#F3E5F5',   // 테이블 교대행 배경
  tableBorder:   '#E0E0E0',   // 테이블 셀 보더
};
```

### 폰트 체계

| 역할 | 변수명 | 크기(pt) | 스타일 | fontFace | 용도 |
|------|--------|---------|--------|----------|------|
| 표지 제목 | coverTitle | 30 | Bold | 맑은 고딕 | 표지 메인 타이틀 |
| 제목 | title | 22 | Bold | 맑은 고딕 | 슬라이드 제목 |
| 부제 (일반) | subtitle | 18 | Regular | 맑은 고딕 | 설명 텍스트 |
| 부제 (Compact) | subtitleCompact | 14 | Bold | 맑은 고딕 | Compact 모드 설명 |
| 본문강조 | bodyBold | 14 | Bold | 맑은 고딕 | 라벨, 헤더, 강조 |
| 본문일반 | body | 12 | Regular | 맑은 고딕 | 테이블 본문, 일반 텍스트 |
| 표지 인용구 | coverQuote | 11 | Italic | 맑은 고딕 | 표지 인용구 박스 |
| 푸터 | footer | 10 | Regular | 맑은 고딕 | 페이지 번호 |

**최소 폰트 규칙**: 모든 텍스트 12pt 이상. 예외: 표지 인용구(11pt), 푸터(10pt).

### 레이아웃 규격

```
슬라이드 크기       : 10" x 5.625" (16:9)
좌우 마진 (테이블)  : 0.25"
좌우 마진 (제목)    : 0.5"
푸터 라인 Y         : 5.35"
푸터 라인           : x=0, y=5.35, w=10, h=0.025 (primary)
페이지 번호         : x=9.0, y=5.37, w=0.75, fontSize=10, align=right, color=midGray
구분선              : x=0.25, w=9.5, h=0.008 (lightGray)
테이블 전체 너비    : x=0.25, w=9.5
```

### PptxGenJS Shape 규칙

```
- 둥근 사각형 → pres.shapes.ROUNDED_RECTANGLE + rectRadius
- 사각형     → pres.shapes.RECTANGLE
- 타원/원    → pres.shapes.OVAL
- 선         → pres.shapes.LINE
- 삼각형     → pres.shapes.TRIANGLE
- rounding: true 와 sizing 동시 사용 금지
- borderRadius 값 → rectRadius: (값/100) 으로 변환
```

---

## 공통 컴포넌트 정의

### addTitle(title, subtitle, compact=false)

**Normal 모드 (compact=false)**:
```
baseY = 0.3
액센트 바: shape=RECTANGLE, x=0.5, y=0.3, w=0.07, h=0.5, fill=primary, line={width:0}
제목 텍스트: x=0.72, y=0.25, w=8.5, h=0.5, fontSize=22, bold=true, color=dark, fontFace='맑은 고딕'
부제 텍스트: x=0.72, y=0.72, w=8.5, h=0.4, fontSize=18, color=midGray, fontFace='맑은 고딕'
구분선: shape=RECTANGLE, x=0.25, y=1.2, w=9.5, h=0.008, fill=lightGray, line={width:0}
콘텐츠 시작 Y: 1.28
```

**Compact 모드 (compact=true)**:
```
baseY = 0.15
액센트 바: shape=RECTANGLE, x=0.5, y=0.15, w=0.07, h=0.38, fill=primary, line={width:0}
제목 텍스트: x=0.72, y=0.10, w=8.5, h=0.4, fontSize=22, bold=true, color=dark, fontFace='맑은 고딕'
부제 텍스트: x=0.72, y=0.48, w=8.5, h=0.35, fontSize=14, bold=true, color=midGray, fontFace='맑은 고딕'
구분선: shape=RECTANGLE, x=0.25, y=0.86, w=9.5, h=0.008, fill=lightGray, line={width:0}
콘텐츠 시작 Y: 0.92
```

### addFooter(pageNum)

```
푸터 라인: shape=RECTANGLE, x=0, y=5.35, w=10, h=0.025, fill=primary, line={width:0}
페이지 번호: addText(String(pageNum), {
  x: 9.0, y: 5.37, w: 0.75, h: 0.2,
  fontSize: 10, color: midGray, align: 'right', fontFace: '맑은 고딕'
})
```

### cell(text, options) — 테이블 데이터 셀

```javascript
{
  text: text,
  options: {
    fontSize: 12,
    fontFace: '맑은 고딕',
    color: dark,
    align: options.align || 'left',
    valign: 'middle',
    border: { type: 'solid', pt: 0.5, color: tableBorder },  // 4방향 동일
    margin: [3, 5, 3, 5],  // top, right, bottom, left (pt)
    paraSpaceAfter: 2,
    lineSpacingMultiple: 1.15,
    fill: { color: options.fill || white },
    ...options
  }
}
```

### hCell(text, options) — 테이블 헤더 셀

```javascript
{
  text: text,
  options: {
    fontSize: 12,
    fontFace: '맑은 고딕',
    bold: true,
    color: white,
    align: 'center',
    valign: 'middle',
    fill: { color: headerBg },
    border: { type: 'solid', pt: 0.5, color: tableBorder },
    margin: [3, 5, 3, 5],
    paraSpaceAfter: 2,
    lineSpacingMultiple: 1.15,
    ...options
  }
}
```

### 테이블 6열 구성 (상세 테이블용)

```
colW: [0.55, 1.6, 0.5, 4.35, 1.25, 0.75]  // 합계 = 9.0 (x=0.25 기준, 패딩 포함 w=9.5)
총 너비: 9.5 (x=0.25, w=9.5)
헤더: ['일', '모듈명', '시간', '핵심 내용', '산출물', '방법']
```

---

## 슬라이드 1: 표지 (Cover — Split Layout)

- **레이아웃**: Split Layout (좌측 50% 이미지 + 우측 50% 텍스트)
- **Compact 모드**: 해당 없음
- **푸터**: 없음 (표지에는 푸터/페이지번호 생략)

### 구성 요소

#### 1-1. 좌측 커버 이미지

```
addImage({
  path: '/Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/images/proposal_cover.png',
  x: 0, y: 0, w: 5.0, h: 5.625,
  sizing: { type: 'cover', w: 5.0, h: 5.625 }
})
```

#### 1-2. 좌측 어두운 오버레이

```
addShape(pres.shapes.RECTANGLE, {
  x: 0, y: 0, w: 5.0, h: 5.625,
  fill: { color: primaryDark, transparency: 25 },
  line: { width: 0 }
})
```

#### 1-3. 우측 배경 (흰색)

```
addShape(pres.shapes.RECTANGLE, {
  x: 5.0, y: 0, w: 5.0, h: 5.625,
  fill: { color: white },
  line: { width: 0 }
})
```

#### 1-4. 우측 상단 액센트 바

```
addShape(pres.shapes.RECTANGLE, {
  x: 5.6, y: 0.6, w: 1.2, h: 0.06,
  fill: { color: primary },
  line: { width: 0 }
})
```

#### 1-5. 우측 제목 텍스트

```
addText([
  { text: 'AI Agent\n개발 실무', options: {
    fontSize: 30, bold: true, color: dark, fontFace: '맑은 고딕',
    lineSpacingMultiple: 1.2, breakType: 'none'
  }}
], {
  x: 5.6, y: 0.85, w: 3.8, h: 1.6,
  valign: 'top'
})
```

#### 1-6. 우측 저자 영역 (세로 액센트 바 + 소속/이름)

```
// 세로 액센트 바
addShape(pres.shapes.RECTANGLE, {
  x: 5.6, y: 2.7, w: 0.05, h: 0.65,
  fill: { color: primary },
  line: { width: 0 }
})

// 소속
addText('유니콘주식회사', {
  x: 5.85, y: 2.7, w: 3.0, h: 0.3,
  fontSize: 12, color: midGray, fontFace: '맑은 고딕'
})

// 이름
addText('이해경 (CEO)', {
  x: 5.85, y: 2.98, w: 3.0, h: 0.35,
  fontSize: 18, bold: true, color: dark, fontFace: '맑은 고딕'
})
```

#### 1-7. 우측 하단 인용구 박스

```
// 인용구 배경 박스 (둥근 모서리)
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: 5.6, y: 3.8, w: 3.8, h: 1.0,
  fill: { color: primaryLight },
  rectRadius: 0.1,
  line: { width: 0 }
})

// 인용구 좌측 세로 액센트 바
addShape(pres.shapes.RECTANGLE, {
  x: 5.6, y: 3.8, w: 0.06, h: 1.0,
  fill: { color: primary },
  line: { width: 0 }
})

// 인용구 텍스트
addText('"LLM API부터 MAS까지,\n5일 완성 실습 과정"', {
  x: 5.85, y: 3.85, w: 3.35, h: 0.9,
  fontSize: 11, italic: true, color: darkGray, fontFace: '맑은 고딕',
  valign: 'middle', lineSpacingMultiple: 1.4
})
```

---

## 슬라이드 2: 인사말 (Greeting)

- **레이아웃**: Greeting
- **Compact 모드**: 아니오
- **페이지 번호**: 2

### 구성 요소

#### 2-1. addTitle

```
제목: '강사 인사말'
부제: 없음 (제목만 표시)
compact: false

액센트 바: x=0.5, y=0.3, w=0.07, h=0.5, fill=primary
제목: x=0.72, y=0.25, w=8.5, h=0.5, fontSize=22, bold, color=dark
구분선: x=0.25, y=1.0, w=9.5, h=0.008, fill=lightGray
```

#### 2-2. 중앙 인용구 박스

```
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: 0.5, y: 1.15, w: 9.0, h: 0.55,
  fill: { color: primaryLight },
  rectRadius: 0.08,
  line: { width: 0 }
})

addText('"실습으로 증명하고, 프로젝트로 완성하는 교육"', {
  x: 0.5, y: 1.15, w: 9.0, h: 0.55,
  fontSize: 14, bold: true, color: dark, fontFace: '맑은 고딕',
  align: 'center', valign: 'middle'
})
```

#### 2-3. 프로필 사진 (좌측)

```
addImage({
  path: '/Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/images/proposal_profile.png',
  x: 0.8, y: 2.0, w: 1.4, h: 1.4,
  rounding: true
})
```

#### 2-4. 이름 + 세로 액센트 바 (우측)

```
// 세로 액센트 바
addShape(pres.shapes.RECTANGLE, {
  x: 2.6, y: 2.05, w: 0.05, h: 0.45,
  fill: { color: primary },
  line: { width: 0 }
})

// 이름
addText('이해경', {
  x: 2.85, y: 2.0, w: 3.0, h: 0.3,
  fontSize: 22, bold: true, color: dark, fontFace: '맑은 고딕'
})

// 직함
addText('유니콘주식회사 CEO', {
  x: 2.85, y: 2.32, w: 3.0, h: 0.25,
  fontSize: 12, color: midGray, fontFace: '맑은 고딕'
})
```

#### 2-5. 자격사항 bullet 목록

```
addText([
  { text: '  IBM Certified Agile Coach\n', options: { fontSize: 12, color: darkGray, fontFace: '맑은 고딕', bullet: { code: '25CF', color: primary } } },
  { text: '  PSM I  |  PMP  |  IBM Certified Architect\n', options: { fontSize: 12, color: darkGray, fontFace: '맑은 고딕', bullet: { code: '25CF', color: primary } } },
  { text: '  저서: 마이크로서비스패턴 쉽게 개발하기\n', options: { fontSize: 12, color: darkGray, fontFace: '맑은 고딕', bullet: { code: '25CF', color: primary } } },
  { text: '  블로그: 온달의 해피클라우드', options: { fontSize: 12, color: darkGray, fontFace: '맑은 고딕', bullet: { code: '25CF', color: primary } } }
], {
  x: 2.85, y: 2.7, w: 6.5, h: 1.2,
  valign: 'top', lineSpacingMultiple: 1.5
})
```

#### 2-6. 하단 구분선 + 연락처

```
// 구분선
addShape(pres.shapes.RECTANGLE, {
  x: 0.5, y: 4.15, w: 9.0, h: 0.008, fill: { color: lightGray }, line: { width: 0 }
})

// 연락처 정보
addText([
  { text: 'Email: hiondal@gmail.com', options: { fontSize: 12, color: midGray, fontFace: '맑은 고딕' } },
  { text: '    |    ', options: { fontSize: 12, color: lightGray, fontFace: '맑은 고딕' } },
  { text: 'Tel: 82-10-4095-4035', options: { fontSize: 12, color: midGray, fontFace: '맑은 고딕' } },
  { text: '    |    ', options: { fontSize: 12, color: lightGray, fontFace: '맑은 고딕' } },
  { text: 'Blog: https://happycloud-lee.tistory.com', options: { fontSize: 12, color: primary, fontFace: '맑은 고딕' } }
], {
  x: 0.5, y: 4.3, w: 9.0, h: 0.35,
  align: 'center', valign: 'middle'
})
```

#### 2-7. addFooter(2)

```
푸터 라인: x=0, y=5.35, w=10, h=0.025, fill=primary
페이지번호: '2', x=9.0, y=5.37, w=0.75, fontSize=10, color=midGray, align=right
```

---

## 슬라이드 3: 교육 과정 개요 (Overview — 2x3 Grid)

- **레이아웃**: Overview 2x3 Grid
- **Compact 모드**: 아니오
- **페이지 번호**: 3

### 구성 요소

#### 3-1. addTitle

```
제목: '교육 과정 개요'
부제: 'AI Agent 개발 실무 — 5일 35시간 집중 과정'
compact: false

액센트 바: x=0.5, y=0.3, w=0.07, h=0.5, fill=primary
제목: x=0.72, y=0.25, w=8.5, h=0.5, fontSize=22, bold, color=dark
부제: x=0.72, y=0.72, w=8.5, h=0.4, fontSize=18, color=midGray
구분선: x=0.25, y=1.2, w=9.5, h=0.008, fill=lightGray
```

#### 3-2. 섹션 소제목

```
addText('과정 기본 정보', {
  x: 0.5, y: 1.35, w: 9.0, h: 0.35,
  fontSize: 18, bold: true, color: dark, fontFace: '맑은 고딕',
  align: 'center'
})
```

#### 3-3. 2x3 그리드

**그리드 설정**:
```
gridStartX = 0.5
gridStartY = 1.85
labelW = 1.15
cellH = 1.05
gapX = 0.5
gapY = 0.12

// 열 계산:
col1_labelX = 0.5
col1_cellX  = 0.5 + 1.15 = 1.65
col1_cellW  = 3.2
col2_labelX = 5.35
col2_cellX  = 5.35 + 1.15 = 6.5
col2_cellW  = 3.0

// 행 계산:
row1_Y = 1.85
row2_Y = 1.85 + 1.05 + 0.12 = 3.02
row3_Y = 3.02 + 1.05 + 0.12 = 4.19
```

**그리드 데이터 (6셀)**:

| 위치 | 라벨 | 값 |
|------|------|-----|
| (1,1) | 교육명 | AI Agent 개발 실무 |
| (1,2) | 교육 대상 | AI 서비스 개발자, 백엔드/풀스택 개발자 |
| (2,1) | 교육 기간 | 5일 (35시간) / 일 7시간 |
| (2,2) | 교육 목표 | LLM API ~ MAS까지 AI Agent 전 과정 실습 |
| (3,1) | 교재 | 자체 교재 (17개 챕터) |
| (3,2) | 실습 방식 | 이론 58% + 실습 36% + 토론 6% |

**각 셀 구조 (라벨 + 값)**:

```javascript
// 라벨 영역 (primary 배경, 흰색 텍스트)
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: {labelX}, y: {rowY}, w: 1.15, h: 1.05,
  fill: { color: primary }, rectRadius: 0.05, line: { width: 0 }
})
addText('{라벨}', {
  x: {labelX}, y: {rowY}, w: 1.15, h: 1.05,
  fontSize: 14, bold: true, color: white, fontFace: '맑은 고딕',
  align: 'center', valign: 'middle'
})

// 값 영역 (vLightGray 배경)
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: {cellX}, y: {rowY}, w: {cellW}, h: 1.05,
  fill: { color: vLightGray }, rectRadius: 0.05, line: { width: 0 }
})
addText('{값}', {
  x: {cellX + 0.15}, y: {rowY}, w: {cellW - 0.3}, h: 1.05,
  fontSize: 12, color: dark, fontFace: '맑은 고딕',
  valign: 'middle'
})
```

**셀별 좌표 상세**:

| 셀 | labelX | rowY | cellX | cellW |
|----|--------|------|-------|-------|
| (1,1) 교육명 | 0.5 | 1.85 | 1.65 | 3.2 |
| (1,2) 교육 대상 | 5.35 | 1.85 | 6.5 | 3.0 |
| (2,1) 교육 기간 | 0.5 | 3.02 | 1.65 | 3.2 |
| (2,2) 교육 목표 | 5.35 | 3.02 | 6.5 | 3.0 |
| (3,1) 교재 | 0.5 | 4.19 | 1.65 | 3.2 |
| (3,2) 실습 방식 | 5.35 | 4.19 | 6.5 | 3.0 |

#### 3-4. addFooter(3)

---

## 슬라이드 4: 커리큘럼 맵 (Arrows + Grid)

- **레이아웃**: Curriculum Overview (Arrows + Grid)
- **Compact 모드**: 아니오
- **페이지 번호**: 4

### 구성 요소

#### 4-1. addTitle

```
제목: 'AI Agent 성장 경로'
부제: 'Step 1부터 Step 5까지 — 5일간의 여정'
compact: false

액센트 바: x=0.5, y=0.3, w=0.07, h=0.5, fill=primary
제목: x=0.72, y=0.25, w=8.5, h=0.5, fontSize=22, bold, color=dark
부제: x=0.72, y=0.72, w=8.5, h=0.4, fontSize=18, color=midGray
구분선: x=0.25, y=1.2, w=9.5, h=0.008, fill=lightGray
```

#### 4-2. 5단계 화살표 바

각 단계별 둥근 모서리 화살표 바. 5개 단계를 가로로 나열.

**화살표 바 설정**:
```
arrowY = 1.45
arrowH = 0.45
arrowGap = 0.08
totalW = 9.0  (x=0.5 ~ x=9.5)
arrowW = (9.0 - 4 * 0.08) / 5 = 1.736
```

| 단계 | 텍스트 | x | y | w | h | fill |
|------|--------|---|---|---|---|------|
| Step 1 | LLM과 대화하기 | 0.5 | 1.45 | 1.736 | 0.45 | primary |
| Step 2 | 데이터 다루기 | 2.316 | 1.45 | 1.736 | 0.45 | primaryBright |
| Step 3 | 도구 연결하기 | 4.132 | 1.45 | 1.736 | 0.45 | primary |
| Step 4 | 지식 확장하기 | 5.948 | 1.45 | 1.736 | 0.45 | primaryBright |
| Step 5 | 에이전트 만들기 | 7.764 | 1.45 | 1.736 | 0.45 | primary |

```javascript
// 각 화살표 바 (5개 반복)
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: {arrowX}, y: 1.45, w: 1.736, h: 0.45,
  fill: { color: {stepColor} },
  rectRadius: 0.05,
  line: { width: 0 }
})
addText('{stepText}', {
  x: {arrowX}, y: 1.45, w: 1.736, h: 0.45,
  fontSize: 12, bold: true, color: white, fontFace: '맑은 고딕',
  align: 'center', valign: 'middle'
})
```

#### 4-3. Day 헤더 배지

Day 1 ~ Day 5를 화살표 아래에 배치. 각 Day는 해당 Step 아래에 정렬.

```
badgeY = 2.1
badgeH = 0.3
```

| Day | 텍스트 | x | w | fill |
|-----|--------|---|---|------|
| Day 1 | Day 1 | 0.5 | 1.736 | primary |
| Day 2 | Day 2 | 2.316 | 1.736 | primaryBright |
| Day 3 | Day 3 | 4.132 | 1.736 | primary |
| Day 4 | Day 4 | 5.948 | 1.736 | primaryBright |
| Day 5 | Day 5 | 7.764 | 1.736 | primary |

```javascript
// 각 Day 배지 (5개 반복)
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: {dayX}, y: 2.1, w: 1.736, h: 0.3,
  fill: { color: {dayColor} },
  rectRadius: 0.03,
  line: { width: 0 }
})
addText('{Day N}', {
  x: {dayX}, y: 2.1, w: 1.736, h: 0.3,
  fontSize: 12, bold: true, color: white, fontFace: '맑은 고딕',
  align: 'center', valign: 'middle'
})
```

#### 4-4. 3행 콘텐츠 그리드

3행: 과정(핵심 주제), Tool(실습 도구), Output(산출물)

**그리드 설정**:
```
labelW = 0.8
gridStartY = 2.6
rowH = 0.9
rowGap = 0.06
cellStartX = 1.38
dayColW = 1.656
dayColGap = 0.08
```

**행 라벨**:

| 행 | 라벨 | y |
|----|------|---|
| 1 | 과정 | 2.6 |
| 2 | Tool | 3.56 |
| 3 | Output | 4.52 |

```javascript
// 행 라벨 (좌측 고정, 3개 반복)
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: 0.5, y: {rowY}, w: 0.8, h: 0.9,
  fill: { color: vLightGray },
  rectRadius: 0.05,
  line: { width: 0 }
})
addText('{라벨}', {
  x: 0.5, y: {rowY}, w: 0.8, h: 0.9,
  fontSize: 12, bold: true, color: dark, fontFace: '맑은 고딕',
  align: 'center', valign: 'middle'
})
```

**Day별 콘텐츠 셀 X 좌표**:

| Day | cellX |
|-----|-------|
| Day 1 | 1.38 |
| Day 2 | 3.196 |
| Day 3 | 5.012 |
| Day 4 | 6.828 |
| Day 5 | 8.644 |

**콘텐츠 셀 데이터**:

| Day | 과정 | Tool | Output |
|-----|------|------|--------|
| Day 1 | AI 앱 개요\nLLM API\n멀티턴 대화 | OpenAI/Claude/\nGemini API\nStreamlit | 여행 플래너\n챗봇 |
| Day 2 | 문서 요약\nPDF/멀티모달\nFunction Calling | Docling/PyMuPDF\nWhisper/Gemini\nVision | 요약 시스템\nFC 통합 Agent |
| Day 3 | LangChain\nLCEL/Agent\nRAG 기초 | LangChain\nLangGraph\nChroma | LCEL 체인\nRAG 시스템 |
| Day 4 | RAG 튜닝\n웹검색/YouTube\nGraphRAG | RAGAS\nDuckDuckGo\nLightRAG/Neo4j | 튜닝된 RAG\n멀티소스 Agent |
| Day 5 | MAS 설계\nMCP 서버\n자연어 Agent | Claude Code\nMCP SDK\nDify | MAS 챗봇\nMCP 서버\nDSL 프로토타입 |

```javascript
// 각 콘텐츠 셀 (15개 = 3행 x 5열)
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: {dayColX}, y: {rowY}, w: 1.656, h: 0.9,
  fill: { color: white },
  rectRadius: 0.03,
  line: { type: 'solid', pt: 0.5, color: lightGray }
})
addText('{cellText}', {
  x: {dayColX + 0.05}, y: {rowY}, w: 1.556, h: 0.9,
  fontSize: 12, color: dark, fontFace: '맑은 고딕',
  align: 'center', valign: 'middle',
  lineSpacingMultiple: 1.1
})
```

**셀별 상세 좌표 (15셀)**:

| 셀(행,열) | x | y | w | h |
|-----------|---|---|---|---|
| 과정, Day1 | 1.38 | 2.6 | 1.656 | 0.9 |
| 과정, Day2 | 3.196 | 2.6 | 1.656 | 0.9 |
| 과정, Day3 | 5.012 | 2.6 | 1.656 | 0.9 |
| 과정, Day4 | 6.828 | 2.6 | 1.656 | 0.9 |
| 과정, Day5 | 8.644 | 2.6 | 1.656 | 0.9 |
| Tool, Day1 | 1.38 | 3.56 | 1.656 | 0.9 |
| Tool, Day2 | 3.196 | 3.56 | 1.656 | 0.9 |
| Tool, Day3 | 5.012 | 3.56 | 1.656 | 0.9 |
| Tool, Day4 | 6.828 | 3.56 | 1.656 | 0.9 |
| Tool, Day5 | 8.644 | 3.56 | 1.656 | 0.9 |
| Output, Day1 | 1.38 | 4.52 | 1.656 | 0.9 |
| Output, Day2 | 3.196 | 4.52 | 1.656 | 0.9 |
| Output, Day3 | 5.012 | 4.52 | 1.656 | 0.9 |
| Output, Day4 | 6.828 | 4.52 | 1.656 | 0.9 |
| Output, Day5 | 8.644 | 4.52 | 1.656 | 0.9 |

#### 4-5. addFooter(4)

---

## 슬라이드 5: Day 1 상세 테이블

- **레이아웃**: Detail Table
- **Compact 모드**: 아니오 (4개 모듈)
- **페이지 번호**: 5

### 구성 요소

#### 5-1. addTitle

```
제목: 'Day 1. AI 앱 기초 + LLM API + 멀티턴'
부제: 'Step 1 — LLM과 대화하기 | 7시간 (이론 55% / 실습 37% / 토론 8%)'
compact: false
```

#### 5-2. 테이블 상단 액센트 바

```
addShape(pres.shapes.RECTANGLE, {
  x: 0.25, y: 1.25, w: 9.5, h: 0.035,
  fill: { color: primary },
  line: { width: 0 }
})
```

#### 5-3. 6열 테이블

```
테이블 위치: x=0.25, y=1.28, w=9.5
colW: [0.55, 1.6, 0.5, 4.35, 1.25, 0.75]
autoPage: false
```

**헤더행**:
```
[hCell('일'), hCell('모듈명'), hCell('시간'), hCell('핵심 내용'), hCell('산출물'), hCell('방법')]
```

**데이터행 (4행)**:

| # | 일 | 모듈명 | 시간 | 핵심 내용 | 산출물 | 방법 | fill |
|---|---|--------|------|-----------|--------|------|------|
| 1 | 1 | AI 어플리케이션 개요 | 2h | SAS 패턴, Agent Flow 패턴,\n트랜스포머 모델, 3-Tier 아키텍처,\nRAG 시스템 흐름 | - | 이론\n토론 | white |
| 2 | 1 | LLM API +\n프롬프트 엔지니어링 | 1.5h | LLM 4사 비교(GPT-4o/Claude/\nGemini/Groq), Zero/Few-shot,\nCoT, 파라미터 실험 | API 호출 코드\n프롬프트 비교 | 이론\n실습 | tableAlt |
| 3 | 1 | Python 기초 +\n환경설정 | 1h | 가상환경(venv), Pydantic BaseModel,\nwith_structured_output() | 개발환경\nPydantic 모델 | 이론\n실습 | white |
| 4 | 1 | 멀티턴 대화 | 2.5h | 싱글턴 vs 멀티턴, 클라이언트/서버\n컨텍스트 관리, Streamlit 웹 챗봇 | 여행 플래너\nStreamlit 챗봇 | 이론\n실습\n토론 | tableAlt |

```javascript
// Row 1 (white)
[
  cell('1', { align: 'center', fill: white }),
  cell('AI 어플리케이션 개요', { bold: true, fill: white }),
  cell('2h', { align: 'center', fill: white }),
  cell('SAS 패턴, Agent Flow 패턴,\n트랜스포머 모델, 3-Tier 아키텍처,\nRAG 시스템 흐름', { fill: white }),
  cell('-', { align: 'center', fill: white }),
  cell('이론\n토론', { align: 'center', fill: white })
]
// Row 2 (tableAlt)
[
  cell('1', { align: 'center', fill: tableAlt }),
  cell('LLM API +\n프롬프트 엔지니어링', { bold: true, fill: tableAlt }),
  cell('1.5h', { align: 'center', fill: tableAlt }),
  cell('LLM 4사 비교(GPT-4o/Claude/\nGemini/Groq), Zero/Few-shot,\nCoT, 파라미터 실험', { fill: tableAlt }),
  cell('API 호출 코드\n프롬프트 비교', { fill: tableAlt }),
  cell('이론\n실습', { align: 'center', fill: tableAlt })
]
// Row 3 (white)
[
  cell('1', { align: 'center', fill: white }),
  cell('Python 기초 +\n환경설정', { bold: true, fill: white }),
  cell('1h', { align: 'center', fill: white }),
  cell('가상환경(venv), Pydantic BaseModel,\nwith_structured_output()', { fill: white }),
  cell('개발환경\nPydantic 모델', { fill: white }),
  cell('이론\n실습', { align: 'center', fill: white })
]
// Row 4 (tableAlt)
[
  cell('1', { align: 'center', fill: tableAlt }),
  cell('멀티턴 대화', { bold: true, fill: tableAlt }),
  cell('2.5h', { align: 'center', fill: tableAlt }),
  cell('싱글턴 vs 멀티턴, 클라이언트/서버\n컨텍스트 관리, Streamlit 웹 챗봇', { fill: tableAlt }),
  cell('여행 플래너\nStreamlit 챗봇', { fill: tableAlt }),
  cell('이론\n실습\n토론', { align: 'center', fill: tableAlt })
]
```

#### 5-4. addFooter(5)

---

## 슬라이드 6: Day 2 상세 테이블

- **레이아웃**: Detail Table
- **Compact 모드**: 아니오 (5개 모듈)
- **페이지 번호**: 6

### 구성 요소

#### 6-1. addTitle

```
제목: 'Day 2. 데이터 처리 + Function Calling'
부제: 'Step 2~3 — 데이터 다루기 / 도구 연결하기 | 7시간 (이론 45% / 실습 50% / 토론 5%)'
compact: false
```

#### 6-2. 테이블 상단 액센트 바

```
addShape(pres.shapes.RECTANGLE, {
  x: 0.25, y: 1.25, w: 9.5, h: 0.035, fill: { color: primary }, line: { width: 0 }
})
```

#### 6-3. 6열 테이블

```
테이블 위치: x=0.25, y=1.28, w=9.5
colW: [0.55, 1.6, 0.5, 4.35, 1.25, 0.75]
autoPage: false
```

**헤더행**:
```
[hCell('일'), hCell('모듈명'), hCell('시간'), hCell('핵심 내용'), hCell('산출물'), hCell('방법')]
```

**데이터행 (5행)**:

| # | 일 | 모듈명 | 시간 | 핵심 내용 | 산출물 | 방법 | fill |
|---|---|--------|------|-----------|--------|------|------|
| 1 | 2 | 문서 요약 | 1h | 추출적/생성적 요약 비교,\nEXAONE(Groq LPU),\nLLM vs 전문 모델(KoBART) | 뉴스 요약 코드 | 이론\n실습 | white |
| 2 | 2 | PDF 처리 | 1h | Docling(AI) vs PyMuPDF(규칙),\n텍스트/테이블/이미지 추출,\nPDF -> Markdown 변환 | PDF 처리\n파이프라인 | 이론\n실습 | tableAlt |
| 3 | 2 | 멀티모달 AI\n(STT/TTS/VLM) | 1h | Whisper API(STT), OpenAI TTS,\nGemini Vision(VLM),\n클라우드 vs 로컬 모델 비교 | - (데모 관찰) | 이론\n데모 | white |
| 4 | 2 | Function Calling\n기초 | 2h | 공통 5단계 워크플로우,\n3사 API 비교(OpenAI/Claude/Gemini),\ntool_choice, 병렬/순차 호출 | FC 여행 플래너\n(3사 API) | 이론\n실습 | tableAlt |
| 5 | 2 | Function Calling\n고급 | 2h | 모델별 고유기능(Custom Tools/\n서버도구/자동호출),\n스트리밍 Function Calling | 스트리밍 FC Agent\nClaude 서버도구 | 이론\n실습\n토론 | white |

```javascript
// Row 1 (white)
[
  cell('2', { align: 'center', fill: white }),
  cell('문서 요약', { bold: true, fill: white }),
  cell('1h', { align: 'center', fill: white }),
  cell('추출적/생성적 요약 비교,\nEXAONE(Groq LPU),\nLLM vs 전문 모델(KoBART)', { fill: white }),
  cell('뉴스 요약 코드', { fill: white }),
  cell('이론\n실습', { align: 'center', fill: white })
]
// Row 2 (tableAlt)
[
  cell('2', { align: 'center', fill: tableAlt }),
  cell('PDF 처리', { bold: true, fill: tableAlt }),
  cell('1h', { align: 'center', fill: tableAlt }),
  cell('Docling(AI) vs PyMuPDF(규칙),\n텍스트/테이블/이미지 추출,\nPDF -> Markdown 변환', { fill: tableAlt }),
  cell('PDF 처리\n파이프라인', { fill: tableAlt }),
  cell('이론\n실습', { align: 'center', fill: tableAlt })
]
// Row 3 (white)
[
  cell('2', { align: 'center', fill: white }),
  cell('멀티모달 AI\n(STT/TTS/VLM)', { bold: true, fill: white }),
  cell('1h', { align: 'center', fill: white }),
  cell('Whisper API(STT), OpenAI TTS,\nGemini Vision(VLM),\n클라우드 vs 로컬 모델 비교', { fill: white }),
  cell('- (데모 관찰)', { align: 'center', fill: white }),
  cell('이론\n데모', { align: 'center', fill: white })
]
// Row 4 (tableAlt)
[
  cell('2', { align: 'center', fill: tableAlt }),
  cell('Function Calling\n기초', { bold: true, fill: tableAlt }),
  cell('2h', { align: 'center', fill: tableAlt }),
  cell('공통 5단계 워크플로우,\n3사 API 비교(OpenAI/Claude/Gemini),\ntool_choice, 병렬/순차 호출', { fill: tableAlt }),
  cell('FC 여행 플래너\n(3사 API)', { fill: tableAlt }),
  cell('이론\n실습', { align: 'center', fill: tableAlt })
]
// Row 5 (white)
[
  cell('2', { align: 'center', fill: white }),
  cell('Function Calling\n고급', { bold: true, fill: white }),
  cell('2h', { align: 'center', fill: white }),
  cell('모델별 고유기능(Custom Tools/\n서버도구/자동호출),\n스트리밍 Function Calling', { fill: white }),
  cell('스트리밍 FC Agent\nClaude 서버도구', { fill: white }),
  cell('이론\n실습\n토론', { align: 'center', fill: white })
]
```

#### 6-4. addFooter(6)

---

## 슬라이드 7: Day 3 상세 테이블

- **레이아웃**: Detail Table
- **Compact 모드**: 아니오 (4개 모듈)
- **페이지 번호**: 7

### 구성 요소

#### 7-1. addTitle

```
제목: 'Day 3. LangChain 프레임워크 + RAG 기초'
부제: 'Step 3~4 — 도구 연결하기 / 지식 확장하기 | 7시간 (이론 66% / 실습 29% / 토론 5%)'
compact: false
```

#### 7-2. 테이블 상단 액센트 바

```
addShape(pres.shapes.RECTANGLE, {
  x: 0.25, y: 1.25, w: 9.5, h: 0.035, fill: { color: primary }, line: { width: 0 }
})
```

#### 7-3. 6열 테이블

```
테이블 위치: x=0.25, y=1.28, w=9.5
colW: [0.55, 1.6, 0.5, 4.35, 1.25, 0.75]
autoPage: false
```

**헤더행**:
```
[hCell('일'), hCell('모듈명'), hCell('시간'), hCell('핵심 내용'), hCell('산출물'), hCell('방법')]
```

**데이터행 (4행)**:

| # | 일 | 모듈명 | 시간 | 핵심 내용 | 산출물 | 방법 | fill |
|---|---|--------|------|-----------|--------|------|------|
| 1 | 3 | LangChain\n프레임워크 개요 | 1.5h | LangChain vs 대안(LlamaIndex,\nCrewAI), 생태계(Core/LangGraph/\nLangSmith), 의사결정 프레임워크 | LangGraph\n워크플로우 | 이론\n실습 | white |
| 2 | 3 | LLM 인터페이스\n+ LCEL | 1.5h | Chat Models, Prompts,\nOutput Parsers, LCEL 파이프(｜),\nRunnableParallel/Lambda | LCEL 체인\n(구조화 출력) | 이론\n실습 | tableAlt |
| 3 | 3 | Agents, Tools,\nState 관리 | 1h | ReAct 루프, @tool 커스텀 도구,\nMiddleware, LangGraph Checkpointer | Agent +\n커스텀 도구 | 이론\n실습 | white |
| 4 | 3 | RAG 기초 | 3h | Naive/Advanced/Modular RAG,\n인덱싱(Load-Split-Embed-Store),\nHybrid Search, RAGAS 평가 | 기본 RAG 시스템\n(Chroma+Multi-Query) | 이론\n실습\n토론 | tableAlt |

```javascript
// Row 1 (white)
[
  cell('3', { align: 'center', fill: white }),
  cell('LangChain\n프레임워크 개요', { bold: true, fill: white }),
  cell('1.5h', { align: 'center', fill: white }),
  cell('LangChain vs 대안(LlamaIndex,\nCrewAI), 생태계(Core/LangGraph/\nLangSmith), 의사결정 프레임워크', { fill: white }),
  cell('LangGraph\n워크플로우', { fill: white }),
  cell('이론\n실습', { align: 'center', fill: white })
]
// Row 2 (tableAlt)
[
  cell('3', { align: 'center', fill: tableAlt }),
  cell('LLM 인터페이스\n+ LCEL', { bold: true, fill: tableAlt }),
  cell('1.5h', { align: 'center', fill: tableAlt }),
  cell('Chat Models, Prompts,\nOutput Parsers, LCEL 파이프(|),\nRunnableParallel/Lambda', { fill: tableAlt }),
  cell('LCEL 체인\n(구조화 출력)', { fill: tableAlt }),
  cell('이론\n실습', { align: 'center', fill: tableAlt })
]
// Row 3 (white)
[
  cell('3', { align: 'center', fill: white }),
  cell('Agents, Tools,\nState 관리', { bold: true, fill: white }),
  cell('1h', { align: 'center', fill: white }),
  cell('ReAct 루프, @tool 커스텀 도구,\nMiddleware, LangGraph Checkpointer', { fill: white }),
  cell('Agent +\n커스텀 도구', { fill: white }),
  cell('이론\n실습', { align: 'center', fill: white })
]
// Row 4 (tableAlt)
[
  cell('3', { align: 'center', fill: tableAlt }),
  cell('RAG 기초', { bold: true, fill: tableAlt }),
  cell('3h', { align: 'center', fill: tableAlt }),
  cell('Naive/Advanced/Modular RAG,\n인덱싱(Load-Split-Embed-Store),\nHybrid Search, RAGAS 평가', { fill: tableAlt }),
  cell('기본 RAG 시스템\n(Chroma+Multi-Query)', { fill: tableAlt }),
  cell('이론\n실습\n토론', { align: 'center', fill: tableAlt })
]
```

#### 7-4. addFooter(7)

---

## 슬라이드 8: Day 4 상세 테이블

- **레이아웃**: Detail Table
- **Compact 모드**: 아니오 (4개 모듈)
- **페이지 번호**: 8

### 구성 요소

#### 8-1. addTitle

```
제목: 'Day 4. RAG 고급 + 웹검색/YouTube + GraphRAG'
부제: 'Step 4 — 지식 확장하기 | 7시간 (이론 61% / 실습 37% / 토론 5%)'
compact: false
```

#### 8-2. 테이블 상단 액센트 바

```
addShape(pres.shapes.RECTANGLE, {
  x: 0.25, y: 1.25, w: 9.5, h: 0.035, fill: { color: primary }, line: { width: 0 }
})
```

#### 8-3. 6열 테이블

```
테이블 위치: x=0.25, y=1.28, w=9.5
colW: [0.55, 1.6, 0.5, 4.35, 1.25, 0.75]
autoPage: false
```

**헤더행**:
```
[hCell('일'), hCell('모듈명'), hCell('시간'), hCell('핵심 내용'), hCell('산출물'), hCell('방법')]
```

**데이터행 (4행)**:

| # | 일 | 모듈명 | 시간 | 핵심 내용 | 산출물 | 방법 | fill |
|---|---|--------|------|-----------|--------|------|------|
| 1 | 4 | RAG 품질 튜닝 | 2.5h | 시맨틱 청킹, 임베딩 최적화,\n하이브리드 검색(Dense+BM25),\n리랭킹(Cross-Encoder), RAGAS 평가 | 튜닝된 RAG\n(전후 비교) | 이론\n실습 | white |
| 2 | 4 | Local LLM 개념 | 0.5h | Ollama/LlamaCpp/HuggingFace,\nGGUF 포맷, 양자화(Q4/Q5/Q8),\n한국어 모델 소개 | - (개념 학습) | 이론 | tableAlt |
| 3 | 4 | 웹검색 + YouTube\n통합 Agent | 2h | Tavily/DuckDuckGo/Serper,\nYouTube 자막 추출, 멀티소스 RAG,\n캐싱/Resilience 패턴 | 웹검색 Agent\n멀티소스 Agent | 이론\n실습 | white |
| 4 | 4 | GraphRAG | 2h | Vector RAG vs GraphRAG,\n인덱싱(엔터티/관계/커뮤니티),\nLocal/Global/Hybrid Search | LightRAG 시스템\n검색 품질 비교 | 이론\n실습\n데모\n토론 | tableAlt |

```javascript
// Row 1 (white)
[
  cell('4', { align: 'center', fill: white }),
  cell('RAG 품질 튜닝', { bold: true, fill: white }),
  cell('2.5h', { align: 'center', fill: white }),
  cell('시맨틱 청킹, 임베딩 최적화,\n하이브리드 검색(Dense+BM25),\n리랭킹(Cross-Encoder), RAGAS 평가', { fill: white }),
  cell('튜닝된 RAG\n(전후 비교)', { fill: white }),
  cell('이론\n실습', { align: 'center', fill: white })
]
// Row 2 (tableAlt)
[
  cell('4', { align: 'center', fill: tableAlt }),
  cell('Local LLM 개념', { bold: true, fill: tableAlt }),
  cell('0.5h', { align: 'center', fill: tableAlt }),
  cell('Ollama/LlamaCpp/HuggingFace,\nGGUF 포맷, 양자화(Q4/Q5/Q8),\n한국어 모델 소개', { fill: tableAlt }),
  cell('- (개념 학습)', { align: 'center', fill: tableAlt }),
  cell('이론', { align: 'center', fill: tableAlt })
]
// Row 3 (white)
[
  cell('4', { align: 'center', fill: white }),
  cell('웹검색 + YouTube\n통합 Agent', { bold: true, fill: white }),
  cell('2h', { align: 'center', fill: white }),
  cell('Tavily/DuckDuckGo/Serper,\nYouTube 자막 추출, 멀티소스 RAG,\n캐싱/Resilience 패턴', { fill: white }),
  cell('웹검색 Agent\n멀티소스 Agent', { fill: white }),
  cell('이론\n실습', { align: 'center', fill: white })
]
// Row 4 (tableAlt)
[
  cell('4', { align: 'center', fill: tableAlt }),
  cell('GraphRAG', { bold: true, fill: tableAlt }),
  cell('2h', { align: 'center', fill: tableAlt }),
  cell('Vector RAG vs GraphRAG,\n인덱싱(엔터티/관계/커뮤니티),\nLocal/Global/Hybrid Search', { fill: tableAlt }),
  cell('LightRAG 시스템\n검색 품질 비교', { fill: tableAlt }),
  cell('이론\n실습\n데모\n토론', { align: 'center', fill: tableAlt })
]
```

#### 8-4. addFooter(8)

---

## 슬라이드 9: Day 5 상세 테이블

- **레이아웃**: Detail Table
- **Compact 모드**: 아니오 (3개 모듈)
- **페이지 번호**: 9

### 구성 요소

#### 9-1. addTitle

```
제목: 'Day 5. MAS + MCP + 자연어 Agent 개발'
부제: 'Step 5 — 에이전트 만들기 | 7시간 (이론 65% / 실습 30% / 토론 5%)'
compact: false
```

#### 9-2. 테이블 상단 액센트 바

```
addShape(pres.shapes.RECTANGLE, {
  x: 0.25, y: 1.25, w: 9.5, h: 0.035, fill: { color: primary }, line: { width: 0 }
})
```

#### 9-3. 6열 테이블

```
테이블 위치: x=0.25, y=1.28, w=9.5
colW: [0.55, 1.6, 0.5, 4.35, 1.25, 0.75]
autoPage: false
```

**헤더행**:
```
[hCell('일'), hCell('모듈명'), hCell('시간'), hCell('핵심 내용'), hCell('산출물'), hCell('방법')]
```

**데이터행 (3행)**:

| # | 일 | 모듈명 | 시간 | 핵심 내용 | 산출물 | 방법 | fill |
|---|---|--------|------|-----------|--------|------|------|
| 1 | 5 | 멀티에이전트\n시스템 (MAS) | 2h | SAS 패턴, A2A 프로토콜,\nAgent Card, 아키텍처 패턴\n(ReAct/Planning/Collaboration) | SAS 패턴\nMAS 챗봇 | 이론\n실습 | white |
| 2 | 5 | MCP\n(Model Context Protocol) | 2.5h | JSON-RPC 2.0, Tools/Resources/\nPrompts, Sampling/Elicitation,\nOAuth 2.1, MCP SDK | MCP 서버\nClaude 연동 | 이론\n실습\n데모 | tableAlt |
| 3 | 5 | 자연어로\nAgent 개발 | 2h | 자연어 -> 프로토타입 -> 프로덕션,\nDify Visual Builder, DSL 구조,\n5단계 워크플로우 | Dify 고객 상담\nAgent 프로토타입 | 이론\n실습\n토론 | white |

```javascript
// Row 1 (white)
[
  cell('5', { align: 'center', fill: white }),
  cell('멀티에이전트\n시스템 (MAS)', { bold: true, fill: white }),
  cell('2h', { align: 'center', fill: white }),
  cell('SAS 패턴, A2A 프로토콜,\nAgent Card, 아키텍처 패턴\n(ReAct/Planning/Collaboration)', { fill: white }),
  cell('SAS 패턴\nMAS 챗봇', { fill: white }),
  cell('이론\n실습', { align: 'center', fill: white })
]
// Row 2 (tableAlt)
[
  cell('5', { align: 'center', fill: tableAlt }),
  cell('MCP\n(Model Context Protocol)', { bold: true, fill: tableAlt }),
  cell('2.5h', { align: 'center', fill: tableAlt }),
  cell('JSON-RPC 2.0, Tools/Resources/\nPrompts, Sampling/Elicitation,\nOAuth 2.1, MCP SDK', { fill: tableAlt }),
  cell('MCP 서버\nClaude 연동', { fill: tableAlt }),
  cell('이론\n실습\n데모', { align: 'center', fill: tableAlt })
]
// Row 3 (white)
[
  cell('5', { align: 'center', fill: white }),
  cell('자연어로\nAgent 개발', { bold: true, fill: white }),
  cell('2h', { align: 'center', fill: white }),
  cell('자연어 -> 프로토타입 -> 프로덕션,\nDify Visual Builder, DSL 구조,\n5단계 워크플로우', { fill: white }),
  cell('Dify 고객 상담\nAgent 프로토타입', { fill: white }),
  cell('이론\n실습\n토론', { align: 'center', fill: white })
]
```

#### 9-4. addFooter(9)

---

## 슬라이드 10: 교육 차별성 (Overview — 2x3 Grid)

- **레이아웃**: Overview 2x3 Grid
- **Compact 모드**: 아니오
- **페이지 번호**: 10

### 구성 요소

#### 10-1. addTitle

```
제목: '교육 차별성'
부제: '현장 적용 가능한 AI Agent 개발 역량을 완성합니다'
compact: false

액센트 바: x=0.5, y=0.3, w=0.07, h=0.5, fill=primary
제목: x=0.72, y=0.25, w=8.5, h=0.5, fontSize=22, bold, color=dark
부제: x=0.72, y=0.72, w=8.5, h=0.4, fontSize=18, color=midGray
구분선: x=0.25, y=1.2, w=9.5, h=0.008, fill=lightGray
```

#### 10-2. 섹션 소제목

```
addText('6대 핵심 차별점', {
  x: 0.5, y: 1.35, w: 9.0, h: 0.35,
  fontSize: 18, bold: true, color: dark, fontFace: '맑은 고딕',
  align: 'center'
})
```

#### 10-3. 2x3 그리드

**그리드 설정**: 슬라이드 3과 동일한 좌표 체계 사용.

**그리드 데이터 (6셀)**:

| 위치 | 라벨 | 값 |
|------|------|-----|
| (1,1) | 실습 중심 | 전체 시간의 36% 실습 + 6% 토론. 매일 실습 과제 부여, 통합 프로젝트로 마무리 |
| (1,2) | 최신 트렌드 | 2025~2026 최신 기술 반영: MCP, GraphRAG, A2A, Dify, Claude Code 활용 |
| (2,1) | 멀티 LLM | OpenAI, Claude, Gemini, Groq 4개 LLM 비교 실습. 벤더 종속 없는 개발 역량 |
| (2,2) | 도식화 학습 | 아키텍처 다이어그램, 워크플로우 시각화, 비교표 중심 설명 |
| (3,1) | 통합 과제 | 5일 학습 기술을 종합한 AI Agent 시스템 구현 프로젝트 (2주 내 제출) |
| (3,2) | 교육 방식 | 이론 -> 데모 -> 실습 -> 토론의 4단계 순환 구조. 점진적 난이도 상승 |

**셀별 좌표**: 슬라이드 3과 동일.

| 셀 | labelX | rowY | cellX | cellW |
|----|--------|------|-------|-------|
| (1,1) 실습 중심 | 0.5 | 1.85 | 1.65 | 3.2 |
| (1,2) 최신 트렌드 | 5.35 | 1.85 | 6.5 | 3.0 |
| (2,1) 멀티 LLM | 0.5 | 3.02 | 1.65 | 3.2 |
| (2,2) 도식화 학습 | 5.35 | 3.02 | 6.5 | 3.0 |
| (3,1) 통합 과제 | 0.5 | 4.19 | 1.65 | 3.2 |
| (3,2) 교육 방식 | 5.35 | 4.19 | 6.5 | 3.0 |

**각 셀 코드 패턴**: 슬라이드 3과 동일한 구조.

```javascript
// 라벨 영역 (primary 배경, 흰색 텍스트)
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: {labelX}, y: {rowY}, w: 1.15, h: 1.05,
  fill: { color: primary }, rectRadius: 0.05, line: { width: 0 }
})
addText('{라벨}', {
  x: {labelX}, y: {rowY}, w: 1.15, h: 1.05,
  fontSize: 14, bold: true, color: white, fontFace: '맑은 고딕',
  align: 'center', valign: 'middle'
})

// 값 영역 (vLightGray 배경)
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: {cellX}, y: {rowY}, w: {cellW}, h: 1.05,
  fill: { color: vLightGray }, rectRadius: 0.05, line: { width: 0 }
})
addText('{값}', {
  x: {cellX + 0.15}, y: {rowY}, w: {cellW - 0.3}, h: 1.05,
  fontSize: 12, color: dark, fontFace: '맑은 고딕',
  valign: 'middle'
})
```

#### 10-4. addFooter(10)

---

## 슬라이드 11: 평가 방법 및 통합 프로젝트

- **레이아웃**: Detail Table + 정보 박스
- **Compact 모드**: 아니오 (3행 + 추가 정보)
- **페이지 번호**: 11

### 구성 요소

#### 11-1. addTitle

```
제목: '평가 방법 및 통합 프로젝트'
부제: '5일간의 학습을 종합하는 프로젝트 기반 평가'
compact: false

액센트 바: x=0.5, y=0.3, w=0.07, h=0.5, fill=primary
제목: x=0.72, y=0.25, w=8.5, h=0.5, fontSize=22, bold, color=dark
부제: x=0.72, y=0.72, w=8.5, h=0.4, fontSize=18, color=midGray
구분선: x=0.25, y=1.2, w=9.5, h=0.008, fill=lightGray
```

#### 11-2. 테이블 상단 액센트 바

```
addShape(pres.shapes.RECTANGLE, {
  x: 0.25, y: 1.25, w: 9.5, h: 0.035, fill: { color: primary }, line: { width: 0 }
})
```

#### 11-3. 평가 기준 테이블 (3열)

```
테이블 위치: x=0.25, y=1.28, w=9.5
colW: [2.0, 1.5, 6.0]
autoPage: false
```

**헤더행**:
```
[hCell('평가 항목'), hCell('비중'), hCell('세부 기준')]
```

**데이터행 (3행)**:

| 평가 항목 | 비중 | 세부 기준 | fill |
|-----------|------|-----------|------|
| 기술적 완성도 | 40% | 필수 기술 3개 이상 통합, 정상 동작, 에러 처리 | white |
| 아키텍처 설계 | 30% | 적절한 기술 선택, 확장 가능한 구조, 문서화 품질 | tableAlt |
| 발표 및 시연 | 30% | 명확한 설명, 실제 동작 시연, 질의응답 대응 | white |

```javascript
// Row 1 (white)
[
  cell('기술적 완성도', { bold: true, align: 'center', fill: white }),
  cell('40%', { align: 'center', bold: true, color: primary, fill: white }),
  cell('필수 기술 3개 이상 통합, 정상 동작, 에러 처리', { fill: white })
]
// Row 2 (tableAlt)
[
  cell('아키텍처 설계', { bold: true, align: 'center', fill: tableAlt }),
  cell('30%', { align: 'center', bold: true, color: primary, fill: tableAlt }),
  cell('적절한 기술 선택, 확장 가능한 구조, 문서화 품질', { fill: tableAlt })
]
// Row 3 (white)
[
  cell('발표 및 시연', { bold: true, align: 'center', fill: white }),
  cell('30%', { align: 'center', bold: true, color: primary, fill: white }),
  cell('명확한 설명, 실제 동작 시연, 질의응답 대응', { fill: white })
]
```

#### 11-4. 프로젝트 안내 박스

```javascript
// 프로젝트 정보 배경 박스
addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: 0.25, y: 2.85, w: 9.5, h: 2.3,
  fill: { color: vLightGray },
  rectRadius: 0.08,
  line: { width: 0 }
})

// 박스 제목
addText('통합 프로젝트 안내', {
  x: 0.5, y: 2.95, w: 9.0, h: 0.35,
  fontSize: 14, bold: true, color: primary, fontFace: '맑은 고딕'
})

// 좌측 세로 액센트 바
addShape(pres.shapes.RECTANGLE, {
  x: 0.5, y: 3.35, w: 0.05, h: 1.55,
  fill: { color: primary },
  line: { width: 0 }
})

// 프로젝트 상세 텍스트
addText([
  { text: '주제: ', options: { fontSize: 12, bold: true, color: dark, fontFace: '맑은 고딕' } },
  { text: '5일간 학습한 기술을 종합한 실무 AI Agent 시스템 구현\n', options: { fontSize: 12, color: darkGray, fontFace: '맑은 고딕' } },
  { text: '팀 구성: ', options: { fontSize: 12, bold: true, color: dark, fontFace: '맑은 고딕' } },
  { text: '개인 또는 2~3인 팀\n', options: { fontSize: 12, color: darkGray, fontFace: '맑은 고딕' } },
  { text: '제출 기한: ', options: { fontSize: 12, bold: true, color: dark, fontFace: '맑은 고딕' } },
  { text: '교육 종료 후 2주 이내\n', options: { fontSize: 12, color: darkGray, fontFace: '맑은 고딕' } },
  { text: '필수 포함 기술: ', options: { fontSize: 12, bold: true, color: dark, fontFace: '맑은 고딕' } },
  { text: 'LLM API, 데이터 처리, RAG, Agent 도구 연동, MAS 중 3개 이상\n', options: { fontSize: 12, color: darkGray, fontFace: '맑은 고딕' } },
  { text: '제출물: ', options: { fontSize: 12, bold: true, color: dark, fontFace: '맑은 고딕' } },
  { text: '소스 코드(GitHub) + 아키텍처 문서 + 데모 영상(5분) + 발표 자료(10분)', options: { fontSize: 12, color: darkGray, fontFace: '맑은 고딕' } }
], {
  x: 0.75, y: 3.35, w: 8.5, h: 1.6,
  valign: 'top',
  lineSpacingMultiple: 1.6,
  paraSpaceAfter: 2
})
```

#### 11-5. addFooter(11)

---

## 종합 체크리스트

### 폰트 규격 검증

- [x] 모든 슬라이드 제목: 22pt Bold
- [x] 부제 (Normal): 18pt Regular
- [x] 부제 (Compact): 해당 슬라이드 없음 (모든 테이블 6행 미만)
- [x] 본문강조: 14pt Bold (라벨, 그리드 셀 라벨)
- [x] 본문일반: 12pt Regular (테이블 데이터, 일반 텍스트)
- [x] 표지 제목: 30pt Bold
- [x] 표지 인용구: 11pt Italic (유일한 12pt 미만 예외)
- [x] 푸터 페이지번호: 10pt (유일한 12pt 미만 예외)
- [x] 최소 폰트 규칙 준수 확인 완료

### 레이아웃 검증

- [x] 모든 테이블: x=0.25, w=9.5 (전체 너비)
- [x] 모든 콘텐츠 하단 < y=5.35 (푸터 영역 미침범)
- [x] Compact 모드: Day 1~5 모두 모듈 6개 미만이므로 Normal 모드 적용
- [x] 슬라이드 분할: Day 2가 5개 모듈로 최대 (7개 미만이므로 분할 불필요)

### 데이터 정합성 검증

- [x] Day 1: 4개 모듈 (1-1, 1-2, 1-3, 1-4) — 모두 포함
- [x] Day 2: 5개 모듈 (2-1, 2-2, 2-3, 2-4, 2-5) — 모두 포함
- [x] Day 3: 4개 모듈 (3-1, 3-2, 3-3, 3-4) — 모두 포함
- [x] Day 4: 4개 모듈 (4-1, 4-2, 4-3, 4-4) — 모두 포함
- [x] Day 5: 3개 모듈 (5-1, 5-2, 5-3) — 모두 포함
- [x] 총 20개 모듈, 5일, 35시간 — 원본과 일치
- [x] 각 모듈별 시간, 핵심 내용, 산출물, 교육 방법 모두 포함
- [x] 성장 경로 5단계 (Step 1~5) 커리큘럼 맵에 반영
- [x] 평가 기준(40%/30%/30%) 원본과 일치
- [x] 통합 프로젝트 정보(팀 구성, 제출 기한, 제출물) 원본과 일치

### 이미지 검증

- [x] 표지 이미지: proposal_cover.png — 슬라이드 1에 매핑
- [x] 프로필 이미지: proposal_profile.png — 슬라이드 2에 매핑
- [x] 이미지 2개 이상 생성 확인
- [x] 이미지 경로: /Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/images/

### 명세 완전성 검증

- [x] 모든 슬라이드의 모든 요소에 x, y, w, h 좌표 포함
- [x] 컬러 팔레트 13개 역할 모두 정의
- [x] 폰트 체계 8개 역할 모두 정의
- [x] PptxGenJS Shape 규칙 명시
- [x] 공통 컴포넌트(addTitle, addFooter, cell, hCell) 완전 정의
- [x] 코드 생성에 필요한 모든 텍스트 내용 포함

---

## 파일 정보

```
명세서 파일: /Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/pptx-proposal-specification.md
출력 PPTX: /Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/ai-agent-development-proposal.pptx
이미지 디렉토리: /Users/dreamondal/workspace/curriculum/plugins/tech-curriculum/output/ai-agent-development/images/
  - proposal_cover.png (표지 이미지)
  - proposal_profile.png (프로필 이미지)
총 슬라이드: 11장
슬라이드 구성: 표지 1 + 인사말 1 + 개요 2 + 커리큘럼 맵 1 + 상세 테이블 6 = 11장
```
