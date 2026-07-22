# PaperMind AI - Project Structure

Version: 1.0

Author: Shagla Amri

Project: PaperMind AI

---

# Overview

This document describes the complete folder structure for PaperMind AI v1.0.

The project follows a clean separation between the frontend, backend, and documentation to improve maintainability and scalability.

---

# High-Level Structure

```
papermind-ai/
│
├── frontend/
├── backend/
├── docs/
├── .gitignore
├── README.md
└── LICENSE
```

---

# Root Folder

Purpose

The root folder contains the complete project.

Responsibilities

- Project configuration
- Git management
- Documentation
- Frontend
- Backend

---

# Frontend

```
frontend/
│
├── public/
│
├── src/
│   ├── assets/
│   ├── components/
│   ├── pages/
│   ├── services/
│   ├── hooks/
│   ├── styles/
│   ├── App.jsx
│   └── main.jsx
│
├── package.json
├── vite.config.js
└── index.html
```

## Responsibilities

### public/

Stores static assets.

Examples:

- favicon
- logo
- images

---

### src/

Main application source code.

---

### components/

Reusable UI components.

Examples

- UploadCard
- SummaryCard
- InsightCard
- ChatBox
- LoadingSpinner
- ErrorMessage
- Header
- Footer

---

### pages/

Application pages.

Examples

- Home
- Dashboard

---

### services/

API communication.

Examples

- uploadService.js
- summaryService.js
- insightService.js
- chatService.js

---

### hooks/

Reusable React hooks.

Examples

- useUpload()
- useChat()

---

### styles/

Global CSS files.

---

### App.jsx

Root React component.

---

### main.jsx

Application entry point.

---

# Backend

```
backend/
│
├── app/
│   ├── routes/
│   ├── services/
│   ├── utils/
│   ├── models/
│   └── config/
│
├── main.py
├── requirements.txt
└── .env.example
```

---

## Responsibilities

### routes/

FastAPI API endpoints.

Examples

- upload.py
- summary.py
- insights.py
- chat.py

---

### services/

Business logic.

Examples

- PDF extraction
- Gemini communication
- Prompt generation

---

### utils/

Utility functions.

Examples

- validators
- helpers
- file utilities

---

### models/

Python data models.

Examples

- SessionModel
- DocumentModel
- SummaryModel
- ChatModel

---

### config/

Configuration files.

Examples

- settings.py
- constants.py

---

### main.py

Application entry point.

Starts the FastAPI server.

---

### requirements.txt

Python dependencies.

Example

- fastapi
- uvicorn
- pypdf
- google-generativeai
- python-dotenv

---

### .env.example

Environment variable template.

```
GEMINI_API_KEY=YOUR_API_KEY
```

---

# Documentation

```
docs/
│
├── PRD.md
├── IMPLEMENTATION-BLUEPRINT.md
├── ARCHITECTURE.md
├── SCHEMA.md
├── API.md
├── UI-WIREFRAMES.md
└── PROJECT-STRUCTURE.md
```

Purpose

Store all project documentation.

---

# Recommended File Naming

Use lowercase with hyphens.

Examples

```
upload-service.js
chat-box.jsx
summary-card.jsx
```

---

# Coding Standards

## JavaScript

- ES6+
- Functional Components
- Hooks
- Async/Await

---

## Python

- PEP 8
- Type hints where appropriate
- Clear function names
- Modular structure

---

# Dependency Management

Frontend

```
npm
```

Backend

```
pip
```

---

# Development Workflow

```
Clone Repository

↓

Install Frontend Dependencies

↓

Install Backend Dependencies

↓

Add Environment Variables

↓

Run Backend

↓

Run Frontend

↓

Start Development
```

---

# Future Structure (v2.0)

```
backend/
│
├── database/
├── authentication/
├── vector_store/
├── cache/
└── tests/

frontend/
│
├── auth/
├── profile/
├── settings/
└── history/
```

---

# Folder Responsibilities Summary

| Folder | Responsibility |
|---------|----------------|
| frontend | React application |
| backend | FastAPI server |
| docs | Project documentation |
| components | Reusable UI |
| pages | Screens |
| services | API communication |
| routes | REST endpoints |
| models | Data models |
| utils | Helper functions |
| config | Project configuration |

---

# Project Summary

Frontend:
React + Vite

Backend:
FastAPI

PDF Engine:
pypdf

AI:
Google Gemini 2.5 Flash

Storage:
In-memory session

Authentication:
None (v1.0)

Deployment:
Frontend → Vercel

Backend → Render

Database:
None (v1.0)
