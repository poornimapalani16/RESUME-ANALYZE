# 🤖 ResumeAI – AI-Powered Resume Analyzer

Full-stack web app that uses Claude AI to compare a resume against a job description and return a match score, missing skills, strengths, and actionable suggestions.

---

## 📁 Folder Structure

```
resume-analyzer/
├── backend/
│   ├── server.js          # Express server (all routes)
│   ├── db.js              # PostgreSQL connection + table init
│   ├── package.json
│   └── .env.example       # Copy to .env and fill in values
│
└── frontend/
    ├── src/
    │   ├── pages/
    │   │   ├── Login.jsx
    │   │   ├── Signup.jsx
    │   │   └── Dashboard.jsx
    │   ├── App.jsx         # Router + auth state
    │   ├── main.jsx        # React entry point
    │   ├── index.css       # All styles
    │   └── config.js       # API base URL
    ├── index.html
    ├── vite.config.js
    ├── package.json
    └── .env.example        # Copy to .env and fill in values
```

---

## ⚙️ Prerequisites

- Node.js v18+
- PostgreSQL database (local or [Supabase](https://supabase.com) free tier)
- Anthropic API key ([get one here](https://console.anthropic.com))

---

## 🚀 Setup & Run

### 1. Backend

```bash
cd backend
cp .env.example .env
# Fill in .env values (see below)
npm install
npm run dev
# Server runs on http://localhost:5000
```

**`backend/.env`**:
```
CLAUDE_API_KEY=sk-ant-...
DATABASE_URL=postgresql://user:password@localhost:5432/resume_analyzer
JWT_SECRET=some_long_random_string_here
PORT=5000
```

### 2. Frontend

```bash
cd frontend
cp .env.example .env
# .env already has: VITE_API_URL=http://localhost:5000
npm install
npm run dev
# App runs on http://localhost:3000
```

---

## 🗄️ Database Setup

The app auto-creates tables on startup. Just make sure your PostgreSQL database exists:

```sql
-- Run once if using local Postgres:
CREATE DATABASE resume_analyzer;
```

For **Supabase**: just copy the connection string from your project's Settings → Database → Connection string (URI mode).

---

## 🔌 API Endpoints

| Method | Endpoint       | Auth | Description                    |
|--------|----------------|------|--------------------------------|
| POST   | /api/register  | No   | Create account (email+password)|
| POST   | /api/login     | No   | Login, returns JWT             |
| POST   | /api/analyze   | JWT  | Analyze resume vs JD           |
| GET    | /api/history   | JWT  | Last 10 analyses for user      |
| GET    | /api/health    | No   | Health check                   |

---

## ✅ Features

- 🔐 JWT authentication (register/login)
- 🤖 Claude AI analysis (score, skills, strengths, suggestions)
- 💾 Results saved to PostgreSQL per user
- 📊 Visual score ring with color coding
- 🌑 Dark editorial UI with Google Fonts
- 🔒 Protected dashboard route
