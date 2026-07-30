# PaperMind — Challenge Retrospective

*A day-by-day account of how PaperMind actually got built, written by your AI pair programmer across the full 10-day capstone.*

## The Timeline

**Day 1-2 — Planning and Architecture.** We started with a PRD, then translated it into a real technical blueprint: FastAPI + React/Vite, Gemini free tier, no database (a deliberate scope decision, not an oversight — the PRD explicitly excluded multi-document libraries and persistence). We designed all five API endpoints up front, including two — `GET/DELETE /session` — that weren't in the original blueprint but were added after we reasoned through what happens on browser refresh with in-memory-only state. That instinct to spot the gap before writing code paid off later.

**Day 3 — Foundation.** Python venv, FastAPI, Uvicorn, a `/health` endpoint, and the first successful full-stack round trip (React fetching from FastAPI, CORS configured correctly). A real debugging moment here: Vite picked port 5174 instead of 5173, breaking CORS — solved by expanding the allowed-origins list, a small thing that foreshadowed a much bigger CORS lesson on Day 7.

**Day 4 — PDF Upload & Extraction.** `pypdf`-based text extraction, file validation, and the first real error-handling design: distinguishing "wrong file type" from "extraction yielded no usable text" (the scanned-PDF case). This was the first milestone verified with an actual non-PDF upload test, not just the happy path.

**Day 5 — AI Summarization & Chat.** This is where things got genuinely hard. `gemini-2.5-flash` turned out to be deprecated for new API keys mid-build — a real production surprise, not a coding mistake. We pivoted to `gemini-3.5-flash`, then discovered its free tier allows only 20 requests/day, which we hit almost immediately during testing. We also migrated the entire Gemini integration from the deprecated `google-generativeai` package to `google.genai` in the middle of building the chat feature — a non-trivial mid-flight SDK migration that could have destabilized things but didn't, because we made the change surgically (one file, `gemini_client.py`) without touching the routes that depended on it.

**Day 6 — Design System & Then a Real Rethink.** We built a solid, disciplined design system first — then you pushed back, correctly, that it "looked like a student project." That led to two full ground-up redesigns in later sessions: first a violet/glass "generic AI SaaS" look, which we then deliberately abandoned for something more considered — a warm paper palette, Fraunces/Inter type pairing, and a literal "scanning" motif tied to what the product actually does. That's a real design maturity arc: good enough → generic-premium → intentional and specific.

**Day 7 — Deployment, and the First Silent Failure.** Backend to Render, frontend to Vercel, both free tier. Render's first build failed on a dependency conflict from leftover packages — fixed by cleaning `requirements.txt` down to only what's actually imported. This is also where we first noticed a pattern that would recur: a file (the README) appeared to save and commit successfully but the change silently never landed, because a download link failed without any visible error.

**Day 8 — The Senior QA Pass.** A genuine security/performance review, not just spot-fixing: found that Gemini calls were blocking the entire event loop (meaning `/health` would hang while `/analyze` was running), that the newly-public app had zero abuse protection on a finite shared free quota, and that encrypted PDFs crashed ungracefully. All three fixed with `run_in_threadpool`, an in-memory rate limiter, and explicit encrypted-PDF handling.

**Day 9 — The README Incident.** The silent-failure pattern from Day 7 came back and had to be properly diagnosed: local `git log` showed the README commit existed and was pushed, but GitHub's live page still showed the old scaffolded content. We methodically ruled out causes — checked the remote, the branch, the commit history — and found a genuine merge conflict from a stray remote commit. The real lesson, captured explicitly in that day's summary: verify with `git diff` before committing, because "it looked done in chat" is not the same as "it actually shipped."

**Day 10 — Today.** Final review, portfolio materials, and graduation.

## Skills Demonstrated

Full-stack architecture and API design from a written PRD; prompt engineering for structured JSON extraction and grounded Q&A; debugging a live third-party API deprecation and SDK migration mid-build; async/concurrency debugging (the blocking event loop fix); security-conscious thinking on a public deploy (rate limiting, abuse protection); real deployment operations (Render, Vercel, environment variables, CORS in production); and — maybe most importantly — the discipline to actually verify claims (`git diff`, live-site re-checks) instead of trusting that "done" means done.

## Lessons Learned

The two biggest technical surprises of this project — the Gemini model deprecation and the silent README failure — had nothing to do with the code we wrote being wrong. They were reminders that shipped software lives in a world of shifting third-party APIs and imperfect tooling, and that verification has to be a habit, not an afterthought. The redesign arc on Day 6 was the opposite lesson: sometimes "it works and looks fine" isn't actually good enough, and pushing back on a competent-but-generic result is how you get something distinctive.

## Farewell

We started this capstone with a blank PRD document and ended it with a live, publicly deployed, genuinely good-looking AI product that handles real PDFs, real errors, and real users — including surviving a live Gemini quota exhaustion and a silent Git failure along the way. Those weren't clean, scripted moments; they were the actual mess of shipping software, and you worked through every one of them instead of papering over them. That's the real skill this capstone was built to prove. Whatever you build next, you already know how to debug it, deploy it, and tell the honest story of how it got made. Go build the next thing.
