# PPTX 자연어 명세서

## 전역 스타일 설정

- **파일명**: curriculum_presentation.pptx
- **저장 경로**: /Users/dreamondal/workspace/tech-curriculum/output/ai-curriculum/curriculum_presentation.pptx
- **이미지 디렉토리**: /Users/dreamondal/workspace/tech-curriculum/output/ai-curriculum/images/
- **테마**: Professional
- **배경색**: 흰색 (#FFFFFF)
- **주 강조색**: Forest Green (#228B22)
- **보조 강조색**: Tea Green (#D0F0C0)
- **액센트색**: Emerald (#50C878)
- **텍스트색**: Dark Gray (#333333)
- **폰트**: 맑은 고딕
  - 슬라이드 제목: 22pt, Bold, Forest Green
  - 슬라이드 설명: 18pt, SemiBold, Dark Gray
  - 본문강조: 16pt, Regular, Dark Gray
  - 본문일반: 14pt, Regular, Gray
- **레이아웃 원칙**: 상하좌우 5% 마진, 한 슬라이드 최대 3개 핵심 메시지

---

## 슬라이드 1: 표지 (Title Slide)

**레이아웃**: Title Slide
**배경**: 흰색 배경, 우측 상단에 연한 녹색 그라데이션 장식

**제목**:
```
생성형 AI 어플리케이션 개발 교육
```
(중앙 정렬, 맑은 고딕 32pt Bold, Forest Green)

**부제**:
```
기초부터 고급까지, 7일간의 완벽한 여정
```
(중앙 정렬, 맑은 고딕 20pt SemiBold, Dark Gray)

**하단 정보**:
```
2026년 교육 과정
```
(중앙 정렬, 맑은 고딕 14pt Regular, Gray)

**시각 요소**: 중앙 하단에 AI 네트워크 이미지 (녹색 계열, 투명도 30%)
**이미지 파일**: `images/slide_01_cover.png` — 표지 중앙 하단 또는 배경 장식으로 삽입

---

## 슬라이드 2: 왜 이 교육이 필요한가? (Problem Statement)

**레이아웃**: Title and Content
**제목**:
```
AI 시대, 개발자에게 요구되는 새로운 역량
```
(좌측 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
현재 개발자들이 겪고 있는 3가지 Pain Point
```
(좌측 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**본문 내용** (3개 박스로 구성):

**박스 1** (연한 녹색 배경):
```
❌ LLM API는 알지만, 실전 적용 방법을 모른다
• API 호출은 할 수 있지만, 실무에 어떻게 적용해야 할지 막막함
• 단순 챗봇을 넘어서는 복잡한 시스템 구현 경험 부족
```

**박스 2** (연한 녹색 배경):
```
❌ RAG, Agent 같은 용어는 들었지만 구현은 막막하다
• 개념은 이해하지만, 실제 코드로 구현하는 방법을 모름
• 프레임워크(LangChain)는 복잡하고 러닝커브가 높음
```

**박스 3** (연한 녹색 배경):
```
❌ 빠르게 변하는 AI 생태계, 체계적 학습 경로가 필요하다
• GraphRAG, MCP 등 새로운 기술이 너무 빠르게 등장
• 단편적인 튜토리얼만 보면서 학습하기엔 한계가 있음
```

(각 박스: 16pt Regular, Dark Gray, 좌측 정렬, Tea Green 배경)

---

## 슬라이드 3: 교육 과정 개요 (Overview)

**레이아웃**: Title and Content
**제목**:
```
7일간의 완벽한 AI 개발 로드맵
```
(좌측 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
이론 40% : 실습 60%의 실전 중심 커리큘럼
```
(좌측 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**타임라인 그래픽** (좌측에서 우측으로):

**PART 1: 기본과정** (연한 녹색 박스):
```
📅 3일 (24시간)
🎯 학습 목표: AI 개요부터 멀티모달까지

Day 1: AI 어플리케이션 기초 (8시간)
• LLM API, 프롬프트 엔지니어링, 멀티턴 대화

Day 2: 문서 처리와 음성 AI (8시간)
• 문서 요약, PDF 처리, STT/TTS 파이프라인

Day 3: 비전 AI와 Local LLM (8시간)
• VLM, Ollama, 종합 프로젝트
```

**화살표** (→) (Emerald 색상)

**PART 2: 심화과정** (진한 녹색 박스):
```
📅 4일 (32시간)
🎯 학습 목표: RAG, Agent, MCP까지

Day 1: 도구 연동과 프레임워크 (8시간)
• Function Call, LangChain, Memory

Day 2: RAG 구축과 튜닝 (8시간)
• RAG 파이프라인, 품질 튜닝, 웹검색

Day 3: 고급 RAG와 에이전트 (8시간)
• GraphRAG, Multi-Agent System

Day 4: 통합과 실무 적용 (8시간)
• MCP, Dify, 종합 프로젝트
```

(본문: 16pt Regular, Dark Gray, 좌측 정렬)

---

## 슬라이드 4: 기본과정 섹션 헤더 (Section Header)

**레이아웃**: Section Header
**배경**: 연한 녹색 그라데이션 (좌측 진함 → 우측 연함)

**제목**:
```
PART 1. 기본과정
```
(중앙 정렬, 맑은 고딕 28pt Bold, White)

**부제**:
```
LLM API 기초부터 멀티모달 AI까지
3일 (24시간) | 이론 40% : 실습 60%
```
(중앙 정렬, 맑은 고딕 20pt SemiBold, White)

**시각 요소**: 중앙에 큰 숫자 "1" (투명도 20%, Forest Green)
**이미지 파일**: `images/slide_04_section_basic.png` — 배경 장식 또는 우측 하단에 삽입

---

## 슬라이드 5: Day 1 - AI 어플리케이션 기초 (Content Slide)

**레이아웃**: Title and Content
**제목**:
```
Day 1. AI 어플리케이션 기초 (8시간)
```
(좌측 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
생성형 AI 개요부터 멀티턴 대화 시스템까지
```
(좌측 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**본문 내용** (3개 모듈, 아이콘 + 텍스트):

**모듈 1** (아이콘: 💡):
```
생성형 AI 개요와 개발환경 구축
• 생성형 AI 기본 개념 이해
• Claude API, OpenAI API 설정
• Python 개발환경 구성 (VSCode, Jupyter)
```

**모듈 2** (아이콘: 🎯):
```
LLM API 기초와 프롬프트 엔지니어링
• API 호출 메커니즘 이해
• 프롬프트 작성 전략 (Few-shot, Chain-of-Thought)
• Temperature, Max Tokens 등 파라미터 튜닝
```

**모듈 3** (아이콘: 💬):
```
멀티턴 대화 시스템 구현
• 대화 히스토리 관리 패턴
• 컨텍스트 윈도우 최적화
• 실습: 역할극 챗봇 구현
```

**하단 강조 박스** (Tea Green 배경):
```
✅ 실습 예제: "페르소나를 가진 역할극 챗봇 구현"
• 다양한 역할(상담사, 면접관 등)을 수행하는 챗봇
• 대화 히스토리를 유지하며 자연스러운 응답 생성
```

(본문: 16pt Regular, Dark Gray, 좌측 정렬)

---

## 슬라이드 6: Day 2 - 문서 처리와 음성 AI (Content Slide)

**레이아웃**: Title and Content
**제목**:
```
Day 2. 문서 처리와 음성 AI (8시간)
```
(좌측 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
문서 요약부터 음성 대화 파이프라인까지
```
(좌측 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**본문 내용** (3개 모듈):

**모듈 1** (아이콘: 📄):
```
문서 요약과 텍스트 분석
• Map-Reduce 패턴으로 긴 문서 처리
• 요약 품질 향상 전략 (청킹, 계층적 요약)
• 감정 분석, 키워드 추출
```

**모듈 2** (아이콘: 📑):
```
PDF 문서 처리 및 Q&A
• PyPDF2, pdfplumber를 활용한 PDF 파싱
• 구조화된 텍스트 추출 (테이블, 이미지 캡션)
• 문서 기반 질의응답 시스템 구현
```

**모듈 3** (아이콘: 🎤):
```
음성 AI: STT + LLM + TTS 파이프라인
• Whisper API로 음성을 텍스트로 변환
• LLM으로 응답 생성
• TTS API로 음성 출력
• 실습: 음성 대화 파이프라인 구현
```

**하단 강조 박스** (Tea Green 배경):
```
✅ 실습 예제: "음성 대화 파이프라인 구현"
• 음성 입력 → 텍스트 변환 → LLM 응답 → 음성 출력
• 실시간 대화 시스템 프로토타입
```

(본문: 16pt Regular, Dark Gray, 좌측 정렬)

---

## 슬라이드 7: Day 3 - 비전 AI와 Local LLM (Content Slide)

**레이아웃**: Title and Content
**제목**:
```
Day 3. 비전 AI와 Local LLM (8시간)
```
(좌측 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
멀티모달 AI와 로컬 LLM 구축
```
(좌측 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**본문 내용** (3개 모듈):

**모듈 1** (아이콘: 🖼️):
```
VLM: 이미지를 이해하는 AI
• Vision Language Model 개요
• Claude Vision API, GPT-4 Vision 활용
• 이미지 분석, 캡션 생성, OCR
```

**모듈 2** (아이콘: 🖥️):
```
Local LLM 구축 (Ollama)
• Ollama 설치 및 모델 다운로드
• Llama 3, Mistral 등 오픈소스 모델 활용
• Cloud vs Local 비교 및 선택 기준
```

**비교 표**:
```
Cloud LLM                    Local LLM
✅ 최신 성능                  ✅ 데이터 프라이버시
✅ 관리 불필요                ✅ 비용 효율성
❌ 비용 발생                  ❌ 성능 제한
❌ 데이터 전송 필요           ❌ 인프라 관리 필요
```

**모듈 3** (아이콘: 🎯):
```
기본과정 종합 프로젝트
• 실습: 멀티모달 리포트 생성기
• 이미지 분석 + 문서 요약 + 음성 출력 통합
```

(본문: 16pt Regular, Dark Gray, 좌측 정렬)

---

## 슬라이드 8: 심화과정 섹션 헤더 (Section Header)

**레이아웃**: Section Header
**배경**: 진한 녹색 그라데이션 (좌측 진함 → 우측 연함)

**제목**:
```
PART 2. 심화과정
```
(중앙 정렬, 맑은 고딕 28pt Bold, White)

**부제**:
```
Function Call부터 Multi-Agent까지
4일 (32시간) | 실전 중심 고급 기술
```
(중앙 정렬, 맑은 고딕 20pt SemiBold, White)

**시각 요소**: 중앙에 큰 숫자 "2" (투명도 20%, Emerald)
**이미지 파일**: `images/slide_08_section_advanced.png` — 배경 장식 또는 우측 하단에 삽입

---

## 슬라이드 9: Day 1 - 도구 연동과 프레임워크 (Content Slide)

**레이아웃**: Title and Content
**제목**:
```
심화 Day 1. 도구 연동과 프레임워크 (8시간)
```
(좌측 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
Function Calling과 LangChain 마스터하기
```
(좌측 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**본문 내용** (3개 모듈):

**모듈 1** (아이콘: 🔧):
```
Function Calling: LLM에 도구 연결
• Function Calling 메커니즘 이해
• 외부 API 연동 (날씨, 검색, DB 등)
• 에러 핸들링과 재시도 전략
```

**모듈 2** (아이콘: 🔗):
```
LangChain 기초와 LCEL
• LangChain 아키텍처 이해
• LangChain Expression Language (LCEL)
• Prompt Template, Output Parser 활용
```

**모듈 3** (아이콘: 🧠):
```
Memory를 활용한 대화형 체인
• Conversation Buffer Memory
• Conversation Summary Memory
• 실습: LangChain Agent 챗봇 구현
```

**하단 강조 박스** (Tea Green 배경):
```
✅ 실습 예제: "도구를 사용하는 LangChain Agent 챗봇"
• 웹검색, 계산기, 날씨 API 등 도구 활용
• 사용자 요청에 따라 자동으로 적절한 도구 선택
```

(본문: 16pt Regular, Dark Gray, 좌측 정렬)

---

## 슬라이드 10: Day 2 - RAG 구축과 튜닝 (Content Slide)

**레이아웃**: Title and Content
**제목**:
```
심화 Day 2. RAG 구축과 튜닝 (8시간)
```
(좌측 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
Retrieval-Augmented Generation 완벽 정복
```
(좌측 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**본문 내용** (3개 모듈):

**모듈 1** (아이콘: 🏗️):
```
RAG 파이프라인: 인덱싱 → 검색 → 생성
• Document Loader로 문서 로드
• Text Splitter로 청킹
• Vector Store (Chroma, FAISS)에 임베딩 저장
• Retriever로 관련 문서 검색 후 LLM 생성
```

**모듈 2** (아이콘: ⚙️):
```
품질 튜닝: 청킹, 리랭킹, 하이브리드 검색
• Chunk Size 최적화 전략
• Cohere Reranker로 정확도 향상
• BM25 + Vector Search 하이브리드
• Metadata 필터링 활용
```

**모듈 3** (아이콘: 🌐):
```
웹검색 통합 RAG
• Tavily, Google Search API 연동
• 실시간 정보 + 내부 문서 통합
• 실습: 사내 문서 Q&A 시스템 구현
```

**하단 강조 박스** (Tea Green 배경):
```
✅ 실습 예제: "사내 문서 Q&A 시스템"
• 회사 내부 PDF, Word 문서 인덱싱
• 질문에 대한 정확한 답변 + 출처 제공
```

(본문: 16pt Regular, Dark Gray, 좌측 정렬)

**이미지 파일**: `images/slide_10_rag_architecture.png` — RAG 파이프라인 다이어그램으로 슬라이드 상단 또는 모듈 1 옆에 삽입

---

## 슬라이드 11: Day 3 - 고급 RAG와 에이전트 (Content Slide)

**레이아웃**: Title and Content
**제목**:
```
심화 Day 3. 고급 RAG와 에이전트 (8시간)
```
(좌측 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
GraphRAG와 Multi-Agent System 설계
```
(좌측 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**본문 내용** (3개 모듈):

**모듈 1** (아이콘: 🕸️):
```
GraphRAG: 지식 그래프 기반 RAG
• 기존 RAG의 한계와 GraphRAG의 필요성
• Neo4j, NetworkX로 지식 그래프 구축
• 엔티티 추출 → 관계 추출 → 그래프 쿼리
• 복잡한 질문에 대한 추론 능력 향상
```

**모듈 2** (아이콘: 🤖):
```
Multi-Agent System 설계
• 에이전트 역할 분담 전략
• Researcher, Coder, Reviewer 등 전문 에이전트
• 에이전트 간 통신 및 협업 패턴
```

**모듈 3** (아이콘: 📊):
```
LangGraph를 활용한 에이전트 워크플로우
• LangGraph로 복잡한 에이전트 흐름 설계
• 조건부 분기, 병렬 실행, 재귀 루프
• 실습: 멀티에이전트 리서치봇 구현
```

**하단 강조 박스** (Tea Green 배경):
```
✅ 실습 예제: "멀티에이전트 리서치봇"
• Researcher 에이전트: 웹검색으로 정보 수집
• Analyzer 에이전트: 수집된 정보 분석
• Writer 에이전트: 최종 리포트 작성
```

(본문: 16pt Regular, Dark Gray, 좌측 정렬)

---

## 슬라이드 12: Day 4 - 통합과 실무 적용 (Content Slide)

**레이아웤**: Title and Content
**제목**:
```
심화 Day 4. 통합과 실무 적용 (8시간)
```
(좌측 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
MCP와 Dify로 실전 프로젝트 완성
```
(좌측 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**본문 내용** (3개 모듈):

**모듈 1** (아이콘: 🔌):
```
MCP: 표준화된 도구 통합
• Model Context Protocol 개요
• MCP 서버 구축 및 클라이언트 연결
• 다양한 도구(DB, API, 파일 시스템)를 표준 인터페이스로 통합
• Claude Desktop, IDE에서 MCP 활용
```

**모듈 2** (아이콘: 🎨):
```
Dify: 노코드 AI Agent 플랫폼
• Dify 플랫폼 소개 및 설치
• 드래그앤드롭으로 RAG, Agent 워크플로우 구성
• Knowledge Base, Tools 관리
• API 배포 및 프론트엔드 연동
```

**모듈 3** (아이콘: 🚀):
```
심화과정 종합 프로젝트
• 실습: 노코드 + 코드 하이브리드 Agent
• Dify로 빠른 프로토타입 → Python으로 커스텀 확장
• MCP로 외부 시스템 통합
```

**하단 강조 박스** (Tea Green 배경):
```
✅ 실습 예제: "하이브리드 AI Agent 시스템"
• Dify로 UI와 기본 워크플로우 구성
• Python으로 고급 로직(GraphRAG, 커스텀 도구) 구현
• MCP로 사내 시스템(CRM, ERP) 연동
```

(본문: 16pt Regular, Dark Gray, 좌측 정렬)

---

## 슬라이드 13: 차별화 포인트 (Highlight Slide)

**레이아웃**: Title and Content
**제목**:
```
이 교육 과정의 3가지 차별점
```
(중앙 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
왜 이 교육을 선택해야 하는가?
```
(중앙 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**본문 내용** (3개 큰 박스, 좌우 배치):

**차별점 1** (큰 아이콘: 🎯 + Tea Green 배경):
```
실전 즉시 투입 가능

✅ 실습 비중 60%
• 매 모듈마다 hands-on 랩 제공
• 이론 학습 직후 바로 코딩 실습

✅ 5가지 실무 조합 패턴
• 사내 문서 Q&A (RAG)
• AI 회의록 자동화 (STT + 요약 + TTS)
• 멀티에이전트 리서치봇 (MAS + 웹검색)
• 고객 상담 챗봇 (Function Call + Memory)
• 이미지 분석 리포트 (VLM + 문서 생성)
```

**차별점 2** (큰 아이콘: 🔥 + Tea Green 배경):
```
2025년 최신 트렌드 반영

✅ GraphRAG
• Microsoft가 개발한 차세대 RAG 기술
• 복잡한 추론 질문에 대한 답변 능력 향상

✅ Multi-Agent System (MAS)
• 여러 에이전트가 협업하는 시스템 설계
• LangGraph로 복잡한 워크플로우 구현

✅ Model Context Protocol (MCP)
• Anthropic이 제안한 표준화된 도구 통합 프로토콜
• 다양한 시스템을 일관된 인터페이스로 연결

✅ Dify 노코드 플랫폼
• 빠른 프로토타입 + 코드 확장의 하이브리드 접근
```

**차별점 3** (큰 아이콘: 📊 + Tea Green 배경):
```
체계적 평가 시스템

✅ 일일 실습 평가 (50%)
• 매일 실습 과제 제출 및 피드백

✅ 종합 프로젝트 (30%)
• 기본/심화 각 1회씩 실전 프로젝트
• 실무 시나리오 기반 과제

✅ 이론 퀴즈 (20%)
• 핵심 개념 확인 퀴즈
• 즉각적인 피드백 제공
```

(본문: 16pt Regular, Dark Gray, 좌측 정렬)

---

## 슬라이드 14: 실무 적용 패턴 (Application Examples)

**레이아웃**: Title and Content
**제목**:
```
교육 후 바로 적용 가능한 5가지 패턴
```
(좌측 정렬, 맑은 고딕 22pt Bold, Forest Green)

**부제**:
```
실무 시나리오별 기술 조합 가이드
```
(좌측 정렬, 맑은 고딕 18pt SemiBold, Dark Gray)

**본문 내용** (5개 패턴, 아이콘 + 설명):

**패턴 1** (아이콘: 📚):
```
사내 문서 Q&A 시스템
• 기술 조합: RAG + Vector DB + Reranker
• 적용 분야: HR 정책 문서, 기술 매뉴얼, 법률 계약서
• 구현 시간: 2-3일
```

**패턴 2** (아이콘: 🎤):
```
AI 회의록 자동화
• 기술 조합: STT (Whisper) + 요약 (Map-Reduce) + TTS
• 적용 분야: 주간 회의, 고객 미팅, 교육 세션
• 구현 시간: 1-2일
```

**패턴 3** (아이콘: 🤖):
```
멀티에이전트 리서치봇
• 기술 조합: Multi-Agent System + 웹검색 + GraphRAG
• 적용 분야: 시장 조사, 경쟁사 분석, 기술 동향 분석
• 구현 시간: 3-5일
```

**패턴 4** (아이콘: 💬):
```
고객 상담 챗봇
• 기술 조합: Function Call + Conversation Memory + RAG
• 적용 분야: 고객 지원, 제품 추천, FAQ 자동 응답
• 구현 시간: 2-3일
```

**패턴 5** (아이콘: 🖼️):
```
이미지 분석 리포트 생성
• 기술 조합: VLM + 문서 생성 + 템플릿 엔진
• 적용 분야: 품질 검사, 매장 모니터링, 의료 이미지 분석
• 구현 시간: 2-3일
```

**하단 강조 박스** (Emerald 배경, 흰색 텍스트):
```
💡 교육 수료 후 1주일 내 실무 프로젝트 시작 가능
```

(본문: 16pt Regular, Dark Gray, 좌측 정렬)

---

## 슬라이드 15: 마무리 및 Q&A (Closing Slide)

**레이아웃**: Closing Slide
**배경**: 연한 녹색 그라데이션 (좌측 상단 → 우측 하단)

**제목**:
```
7일 후, 당신은 AI 개발 전문가가 됩니다
```
(중앙 정렬, 맑은 고딕 24pt Bold, Forest Green)

**본문**:
```
✅ LLM API부터 GraphRAG까지 완벽 마스터
✅ 실무에 바로 적용 가능한 5가지 패턴 습득
✅ 최신 트렌드(MCP, Dify, Multi-Agent) 완전 정복
```
(중앙 정렬, 맑은 고딕 18pt Regular, Dark Gray)

**CTA (Call-to-Action)** (큰 박스, Forest Green 배경, 흰색 텍스트):
```
🚀 지금 바로 시작하세요
```
(중앙 정렬, 맑은 고딕 22pt Bold)

**연락처 정보** (하단):
```
📧 Email: education@example.com
📞 Tel: 02-1234-5678
🌐 Web: www.ai-education.com
```
(중앙 정렬, 맑은 고딕 14pt Regular, Dark Gray)

**하단 캡션**:
```
Thank you for your attention!
Q&A Session
```
(중앙 정렬, 맑은 고딕 16pt SemiBold, Gray)

**이미지 파일**: `images/slide_15_closing.png` — 배경 장식 또는 CTA 박스 상단에 삽입

---

## 종합 체크리스트

✅ 총 15장 슬라이드 (표지 ~ 마무리)
✅ Professional 스타일, Forest Green 강조, 흰색 배경
✅ 맑은 고딕 폰트 (제목 22pt / 부제 18pt / 본문 16pt / 캡션 14pt)
✅ 한 슬라이드 최대 3개 핵심 메시지
✅ 골든써클 프레임워크 (WHY → HOW → WHAT) 반영
✅ 기본/심화 과정 색상 구분 (연녹색 / 진녹색)
✅ 실습 중심 교육 특성 강조
✅ 최신 트렌드(GraphRAG, MAS, MCP, Dify) 포함
✅ 실무 적용 패턴 5가지 제시
✅ 구체적 수치와 예시 포함

---

## 파일 정보

- **파일명**: curriculum_presentation.pptx
- **저장 경로**: /Users/dreamondal/workspace/tech-curriculum/output/ai-curriculum/curriculum_presentation.pptx
- **슬라이드 수**: 15장
- **예상 발표 시간**: 20-25분
