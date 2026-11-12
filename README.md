# SupportMind
An AI customer support agent that answers questions from your product
documentation using **RAG** and **GraphRAG**. When it can't resolve an issue,
it **creates a ticket and assigns it** to a developer.

> **Status:**  Early development. The backend (`brain`) is being built first;
> the frontend (`lens`) comes later.

## Features (planned)

- 📚 Answers grounded in product docs, with source citations
- 🔎 Hybrid retrieval: vector + keyword search, with reranking
- 🕸️ GraphRAG for questions that span multiple documents
- 🤖 LangGraph agent that decides whether to answer or escalate
- 🎫 Automatic ticket creation and developer assignment
- 💬 Persistent conversation memory
- 🛡️ Guardrails: input/output checks and prompt-injection defense
- 📊 Evaluation suite to measure answer quality

## Repository Layout

```
supportmind/
├── brain/          # Backend: FastAPI API, RAG, GraphRAG, agents, database
│   ├── src/brain/
│   ├── pyproject.toml
│   ├── uv.lock
│   └── README.md   # backend details and planned module structure
├── lens/           # Frontend (planned, not started yet)
├── LICENSE
└── README.md
```

See [brain/README.md](brain/README.md) for the full planned backend module
structure.

## Tech Stack

| Layer    | Technology                                   |
|----------|----------------------------------------------|
| Backend  | Python, FastAPI, Uvicorn, Pydantic Settings  |
| AI       | LangChain, LangGraph *(planned)*             |
| Database | PostgreSQL + pgvector *(planned)*            |
| Frontend | Next.js *(planned)*                          |
| Tooling  | uv, Docker, Alembic, pytest *(partly planned)* |

## Getting Started

### Prerequisites

- Python 3.10+ (pinned in `brain/.python-version`)
- [uv](https://docs.astral.sh/uv/)
- Docker & Docker Compose (needed once the database is added)

### Backend setup

```bash
git clone <your-repo-url>
cd supportmind/brain

# Install dependencies into brain/.venv
uv sync

# Run the API (once the FastAPI app is defined in src/brain/main.py)
uv run uvicorn brain.main:app --reload
```

When the server is running, interactive API docs are at
<http://localhost:8000/docs>.

## Configuration

Settings are read from environment variables (via `pydantic-settings` and
`python-dotenv`). Put local values in a `.env` file. It is gitignored, so
never commit it. A `.env.example` listing the required variables will be
added as configuration grows.

## Roadmap

- [ ] Project setup and FastAPI skeleton
- [ ] Database schema and migrations
- [ ] Basic RAG pipeline
- [ ] Evaluation suite
- [ ] GraphRAG
- [ ] LangGraph agent
- [ ] Ticketing and assignment
- [ ] Frontend (`lens`)
- [ ] Auth, guardrails, observability, deployment

