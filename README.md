# 🚀 ByO Target Platform (TVA)

> **Build your Own Target Validation Assistant**  
> 논문은 많지만, 판단에 필요한 구조는 없는 연구 초기 단계를 위해  
> **Multi-Agent 기반 Target Validation 플랫폼**을 제공합니다.
> 🏁 This project was built during a 24-hour hackathon.

---

## ✨ 프로젝트 소개

ByO Target Platform (TVA)은  
🎯 **연구 초기(Target Validation) 단계**에서  
📚 방대한 문헌을 **구조화된 근거와 판단 단위**로 정리해주는  
**AI 기반 의사결정 보조 플랫폼**입니다.

Retriever → Extractor → Synthesizer로 이어지는  
**Multi-Agent 파이프라인**을 통해  
논문 검색, 정보 추출, 종합 리포트 생성을 자동화합니다.

본 프로젝트는 해커톤 환경에서
빠른 의사결정과 확장 가능성을 중심으로 설계되었습니다.

---

## 🧑‍🤝‍🧑 팀 ByO

| 이름 | 역할 | GitHub |
|------|------|--------|
| 강유비 | Frontend / Backend | https://github.com/rocodrama |
| 권태성 | AI | https://github.com/TaeSeongkwon0521 |
| 우서연 | AI | https://github.com/SYWoo02 |
| 이상화 | AI | https://github.com/lsanghwa72 |
| 김지훈 | Backend | https://github.com/Life-00 |

> 각 파트는 역할을 분리하되,  
> **PR 기반 협업**을 통해 코드 품질과 변경 이력을 관리합니다.

---

## 🎯 프로젝트 개요

- **프로젝트 목적**  
  연구 초기 단계에서 타깃(Myostatin 등)에 대한 근거 수준을  
  빠르게 파악하고, “어디까지 검증되었는가”를 구조적으로 제시

- **문제 정의**  
  - 논문은 많지만 판단 기준이 흩어져 있음  
  - 실험 단계(in vitro / in vivo / clinical)가 혼재  
  - 연구자가 직접 정리·비교해야 하는 비용이 큼

- **해결 접근 방식**  
  - 문헌 자동 수집 (PubMed / ArXiv 등)
  - LLM 기반 정보 추출 및 검증
  - Target Dossier 형태의 구조화된 결과 제공

---

## ✨ 주요 기능

- 🔍 **Retriever Agent**
  - 문헌 검색
  - Query expansion 및 semantic ranking

- 🧠 **Extractor Agent**
  - 논문에서 핵심 실험 조건 및 결과 추출
  - 근거 타입(in vitro / in vivo / clinical) 구조화

- 🧩 **Synthesizer Agent**
  - 다수 논문의 결과를 종합
  - Target Dossier 및 요약 리포트 생성

- 💬 **Research / Chat API**
  - 세션 기반 대화형 분석
  - Research / Extract / Report 플로우 지원

- 📊 **Frontend Dashboard**
  - 연구 결과 시각화
  - PDF 업로드 및 분석 결과 확인

---

## 🛠️ 기술 스택

### Frontend
- React
- Vite
- Nginx (Production build)
- Tailwind CSS

### Backend
- Python 3.12
- FastAPI
- SQLAlchemy
- Alembic (DB migration)
- JWT 기반 인증

### AI / ML
- Upstage Solar LLM (`solar-pro2`)
- Upstage Embedding (`solar-embedding-1-large`)
- LangChain
- ChromaDB (Vector DB)
- FAISS / Sentence-Transformers

### Infrastructure
- Docker / Docker Compose
- PostgreSQL 15
- GitHub Actions (CI/CD)

---

## 🧱 아키텍처

```text
[Frontend (React)]
        ↓
[Backend API (FastAPI)]
        ↓
[Multi-Agent Pipeline]
 Retriever → Extractor → Synthesizer
        ↓
[LLM (Upstage Solar)]
[Vector DB (Chroma)]
[PostgreSQL]
```

---

## 📁 레포지토리 구조 (상세)

```bash
ByO-Target-Platform
├── .dockerignore
├── .gitignore
├── .python-version
├── docker-compose.yml
├── env_example
├── CONTRIBUTING.md
├── README.md
├── README_Docker.md
├── .github/
│   └── workflows/
│       └── deploy.yml
├── backend/
│   ├── .python-version
│   ├── Dockerfile
│   ├── README.md
│   ├── main.py
│   ├── pyproject.toml
│   ├── uv.lock
│   ├── alembic.ini
│   ├── requirementst.txt
│   ├── alembic/
│   │   ├── README
│   │   ├── env.py
│   │   ├── script.py.mako
│   │   └── versions/
│   │       └── 0fc328c2ff1b_init_schema.py
│   └── app/
│       ├── __init__.py
│       ├── agents/
│       │   ├── extractor/
│       │   │   ├── agent.py
│       │   │   ├── parser.py
│       │   │   ├── prompts.py
│       │   │   ├── claim_filter.py
│       │   │   ├── claim_type_classifier.py
│       │   │   ├── outcome_claim_builder.py
│       │   │   └── outcome_sentence_selector.py
│       │   ├── retriever/
│       │   │   ├── agent.py
│       │   │   ├── pipeline.py
│       │   │   ├── prompts.py
│       │   │   ├── state.py
│       │   │   ├── types.py
│       │   │   ├── query_expander.py
│       │   │   ├── semantic_ranker.py
│       │   │   ├── paper_filter.py
│       │   │   ├── pubmed_fetcher.py
│       │   │   ├── arxiv_fetcher.py
│       │   │   └── pdf_fetcher.py
│       │   ├── synthesizer/
│       │   │   ├── __init__.py
│       │   │   ├── agent.py
│       │   │   ├── assembler.py
│       │   │   ├── guards.py
│       │   │   ├── prompts.py
│       │   │   ├── renderer.py
│       │   │   ├── renderer_markdown.py
│       │   │   ├── renderer_pdf.py
│       │   │   └── test_dossier_shape.py
│       │   └── tests/
│       │       ├── conftest.py
│       │       ├── test_retriever_integration.py
│       │       └── test_retriever_preview.py
│       ├── api/
│       │   ├── __init__.py
│       │   ├── deps.py
│       │   └── v1/
│       │       ├── __init__.py
│       │       ├── auth.py
│       │       ├── chat.py
│       │       ├── extract.py
│       │       ├── files.py
│       │       ├── report.py
│       │       ├── research.py
│       │       ├── selections.py
│       │       └── sessions.py
│       ├── core/
│       │   ├── __init__.py
│       │   ├── config.py
│       │   ├── database.py
│       │   ├── embeddings.py
│       │   ├── llm.py
│       │   └── tokenizer.py
│       ├── models/
│       │   ├── __init__.py
│       │   ├── base.py
│       │   ├── chat.py
│       │   ├── pipeline.py
│       │   └── user.py
│       ├── schemas/
│       │   ├── __init__.py
│       │   ├── auth.py
│       │   ├── chat.py
│       │   ├── dossier.py
│       │   ├── extract.py
│       │   ├── files.py
│       │   ├── knowledge.py
│       │   ├── messages.py
│       │   ├── query.py
│       │   ├── report.py
│       │   ├── research.py
│       │   ├── retrieval.py
│       │   ├── selections.py
│       │   ├── sessions.py
│       │   ├── users.py
│       │   └── vector_hit.py
│       └── service/
│           ├── __init__.py
│           ├── auth_service.py
│           ├── rag_service.py
│           ├── solar_service.py
│           ├── chromadb/
│           │   ├── __init__.py
│           │   └── ingest_chunk.py
│           └── pubmed/
│               ├── client.py
│               ├── parser.py
│               ├── service.py
│               └── (non-ascii filename).txt
└── frontend/
    ├── .gitignore
    ├── Dockerfile
    ├── README.md
    ├── eslint.config.js
    ├── index.html
    ├── package.json
    ├── package-lock.json
    ├── vite.config.js
    ├── public/
    │   └── TVA.png
    └── src/
        ├── main.jsx
        ├── App.jsx
        ├── App.css
        ├── index.css
        ├── api/
        │   └── index.js
        └── components/
            ├── Auth/
            │   ├── AuthContainer.jsx
            │   └── AuthContainer.css
            └── Dashboard/
                ├── Dashboard.jsx
                ├── Dashboard.css
                ├── PdfAnalyzer.jsx
                └── PdfAnalyzer.css

```


---

## ⚙️ 설치 및 실행
요구사항

- Docker & Docker Compose

- (로컬 실행 시) Python 3.12, Node.js 20+

- 환경 변수 설정
```bash
cp .env.example .env
# .env 파일에 API KEY 등 필수 값 입력
```

- Docker 실행 (권장)
```bash
docker compose up --build
```
- Frontend: http://localhost
- Backend API: http://localhost:8000
- ChromaDB: http://localhost:8001
- PostgreSQL: http://localhost:5432

---

```env
## 🔐 주요 환경 변수
# Upstage
UPSTAGE_API_KEY=
UPSTAGE_MODEL=solar-pro2
UPSTAGE_EMBED_MODEL=solar-embedding-1-large

# JWT
JWT_SECRET_KEY=
ACCESS_TOKEN_EXPIRE_MINUTES=60

# Database
DB_USER=postgres
DB_PASSWORD=password
DB_NAME=tva-db

# Chroma
CHROMA_HOST=localhost
CHROMA_PORT=8000

# Frontend
VITE_API_BASE_URL=http://localhost:8000/api/v1
CORS_ORIGINS=http://localhost:5173,http://localhost:80
```

---

## 📌 협업 규칙(Hackathon)

 - main 브랜치는 PR로 병합

 - 기능 단위 feature 브랜치 사용

 - 리뷰는 가능한 범위 내에서 간단히

 - 데모 안정성을 우선하여 merge 관리
