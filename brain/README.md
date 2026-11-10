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