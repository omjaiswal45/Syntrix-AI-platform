<h1 align="center">⚡ NexusAI — Full Stack Agentic AI Platform</h1>

<p align="center">
  <i>A production-ready full stack platform with AI agents, RAG pipeline, real-time streaming, and enterprise-grade infrastructure — built from scratch.</i>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white" alt="FastAPI">
  <img src="https://img.shields.io/badge/Next.js_15-000000?logo=next.js&logoColor=white" alt="Next.js">
  <img src="https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white" alt="TypeScript">
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white" alt="MongoDB">
  <img src="https://img.shields.io/badge/Redis-DC382D?logo=redis&logoColor=white" alt="Redis">
  <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/LangGraph-005A9C?logoColor=white" alt="LangGraph">
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="MIT License">
</p>

---

## 👋 About This Project

I built **NexusAI** because I wanted a single platform that combines everything I've been learning — full stack development with TypeScript and Python, agentic AI with LangGraph, real-time WebSocket communication, RAG pipelines, and production DevOps with Docker and Kubernetes.

Most AI projects I found online were either just a Python script calling an API, or a simple chatbot with no real backend. I wanted to build something that feels like a real production system — with proper authentication, background workers, observability, and a clean architecture.

This is that project.

---

## 🧠 What It Does

NexusAI is a full stack AI agent platform where users can:

- **Chat with AI agents** that can use tools (web search, database queries, file reading)
- **Upload documents** and query them using RAG (Retrieval-Augmented Generation)
- **Stream responses in real time** via WebSocket — no waiting for the full response
- **Manage conversations** with full history persistence
- **Monitor everything** — agent runs, API latency, token usage, errors

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────┐
│              Frontend (Next.js 15)               │
│   React 19 · TypeScript · Tailwind · Zustand    │
└───────────────────┬─────────────────────────────┘
                    │  REST + WebSocket
                    ▼
┌─────────────────────────────────────────────────┐
│               Backend (FastAPI)                  │
│                                                 │
│  ┌──────────────────────────────────────────┐   │
│  │           AI Agents (LangGraph)          │   │
│  │  Planner → Tool Use → Critic → Response  │   │
│  │  Tools: search · code · database · files │   │
│  └──────────────────────────────────────────┘   │
│                                                 │
│  ┌──────────────────────────────────────────┐   │
│  │            RAG Pipeline                  │   │
│  │  Ingest → Chunk → Embed → Store → Search │   │
│  └──────────────────────────────────────────┘   │
│                                                 │
│  Auth · Rate Limiting · Webhooks · Admin Panel  │
│  Celery Workers · Prometheus · Sentry           │
└────────┬──────────┬──────────┬──────────────────┘
         │          │          │
         ▼          ▼          ▼
    PostgreSQL    Redis    Vector DB
    MongoDB               (Qdrant/Chroma)
```

---

## 🛠️ Tech Stack

### Frontend
| Technology | Purpose |
|-----------|---------|
| Next.js 15 + React 19 | UI framework with App Router |
| TypeScript | Type safety across the entire frontend |
| Tailwind CSS v4 | Styling |
| Zustand | State management |
| WebSocket client | Real-time streaming |

### Backend
| Technology | Purpose |
|-----------|---------|
| Python 3.11 + FastAPI | High-performance async API |
| LangGraph + LangChain | Multi-agent orchestration |
| Pydantic v2 | Data validation |
| SQLAlchemy (async) | ORM for PostgreSQL |
| Celery + Redis | Background task queue |
| JWT + OAuth2 | Authentication |

### Databases & Infrastructure
| Technology | Purpose |
|-----------|---------|
| PostgreSQL | Primary relational database |
| MongoDB | Document storage |
| Redis | Caching, sessions, task queue |
| Qdrant / ChromaDB | Vector database for RAG |
| Docker + Kubernetes | Containerization and orchestration |
| GitHub Actions | CI/CD pipeline |
| Prometheus + Sentry | Monitoring and error tracking |

---

## ✨ Key Features

### 🤖 Multi-Agent AI System
Built with LangGraph — agents follow a **Planner → Tool Use → Critic → Synthesizer** pipeline. Each agent can call tools autonomously, maintain memory across sessions, and stream tokens back to the frontend in real time.

### 📄 RAG Pipeline
Upload PDFs, DOCX, or plain text files. The system parses, chunks, embeds, and stores them in a vector database. Agents automatically search the knowledge base when answering questions.

### ⚡ Real-time Streaming
WebSocket-based streaming means users see tokens as they're generated — not a loading spinner for 10 seconds. Includes tool call visualization so users can see what the agent is doing.

### 🔒 Production Auth
JWT access tokens + refresh tokens, API key support, and Google OAuth2. HTTP-only cookies on the frontend. Role-based access control.

### 📊 Observability
Full tracing via Logfire (for PydanticAI) and LangSmith (for LangChain). Prometheus metrics endpoint. Sentry for error tracking. Every agent run, tool call, and LLM request is traced.

### 🖥️ Admin Panel
SQLAdmin panel with authentication — manage users, view database records, monitor background tasks via Celery Flower.

---

## 🚀 Getting Started

### Prerequisites
- Python 3.11+
- Node.js 18+ (or Bun)
- Docker + Docker Compose
- An OpenAI or Anthropic API key

### 1. Clone the repo
```bash
git clone https://github.com/arpitkasaudhan/ai-fullstack-platform.git
cd ai-fullstack-platform
```

### 2. Set up environment variables
```bash
cp .env.example .env
# Edit .env and add your API keys
```

### 3. Start with Docker (easiest)
```bash
docker-compose up -d
```

### 4. Or run locally

**Backend:**
```bash
cd backend
pip install -r requirements.txt
uvicorn app.main:app --reload
```

**Frontend:**
```bash
cd frontend
bun install
bun dev
```

### 5. Access the app
| Service | URL |
|---------|-----|
| Frontend | http://localhost:3000 |
| API | http://localhost:8000 |
| API Docs | http://localhost:8000/docs |
| Admin Panel | http://localhost:8000/admin |

---

## 📁 Project Structure

```
ai-fullstack-platform/
├── backend/
│   ├── app/
│   │   ├── main.py              # FastAPI app entry point
│   │   ├── api/
│   │   │   └── routes/v1/       # API endpoints (auth, chat, rag, users)
│   │   ├── core/                # Config, security, middleware
│   │   ├── db/                  # Database models (SQLAlchemy + MongoDB)
│   │   ├── schemas/             # Pydantic request/response schemas
│   │   ├── repositories/        # Data access layer
│   │   ├── services/            # Business logic
│   │   ├── agents/              # LangGraph AI agents
│   │   ├── rag/                 # RAG pipeline (ingest, embed, search)
│   │   └── worker/              # Celery background tasks
│   ├── tests/                   # pytest test suite
│   └── alembic/                 # DB migrations
├── frontend/
│   ├── src/
│   │   ├── app/                 # Next.js App Router pages
│   │   ├── components/          # React components
│   │   ├── hooks/               # useChat, useWebSocket, useAuth
│   │   └── stores/              # Zustand state stores
│   └── e2e/                     # Playwright end-to-end tests
├── docker-compose.yml
├── Makefile
└── README.md
```

---

## 🔌 API Overview

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/auth/login` | Login and get JWT tokens |
| POST | `/api/v1/auth/refresh` | Refresh access token |
| GET | `/api/v1/chat/conversations` | List user conversations |
| POST | `/api/v1/chat/message` | Send message to AI agent |
| WS | `/api/v1/chat/ws` | WebSocket for streaming |
| POST | `/api/v1/rag/upload` | Upload document to knowledge base |
| GET | `/api/v1/rag/search` | Search knowledge base |
| GET | `/api/v1/users/me` | Get current user profile |

Full interactive docs available at `/docs` (Swagger) and `/redoc`.

---

## 🧪 Running Tests

```bash
# Backend tests
cd backend
pytest tests/ -v

# Frontend tests
cd frontend
bun test

# E2E tests
bun playwright test
```

---

## 🐳 Docker Services

```yaml
services:
  backend    # FastAPI app
  frontend   # Next.js app
  postgres   # Primary database
  mongodb    # Document store
  redis      # Cache + task queue
  celery     # Background workers
  qdrant     # Vector database
  flower     # Celery monitoring UI
  prometheus # Metrics collection
```

Start everything: `docker-compose up -d`

---

## 📈 What I Learned Building This

- **LangGraph agent patterns** — how to properly structure multi-step agents with tool use, memory, and human-in-the-loop checkpoints
- **WebSocket streaming** with FastAPI and how to handle backpressure and reconnection on the frontend
- **RAG pipeline design** — the difference between naive chunking and recursive character splitting, and why reranking matters
- **Async Python** — SQLAlchemy async sessions, async Celery tasks, and how to avoid common pitfalls
- **Production TypeScript patterns** — Zustand for state, React Query for server state, and proper error boundaries

---

## 🤝 Contributing

Contributions, issues and feature requests are welcome. Feel free to open an issue or submit a PR.

---

## 📄 License

MIT License — see [LICENSE](./LICENSE) for details.

---

<div align="center">
  <p>Built with ❤️ by <a href="https://github.com/arpitkasaudhan"><b>Arpit Kasaudhan</b></a></p>
  <p>
    <a href="https://github.com/arpitkasaudhan">GitHub</a> •
    <a href="https://linkedin.com/in/arpitkasaudhan">LinkedIn</a>
  </p>
</div>"# Syntrix-AI-platform" 
