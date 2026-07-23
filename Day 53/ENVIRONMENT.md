# PaperMind — Environment & Configuration

## Tools & Versions Confirmed Working

| Tool | Version used | Purpose |
|---|---|---|
| Python | 3.12.5 | Runs the FastAPI backend |
| pip | 24.2 (installed) | Python package manager |
| Node.js / npm | (per `npm create vite@latest` success) | Runs the React frontend |
| FastAPI | 0.139.2 | Backend web framework |
| Uvicorn | 0.51.0 | ASGI server that runs FastAPI |
| pypdf | 6.14.2 | PDF text extraction (Day 4+) |
| python-dotenv | 1.2.2 | Loads `.env` secrets into the backend |
| google-generativeai | 0.8.6 | Gemini API SDK (Day 4+) |
| Vite | 8.1.5 | Frontend dev server/build tool |

Full pinned list lives in `backend/requirements.txt`.

## Environment Variables

### Backend (`backend/.env` — gitignored, never committed)

| Variable | Purpose | Example |
|---|---|---|
| `GEMINI_API_KEY` | Authenticates backend calls to the Google Gemini API | `AIza...` (get from https://aistudio.google.com/apikey) |

A template with no real secret lives in `backend/.env.example`, safe to commit:
```
GEMINI_API_KEY=your_gemini_api_key_here
```

### Frontend

No environment variables required yet for local development (backend URL is currently hardcoded to `http://localhost:8000` in `frontend/src/api/client.js`). This will change on Day 7 (deployment) when we introduce `VITE_API_URL` to point at the deployed backend instead of localhost.

## Local Ports

| Service | Default port | Notes |
|---|---|---|
| Backend (Uvicorn) | 8000 | Fixed via `uvicorn main:app --reload` |
| Frontend (Vite) | 5173 | Vite auto-increments to 5174, 5175, etc. if the port is already in use — always check terminal output for the actual port |

## CORS Configuration

Located in `backend/main.py`. Must explicitly list every frontend origin used during development:

```python
allow_origins=["http://localhost:5173", "http://localhost:5174"],
```

**Why this matters:** if Vite starts on a port not listed here, the browser will block all frontend→backend requests with a CORS error, and the frontend will show "Backend status: unreachable" instead of "ok". Add any new port you see in the Vite terminal output to this list.

## Verifying Your Setup

1. Backend health check: visit `http://127.0.0.1:8000/health` → expect `{"status":"ok"}`
2. Frontend connection check: visit your Vite URL → expect "Backend status: ok" displayed on the page
3. Secret safety check: run `git check-ignore -v backend\.env` → should print a match against `.gitignore`, confirming the file will never be committed
