# PaperMind — Future Scope

How this specific v1.0 could evolve, grounded in what's actually built today: a single-session, single-document PDF assistant with in-memory state, Gemini `gemini-3.1-flash-lite`, FastAPI, React/Vite, deployed free-tier on Render + Vercel.

## Next 3 Months: Solidify the Single-User Experience

The current architecture deliberately has no database (per the original PRD scope decision) and no auth. The highest-value near-term work is making the *single-session* experience more robust before ever touching multi-user complexity:

- **Persistent sessions via browser storage**: use the already-built `GET/DELETE /session` endpoints (added Day 3, initially unused until Day 8) to sync with `localStorage` on the frontend, so a page refresh doesn't lose an in-progress document if the backend hasn't restarted.
- **Streaming responses**: Gemini's API supports streaming; both `/analyze` and `/chat` currently wait for a complete response before returning. Streaming would let the summary and chat answers appear token-by-token, meaningfully improving perceived speed on Render's free tier (which already has cold-start latency).
- **Multi-document support within a session**: allow uploading 2-3 PDFs and asking questions across all of them, still without a database — just extend `current_document` into a small in-memory list. This was explicitly out of scope for v1.0 but is the most natural next feature given the existing architecture.
- **Real automated tests**: the project has zero automated tests today — everything was manually verified via screenshots throughout the 10 days. A `pytest` suite for the backend (upload validation, PDF extraction edge cases, Gemini error handling) would be the highest-leverage quality investment.

## Next 6 Months: Real Persistence and Accounts

- **Add a real database** (Supabase or Firebase free tier, both already considered acceptable per project constraints) to support saved document history and multi-session persistence — the `SessionState` model documented in `docs/SCHEMA.md` was designed from day one to make this swap contained to one module (`state.py`/`main.py`'s in-memory dict), so this is a bounded, well-scoped migration rather than a rewrite.
- **Lightweight authentication** (magic-link email or GitHub OAuth via Supabase Auth) so documents and chat history belong to a specific user instead of a shared global session — directly resolves the "global session" limitation flagged in `docs/BUGS.md`.
- **Per-user rate limiting** replacing the current global in-memory limiter (15 calls/10 min shared across all visitors) with per-user quotas, now that accounts exist to key off of.
- **Embeddings-based retrieval for long documents**: right now, documents are truncated at 100,000 characters before being sent to Gemini. A vector index (e.g., using Gemini's embedding API, still free-tier) would let PaperMind handle genuinely long documents (200+ pages) by retrieving only relevant chunks for each chat question instead of truncating.

## Next 12 Months: Multi-Document Knowledge Base

- **A true document library**: multiple saved PDFs per user, searchable, with cross-document chat ("what do my last three uploaded contracts have in common?") — this was explicitly called out as out-of-scope in the original PRD and is the natural ceiling of the current single-document design.
- **Collaborative sharing**: share a summarized document + its chat thread via a read-only link, useful for the "professional receives a report" persona from the original PRD's target users.
- **Support for more file types**: Word documents and plain text, reusing the existing `pdf_utils.py`-style extraction pattern with format-specific extractors behind the same interface.
- **Usage-based cost model**: if this ever moved beyond a free-tier demo, introducing a paid tier would fund a non-free Gemini quota, removing the current shared-quota fragility entirely (the exact issue that caused the Day 8 429 errors during heavy testing).
