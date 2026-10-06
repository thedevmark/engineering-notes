# engineering-notes

Technical write-ups on some of the harder problems I came across.

| Paper | Topic | Stack |
|---|---|---|
| [4K60 Native Ingest](4k60-native-ingest/) | Findings from 40+ videos testing codecs, bitrates, resolutions, a Chrome extension, and native iPhone uploads | iOS media pipeline, short-form video, Video Drop |
| [Scaling Streamer Online on Cloudflare](scaling-streamer-online/) | Designing a per-user multi-overlay platform so cost-per-user stays roughly flat as you grow — edge push, Hibernatable WebSockets, EventSub | Cloudflare Workers, KV, Durable Objects, Hibernatable WebSockets, EventSub |
| [Chat bot memory](chat-bot-memory/) | Persistent memory for a Twitch chat bot without storing raw chat logs | C#, Streamer.bot, Gemini Flash |
| [Building Pathos](how-i-built-pathos/) | A worker-side job-search system connecting roles, evidence-backed resumes, application tracking, and a review-first browser extension | React 19, Vite, Supabase, Cloudflare Workers, Chrome MV3 |

---

## deutschmark's other apps

<table>
<tr><td align="center" width="56"><img src=".github/apps/pathos.svg" width="44" alt=""></td><td><a href="https://yourpathos.app"><b>Pathos</b></a><br>Worker-side job search with source-linked roles, evidence-checked resumes, and application tracking.</td></tr>
<tr><td align="center" width="56"><img src=".github/apps/markskill.svg" width="44" alt=""></td><td><a href="https://github.com/thedevmark/markskill"><b>Markskill</b></a><br>A product-engineering skill for AI agents: trace behavior to its owner, fix root causes, shape interfaces around real tasks, and verify claims with evidence.</td></tr>
<tr><td align="center" width="56"><img src=".github/apps/alert-alert.svg" width="39" alt=""></td><td><a href="https://github.com/thedevmark/alert-alert"><b>Alert! Alert!</b></a><br>Turn a video URL or local file into a cropped, trimmed stream alert.</td></tr>
<tr><td align="center" width="56"><img src=".github/apps/auto-iphone-uploader.svg" width="39" alt=""></td><td><a href="https://github.com/thedevmark/auto-iphone-uploader"><b>Auto iPhone Uploader</b></a><br>Write a video's title and captions once on your PC, then post it from the real apps on your iPhone. Early preview.</td></tr>
<tr><td align="center" width="56"><img src=".github/apps/streamer-online.png" width="44" alt=""></td><td><a href="https://streamer.deutschmark.online"><b>Streamer Online</b></a><br>Build OBS scenes and browser-source overlays with connected streamer tools.</td></tr>
<tr><td align="center" width="56"><img src=".github/apps/forgetmenot.png" width="32" alt=""></td><td><a href="https://github.com/thedevmark/forgetmenot"><b>ForgetMeNot</b></a><br>A local-first Twitch bot that remembers regulars, callbacks, and stream lore.</td></tr>
</table>

<sub>All projects → <a href="https://github.com/thedevmark">github.com/thedevmark</a></sub>
