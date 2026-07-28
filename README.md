<div align="center">
# 🎬 MoodFlix AI
 
**AI-powered, mood-based movie recommendation platform**
 
Tell it how you feel — get movies that actually match, with a plain-language explanation of *why*.
 
</div>
---
 
## ✨ What It Does
 
MoodFlix AI takes a free-text description of your mood (*"long stressful week, I want something visually beautiful and calming"*) and turns it into a ranked list of movie recommendations using Google's Gemini API. Instead of generic genre filters, it reasons over mood, tone, pacing, and language preferences to explain **why** each pick fits.
 
Key features:
 
- **Natural-language mood input** — describe how you feel instead of picking checkboxes
- **AI-generated recommendations** — powered by the Gemini API, with a natural-language rationale per movie
- **Featured pick + Quick Picks row** for at-a-glance browsing
- **Language filtering** (English, Japanese, Korean, Hindi, French, Spanish, Portuguese, and more)
- **Watchlist & viewing history**, scoped per user and persisted locally
- **Authentication** — email/password and Google sign-in, with onboarding flow for new users
- **User preference profiles** — favorite genres, disliked genres, preferred decades, content rating limits, favorite actors/directors
- **Admin dashboard** — user management, role promotion, and content-ingestion pipeline controls
- **AI pipeline visualizer** — see how the recommendation/ingestion pipeline processes data
- **SRS document viewer** — in-app view of the project's software requirements specification
---
 
## 🛠 Tech Stack
 
| Layer | Technology |
|---|---|
| Frontend | React 19, TypeScript, Vite, Tailwind CSS 4 |
| Backend | Express (Node.js), TypeScript |
| AI | Google Gemini API (`@google/genai`) |
| Icons / Animation | lucide-react, motion |
| Build | Vite (client) + esbuild (server bundle) |
 
---
 
## 📁 Project Structure
 
```
moodflix-ai/
├── server.ts                     # Express API server (auth, movies, recommendations, admin)
├── index.html                    # App entry HTML
├── src/
│   ├── App.tsx                   # Root app component & tab routing
│   ├── main.tsx                  # React entry point
│   ├── types.ts                  # Shared TypeScript types
│   ├── index.css                 # Global styles (Tailwind)
│   ├── components/
│   │   ├── Header.tsx
│   │   ├── MoodInputSection.tsx
│   │   ├── FeaturedRecommendation.tsx
│   │   ├── QuickPicksRow.tsx
│   │   ├── MovieDetailModal.tsx
│   │   ├── WatchlistAndHistory.tsx
│   │   ├── AIPipelineVisualizer.tsx
│   │   ├── SRSDocumentViewer.tsx
│   │   ├── AuthModal.tsx
│   │   ├── OnboardingModal.tsx
│   │   ├── AdminDashboard.tsx
│   │   └── Footer.tsx
│   ├── data/
│   │   ├── movies.ts              # Movie catalog / seed data
│   │   ├── ingestionPipeline.ts    # Content ingestion pipeline logic
│   │   └── srsDocument.ts          # SRS document content
│   └── hooks/
│       └── useAuth.tsx            # Auth context/provider hook
├── metadata.json
├── package.json
├── vite.config.ts
└── tsconfig.json
```
 
---
 
## 🔌 API Overview
 
The Express server (`server.ts`) exposes:
 
**Auth**
- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/me`
- `POST /api/auth/google`
- `POST /api/auth/logout`
**User preferences**
- `GET /api/users/me/preferences`
- `PUT /api/users/me/preferences`
- `POST /api/users/me/onboarding`
**Admin** (requires admin role)
- `GET /api/admin/users`
- `POST /api/admin/promote-user`
- `POST /api/admin/ingestion-sync`
**Core**
- `GET /api/health`
- `GET /api/movies`
- `GET /api/srs`
- `POST /api/recommend` — the main mood → recommendation endpoint (Gemini-powered)
---
 
## 🚀 Run Locally
 
**Prerequisites:** Node.js 18+
 
1. Install dependencies:
```bash
   npm install
```
2. Copy the environment template and add your key:
```bash
   cp .env.example .env.local
```
   Then set `GEMINI_API_KEY` in `.env.local` to your Gemini API key.
3. Start the dev server:
```bash
   npm run dev
```
4. Open the app at the local URL printed in your terminal.
### Other scripts
 
| Command | Description |
|---|---|
| `npm run dev` | Start local dev server (`tsx server.ts`) |
| `npm run build` | Build client (Vite) + bundle server (esbuild) into `dist/` |
| `npm start` | Run the production build (`dist/server.cjs`) |
| `npm run lint` | Type-check the project (`tsc --noEmit`) |
| `npm run clean` | Remove build output |
 
---
 
## 🔐 Environment Variables
 
| Variable | Description |
|---|---|
| `GEMINI_API_KEY` | Required. Your Google Gemini API key, used server-side for recommendations. |
| `APP_URL` | The URL this app is hosted at (used for self-referential links/callbacks). |
 
> ⚠️ Never commit `.env.local` or real API keys — `.gitignore` already excludes them.
 
---
 
## 📝 Notes
 
- This project was originally scaffolded in Google AI Studio; the in-app **SRS Document Viewer** and **AI Pipeline Visualizer** tabs document the app's own requirements and data pipeline for reference.
- User data (watchlist, history, auth) is currently stored in-memory on the server and in the browser's `localStorage` — restarting the server clears server-side user records. Swap in a real database for production use.
---
 
<div align="center">
Built with React, Express, and the Gemini API.
</div>

