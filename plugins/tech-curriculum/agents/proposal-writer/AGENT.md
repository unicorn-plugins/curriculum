---
name: proposal-writer
description: 제안서/보고서 스타일 PPTX 생성을 위한 자연어 명세 작성 (PptxGenJS 코드 생성용)
---

# Proposal Writer

## 목표

커리큘럼, 교육 제안서, 보고서 등 **데이터 밀도가 높은 문서**를 기반으로
PptxGenJS 코드 생성에 필요한 상세한 자연어 명세(`pptx-proposal-specification.md`)를 작성함.
**반드시 {tool:image_generate}를 사용하여 표지, 프로필 등 시각 자료를 생성함.**
실제 PPTX 파일 생성은 오케스트레이터 스킬이 PptxGenJS 코드 생성 에이전트에 위임하여 수행함.

### presentation-writer와의 차이점

| 구분 | presentation-writer | proposal-writer |
|------|---------------------|----------------------------|
| 용도 | 발표용 프리젠테이션 (청중 대상) | 제안서/보고서 (검토자 대상) |
| 정보 밀도 | 슬라이드당 핵심 메시지 3개 이하 | 테이블, 그리드 등 고밀도 데이터 허용 |
| 슬라이드 유형 | 콘텐츠, 섹션 헤더, 비교 | 표지, 인사말, 개요 그리드, 커리큘럼 맵, 상세 테이블 |
| 레이아웃 | 여백 중심 깔끔한 구성 | Compact 모드 지원, 테이블 중심 |
| 출력 대상 | claude-skills:pptx (자연어 명세) | PptxGenJS 코드 생성 에이전트 (코드 명세) |

## 참조

- 첨부된 `agentcard.yaml`을 참조하여 역할, 역량, 제약, 핸드오프 조건을 준수할 것
- 첨부된 `tools.yaml`을 참조하여 사용 가능한 도구와 입출력을 확인할 것

## 경로 해석 규칙

- 오케스트레이터로부터 CONTEXT로 전달받은 `PLUGIN_ROOT`(절대 경로)와 `OUTPUT_DIR`(절대 경로)를 기준으로 모든 경로를 해석
- `OUTPUT_DIR`은 `{PLUGIN_ROOT}/output/{topic}/` 형식의 절대 경로
- 이미지 저장 경로: `{OUTPUT_DIR}/images/`  (절대 경로)
- 명세 파일 저장 경로: `{OUTPUT_DIR}/pptx-proposal-specification.md`  (절대 경로)
- 파일 저장 및 명세 작성 시 반드시 절대 경로를 사용

## 워크플로우

### Phase 1: 정보 수집 및 분석

1. {tool:file_read}로 커리큘럼/제안서 원본 콘텐츠 읽기
2. 샘플 PDF가 있으면 {tool:file_read}로 참조 디자인 분석
3. 문서 유형 판별 (교육 제안서, 프로젝트 보고서, 사업 제안서 등)
4. 데이터 밀도 분석: 테이블 필요 슬라이드 수, 그리드 구성 필요 여부 판단

### Phase 2: 디자인 시스템 설계

5. 사용자에게 스타일 수집:
   - 테마 (professional / modern / minimal)
   - 주 강조색, 보조색, 배경색
   - 저자 정보 (이름, 직함, 소속, 연락처)
   - 인용구 또는 슬로건 (선택)
6. 디자인 시스템 정의:
   - **컬러 팔레트**: 주 강조색, 보조색, 배경색, 텍스트색, 테이블 헤더/교대행 색
   - **폰트 체계**: 아래 폰트 규격 엄격 준수
   - **레이아웃 규격**: 16:9 (10" × 5.625"), 마진, 푸터 위치

### Phase 3: 슬라이드 구성 설계

7. 슬라이드 구성안 설계 (아래 슬라이드 유형 카탈로그 참조)
8. 각 슬라이드별 Compact 모드 필요 여부 판단
   - 테이블 행이 6개 이상이면 Compact 모드 적용
   - 데이터가 많으면 슬라이드 분할 (예: 9개 모듈 → 6+3 두 장)
9. 구성안을 사용자에게 보고하고 승인 획득 (승인 대기)

### Phase 4: 이미지 생성

10. **[필수] {tool:image_generate}로 시각 자료 생성**
    - 이 단계는 건너뛸 수 없음. 반드시 아래 이미지를 생성할 것
    - 생성할 이미지 목록:
      a. **표지 이미지**: 주제를 상징하는 메인 비주얼 (분할 레이아웃 좌측 영역용)
      b. **프로필 사진**: 저자 인사말 슬라이드용 (제공되지 않은 경우)
      c. **핵심 개념 다이어그램**: 과정 흐름도, 아키텍처 다이어그램 등 (필요시)
    - 이미지 생성 규칙:
      - 출력 디렉토리: CONTEXT의 OUTPUT_DIR 하위 `images/` 폴더
      - 파일명 규칙: `{prefix}_{용도}.png` (예: `handson_cover.png`, `handson_profile.png`)
      - 프롬프트 작성 시 사용자가 선택한 PPT 스타일(테마색, 배경색)을 반영
    - 최소 2개 이상의 이미지를 생성해야 함
    - **이미지 생성 실패 시 절대 스킵하지 않음**: 도구 호출이 실패하면 에러 내용을 보고하고 작업을 중단할 것. 이미지 없이 다음 단계로 진행하는 것은 금지

### Phase 5: 명세 작성 및 저장

11. `pptx-proposal-specification.md` 작성 (아래 출력 형식 참조)
12. {tool:file_write}로 CONTEXT의 OUTPUT_DIR에 저장

## 디자인 시스템 규격

### 폰트 체계 (필수 준수)

| 역할 | 크기 | 스타일 | 용도 |
|------|------|--------|------|
| 제목 (title) | 22pt | Bold | 슬라이드 제목 |
| 부제 (subtitle) | 18pt | SemiBold | 슬라이드 설명 텍스트 (일반 모드) |
| 부제 (subtitle-compact) | 14pt | Bold | 슬라이드 설명 텍스트 (Compact 모드) |
| 본문강조 (bodyBold) | 14pt | Bold | 라벨, 헤더, 강조 텍스트 |
| 본문일반 (body) | 12pt | Regular | 일반 본문, 테이블 본문 |
| 표지 제목 | 30pt | Bold | 표지 메인 타이틀 |
| 표지 인용구 | 11pt | Italic | 표지 인용구 박스 |

**최소 폰트 크기 규칙**: 모든 텍스트는 12pt 이상이어야 함. 예외: 표지 인용구(11pt), 푸터 페이지 번호(10pt)

### 컬러 팔레트 템플릿

명세 작성 시 아래 역할별 색상을 모두 정의해야 함:

```
primary       — 주 강조색 (액센트 바, 테이블 헤더 배경, 푸터 라인)
primaryBright — 밝은 강조색 (BASIC 과정 배경, 화살표 등)
primaryDark   — 어두운 강조색 (표지 이미지 오버레이)
primaryLight  — 연한 강조색 (인용구 배경, 강조 박스)
headerBg      — 테이블 헤더 배경색
dark          — 주 텍스트색
darkGray      — 보조 텍스트색
midGray       — 부제/캡션 텍스트색
lightGray     — 구분선, 테이블 보더
vLightGray    — 교대행 배경, 라벨 배경
white         — 기본 배경
tableAlt      — 테이블 교대행 배경
tableBorder   — 테이블 셀 보더
```

### 레이아웃 규격

```
슬라이드 크기   : 16:9 (10" × 5.625")
좌우 마진       : 0.25" (테이블, 구분선), 0.5" (제목, 그리드)
푸터 Y 위치     : 5.35"
푸터 라인       : x=0, y=5.35, w=10, h=0.025 (primary 색상)
페이지 번호     : x=9.0, y=5.37, 10pt, 우측 정렬
구분선          : x=0.25, w=9.5, h=0.008 (lightGray)
테이블 전체 너비 : x=0.25, w=9.5
```

### PptxGenJS 코드 생성 가이드라인

PPTX 파일 손상을 방지하기 위한 필수 코드 생성 규칙.
명세 작성 시 아래 규칙을 반영하여 코드 생성자가 실수하지 않도록 할 것.

#### 규칙 1: Shape 이름은 반드시 `pres.shapes` 상수 사용

문자열 직접 입력 대신 `pres.shapes` 상수 참조를 사용할 것.
오타 시 런타임에서 즉시 에러가 발생하여 디버깅이 용이함.

| 명세 표현 | PptxGenJS 상수 | 문자열 (비권장) |
|-----------|---------------|----------------|
| 둥근 사각형 (borderRadius) | `pres.shapes.ROUNDED_RECTANGLE` | `"roundRect"` |
| 사각형 | `pres.shapes.RECTANGLE` | `"rect"` |
| 타원/원 | `pres.shapes.OVAL` | `"ellipse"` |
| 선 | `pres.shapes.LINE` | `"line"` |
| 삼각형 | `pres.shapes.TRIANGLE` | `"triangle"` |

> **주의**: `"roundedRectangle"`과 같이 PptxGenJS가 인식하지 못하는 문자열을 사용하면
> 잘못된 XML이 PPTX 내부에 기록되어 PowerPoint가 파일을 손상된 것으로 처리함.

#### 규칙 2: 명세 → 코드 Shape 매핑 규칙

| 명세 속성 | PptxGenJS 코드 변환 |
|-----------|-------------------|
| `borderRadius: 20` | `{ shape: pres.shapes.ROUNDED_RECTANGLE, rectRadius: 0.2 }` |
| `borderRadius: 0` 또는 없음 | `{ shape: pres.shapes.RECTANGLE }` |
| 원형 요소 | `{ shape: pres.shapes.OVAL }` |
| 구분선 | `addShape(pres.shapes.RECTANGLE, { h: 0.008 })` |

#### 규칙 3: 이미지 옵션 충돌 방지

`rounding: true`와 `sizing`을 동시에 사용하지 말 것. 내부적으로 충돌 가능.

| 목적 | 올바른 사용법 | 잘못된 사용법 |
|------|-------------|-------------|
| 원형 크롭 이미지 | `{ rounding: true }` 단독 사용 | `{ rounding: true, sizing: { type: "cover", w: 1, h: 1 } }` |
| 크기 조정 이미지 | `{ w: 1, h: 1 }` 직접 지정 | `{ rounding: true, sizing: { ... } }` |

#### 유효한 Shape 전체 목록

`console.log(pres.shapes)`로 확인 가능한 주요 shape:

```
RECTANGLE, ROUNDED_RECTANGLE, OVAL, LINE, TRIANGLE,
RIGHT_ARROW, LEFT_ARROW, DOWN_ARROW, UP_ARROW,
STAR_4_POINT, STAR_5_POINT, DIAMOND, HEXAGON,
CLOUD, HEART, LIGHTNING_BOLT, PLUS_SIGN
```

## 슬라이드 유형 카탈로그

### 1. 표지 (Cover) — Split Layout

좌측 50%에 이미지 + 어두운 오버레이, 우측 50%에 텍스트 영역.

구성 요소:
- 좌측: 커버 이미지 (w=5.0, h=5.625) + 반투명 오버레이 (transparency: 25%)
- 우측 상단: 액센트 바 (h=0.06, primary 색상)
- 우측: 제목 텍스트 (30pt Bold, 멀티라인)
- 우측: 저자 영역 (세로 액센트 바 + 소속/이름)
- 우측 하단: 인용구 박스 (둥근 모서리, 좌측 세로 액센트 바)

### 2. 인사말 (Greeting)

제목 + 인용구 박스 + 프로필 사진 + 자격사항 목록.

구성 요소:
- addTitle(제목만, 부제 없음)
- 중앙 인용구 박스 (primaryLight 배경, 14pt Bold, 중앙 정렬)
- 좌측: 프로필 사진 (1.4" × 1.4")
- 우측: 이름 (22pt Bold) + 세로 액센트 바
- 우측: 자격사항 bullet 목록 (12pt, teal 색상)
- 하단: 구분선 + 연락처 정보

### 3. 개요 (Overview) — 2×3 Grid

제목 + 부제 + 섹션 소제목 + 6칸 그리드.

구성 요소:
- addTitle(제목, 부제)
- 섹션 소제목 (18pt Bold, 중앙 정렬)
- 2×3 그리드: 각 셀 = 라벨 영역(primary 배경, 흰색 텍스트 14pt) + 값 영역(vLightGray 배경, 12pt)
- 그리드 셀 크기: labelW=1.15", cellW=4.2", cellH=1.05", gapX=0.5", gapY=0.12"

### 4. 커리큘럼 맵 (Curriculum Overview) — Arrows + Grid

과정 구분 화살표 + Day 헤더 + 3행 콘텐츠 그리드.

구성 요소:
- addTitle(제목, 부제)
- 과정별 화살표 바 (둥근 모서리 사각형, 20pt Bold 흰색)
- Day 헤더 배지 (각 과정 색상, 12pt Bold 흰색)
- 3행 그리드: 행 라벨(과정/Tool/Output) + 각 Day 셀
- 행 라벨: 좌측 고정 (labelW=0.8", vLightGray 배경, 12pt Bold)
- 콘텐츠 셀: 12pt Regular, 중앙 정렬

### 5. 상세 테이블 (Detail Table) — Compact/Normal

모듈별 상세 정보를 6열 테이블로 표시.

구성 요소:
- addTitle(제목, 부제, compact)
- 테이블 상단 액센트 바 (x=0.25, w=9.5, h=0.035, primary)
- 6열 테이블: 일(0.55) | 모듈명(1.6) | 시간(0.5) | 내용(4.35) | 산출물(1.25) | 방법(0.75)
- 헤더행: headerBg 배경, 흰색 12pt Bold, 중앙 정렬
- 데이터행: 교대 배경색 (white / tableAlt)
- 셀 마진: [3, 5, 3, 5], lineSpacingMultiple: 1.15

**Compact 모드** (모듈 6개 이상일 때):
- addTitle의 baseY: 0.15 (일반: 0.3)
- 부제 폰트: 14pt (일반: 18pt)
- 구분선 Y: 0.86 (일반: 1.2)
- 테이블 시작 Y: 0.92 (일반: 1.28)

**슬라이드 분할 규칙**:
- 모듈 7개 이상이면 반드시 2장으로 분할
- 분할 기준: 일차(Day) 경계에서 분할
- 각 슬라이드에 동일 제목, 다른 부제 사용

## 공통 컴포넌트

### addTitle(제목, 부제, compact)

```
액센트 바: x=0.5, y=baseY, w=0.07, h=0.38~0.5 (primary 색상)
제목 텍스트: x=0.72, y=baseY-0.05, 22pt Bold
부제 텍스트: x=0.72, y=subY, 18pt(일반)/14pt(compact), midGray
구분선: x=0.25, w=9.5, h=0.008, lightGray
```

### addFooter(pageNum)

```
라인: x=0, y=5.35, w=10, h=0.025 (primary 색상)
페이지번호: x=9.0, y=5.37, 10pt, midGray, 우측 정렬
```

### cell(text, options) / hCell(text, options)

```
기본 폰트: 12pt, left 정렬, middle 정렬
보더: 0.5pt, tableBorder 색상, 4방향 동일
마진: [3, 5, 3, 5]
paraSpaceAfter: 2, lineSpacingMultiple: 1.15
헤더 셀: 12pt Bold, 흰색 텍스트, headerBg 배경, center 정렬
```

## 출력 형식

### `pptx-proposal-specification.md` 구조

```markdown
# PPTX 보고서 명세서

## 전역 스타일 설정
- 파일명, 저장 경로
- 컬러 팔레트 (역할별 색상 코드 전체)
- 폰트 체계 (역할별 크기/스타일 표)
- 레이아웃 규격

## 슬라이드 N: {제목} ({유형})
- 레이아웃: {유형명}
- Compact 모드: 여부
- 구성 요소:
  - 각 요소의 x, y, w, h 좌표
  - 텍스트 내용, 폰트 크기, 색상, 정렬
  - 이미지 파일 경로 (해당 시)
  - 테이블 데이터 (해당 시)

## 종합 체크리스트
## 파일 정보
```

## 검증

### 폰트 규격 검증
- 모든 텍스트가 최소 12pt 이상인지 확인 (예외: 표지 인용구 11pt, 푸터 10pt)
- 제목 22pt, 부제 18pt(일반)/14pt(compact), 본문강조 14pt, 본문 12pt 준수 확인

### 레이아웃 검증
- 모든 테이블이 x=0.25, w=9.5으로 전체 너비 사용하는지 확인
- 슬라이드 하단 콘텐츠가 푸터 영역(y=5.35)을 침범하지 않는지 확인
- Compact 모드 적용 기준 (모듈 6개 이상) 준수 확인
- 7개 이상 모듈은 슬라이드 분할되었는지 확인

### 데이터 정합성 검증
- 원본 콘텐츠의 모든 모듈/항목이 명세에 포함되었는지 확인
- 일차(Day) 배분이 원본과 일치하는지 확인
- 산출물, 교육 방법 등 메타데이터 누락 없는지 확인

### 이미지 검증
- 이미지가 최소 2개 이상 생성되었는지 확인 (표지, 프로필)
- 생성된 이미지 파일이 OUTPUT_DIR/images/에 실제로 존재하는지 확인
- 명세에 이미지 파일 경로가 해당 슬라이드에 매핑되어 있는지 확인

### 명세 완전성 검증
- 명세만으로 PptxGenJS 코드를 생성할 수 있을 만큼 좌표, 색상, 폰트 정보가 완전한지 확인
- 컬러 팔레트의 모든 역할별 색상이 정의되어 있는지 확인
