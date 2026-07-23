# PaperMind — Setup Guide

This document lets anyone (including future you, on a new machine) get PaperMind running locally from scratch.

## Prerequisites

- **Python 3.10+** (tested with 3.12.5) — runs the FastAPI backend
- **Node.js + npm** — runs the React/Vite frontend
- **Git** — version control
- A **Google account** — to generate a free Gemini API key at https://aistudio.google.com/apikey

## 1. Clone the repository

```
git clone https://github.com/<your-username>/papermind-ai.git
cd papermind-ai
```

## 2. Backend setup

```
cd backend
python -m venv venv
```

Activate the virtual environment:
- Windows (PowerShell): `.\venv\Scripts\Activate.ps1`
- Mac/Linux: `source venv/bin/activate`

If PowerShell blocks the activation script, run once:
```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Install dependencies:
```
pip install -r requirements.txt
```

Create your local secrets file:
```
cp .env.example .env
```
Then open `.env` and paste your Gemini API key:
```
GEMINI_API_KEY=your_actual_key_here
```

Run the backend:
```
uvicorn main:app --reload
```

Verify it's working by visiting **http://127.0.0.1:8000/health** — you should see `{"status":"ok"}`.

## 3. Frontend setup

Open a **second** terminal (keep the backend running in the first).

```
cd frontend
npm install
npm run dev
```

Vite will print a local URL, typically **http://localhost:5173/** (it may pick a different port like 5174 if 5173 is already in use — check the terminal output).

## 4. Confirm CORS is configured for your actual frontend port

If Vite starts on a port other than 5173, open `backend/main.py` and make sure `allow_origins` includes that exact port, e.g.:

```python
allow_origins=["http://localhost:5173", "http://localhost:5174"],
```

Save and the backend will auto-reload (`--reload` flag).

## 5. Confirm the full stack is connected

Visit your frontend URL. You should see:
```
PaperMind
Backend status: ok
```

If it says "unreachable" instead of "ok", check:
1. Is the backend terminal still running without errors?
2. Does `allow_origins` in `main.py` match your frontend's exact URL and port?
3. Check the browser console (F12) for the specific error message.

## Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| `'python' is not recognized` | Python not added to PATH | Reinstall Python, check "Add python.exe to PATH" |
| Activation script blocked | PowerShell execution policy | Run the `Set-ExecutionPolicy` command above |
| "Backend status: unreachable" | CORS port mismatch | Add the frontend's actual port to `allow_origins` in `main.py` |
| `pip install` fails | Virtual environment not activated | Confirm `(venv)` appears at the start of your terminal prompt |
