# PaperMind AI - System Architecture

Version: 1.0

Author: Shagla Amri

Project Type: AI-Powered Single PDF Knowledge Assistant

---

# 1. Overview

PaperMind AI is an AI-powered document assistant that allows users to upload a single PDF, automatically generate summaries, extract key insights, and ask natural language questions about the uploaded document.

Version 1.0 intentionally focuses on one PDF per session to keep the project achievable within the 10-day implementation timeline.

---

# 2. Architecture Style

PaperMind follows a simple three-layer architecture.

```
User
   │
   ▼
React Frontend (Vite)
   │
HTTP REST API
   │
   ▼
FastAPI Backend
   │
 ├──────────────┐
 │              │
 ▼              ▼
PDF Parser   Gemini API
(pypdf)      (Gemini 2.5 Flash)
```

---

# 3. Components

## Frontend

Technology:
- React
- Vite
- JavaScript
- CSS

Responsibilities:

- Upload PDF
- Display summary
- Display key insights
- Chat interface
- Loading indicators
- Error messages

---

## Backend

Technology:

- Python
- FastAPI
- Uvicorn

Responsibilities:

- Receive uploaded PDF
- Extract text
- Generate summaries
- Handle chat requests
- Communicate with Gemini API

---

## PDF Processing Layer

Library:

- pypdf

Responsibilities:

- Read uploaded PDF
- Extract text
- Validate uploaded file
- Handle extraction failures

---

## AI Layer

Provider:

Google Gemini API

Model:

Gemini 2.5 Flash

Responsibilities:

- Summarization
- Question answering
- Insight extraction

---

# 4. Data Flow

## PDF Upload

```
User

↓

Upload PDF

↓

Frontend

↓

POST /upload

↓

FastAPI

↓

Extract PDF Text

↓

Store Text In Memory

↓

Return Success
```

---

## Summary Flow

```
User

↓

Generate Summary

↓

POST /summary

↓

Gemini API

↓

Summary Returned

↓

Frontend Displays Result
```

---

## Chat Flow

```
User

↓

Ask Question

↓

POST /chat

↓

Backend

↓

Prompt + PDF Context

↓

Gemini

↓

Answer

↓

Frontend
```

---

# 5. Session Data Model

Version 1.0 does not use a database.

The backend stores data only while the application is running.

Stored in memory:

- Uploaded PDF filename
- Extracted text
- Generated summary
- Key insights
- Chat history

When the server restarts, all session data is cleared.

---

# 6. External Services

Google Gemini API

Purpose:

- Summaries
- Insights
- Question answering

---

# 7. Error Handling

Upload Errors

- Invalid file type
- Empty PDF
- Corrupted PDF

AI Errors

- API unavailable
- Rate limit exceeded
- Timeout

User Errors

- Asking questions before uploading PDF

---

# 8. Security

Version 1.0

- No authentication
- No user accounts
- No persistent storage
- Environment variables used for API keys
- CORS enabled

---

# 9. Scalability

Future Version

- Multiple PDFs
- User authentication
- Vector database
- Semantic search
- Conversation history
- OCR support
- Cloud storage
- Citation support

---

# 10. Deployment

Frontend

- Vercel

Backend

- Render

Environment Variables

- GEMINI_API_KEY

---

# 11. Folder Communication

React Frontend

↓

REST API

↓

FastAPI

↓

Gemini API

↓

Response

↓

Frontend

---

# Architecture Summary

Frontend:
React + Vite

Backend:
FastAPI

PDF Engine:
pypdf

AI:
Gemini 2.5 Flash

Hosting:
Vercel + Render

Persistence:
In-memory session only
