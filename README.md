# engineering-notes

Technical write-ups on some of the harder problems I came across.

| Paper | Topic | Stack |
|---|---|---|
| [RLS silently disabled my GIN index](rls-fts-planner/) | Why a public text search 500'd for anonymous users only: `@@` is not leakproof, so row security refused the index and every search became a 10s seq scan | PostgreSQL 17, RLS, GIN, tsvector, Supabase |
| [Scaling streaming toolsets on Cloudflare](scaling-streaming-toolsets/) | Designing a per-user multi-overlay platform so cost-per-user stays roughly flat as you grow — edge push, Hibernatable WebSockets, EventSub | Cloudflare Workers, KV, Durable Objects, Hibernatable WebSockets, EventSub |
| [Chat bot memory](chat-bot-memory/) | Persistent memory for a Twitch chat bot without storing raw chat logs | C#, Streamer.bot, Gemini Flash |
| [Building Pathos](how-i-built-pathos/) | A worker-side job-search system connecting roles, evidence-backed resumes, application tracking, and a review-first browser extension | React 19, Vite, Supabase, Cloudflare Workers, Chrome MV3 |
| [Inbound job-status sync](email-sync/) | Privacy-first status detection from emails users choose to forward, with guarded updates and review | Supabase Edge Functions, TypeScript, Resend |
