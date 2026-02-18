# AI Agent 개발 실무 - 세부 커리큘럼

> 작성일: 2026-02-15
> 버전: 1.0 (승인 완료)
> 총 교육 시간: 35시간 (5일 x 7시간)

---

## 범례

- **[이론]**: 강의, 개념 설명, 아키텍처 다이어그램
- **[실습]**: 코드 작성, 실행, 결과 확인
- **[데모]**: 강사가 시연하며 학습자는 관찰 및 질의
- **[토론]**: 학습자 간 의견 교환, Q&A

---

# Day 1. AI 앱 기초 + LLM API + 멀티턴

> 성장 경로: Step 1 — LLM과 대화하기
> 교재 참조: 01장, 02장
> 핵심 목표: AI 어플리케이션의 전체 그림을 이해하고, LLM API를 직접 호출하며, 멀티턴 대화를 구현할 수 있다.

---

## 모듈 1-1. AI 어플리케이션 개요 (2시간)

### 학습 목표
- AI 어플리케이션의 비즈니스 가치와 핵심 구성요소를 설명할 수 있다
- SAS 패턴과 Agent Flow 패턴의 차이를 구분할 수 있다
- 트랜스포머 모델의 동작 원리를 개념적으로 이해할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 20분 | [이론] | **AI 어플리케이션의 필요성**: 혁신, 자동화, 고객만족 3대 가치 |
| 30분 | [이론] | **핵심 구성요소**: SAS 패턴(Scheduler-Agent-Supervisor), 5대 핵심 구성요소(Workflow 관리, LLM 인터페이스, RAG, Tools 연동, State 관리) |
| 20분 | [이론] | **Agent Flow 패턴**: 패턴 A(RAG 체인 - 선형 파이프라인) vs 패턴 B(ReAct Agent - 자율적 루프). LCEL 체인 구성 예시 소개 |
| 20분 | [이론] | **트랜스포머 모델**: 인코더(Embedding, Self-Attention, FFN) / 디코더(Masked Self-Attention, Cross-Attention, FFN) |
| 15분 | [이론] | **아키텍처와 개발 흐름**: 3-Tier 구조, 데이터 흐름 6단계, RAG 시스템 흐름(인덱싱/검색), MSA 환경 통합(Circuit Breaker, Rate Limit, Retry) |
| 15분 | [토론] | Q&A 및 현업 적용 사례 토론 |

### 참고 교재
- 01장: AI 어플리케이션 개요 > 학습 목표 ~ MSA 환경에서의 AI 서비스 통합

---

## 모듈 1-2. LLM API 비교 및 프롬프트 엔지니어링 (1.5시간)

### 학습 목표
- 주요 LLM 제공사(OpenAI, Claude, Gemini, Groq)의 특징과 비용을 비교할 수 있다
- 프롬프트 엔지니어링 핵심 기법을 실제 코드로 적용할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 20분 | [이론] | **LLM 제공사 비교**: OpenAI(GPT-4o), Anthropic(Claude), Google(Gemini), Groq(LPU 기반 초고속) - 특징, Use Case, 토큰 비용 비교표, Groq Rate Limit |
| 20분 | [이론] | **프롬프트 엔지니어링 기초**: 시스템 메시지 vs 유저 메시지, Zero/One/Few-shot, Chain of Thought(CoT), 효과적 프롬프팅 작성 가이드 |
| 30분 | [실습] | **LLM API 첫 호출**: OpenAI API 호출 코드 작성 및 실행. temperature, max_tokens 파라미터 실험. 시스템 메시지 역할 확인 |
| 20분 | [실습] | **프롬프트 기법 비교 실습**: 동일 질문에 대해 Zero-shot / Few-shot / CoT를 적용하여 결과 품질 비교 |

### 참고 교재
- 01장: LLM API 비교 및 선택 가이드 > 주요 LLM 제공사 개요 ~ 프롬프트 엔지니어링 기초

---

## 모듈 1-3. Python 기초 및 개발 환경 설정 (1시간)

### 학습 목표
- AI 개발에 필요한 Python 핵심 문법을 이해할 수 있다
- 가상환경 구성 및 패키지 관리를 수행할 수 있다
- Pydantic BaseModel을 활용한 데이터 검증 코드를 작성할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 10분 | [이론] | **Python 코드 구성 요소**: 패키지, 모듈, 클래스, 함수, 데코레이터, 인스턴스 계층 구조 |
| 15분 | [실습] | **개발 환경 설정**: Python 버전 확인, VS Code 설정, 가상환경(venv) 생성 및 활성화, requirements.txt 작성 |
| 15분 | [이론] | **AI 개발 필수 문법**: import 문, 환경변수 관리(dotenv), 예외 처리(try/except/finally), 타입 힌트 |
| 20분 | [실습] | **Pydantic 실습**: BaseModel, Field를 활용한 데이터 모델 정의. LangChain with_structured_output()으로 LLM 응답 구조화 파싱 실습 |

### 참고 교재
- 01장: Python 기초 > Python 소개 ~ AI 개발에 자주 쓰이는 문법

---

## 모듈 1-4. 멀티턴 대화 (2.5시간)

### 학습 목표
- 멀티턴 대화의 개념과 컨텍스트 유지 원리를 설명할 수 있다
- 클라이언트/서버 측 컨텍스트 관리 방식의 차이를 비교할 수 있다
- Streamlit을 활용한 웹 챗봇을 구현할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 15분 | [이론] | **멀티턴 개요**: 싱글턴 vs 멀티턴 비교, 주요 활용 사례(고객 상담, 여행 플래너, 교육 튜터링) |
| 25분 | [이론] | **클라이언트 측 관리**: 전체 히스토리 전송(OpenAI 코드), 슬라이딩 윈도우+요약(WINDOW_SIZE, SUMMARY_THRESHOLD) |
| 20분 | [이론] | **서버 측 관리**: OpenAI Responses API(previous_response_id), Gemini Chat Session(send_message), Claude API(클라이언트 방식만 지원). 방식별 비교표 |
| 40분 | [실습] | **여행 플래너 멀티턴 구현**: (1) 전체 히스토리 전송 방식(OpenAI), (2) Responses API 방식, (3) Gemini Chat Session 방식 -- 3가지를 순차 구현하며 비교 |
| 30분 | [실습] | **Streamlit 웹 챗봇**: Gemini Chat Session 기반 여행 플래너를 Streamlit으로 웹 UI 구현. st.session_state 활용, st.empty() + placeholder.markdown() 패턴 적용 |
| 20분 | [토론] | Day 1 종합 Q&A, 핵심 개념 정리, 일별 실습 과제 안내 |

### 참고 교재
- 02장: 멀티턴 대화 > 전체

### Day 1 실습 과제
- 멀티턴 여행 플래너에 Claude API 방식을 추가 구현하고, 3사 API 응답 품질 비교 보고서 작성

---

# Day 2. 데이터 처리 + Function Calling

> 성장 경로: Step 2~3 — 데이터 다루기 → 도구 연결하기
> 교재 참조: 03장, 04장, 05장, 06장, 07장, 08장
> 핵심 목표: 다양한 데이터 소스(문서, PDF, 음성, 이미지)를 처리하고, Function Calling으로 LLM에 외부 도구를 연결할 수 있다.

---

## 모듈 2-1. 문서 요약 (1시간)

### 학습 목표
- 텍스트 요약의 개념과 방식(추출적/생성적)을 구분할 수 있다
- LLM 기반 요약과 전문 요약 모델의 차이를 비교할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 15분 | [이론] | **텍스트 요약 개요**: 추출적(Extractive) vs 생성적(Abstractive) 요약, 주요 활용 사례 |
| 15분 | [이론] | **모델 비교**: LLM 기반(EXAONE - LG AI Research) vs 전문 모델(KoBART - SKT AI). 방식별 비교표 |
| 30분 | [실습] | **문서 요약 실습**: EXAONE(Groq LPU 활용)으로 뉴스 기사 요약 구현, 요약 품질 비교 |

### 참고 교재
- 03장: 문서요약 > 전체

---

## 모듈 2-2. PDF 처리 (1시간)

### 학습 목표
- PDF에서 텍스트, 테이블, 이미지를 추출하는 기술을 비교할 수 있다
- AI 기반(Docling)과 규칙 기반(PyMuPDF) 접근 방식의 장단점을 설명할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 10분 | [이론] | **PDF 처리 개요**: PDF 구조 이해, OCR 개념, RAG 파이프라인에서의 역할 |
| 15분 | [이론] | **처리 도구 비교**: Docling(IBM, AI 기반), PyMuPDF(규칙 기반), pdfplumber(테이블 특화). 방식별 비교표 |
| 35분 | [실습] | **PDF 처리 파이프라인**: (1) PyMuPDF로 텍스트/테이블 추출, (2) Docling으로 복잡한 PDF를 Markdown으로 변환, (3) 추출 결과를 LLM에 전달하여 요약 |

### 참고 교재
- 04장: PDF처리 > 전체

---

## 모듈 2-3. 멀티모달 AI 개요: STT, TTS, VLM (1시간)

### 학습 목표
- STT, TTS, VLM 각 기술의 개념과 활용 사례를 설명할 수 있다
- Cloud API vs 로컬 모델 방식의 선택 기준을 이해할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 15분 | [이론] | **STT**: Speech-to-Text 개념, 화자 인식(Speaker Diarization). Whisper API vs WhisperX vs LLM Diarization 비교 |
| 10분 | [데모] | **STT 데모**: OpenAI Whisper API로 음성 파일을 텍스트로 변환하는 과정 시연 |
| 10분 | [이론] | **TTS**: Text-to-Speech 개념, 기술 발전 흐름. OpenAI TTS API vs Bark(로컬) vs VITS(한국어 특화) 비교 |
| 5분 | [데모] | **TTS 데모**: OpenAI TTS API로 텍스트를 음성으로 변환하는 과정 시연 |
| 10분 | [이론] | **VLM**: Vision Language Model 개념, 이미지 캡셔닝, 시각적 질의응답. Gemini Vision vs Qwen2.5-VL 비교 |
| 10분 | [데모] | **VLM 데모**: Gemini Vision으로 이미지 분석 및 설명 생성 시연 |

### 참고 교재
- 05장: STT > 학습 목표, 개요, 모델 정보
- 06장: TTS > 학습 목표, 개요, 모델 정보
- 07장: VLM > 학습 목표, 개요, 모델 정보

---

## 모듈 2-4. Function Calling 기초 (2시간)

### 학습 목표
- Function Calling의 개념과 필요성을 설명할 수 있다
- OpenAI, Claude, Gemini 3사의 Function Calling 워크플로우를 비교할 수 있다
- 도구 정의 및 호출 제어 옵션을 활용할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 15분 | [이론] | **Function Calling 정의 및 필요성**: LLM 단독 사용의 한계(실시간 데이터, 외부 시스템 연동 불가), Function Calling으로 해결. 용어 비교(Function Calling / Tool Use) |
| 25분 | [이론] | **공통 워크플로우 5단계**: 도구 정의 -> 요청 전송 -> 모델 판단 -> 함수 실행 -> 결과 반환. 3사(OpenAI/Claude/Gemini)별 코드 비교, Function Response role 비교 |
| 10분 | [이론] | **호출 제어 옵션(tool_choice)**: auto / required / none / 특정 도구 지정. 3사별 옵션 비교표 |
| 10분 | [이론] | **고급 기능**: 병렬 함수 호출, 순차(구성) 함수 호출, 스트리밍 |
| 60분 | [실습] | **Function Calling 여행 플래너**: (1) OpenAI 방식으로 날씨 조회 + 관광지/맛집 검색 도구 구현, (2) Claude 방식으로 동일 시나리오 구현, (3) Gemini 방식으로 동일 시나리오 구현. 3사 응답 비교 (examples/function-call/) |

### 참고 교재
- 08장: Function Call > 1. 개요 ~ 4. 고급 기능

---

## 모듈 2-5. Function Calling 고급 및 모델별 고유 기능 (2시간)

### 학습 목표
- OpenAI Custom Tools, Claude Server/System Tools, Gemini 자동 함수 호출 등 각 모델 고유 기능을 이해할 수 있다
- 스트리밍을 활용한 실시간 Function Calling을 구현할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 15분 | [이론] | **OpenAI 고유 기능**: Custom Tools(CFG 기반 출력 제약), 추론 모델(o3, o4-mini, GPT-5)의 Function Calling |
| 15분 | [이론] | **Claude 고유 기능**: 서버 도구(웹 검색, 웹 Fetch), 시스템 도구(Bash, 코드 실행, 텍스트 편집기), Tool Runner(자동 컨텍스트 압축) |
| 10분 | [이론] | **Gemini 고유 기능**: 자동 함수 호출(Python SDK), 생각 서명(Thought Signature). Claude Tool Runner와 비교 |
| 40분 | [실습] | **스트리밍 Function Calling**: OpenAI/Claude/Gemini 각각의 스트리밍 방식으로 여행 플래너를 구현하여 실시간 응답 출력 확인 |
| 20분 | [실습] | **Claude 서버 도구 실습**: Claude의 웹 검색 도구를 활용한 실시간 정보 검색 Agent 구현 |
| 20분 | [토론] | Day 2 종합 Q&A, 핵심 개념 정리, 일별 실습 과제 안내 |

### 참고 교재
- 08장: Function Call > 5. 모델별 고유 기능

### Day 2 실습 과제
- PDF 문서를 로드하여 요약한 후, Function Calling을 통해 관련 웹 검색을 자동 수행하는 통합 파이프라인 구현

---

# Day 3. LangChain 프레임워크 + RAG 기초

> 성장 경로: Step 3~4 — 도구 연결하기 → 지식 확장하기
> 교재 참조: 09장, 10장
> 핵심 목표: LangChain 생태계를 이해하고, RAG 파이프라인을 설계 및 구현할 수 있다.

---

## 모듈 3-1. LangChain 프레임워크 개요 (1.5시간)

### 학습 목표
- LangChain의 필요성과 핵심 가치를 설명할 수 있다
- LangChain 생태계(LangChain Core, LangGraph, LangSmith)의 역할을 구분할 수 있다
- 대안 프레임워크와의 차이를 비교할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 15분 | [이론] | **왜 LangChain인가**: LLM API 직접 호출의 한계(모델 종속, 반복 코드, 상태 관리 부재), LangChain이 해결하는 4가지 핵심 가치 |
| 15분 | [이론] | **LangChain vs 대안**: LangChain vs LlamaIndex, 개발 프레임워크 비교(CrewAI, AutoGen, Semantic Kernel), 노코드/로우코드(Dify, Flowise, n8n). 의사결정 프레임워크 |
| 20분 | [이론] | **생태계 전체 그림**: 구성요소 개요, 패키지 구조(langchain-core, langchain-openai, langchain-anthropic 등), 핵심 개념 5가지 요약 |
| 20분 | [이론] | **LangGraph 워크플로우 관리**: 왜 LangGraph인가, 핵심 개념(State, Node, Edge, Conditional Edge), Human-in-the-loop 패턴 |
| 20분 | [실습] | **LangGraph 첫 워크플로우**: 간단한 상태 기반 그래프를 구성하고, 조건부 분기와 Human-in-the-loop 패턴 구현 |

### 참고 교재
- 09장: LangChain > WHY, HOW 섹션 4~5

---

## 모듈 3-2. LangChain 핵심 개념: LLM 인터페이스 + LCEL (1.5시간)

### 학습 목표
- Chat Models, Prompts, Output Parsers를 활용한 LLM 인터페이스를 구성할 수 있다
- LCEL(LangChain Expression Language)로 체인을 합성할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 15분 | [이론] | **Chat Models**: 다양한 모델 연동(ChatOpenAI, ChatAnthropic, ChatGoogleGenerativeAI) |
| 15분 | [이론] | **Prompts**: PromptTemplate, ChatPromptTemplate, FewShotPromptTemplate, PipelinePromptTemplate, load_prompt, partial_variables |
| 15분 | [이론] | **Output Parsers**: StrOutputParser, SimpleJsonOutputParser, PydanticOutputParser, CommaSeparatedListOutputParser. Structured Output(with_structured_output) |
| 15분 | [이론] | **LCEL**: 파이프 연산자(`\|`), Runnable 인터페이스(invoke, stream, batch, ainvoke), 체인 합성 패턴(RunnablePassthrough, RunnableParallel, RunnableLambda) |
| 30분 | [실습] | **LCEL 체인 구성**: (1) 프롬프트 -> LLM -> 파서 기본 체인, (2) RunnableParallel로 병렬 처리, (3) PydanticOutputParser로 구조화된 출력 생성 |

### 참고 교재
- 09장: LangChain > HOW 섹션 6 (LLM 인터페이스)

---

## 모듈 3-3. LangChain 핵심 개념: Agents, Tools, State 관리 (1시간)

### 학습 목표
- LangChain Agent의 동작 원리를 이해하고 create_agent API를 활용할 수 있다
- 커스텀 도구를 정의하고 Middleware를 적용할 수 있다
- LangGraph Checkpointer를 활용한 State 관리를 구현할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 10분 | [이론] | **Agent란**: ReAct 루프, create_agent API |
| 10분 | [이론] | **Tools 정의**: 기본 도구 사용, @tool 데코레이터로 커스텀 도구 만들기 |
| 10분 | [이론] | **Middleware 시스템**: HumanInTheLoopMiddleware, SummarizationMiddleware, PIIMiddleware |
| 10분 | [이론] | **State 관리**: 두 가지 역할(대화 이력 / 워크플로우 상태), LangGraph Checkpointer(메모리/영속), 레거시 메모리 참고 |
| 20분 | [실습] | **Agent + 커스텀 도구**: Function Calling 여행 플래너를 LangChain Agent로 마이그레이션, 커스텀 도구 정의 및 Checkpointer 연동 |

### 참고 교재
- 09장: LangChain > HOW 섹션 8~9

---

## 모듈 3-4. RAG 기초 (3시간)

### 학습 목표
- RAG의 개념과 필요성을 설명할 수 있다
- 인덱싱 파이프라인(Load-Split-Embed-Store)을 구현할 수 있다
- 검색 메커니즘과 아키텍처 패턴의 차이를 비교할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 10분 | [이론] | **왜 RAG가 필요한가**: LLM의 현실적 한계(할루시네이션, 지식 단절, 도메인 특화 어려움), RAG가 제공하는 가치 |
| 10분 | [이론] | **RAG 패러다임 분류**: Naive RAG, Advanced RAG, Modular RAG |
| 30분 | [이론] | **인덱싱 파이프라인**: (1) 문서 로드(Document Loaders), (2) 텍스트 분할(RecursiveCharacterTextSplitter, chunk_size 결정 가이드), (3) 임베딩(의미를 수치화), (4) 벡터 DB 저장(Vector Stores) |
| 15분 | [이론] | **검색 메커니즘**: Sparse Retrieval(BM25) vs Dense Retrieval(벡터 검색) vs Hybrid Search. GraphRAG 소개(Day 4에서 심화) |
| 15분 | [이론] | **Post-Retrieval**: Re-ranking, Compression, Filtering, Fusion 개요 |
| 20분 | [이론] | **아키텍처 패턴**: Basic RAG, Self-RAG(자기 성찰), CRAG(교정), Adaptive RAG, Agentic RAG -- 각 패턴의 핵심 메커니즘과 적합한 사용 사례 비교 |
| 10분 | [이론] | **RAGAS 평가 지표**: Faithfulness, Answer Relevancy, Context Precision, Context Recall 소개 |
| 50분 | [실습] | **기본 RAG 시스템 구현**: (1) 문서 로드(WebBaseLoader), (2) RecursiveCharacterTextSplitter로 분할, (3) OpenAI 임베딩으로 벡터화, (4) Chroma 벡터 DB에 저장, (5) LCEL로 RAG 체인 구성, (6) Query Transformation(Multi-Query) 적용 |
| 20분 | [토론] | Day 3 종합 Q&A, 핵심 개념 정리, 일별 실습 과제 안내 |

### 참고 교재
- 10장: RAG > 전체 (1~8절)

### Day 3 실습 과제
- 자체 보유 문서(사내 위키, 기술 문서 등)를 소스로 RAG 시스템을 구축하고, 5개 이상의 테스트 쿼리에 대한 응답 품질 평가

---

# Day 4. RAG 고급 + 웹검색/YouTube + GraphRAG

> 성장 경로: Step 4 — 지식 확장하기
> 교재 참조: 11장, 12장, 13장(개념만), 15장
> 핵심 목표: RAG 품질을 체계적으로 튜닝하고, 다양한 소스(웹, YouTube, Knowledge Graph)를 활용한 고급 검색 시스템을 설계할 수 있다.

---

## 모듈 4-1. RAG 품질 튜닝 (2.5시간)

### 학습 목표
- 청킹 전략, 임베딩 최적화, 하이브리드 검색, 리랭킹 기법을 적용할 수 있다
- RAGAS 프레임워크로 RAG 시스템을 평가할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 20분 | [이론] | **청킹 전략**: 고정 크기 분할, 재귀적 문자 분할, 시맨틱 청킹(SemanticChunker), 문서 구조 기반 분할. 청크 크기 권장사항, 오버랩 전략 |
| 15분 | [이론] | **임베딩 최적화**: 주요 임베딩 모델 비교(text-embedding-3-small/large, BGE, Cohere embed), 도메인별 선택 가이드, 파인튜닝 개요 |
| 20분 | [이론] | **하이브리드 검색**: Dense(벡터) + Sparse(BM25) 결합, 결과 융합(가중 조합, RRF), HNSW 인덱스 튜닝 |
| 20분 | [이론] | **리랭킹**: Cross-Encoder, Cohere Rerank, ColBERT(Late Interaction), LLM 기반 Re-ranking. Retrieve More, Rerank Better 전략 |
| 15분 | [이론] | **쿼리 최적화**: HyDE(가상 문서 임베딩), Multi-Query Retrieval, Query Expansion, Query Rewriting |
| 15분 | [이론] | **평가 및 메트릭**: RAGAS 프레임워크(Faithfulness, Answer Relevancy, Context Precision/Recall), 검색 메트릭(MRR, NDCG, Recall@K), LLM 기반 검색 품질 평가, 테스트 쿼리 설계 원칙 |
| 45분 | [실습] | **RAG 품질 튜닝 실습**: Day 3 RAG 시스템을 기반으로 (1) 시맨틱 청킹 적용, (2) 하이브리드 검색(Dense+BM25) 구현, (3) Cross-Encoder 리랭킹 추가, (4) RAGAS로 전후 품질 비교 평가 |

### 참고 교재
- 11장: RAG 품질 튜닝 가이드 > 전체 (1~10절)

---

## 모듈 4-2. Local LLM 개념 소개 (30분)

### 학습 목표
- Local LLM의 필요성과 주요 런타임을 이해할 수 있다
- 양자화 기법과 모델 선택 기준을 설명할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 10분 | [이론] | **왜 Local LLM인가**: 클라우드 API의 한계(비용, 보안, 지연), Local LLM이 제공하는 가치(프라이버시, 비용 절감, 오프라인) |
| 10분 | [이론] | **런타임 비교**: Ollama, LlamaCpp, HuggingFace Transformers, LocalAI. 선택 가이드 |
| 10분 | [이론] | **모델 포맷과 양자화**: GGUF 포맷, 양자화 레벨(Q4_K_M, Q5_K_M, Q8_0), 하드웨어 요구사항. 범용 모델(Gemma 3, Qwen 3, Llama 3, Phi-4), 한국어 특화 모델 소개 |

> 참고: GPU 환경 제약으로 실습은 생략하며, 클라우드 API(Groq의 오픈소스 모델 호스팅)로 유사한 경험을 Day 1~Day 3에서 이미 수행

### 참고 교재
- 13장: Local LLM > 1~3절 (WHY, HOW, WHAT)

---

## 모듈 4-3. 웹검색 + YouTube 통합 Agent (2시간)

### 학습 목표
- LangChain 웹검색/YouTube 도구의 종류와 특성을 비교할 수 있다
- 멀티소스 RAG 패턴으로 웹과 동영상을 통합 검색하는 Agent를 구현할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 10분 | [이론] | **웹검색 도구 개요**: Tool vs Retriever 차이, 멀티소스 RAG 아키텍처 |
| 15분 | [이론] | **프로바이더 비교**: Tavily(AI 최적화), DuckDuckGo(무료), Google Serper, SerpAPI. 선택 가이드 |
| 10분 | [이론] | **YouTube 도구**: YouTubeSearchTool, YouTube Data API v3, YoutubeLoader(자막 추출). YouTube -> Document 파이프라인 |
| 15분 | [이론] | **보조 유틸리티**: WebBaseLoader, BeautifulSoup, Trafilatura |
| 10분 | [이론] | **안정적 운영**: 캐싱, Resilience 패턴(Retry, Fallback, Rate Limiting, Circuit Breaker) |
| 30분 | [실습] | **웹검색 Agent**: (1) DuckDuckGo 기반 무료 웹검색 Agent, (2) YouTube 검색 + 자막 추출 파이프라인 구현 |
| 30분 | [실습] | **멀티소스 Agent**: 웹 + YouTube를 통합하는 LangGraph 기반 멀티소스 Agent 구축. 질문에 따라 적절한 소스를 자동 선택하도록 라우팅 |

### 참고 교재
- 12장: 웹검색+YouTube > 전체

---

## 모듈 4-4. GraphRAG (2시간)

### 학습 목표
- GraphRAG의 개념과 기존 Vector RAG 대비 장점을 설명할 수 있다
- Knowledge Graph 구축 프레임워크를 비교하고, 기본 GraphRAG 시스템을 구현할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 10분 | [이론] | **왜 GraphRAG인가**: 기존 RAG의 한계(문맥 단절, 멀티홉 추론 실패), Vector RAG vs GraphRAG 비교 |
| 15분 | [이론] | **핵심 아키텍처**: 인덱싱 단계(엔터티 추출 -> 관계 추출 -> 그래프 구축 -> 커뮤니티 탐지), 검색 단계(Local/Global/Hybrid Search) |
| 15분 | [이론] | **프레임워크 비교**: MS GraphRAG(인덱싱 프로세스, Local/Global/DRIFT Search), LangChain+Neo4j(LLMGraphTransformer, Vector/Graph QA/Hybrid/Cypher), LightRAG(경량, 증분 업데이트). 선택 가이드 |
| 10분 | [이론] | **GraphRAG와 Vector RAG의 관계**: 상호 보완적 활용 전략, 프로덕션 고려사항 |
| 40분 | [실습] | **LightRAG 구축**: (1) 문서 로드 및 인덱싱(엔터티/관계 자동 추출), (2) Local/Global/Hybrid 검색 모드 비교, (3) Vector RAG 대비 응답 품질 비교 |
| 10분 | [데모] | **LangChain+Neo4j 데모**: Neo4j 그래프 DB에 Knowledge Graph를 구축하고, Cypher 쿼리로 관계 탐색하는 과정 시연 |
| 20분 | [토론] | Day 4 종합 Q&A, 핵심 개념 정리, 일별 실습 과제 안내 |

### 참고 교재
- 15장: GraphRAG > 전체

### Day 4 실습 과제
- Day 3 과제의 RAG 시스템에 하이브리드 검색 + 리랭킹을 적용하고, 적용 전후 RAGAS 평가 점수 비교 보고서 작성

---

# Day 5. MAS + MCP + 자연어 Agent 개발

> 성장 경로: Step 5 — 에이전트 만들기
> 교재 참조: 14장, 16장, 17장
> 핵심 목표: 멀티에이전트 시스템의 아키텍처를 이해하고, MCP로 표준화된 도구 연동을 구현하며, 자연어 기반 Agent 개발 워크플로우를 체험한다.

---

## 모듈 5-1. 멀티에이전트 시스템(MAS) (2시간)

### 학습 목표
- 멀티에이전트 시스템의 아키텍처 패턴과 통신 구조를 설명할 수 있다
- Agent Card를 설계하고, 상태 관리 전략을 비교할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 10분 | [이론] | **멀티에이전트 개요**: 정의, Agent 정의, 필요성(LLM 단독 사용의 한계 → 멀티에이전트로 해결), 실제 활용 사례. 단일 에이전트 vs 멀티에이전트 비교 |
| 15분 | [이론] | **SAS 패턴 심화**: Scheduler-Agent-Supervisor 상세. Supervisor 책임(라우팅, 품질 검증, 에러 처리), 구현 유형(LLM 기반/규칙 기반/하이브리드) |
| 10분 | [이론] | **A2A 소개 및 Agent Card**: A2A(Agent-to-Agent) 프로토콜 개요, Agent Card의 역할(능력 선언, 라우팅 기준), Agent Card 예시(역할, 입력/출력, 도구, 제약조건) |
| 10분 | [이론] | **통신 구조**: 통신 레이어(Agent간 / Agent-Tool / Agent-Human), 프로토콜 선택, 동기/비동기 통신 |
| 10분 | [이론] | **아키텍처 패턴**: ReAct, Planning & Execution, Multi-Agent Collaboration |
| 10분 | [이론] | **상태 관리**: 상태의 종류(Agent/Session/Global), 기법(Checkpointing, Shared State, Persistence), LangGraph 매핑 |
| 10분 | [이론] | **운영 안정성 + MCP 연결**: Loop 종료 조건, Budget, HITL. MAS에서 Function Calling의 역할, MCP가 필요한 이유 (다음 모듈 연결) |
| 5분 | [실습안내] | **MAS 챗봇 요구사항 안내**: 교재 14장 11절의 요청 프롬프트 및 아키텍처 설명 (examples/mas/ 참고) |
| 40분 | [실습] | **Claude Code 기반 MAS 챗봇 개발**: Claude Code에 프롬프트를 입력하여 SAS 패턴 기반 LangGraph MAS 챗봇 생성 → 생성된 코드의 라우터/에이전트 구조 분석 → 실행 및 결과 검증 |

### 참고 교재
- 14장: MAS > 전체 (1~6절)

---

## 모듈 5-2. MCP (Model Context Protocol) (2.5시간)

### 학습 목표
- MCP의 아키텍처와 핵심 기능(Tools, Resources, Prompts)을 설명할 수 있다
- MCP 서버를 구현하고 Claude Code/Desktop에 연동할 수 있다
- MCP 보안 모범 사례를 이해할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 10분 | [이론] | **왜 MCP인가**: 앱-도구 간 인터페이스 표준화, 프레임워크 비종속, 풍부한 생태계. Function Calling과의 관계(FC는 "무엇을 호출", MCP는 "어떻게 연결") |
| 20분 | [이론] | **아키텍처 개요**: Host(Claude Desktop/Code), Client(프로토콜 관리), Server(도구 제공). 통신 프로토콜(JSON-RPC 2.0), 전송 방식(stdio/Streamable HTTP), 연결 수명주기 |
| 20분 | [이론] | **핵심 기능(Primitives)**: Tools(모델이 호출하는 함수), Resources(앱이 읽는 데이터), Prompts(사용자가 선택하는 템플릿). 사용 패턴 비교, 클라이언트 API 비교 |
| 15분 | [이론] | **고급 기능**: Sampling & Elicitation(서버의 역방향 요청), Roots(파일 시스템 경계 설정) |
| 10분 | [이론] | **보안**: OAuth 2.1 인증/인가, JWT 인증, 보안 모범 사례 |
| 10분 | [이론] | **생태계 현황**: MCP 클라이언트 지원 현황, MCP 서버 생태계, 거버넌스 |
| 15분 | [이론] | **개발 환경 설정**: Python MCP SDK 설치(uv 권장, pip 대안) |
| 40분 | [실습] | **MCP 서버 구현 + 연동**: (1) Python MCP SDK로 간단한 MCP 서버 개발(날씨 조회, 데이터베이스 검색 도구), (2) Claude Code에 MCP 서버 등록 및 테스트, (3) Claude Desktop 연동 설정 |
| 10분 | [데모] | **Sampling 실습**: MCP 서버에서 역방향으로 LLM을 호출하는 Sampling 기능 시연 |

### 참고 교재
- 16장: MCP > 전체

---

## 모듈 5-3. 자연어로 Agent 개발 (2시간)

### 학습 목표
- 자연어 입력으로 AI Agent 워크플로우를 설계하는 방법을 이해할 수 있다
- Dify Visual Builder의 DSL 구조와 프로토타이핑 워크플로우를 활용할 수 있다
- 비즈니스 시나리오에서 프로토타입까지의 점진적 개발 프로세스를 체험할 수 있다

### 세부 내용

| 시간 | 구분 | 내용 |
|------|------|------|
| 10분 | [이론] | **왜 자연어 기반 Agent 개발인가**: 기존 개발 방식의 한계, 자연어 -> 프로토타입 -> 프로덕션 패러다임 |
| 10분 | [이론] | **왜 Dify인가**: Dify의 핵심 가치, Visual Builder의 특징 |
| 15분 | [이론] | **전체 워크플로우 5단계**: STEP 1(비즈니스 시나리오 정의) -> STEP 2(Dify DSL 자동 생성) -> STEP 3(시각적 프로토타이핑) -> STEP 4(개발 계획서) -> STEP 5(개발 및 배포) |
| 10분 | [이론] | **Dify DSL 구조**: 노드 유형(Start, LLM, Agent, Knowledge Retrieval, HTTP Request 등), 주요 노드 상세, Knowledge Base와 RAG 연동 |
| 10분 | [이론] | **배포 옵션**: Dify 런타임 활용(API/웹 임베드) vs 코드 기반 전환(LangChain/LangGraph). 선택 기준 |
| 45분 | [실습] | **Dify 기반 고객 상담 Agent 프로토타이핑**: (1) STEP 1: 고객 상담 시나리오 작성, (2) STEP 2: Claude Code로 DSL 자동 생성, (3) STEP 3: Dify에 DSL 임포트 후 시각적 편집, (4) 테스트 실행 및 결과 검증 |
| 20분 | [토론] | **교육 종합 회고**: 5일간 학습 내용 정리(Step 1~5 성장 경로 회고), 실무 적용 가이드(프로젝트별 기술 선택 의사결정 트리), 통합 프로젝트 과제 안내, Q&A |

### 참고 교재
- 17장: 자연어로 Agent 개발 > 전체

### Day 5 실습 과제
- Dify에서 프로토타이핑한 고객 상담 Agent를 LangChain/LangGraph 코드로 전환하는 개발 계획서 작성

---

# 통합 프로젝트 (별도 세션)

## 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **부여 시점** | Day 5 교육 종료 시 |
| **제출 기한** | 교육 종료 후 2주 이내 |
| **발표 세션** | 별도 일정 공지 (온라인/오프라인) |
| **팀 구성** | 개인 또는 2~3인 팀 |

## 프로젝트 주제

5일간 학습한 기술을 종합 활용하여 **실무에 적용 가능한 AI Agent 시스템**을 구현합니다.

### 필수 포함 기술 (최소 3개 이상)

| 기술 영역 | 해당 학습 일차 | 예시 |
|-----------|---------------|------|
| LLM API 활용 | Day 1 | 멀티턴 대화, 프롬프트 엔지니어링 |
| 데이터 처리 | Day 2 | 문서 요약, PDF 처리, Function Calling |
| RAG 시스템 | Day 3~4 | 벡터 검색, 하이브리드 검색, 리랭킹 |
| Agent 도구 연동 | Day 4~5 | 웹검색 Agent, MCP 서버 |
| MAS 아키텍처 | Day 5 | 멀티에이전트 협업, Agent Card 설계 |

### 제출물

1. **소스 코드**: GitHub 리포지토리 또는 ZIP 파일
2. **아키텍처 문서**: 시스템 구성도, 기술 선택 근거
3. **데모 영상 또는 실행 가이드**: 5분 이내 시연 영상 또는 README
4. **발표 자료**: 10분 발표용 슬라이드

### 평가 기준

| 평가 항목 | 비중 | 세부 기준 |
|-----------|------|-----------|
| 기술적 완성도 | 40% | 필수 기술 3개 이상 통합, 정상 동작, 에러 처리 |
| 아키텍처 설계 | 30% | 적절한 기술 선택, 확장 가능한 구조, 문서화 품질 |
| 발표 및 시연 | 30% | 명확한 설명, 실제 동작 시연, 질의응답 대응 |

---

# 부록: 시간 배분 요약표

## Day 1 (7시간)

| 모듈 | 주제 | 이론 | 실습 | 토론 | 합계 |
|------|------|------|------|------|------|
| 1-1 | AI 앱 개요 | 105분 | - | 15분 | 2시간 |
| 1-2 | LLM API + 프롬프트 | 40분 | 50분 | - | 1.5시간 |
| 1-3 | Python 기초 | 25분 | 35분 | - | 1시간 |
| 1-4 | 멀티턴 대화 | 60분 | 70분 | 20분 | 2.5시간 |
| **합계** | | **230분** | **155분** | **35분** | **7시간** |

## Day 2 (7시간)

| 모듈 | 주제 | 이론 | 실습/데모 | 토론 | 합계 |
|------|------|------|-----------|------|------|
| 2-1 | 문서 요약 | 30분 | 30분 | - | 1시간 |
| 2-2 | PDF 처리 | 25분 | 35분 | - | 1시간 |
| 2-3 | 멀티모달(STT/TTS/VLM) | 35분 | 25분(데모) | - | 1시간 |
| 2-4 | Function Calling 기초 | 60분 | 60분 | - | 2시간 |
| 2-5 | Function Calling 고급 | 40분 | 60분 | 20분 | 2시간 |
| **합계** | | **190분** | **210분** | **20분** | **7시간** |

## Day 3 (7시간)

| 모듈 | 주제 | 이론 | 실습 | 토론 | 합계 |
|------|------|------|------|------|------|
| 3-1 | LangChain 개요 | 70분 | 20분 | - | 1.5시간 |
| 3-2 | LLM 인터페이스 + LCEL | 60분 | 30분 | - | 1.5시간 |
| 3-3 | Agents, Tools, State | 40분 | 20분 | - | 1시간 |
| 3-4 | RAG 기초 | 100분 | 50분 | 20분 | ~3시간 |
| **합계** | | **270분** | **120분** | **20분** | **~7시간** |

## Day 4 (7시간)

| 모듈 | 주제 | 이론 | 실습/데모 | 토론 | 합계 |
|------|------|------|-----------|------|------|
| 4-1 | RAG 품질 튜닝 | 105분 | 45분 | - | 2.5시간 |
| 4-2 | Local LLM 개념 | 30분 | - | - | 30분 |
| 4-3 | 웹검색 + YouTube | 60분 | 60분 | - | 2시간 |
| 4-4 | GraphRAG | 60분 | 40분+10분(데모) | 20분 | 2시간+a |
| **합계** | | **255분** | **155분** | **20분** | **~7시간** |

## Day 5 (7시간)

| 모듈 | 주제 | 이론 | 실습/데모 | 토론 | 합계 |
|------|------|------|-----------|------|------|
| 5-1 | MAS | 100분 | 20분 | - | 2시간 |
| 5-2 | MCP | 100분 | 40분+10분(데모) | - | 2.5시간 |
| 5-3 | 자연어 Agent 개발 | 55분 | 45분 | 20분 | 2시간 |
| **합계** | | **255분** | **115분** | **20분** | **~7시간** |

## 전체 요약

| 구분 | Day 1 | Day 2 | Day 3 | Day 4 | Day 5 | 전체 |
|------|-------|-------|-------|-------|-------|------|
| 이론 | 230분 | 190분 | 270분 | 255분 | 255분 | 1,200분 |
| 실습/데모 | 155분 | 210분 | 120분 | 155분 | 115분 | 755분 |
| 토론 | 35분 | 20분 | 20분 | 20분 | 20분 | 115분 |
| **이론 비중** | 55% | 45% | 66% | 61% | 65% | **58%** |
| **실습 비중** | 37% | 50% | 29% | 37% | 30% | **36%** |
| **토론 비중** | 8% | 5% | 5% | 5% | 5% | **6%** |

> 참고: 실습 비중은 Day 2(데이터 처리 + Function Calling)가 가장 높고, Day 3(LangChain + RAG 기초)은 새로운 프레임워크 개념 학습이 많아 이론 비중이 높습니다. Day 4~5는 고급 주제의 개념 이해가 중요하여 이론과 실습이 균형을 이룹니다.
