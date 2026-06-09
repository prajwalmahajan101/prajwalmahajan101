### Hi, I'm Prajwal 👋

Senior backend engineer (Bengaluru) — distributed fintech, robotics, and AI-integrated platforms. I design resilience kernels, push correctness invariants into Postgres, and ship LLM-powered services in production.

**Currently:** Lead architect at [Optimo Capitals](https://optimocapital.in/) — 8 of 14 internal services in 10 months. OptiView dashboard platform, the 5-service co-lending mesh, three AWS Lambda services, AA-consent ingestion.

**Previously:** Backend lead at Viamagus on Quason (VDA 5050 fleet backbone, 100+ AMRs at 10k msgs/sec, zero message loss) and Synthia (RAG legal assistant with a Word plugin agent).

#### What I work on
- Resilience kernels — circuit breakers, retries with backoff, idempotency, tiered rate limiting
- Postgres-enforced invariants — CHECK constraints, BEFORE INSERT/UPDATE triggers, durable-id dedupe
- LLM platforms — RAG pipelines, document extraction, Bedrock / Ollama / GPT-4
- Security at the lowest layer — SSRF, HMAC+nonce webhooks, Fernet, fail-closed boot

#### Building in public

> _Cadence: ships in 1–2 weekend bursts; not full-time on these. Quiet weeks ≠ stalled — they're shipping-elsewhere weeks._

**Platforms**
- [`beacon`](https://github.com/prajwalmahajan101/beacon) — self-hosted OpenTelemetry-native observability platform · M0 contract frozen ([`v0.1-m0`](https://github.com/prajwalmahajan101/beacon/releases/tag/v0.1-m0)) · M1 (Java SDK) starting
- [`BookReader`](https://github.com/prajwalmahajan101/BookReader) — terminal EPUB reader and personal library (Textual, SQLite-backed, inline kitty/sixel images, two-page mode, per-book bookmarks + stats, collections + wishlist) · Phases 1–4 shipped at [`v0.3`](https://github.com/prajwalmahajan101/BookReader/releases/tag/v0.3)

**Libraries**
- [`resilience-kit`](https://github.com/prajwalmahajan101/resilience-kit) — framework-agnostic Python resilience + core-infra kernel · retries, circuit breakers, throttles, cache, SSRF guard, DNS-pinned HTTP client, audit decorators, field crypto · pluggable backends · adapters for Django + FastAPI
- [`toymq`](https://github.com/prajwalmahajan101/toymq) — single-node persistent message broker in Go · append-only WAL with CRC framing, per-message fsync, at-least-once delivery, crash recovery · built as a Go learning exercise

**Starters & services**
- [`django_boilerplate`](https://github.com/prajwalmahajan101/django_boilerplate) — production-shaped Django 6 + DRF starter · consumes `resilience-kit`, structured envelopes, JWT + OAuth, Valkey throttles
- [`fastapi_boilerplate`](https://github.com/prajwalmahajan101/fastapi_boilerplate) — production-shaped FastAPI + async SQLAlchemy starter · same kernel, SSRF-safe HTTP, audit log, AWS Secrets Manager
- [`repay_sync`](https://github.com/prajwalmahajan101/repay_sync) — Django 5 + DRF loan-collection service · audit-logged mutations, agent-officer assignment, PTP/Refused/Partial dispositions

**Terminal tooling**
- [`pomban`](https://github.com/prajwalmahajan101/pomban) — keyboard-driven Pomodoro TUI with kanban board + stats heatmap (Textual)

**Up next** *(public repos forthcoming)*
- Go distributed-systems track — toy KV store, a 3-node Raft cluster, a multi-DB TUI (Bubble Tea)
- Postgres tooling — declarative CHECK / triggers / durable-id idempotency as a Python library

<details>
<summary><strong>Personal tooling</strong> — daily-driver dotfiles & editor config (not maintained as products)</summary>

- [`omarchy-abyss-glass`](https://github.com/prajwalmahajan101/omarchy-abyss-glass) — Hyprland dotfiles · glass-morphic waybar, layered window animations, multi-monitor wallpaper engine
- [`nvim_config`](https://github.com/prajwalmahajan101/nvim_config) — LazyVim setup tuned for backend work · ~60ms cold start

</details>

#### Writing & web
- Long-form at [dev.to/prajwalmahajan101](https://dev.to/prajwalmahajan101) and [prajwalmahajan101.hashnode.dev](https://prajwalmahajan101.hashnode.dev) — backend, distributed systems, AWS · source markdown in [`blog-posts`](https://github.com/prajwalmahajan101/blog-posts) (split into `devto/` and `hashnode/`)
- [`portfolio`](https://github.com/prajwalmahajan101/portfolio) — personal site · [live](https://portfolio-prajwal-mahajan.vercel.app)

<sub>_Feed below is injected nightly from dev.to + Hashnode RSS; may go stale between writing bursts._</sub>

<!-- BLOG-POST-LIST:START -->
<!-- BLOG-POST-LIST:END -->

#### Reach me
- Portfolio: https://portfolio-prajwal-mahajan.vercel.app
- LinkedIn: https://linkedin.com/in/prajwal-mahajan
- Email: prajwal.mahajan101@gmail.com
