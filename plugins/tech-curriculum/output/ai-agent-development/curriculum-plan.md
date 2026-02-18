# AI Agent 개발 실무 - 교육 수행 계획서

> 작성일: 2026-02-15
> 버전: 1.0 (승인 완료)

---

## 1. 교육 개요

| 항목 | 내용 |
|------|------|
| **교육명** | AI Agent 개발 실무 |
| **교육 대상** | 개발자 (Python 기초 이상) |
| **교육 형태** | 정식교육 5일 (1일 7시간, 총 35시간) |
| **교육 목표** | LLM API 활용부터 RAG, MAS, MCP까지 AI Agent 개발 전 과정을 실습 중심으로 학습하여 프로젝트에 즉시 적용 가능한 역량 확보 |
| **교재** | develop-agent/교재 (17개 챕터) + 실습 예제 코드 |

---

## 2. 교육 차별성

| 차별성 요소 | 설명 |
|-------------|------|
| **실습 중심** | 전 과정 실습 비중 50% 이상, 매 모듈마다 실제 동작하는 코드 작성 |
| **최신 트렌드 반영** | LangChain 1.0, MCP, GraphRAG, Dify 등 2025~2026년 최신 기술 포함 |
| **멀티 LLM 비교 학습** | OpenAI, Claude, Gemini, Groq 4개 LLM을 동일 시나리오로 비교 실습 |
| **핵심개념 도식화** | SAS 패턴, RAG 파이프라인, Agent Flow 등 복잡한 개념을 아키텍처 다이어그램으로 명확 전달 |
| **통합 과제** | 5일간 학습 내용을 종합하는 통합 프로젝트를 과제로 부여, 별도 세션에서 리뷰 |

---

## 3. AI Agent 성장 경로

교육 과정은 개발자가 AI Agent를 만들어가는 실제 여정을 따라 구성됩니다.

```
🗣️ 대화하기 → 📄 데이터 다루기 → 🔧 도구 연결하기 → 🧠 지식 확장하기 → 🤖 에이전트 만들기
```

| 단계 | 여정 | 해당 일차 | 핵심 활동 |
|------|------|-----------|-----------|
| **Step 1** | LLM과 대화하기 | Day 1 | LLM API 호출, 프롬프트 설계, 멀티턴 대화 구현 |
| **Step 2** | 데이터 다루기 | Day 2 전반 | 문서 요약, PDF 처리, 음성/이미지 등 멀티모달 I/O |
| **Step 3** | 도구 연결하기 | Day 2 후반 ~ Day 3 | Function Calling으로 외부 도구 연동, LangChain으로 체계화 |
| **Step 4** | 지식 확장하기 | Day 3 후반 ~ Day 4 | RAG로 외부 지식 통합, 품질 튜닝, GraphRAG로 관계 추론 |
| **Step 5** | 에이전트 만들기 | Day 5 | MAS 아키텍처, MCP 프로토콜, 자연어 기반 Agent 개발 |

---

## 4. 전체 일정 구성 (5일 / 35시간)

### 설계 원칙

- 주선(Main Track): 01 - 02 - 08 - 09 - 10 - 11을 축으로 구성
- 멀티모달(03~07)과 고급 주제(14~17)를 분기 배치
- 13장(Local LLM)은 교육 환경의 GPU 제약을 고려하여 Day 4에서 개념만 소개, 실습은 클라우드 API로 대체
- 통합 프로젝트는 과제로 부여하고, 별도 세션에서 발표 및 리뷰 진행

### 일정 요약

| 일차 | 주제 | 성장 경로 | 시간 | 교재 참조 |
|------|------|-----------|------|-----------|
| **Day 1** | AI 앱 기초 + LLM API + 멀티턴 | Step 1: LLM과 대화하기 | 7h | 01, 02 |
| **Day 2** | 데이터 처리(문서요약/PDF/멀티모달) + Function Calling | Step 2~3: 데이터 다루기 → 도구 연결하기 | 7h | 03, 04, 05, 06, 07, 08 |
| **Day 3** | LangChain 프레임워크 + RAG 기초 | Step 3~4: 도구 연결하기 → 지식 확장하기 | 7h | 09, 10 |
| **Day 4** | RAG 품질 튜닝 + 웹검색/YouTube + GraphRAG | Step 4: 지식 확장하기 | 7h | 11, 12, 15 |
| **Day 5** | MAS + MCP + 자연어 Agent 개발 | Step 5: 에이전트 만들기 | 7h | 14, 16, 17 |
| **별도** | 통합 프로젝트 발표 및 리뷰 | 종합 | 별도 | 전체 |

---

## 5. 일자별 구성 개요

### Day 1 - AI 앱 기초 + LLM API + 멀티턴 (7시간)

- AI 어플리케이션 개요: 비즈니스 가치, SAS 패턴, 5대 핵심 구성요소, Agent Flow 패턴
- 트랜스포머 모델 동작 원리 (인코더/디코더)
- LLM API 비교: OpenAI, Claude, Gemini, Groq (토큰 비용, Rate Limit 포함)
- 프롬프트 엔지니어링: Zero/One/Few-shot, Chain of Thought
- Python 기초 및 개발 환경 설정 (가상환경, dotenv, Pydantic)
- 멀티턴 대화: 전체 히스토리, 슬라이딩 윈도우+요약, Responses API, Chat Session
- **실습**: 여행 플래너 챗봇 (멀티턴 + Streamlit 웹 UI)

### Day 2 - 데이터 처리 + Function Calling (7시간)

- 문서 요약: LLM 기반(EXAONE) vs 전문 모델(KoBART)
- PDF 처리: Docling(AI), PyMuPDF/pdfplumber(규칙 기반)
- 멀티모달 개요: STT(Whisper/WhisperX), TTS(OpenAI/Bark), VLM(Gemini Vision/Qwen2.5-VL) -- 핵심 개념 및 데모
- Function Calling 심화: OpenAI/Claude/Gemini 3사 비교, 도구 정의, 호출 제어
- 병렬/순차 함수 호출, 스트리밍
- 모델별 고유 기능: OpenAI Custom Tools, Claude Server/System Tools, Gemini 자동 함수 호출
- **실습**: PDF 문서 요약 파이프라인, Function Calling 여행 플래너 (3사 비교)

### Day 3 - LangChain + RAG 기초 (7시간)

- LangChain 생태계: 필요성, 구성요소, 패키지 구조
- LangGraph 기반 워크플로우 관리 (Human-in-the-loop 포함)
- LLM 인터페이스: Chat Models, Prompts, Output Parsers, LCEL
- Agents & Tools: create_agent, 커스텀 도구, Middleware
- State 관리: LangGraph Checkpointer
- RAG 개념: 인덱싱 파이프라인(Load-Split-Embed-Store), 검색 메커니즘
- RAG 아키텍처 패턴 소개: Basic RAG, Self-RAG, CRAG, Adaptive RAG, Agentic RAG
- **실습**: LangChain 기반 RAG 시스템 구현 (기본 RAG + Query Transformation)

### Day 4 - RAG 고급 + 웹검색/YouTube + GraphRAG (7시간)

- RAG 품질 튜닝: 청킹 전략(시맨틱, 계층적), 임베딩 최적화, 하이브리드 검색(Dense+Sparse)
- 리랭킹: Cross-Encoder, Cohere Rerank, LLM 기반 Re-ranking
- 쿼리 최적화: HyDE, Multi-Query, Query Expansion/Rewriting
- RAGAS 평가 프레임워크, 검색 메트릭(MRR, NDCG, Recall@K)
- Local LLM 개념 소개: Ollama, 양자화, 모델 선택 가이드 (실습은 클라우드 API)
- 웹검색(Tavily, DuckDuckGo) + YouTube 통합 Agent (멀티소스 RAG)
- GraphRAG: Knowledge Graph 기반 검색 (MS GraphRAG, LangChain+Neo4j, LightRAG)
- **실습**: RAG 품질 튜닝(하이브리드 검색 + 리랭킹), 멀티소스 Agent, GraphRAG 구축

### Day 5 - MAS + MCP + 자연어 Agent 개발 (7시간)

- MAS 아키텍처: SAS 패턴 심화, Agent Card, 통신 구조, 상태 관리
- MAS 아키텍처 패턴: ReAct, Planning & Execution, Multi-Agent Collaboration
- MCP: 프로토콜 아키텍처(Host/Client/Server), JSON-RPC 2.0, 전송 방식
- MCP 핵심 기능: Tools, Resources, Prompts, Sampling
- MCP 보안: OAuth 2.1, JWT, 보안 모범 사례
- 자연어 Agent 개발: Dify Visual Builder, DSL 구조, 프로토타이핑 워크플로우
- **실습**: MCP 서버 구현 + Claude Code 연동, Dify 기반 고객 상담 Agent 프로토타이핑
- 교육 회고 및 실무 적용 가이드, 통합 프로젝트 과제 안내

---

## 6. 평가 방법

| 평가 항목 | 비중 | 방법 |
|-----------|------|------|
| 일별 실습 과제 | 40% | 각 일자별 실습 결과물 제출 |
| 통합 프로젝트 | 40% | 별도 세션에서 프로젝트 완성도 및 발표 평가 |
| 참여도 | 20% | 질의응답, 토론 참여 |

### 통합 프로젝트 안내

- **부여 시점**: Day 5 교육 종료 시
- **제출 기한**: 교육 종료 후 2주 이내
- **발표 세션**: 별도 일정 공지
- **주제**: 5일간 학습 내용(LLM API, RAG, MAS, MCP)을 종합 활용한 AI Agent 시스템 구현
- **평가 기준**: 기술적 완성도(40%), 아키텍처 설계(30%), 발표 및 문서화(30%)

---

## 7. 교재 챕터 매핑

| 교재 챕터 | 교육 일차 | 비고 |
|-----------|-----------|------|
| 01. AI 어플리케이션 개요 | Day 1 | 전체 |
| 02. 멀티턴 | Day 1 | 전체 |
| 03. 문서요약 | Day 2 | 전체 |
| 04. PDF처리 | Day 2 | 전체 |
| 05. STT | Day 2 | 핵심 개념 + 데모 |
| 06. TTS | Day 2 | 핵심 개념 + 데모 |
| 07. VLM | Day 2 | 핵심 개념 + 데모 |
| 08. Function Call | Day 2 | 전체 |
| 09. LangChain | Day 3 | 전체 |
| 10. RAG | Day 3 | 전체 |
| 11. RAG 품질 튜닝 | Day 4 | 전체 |
| 12. 웹검색+YouTube | Day 4 | 전체 |
| 13. Local LLM | Day 4 | 개념 소개만 (실습 제외) |
| 14. MAS | Day 5 | 전체 |
| 15. GraphRAG | Day 4 | 전체 |
| 16. MCP | Day 5 | 전체 |
| 17. 자연어로 Agent 개발 | Day 5 | 전체 |
