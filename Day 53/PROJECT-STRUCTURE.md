# PaperMind — Project Structure (updated after Day 3 foundation build)

```
papermind-ai/
├── backend/
│   ├── venv/                    # Python virtual environment (gitignored)
│   ├── main.py                  # FastAPI app instance, CORS, /health endpoint [BUILT]
│   ├── requirements.txt         # Pinned dependency versions [BUILT]
│   ├── .env.example             # GEMINI_API_KEY placeholder, safe to commit [BUILT]
│   └── .env                     # (gitignored) real Gemini API key [BUILT locally, not committed]
│
├── frontend/
│   ├── src/
│   │   ├── main.jsx             # Vite/React entry point (scaffold default)
│   │   ├── App.jsx              # Now calls backend /health and displays status [BUILT]
│   │   ├── App.css
│   │   ├── api/
│   │   │   └── client.js        # fetch wrapper for backend calls [BUILT — checkHealth()]
│   │   └── assets/
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
│
├── .gitignore                   # Covers node_modules, venv, .env, __pycache__
├── README.md
└── docs/
    ├── ARCHITECTURE.md           # Day 2
    ├── SCHEMA.md                 # Day 2
    ├── API.md                    # Day 2
    ├── UI-WIREFRAMES.md          # Day 2
    ├── PROJECT-STRUCTURE.md      # This file, updated Day 3
    ├── BLUEPRINT-ADDENDUM.md     # Day 2
    ├── SETUP.md                  # Day 3
    ├── ENVIRONMENT.md            # Day 3
    └── DAY3-SUMMARY.md           # Day 3
```

## What Changed Since Day 2's Design

The Day 2 design (original `PROJECT-STRUCTURE.md`) planned for `backend/app/routes/`, `backend/app/services/`, `backend/app/models/`, and `backend/app/state.py` as the eventual file layout for the full feature set. As of Day 3, only the **foundation** exists:

- `backend/main.py` is currently a single flat file (FastAPI app + CORS + `/health`). It has **not yet** been split into the `app/routes/`, `app/services/`, `app/models/` structure — that split happens naturally starting Day 4, when `/upload` and `/analyze` endpoints are added and the file would otherwise grow unwieldy.
- `frontend/src/api/client.js` exists now with one function (`checkHealth`). It will grow to include `uploadPdf()`, `analyzeDocument()`, `sendChatMessage()`, etc. as those endpoints are built.
- No component folder (`UploadZone.jsx`, `SummaryPanel.jsx`, etc.) exists yet — `App.jsx` is currently a single flat component. Component splitting begins Day 4 alongside the upload feature.

This is expected and intentional — Day 3's job was foundation only, not the full structure. No design decision has changed; the Day 2 target structure remains the plan for Day 4 onward.
