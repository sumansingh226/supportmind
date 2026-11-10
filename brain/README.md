# SupportMind

An AI customer support agent that answers questions from your product
documentation using **RAG** and **GraphRAG**, and automatically **creates and
assigns tickets** to developers when it can't resolve an issue.

> **Status:** 🚧 Early development. The backend is being built first;
> the frontend comes later.

## Features (planned)

- 📚 Answers grounded in product docs, with source citations
- 🔎 Hybrid retrieval: vector + keyword search
- 🕸️ GraphRAG for questions that span multiple documents
- 🤖 LangGraph agent that routes, answers, or escalates
- 🎫 Automatic ticket creation and developer assignment
- 💬 Persistent conversation memory
- 📊 Evaluation suite to measure answer quality


## folder structure

brain/
├── src/brain/
│   ├── main.py              # app factory, router wiring, startup/shutdown
│   ├── core/                # config, logging, security, exceptions, constants
│   ├── api/
│   │   ├── deps.py          # shared dependencies (db session, auth, services)
│   │   └── v1/              # versioned routes
│   │       ├── health.py
│   │       ├── chat.py
│   │       ├── tickets.py
│   │       └── ingest.py
│   ├── schemas/             # Pydantic request/response models (API contracts)
│   ├── db/
│   │   ├── session.py       # engine + session
│   │   ├── models/          # SQLAlchemy tables
│   │   └── repositories/    # data-access functions (queries live here)
│   ├── services/            # business logic (chat, ticket, assignment)
│   ├── ai/
│   │   ├── llm/             # model clients, provider wrappers
│   │   ├── prompts/         # prompt templates, versioned as files
│   │   ├── embeddings/      # embedding model + batching
│   │   ├── rag/
│   │   │   ├── loaders/     # PDF, markdown, HTML readers
│   │   │   ├── chunking/    # splitting strategies
│   │   │   ├── retrieval/   # vector, keyword, hybrid, reranking
│   │   │   └── pipeline.py  # ties the RAG steps together
│   │   ├── graphrag/        # entity extraction, graph build, graph retrieval
│   │   ├── agents/          # LangGraph: state, nodes, edges, graph builder
│   │   ├── tools/           # tools the agent can call (create_ticket, search_docs)
│   │   └── guardrails/      # input/output checks, injection defense
│   └── utils/               # small shared helpers
├── tests/
│   ├── unit/
│   ├── integration/
│   └── evals/               # RAG/agent quality tests (question + expected answer)
├── scripts/                 # ingest docs, seed db, run evals
├── migrations/              # Alembic
├── data/                    # sample/raw docs (gitignored if large)
├── docs/
├── pyproject.toml, uv.lock, .env.example, Dockerfile



## Tech Stack

| Layer      | Technology                         |
|------------|------------------------------------|
| Backend    | Python 3.12, FastAPI               |
| AI         | LangChain, LangGraph               |
| Database   | PostgreSQL + pgvector              |
| Frontend   | Next.js *(planned)*                |
| Tooling    | uv, Docker, Alembic, pytest        |

## Project Structure

```
supportmind/
├── brain/        # Backend: API, RAG, agents, database
│   ├── src/brain/
│   ├── tests/
│   └── docs/
├── desk/         # Frontend (Next.js), coming later
├── docker-compose.yml
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.12+
- [uv](https://docs.astral.sh/uv/)
- Docker & Docker Compose

### Setup

```bash
# 1. Clone
git clone <your-repo-url>
cd supportmind

# 2. Configure environment
cp .env.example .env        # then fill in your values

# 3. Start PostgreSQL
docker compose up -d

# 4. Install backend dependencies
cd brain
uv sync

# 5. Run the API
uv run uvicorn brain.main:app --reload
```

API docs are available at <http://localhost:8000/docs>.

## Configuration

All settings are read from environment variables. See `.env.example` for the
full list. Never commit your real `.env` file.

## Development

```bash
uv run pytest              # run tests
uv run ruff check .        # lint
```

## Roadmap

- [ ] Project setup and FastAPI skeleton
- [ ] Database schema and migrations
- [ ] Basic RAG pipeline
- [ ] Evaluation suite
- [ ] GraphRAG
- [ ] LangGraph agent
- [ ] Ticketing and assignment
- [ ] Next.js frontend
- [ ] Auth, guardrails, observability, deployment

## License

TBD