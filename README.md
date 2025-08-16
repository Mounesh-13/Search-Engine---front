🚀 AI Semantic Search Engine
A production-ready, agentic AI-powered semantic search engine inspired by Perplexity. Built using Python (Flask), Google Gemini LLM, SerpAPI, and React with a custom Material UI theme and animated space background.

✨ Features
Semantic natural language search (Gemini LLM)

Retrieval-Augmented Generation (RAG): Combines real-time web data (SerpAPI) with advanced LLM reasoning—returns cited, up-to-date answers

Resilient backend: Threaded timeout for live search, fallback to Gemini on error, caching, structured API responses

Perplexity-inspired frontend: Modern React UI, numbered source chips, model-vs-search banners, timing info

Animated galaxy/star background (tsparticles)

Configurable and extendable: Easy plug-in for more tools or models

⚡️ Tech Stack
Backend: Python, Flask, Gunicorn, LangChain, Gemini LLM, SerpAPI, flask-cors, python-dotenv

Frontend: ReactJS, Material UI (custom theme), tsparticles, ReactMarkdown, framer-motion

Deployment: Railway (backend), Netlify (frontend), Docker for local/prod as needed

🚦 Deployment Guide
Option 1: Backend on Railway
Steps:
Prepare backend repo:

Commit app.py, requirements.txt, and a Procfile:

text
web: gunicorn -w 2 -k gthread --threads 8 -b 0.0.0.0:$PORT app:app
Your Flask app should start with the env port:

python
if __name__ == "__main__":
    app.run(host="0.0.0.0", port=int(os.getenv("PORT", "5000")), debug=False)
Deploy:

On Railway: “New Project” → “Deploy from GitHub”

Select your backend folder (or set root if monorepo)

Set environment variables (see below)

Deploy and get API URL (e.g., https://your-backend.up.railway.app)

Set environment variables in Railway:

GOOGLE_API_KEY

SERPAPI_API_KEY

Optional: SERP_TIMEOUT, GEMINI_MODEL, CACHE_TTL_S, MAX_PROMPT_CHARS

Option 2: Frontend on Netlify
Steps:
Prepare frontend repo:

Push React frontend to GitHub

Set a Netlify env var:

text
REACT_APP_API_BASE=https://your-backend.up.railway.app
Build command: npm run build

Publish directory: build

Deploy:

On Netlify: “Add new site” → “Import from Git”

Set build and publish settings

Deploy

Your site will now call the backend via API

Option 3: Local Docker Development (optional)
Install Docker Desktop

Run locally:

bash
docker compose build
docker compose up
Frontend: http://localhost:3000

Backend: http://localhost:5000/api/search

Cloud Docker:

Use platforms like Render or Fly.io for container hosting

⚙️ Environment Variables
Name	Purpose
GOOGLE_API_KEY	Gemini API key (backend, required)
SERPAPI_API_KEY	SerpAPI key (backend, required for live search)
SERP_TIMEOUT	(Optional) Timeout in seconds (default 3)
GEMINI_MODEL	(Optional) Gemini model name
CACHE_TTL_S	(Optional) Cache TTL (default 120)
MAX_PROMPT_CHARS	(Optional) Max prompt length (default 4000)
REACT_APP_API_BASE	Frontend-only: Backend URL
Never commit secrets! Use Railway/Netlify environment managers or .env files locally.

🖥️ API Usage
POST /api/search

json
{
  "query": "What is Retrieval-Augmented Generation?"
}
Response:

json
{
  "query": "...",
  "search_used": true,
  "answer": "...",
  "sources": [
    { "title": "...", "link": "...", "hostname": "..." }
  ],
  "total_ms": ...,
  "search_ms": ...,
  "llm_ms": ...
}
💡 Frontend Features
Search bar with instant feedback

“Live Web Used” and “Model-only answer” banners

Numbered source chips (clickable, with tooltips)

Markdown rendering with theme styling

Loading indicators, error banners

Space-themed animated background

Responsive and accessible design

🛠️ Scripts & Local Development
Backend

Install dependencies:

bash
pip install -r requirements.txt
Start locally:

bash
python app.py
or

bash
gunicorn -w 2 -k gthread --threads 8 -b 0.0.0.0:5000 app:app
Set env vars in .env or Railway dashboard

Frontend

Install and run:

bash
npm install
npm start
Set API base in .env:

text
REACT_APP_API_BASE=http://localhost:5000
📦 Directory Structure
text
/backend        # Flask app, Procfile, requirements.txt
/front          # React app, src/, package.json
/docker-compose.yml, Dockerfile, Dockerfile.backend, nginx.conf
/.dockerignore
🏁 Example Search Queries
“Compare GPT-4 and Gemini Pro for code generation.”

“Best laptops for AI development under $1,000 (2025)”

“What happened in the latest SpaceX launch?”

🚨 Security & Best Practices
Store API keys securely and never commit them.

Monitor usage quotas on third-party APIs.

Add rate limiting for public demos if needed.

📄 License
[MIT]
Specify your project license here.

🤝 Contributing
Pull requests, issues, and suggestions welcome!

🙋 FAQ
Q: How do I run everything locally?
A: Use Docker for both, or run backend with Python/Gunicorn and frontend with npm. Point frontend .env to the backend.

Q: Can I deploy both on Railway?
A: You can, but decoupling (Railway + Netlify) is often easier for SPA apps.

Q: How do I change the theme?
A: Edit src/theme.js in the frontend.

Q: How do I extend the backend with new tools?
A: Add more Tool instances in LangChain and update the orchestration logic in app.py.
