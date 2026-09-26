Yes. I’ll format the GitHub `README.md` professionally based on your project structure and actual features. Your project is a full-stack AI Assistant with FastAPI, Next.js, Ollama, and cloud-provider fallback. 

# 🤖 AI Assistant — Full Stack

A modern full-stack AI chat application built with **FastAPI, Next.js, React, TypeScript, and Ollama**.

The application prioritizes **local AI models through Ollama** and can automatically fall back to cloud AI providers such as **Anthropic, OpenAI, Google Gemini, xAI Grok, and Meta Llama** when a local model is unavailable or fails.

---

## ✨ Features

* 🤖 AI-powered conversational chat
* 🏠 Local AI inference using **Ollama**
* ☁️ Cloud AI fallback support
* 🔄 Automatic provider/model fallback
* ⚡ Real-time streaming responses
* 🎯 Model selection from the frontend
* 🧠 Support for multiple AI providers
* 📡 Server-Sent Events (SSE) for streaming
* 🩺 API health-check endpoint
* 🧪 Backend test suite with Pytest
* 🎨 Modern Next.js frontend
* 🐳 Docker and Docker Compose support
* 🔐 Environment-based configuration
* 📱 Responsive chat interface

---

## 🛠️ Tech Stack

### Backend

* **Python 3.13**
* **FastAPI**
* **Uvicorn**
* **Pydantic**
* **uv**
* **Ollama Python SDK**
* **OpenAI SDK**
* **Anthropic SDK**
* **HTTPX**
* **Pytest**
* **Ruff**

### Frontend

* **Next.js 16**
* **React 19**
* **TypeScript**
* **Tailwind CSS 4**
* **shadcn/ui**

### AI Providers

| Provider         | Type     |
| ---------------- | -------- |
| Ollama           | 🏠 Local |
| Anthropic Claude | ☁️ Cloud |
| OpenAI           | ☁️ Cloud |
| Google Gemini    | ☁️ Cloud |
| xAI Grok         | ☁️ Cloud |
| Meta Llama       | ☁️ Cloud |

The project uses Ollama as the first-choice local provider and configured cloud providers as fallbacks. 

---

## 📁 Project Structure

```text
hammad-ahmad-suja-ai.assistant/
│
├── ai-assistant/
│   │
│   ├── api/                         # FastAPI Backend
│   │   ├── app/
│   │   │   ├── core/
│   │   │   │   ├── config.py
│   │   │   │   └── logging.py
│   │   │   │
│   │   │   ├── providers/
│   │   │   │   ├── anthropic.py
│   │   │   │   ├── base.py
│   │   │   │   ├── ollama.py
│   │   │   │   ├── openai_compat.py
│   │   │   │   └── registry.py
│   │   │   │
│   │   │   ├── routes/
│   │   │   │   ├── chat.py
│   │   │   │   ├── health.py
│   │   │   │   └── models.py
│   │   │   │
│   │   │   ├── services/
│   │   │   │   └── chat.py
│   │   │   │
│   │   │   ├── deps.py
│   │   │   ├── main.py
│   │   │   └── schemas.py
│   │   │
│   │   ├── tests/
│   │   ├── Dockerfile
│   │   ├── pyproject.toml
│   │   ├── .env.example
│   │   └── README.md
│   │
│   ├── web/                         # Next.js Frontend
│   │   ├── app/
│   │   ├── components/
│   │   │   ├── chat/
│   │   │   └── ui/
│   │   ├── hooks/
│   │   ├── lib/
│   │   ├── package.json
│   │   ├── Dockerfile
│   │   └── README.md
│   │
│   ├── docker-compose.yml
│   └── README.md
│
└── .claude/
    └── skills/
```

The repository separates the application into an `api` FastAPI backend and a `web` Next.js frontend. 

---

# 🚀 Getting Started

## 📋 Requirements

Install the following before running the project:

* Python **3.13**
* [uv](https://docs.astral.sh/uv/)
* Node.js **20.9+**
* npm
* Ollama *(optional, but recommended for local AI)*

---

## 🏠 1. Install Ollama

Download and install Ollama from:

[https://ollama.com](https://ollama.com)

Then download a local model:

```bash
ollama pull llama3.2
```

You can verify your installed models with:

```bash
ollama list
```

---

# ⚙️ 2. Run the Backend

Open a terminal and move into the API directory:

```bash
cd ai-assistant/api
```

Install dependencies:

```bash
uv sync
```

Create your environment file:

```bash
cp .env.example .env
```

On Windows PowerShell, you can also use:

```powershell
Copy-Item .env.example .env
```

Start the FastAPI server:

```bash
uv run fastapi dev app/main.py
```

The backend will be available at:

```text
http://localhost:8000
```

FastAPI documentation:

```text
http://localhost:8000/docs
```

The backend exposes health, model-listing, and streaming chat endpoints. 

---

# 🎨 3. Run the Frontend

Open another terminal:

```bash
cd ai-assistant/web
```

Install dependencies:

```bash
npm install
```

Create the environment file:

```bash
cp .env.example .env.local
```

On Windows PowerShell:

```powershell
Copy-Item .env.example .env.local
```

Start the development server:

```bash
npm run dev
```

Open:

```text
http://localhost:3000
```

---

# 🔑 Environment Configuration

The backend uses environment variables for application settings, Ollama configuration, and optional cloud API keys.

Example:

```env
ENVIRONMENT=development
LOG_LEVEL=INFO

CORS_ORIGINS=["http://localhost:3000"]

SYSTEM_PROMPT="You are a helpful, accurate and concise AI assistant."

ALLOW_CLOUD_FALLBACK=true

OLLAMA_ENABLED=true
OLLAMA_HOST=http://localhost:11434
```

### Cloud Providers

You can optionally configure cloud providers:

```env
ANTHROPIC_API_KEY=
ANTHROPIC_MODEL=

OPENAI_API_KEY=
OPENAI_MODEL=

GEMINI_API_KEY=
GEMINI_MODEL=

GROK_API_KEY=
GROK_MODEL=

META_API_KEY=
META_MODEL=
```

A cloud provider becomes available when its API key is configured. 

> ⚠️ Never commit your `.env` file or API keys to GitHub.

---

# 🧠 How AI Model Selection Works

The application provides an automatic model-selection and fallback system.

### Default behavior

```text
User
 │
 ▼
Frontend
 │
 ▼
FastAPI API
 │
 ▼
Selected Model
 │
 ├── Ollama Local Model
 │
 ├── Anthropic
 │
 ├── OpenAI
 │
 ├── Gemini
 │
 ├── Grok
 │
 └── Meta Llama
```

When **Auto** mode is used, the application first looks for an available local Ollama model. If no local model is available, it checks configured cloud providers.

If the selected model fails **before generating a response**, the API can automatically try another available provider.

This fallback behavior is implemented so that a response is not mixed between two models after streaming has already started. 

---

# 📡 API Endpoints

| Method | Endpoint      | Description                            |
| ------ | ------------- | -------------------------------------- |
| `GET`  | `/api/health` | Check API status                       |
| `GET`  | `/api/models` | Get available AI models                |
| `POST` | `/api/chat`   | Send chat messages and stream response |

### Health Check

```http
GET /api/health
```

Example response:

```json
{
  "status": "ok",
  "version": "1.0.0"
}
```

### Get Models

```http
GET /api/models?refresh=true
```

### Chat

```http
POST /api/chat
```

Example request:

```json
{
  "messages": [
    {
      "role": "user",
      "content": "Hello!"
    }
  ],
  "provider": "ollama",
  "model": "llama3.2:latest"
}
```

The chat endpoint streams responses using **Server-Sent Events (SSE)**. 

---

# 🐳 Docker

The project also supports Docker Compose.

First create the environment file:

```bash
cp ai-assistant/api/.env.example ai-assistant/api/.env
```

Then run:

```bash
cd ai-assistant
docker compose up --build
```

The services will be available at:

```text
Frontend: http://localhost:3000
Backend:  http://localhost:8000
```

The Docker Compose configuration contains separate `api` and `web` services and can optionally run Ollama in Docker. 

---

# 🧪 Testing

## Backend Tests

Run:

```bash
cd ai-assistant/api
uv run pytest
```

Run linting:

```bash
uv run ruff check .
```

Check formatting:

```bash
uv run ruff format --check .
```

## Frontend Checks

```bash
cd ai-assistant/web
npm run typecheck
```

Build the frontend:

```bash
npm run build
```

The project includes backend tests for chat, models, and provider behavior. 

---

# 🔄 Fallback Configuration

Cloud fallback can be enabled or disabled using:

```env
ALLOW_CLOUD_FALLBACK=true
```

To disable automatic cloud fallback:

```env
ALLOW_CLOUD_FALLBACK=false
```

Cloud provider priority can be configured with:

```env
CLOUD_PRIORITY=["anthropic","openai","gemini","grok","meta"]
```

The application tries providers according to this configured order. 

---

# 🔒 Security Notes

Before deploying this application publicly:

* Use HTTPS.
* Configure proper CORS origins.
* Add authentication.
* Add rate limiting.
* Keep API keys in environment variables.
* Never commit `.env` files.
* Protect cloud API credentials.
* Use production configuration.

The project documentation specifically recommends authentication and rate limiting before exposing the API publicly. 

---

# 📌 Production Checklist

Before production deployment:

```text
☐ Configure HTTPS
☐ Configure production CORS
☐ Set ENVIRONMENT=production
☐ Add authentication
☐ Add rate limiting
☐ Configure API keys securely
☐ Test Ollama/cloud providers
☐ Build frontend
☐ Run backend tests
☐ Run frontend type checks
```

---

# 👨‍💻 Author

**Hammad Ahmad Suja**

GitHub:
`https://github.com/hammad-ahmad-suja`

---

# 📄 License

This project is intended for educational and development purposes.

Add your preferred open-source license here, such as **MIT License**, if you plan to publish the project under an open-source license.

This is ready to paste into your repository's **`ai-assistant/README.md`**. I kept the commands and architecture aligned with the files you provided rather than inventing features. 
