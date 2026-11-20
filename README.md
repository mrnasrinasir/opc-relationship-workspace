# Relate — OPC Relationship Workspace

A relationship workspace for one-person companies. Your network shouldn't depend on your memory, and your relationships shouldn't feel automated.

**Live app:** https://9c23hs4a.qwenwork.page/

## What it does

1. **Fast onboarding** — scan your LinkedIn QR, upload a photo/card, or paste a URL. Your public profile is pulled (via [Apify](https://apify.com) `harvestapi/linkedin-profile-scraper`) and stored as a profile card with photo.
2. **Guided capture** — one question at a time: who did you meet, their company, their LinkedIn (QR scan / business card OCR / URL pull), and context notes. Optional voice notes.
3. **Assessment** — a QwenWork agent researches the person with real web searches (sources cited, gaps flagged) and scores the fit on a matrix: relevance, evidence of need, access, timing. **You decide:** worth pursuing / consider / reject.
4. **Insight deck** — when you pursue, the agent drafts a professional, two-party intro deck (why connect, opportunities, value, next step) published at a shareable link, exportable as PDF. The recipient can **accept** the intro, and the response flows back into your records.
5. **Continue the journey** — generated follow-up drafts, a comment/voice-note timeline, and next actions. Nothing is ever auto-sent.

## Architecture

- **Frontend:** single-page dark UI (`index.html`) — no build step.
- **Backend:** dependency-free Node.js server (`server.js`) with a REST API, backed by a Postgres database (Supabase-compatible) storing relationships, profiles, research jobs, deck jobs, OCR and transcription queues.
- **Integrations:**
  - **Apify** for instant LinkedIn profile pulls (token stored server-side via the in-app Settings screen — never in source).
  - **QwenWork agents** (scheduled workers) for research + assessment and insight deck generation, including PDF rendering.
- **Privacy by design:** private notes and unverified research are never shared; public links serve only the deck. Capture is user-initiated; nothing is auto-sent.

## Run locally

```bash
npm start          # serves on PORT (default 8081)
```

Requires `SUPABASE_URL` / `SUPABASE_ANON_KEY` in the environment (or adapt `sb()` in `server.js` to your database).

## License

MIT
