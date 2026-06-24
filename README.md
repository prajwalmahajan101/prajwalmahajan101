### Hi, I'm Prajwal 👋

Senior backend engineer (Bengaluru) — distributed fintech, robotics, and AI-integrated platforms. I build **resilience kernels**, push correctness invariants into **Postgres**, and ship **LLM-powered services** in production. On the side, I'm rebuilding the bottom of the distributed-systems stack — broker, KV, consensus — from scratch in Go.

> **Track record at a glance** — 8 of 14 internal services shipped in 10 months at a regulated fintech · 100+ AMRs coordinated at ~10k msgs/sec with zero observed message loss · `resilience-kit` on PyPI (kernel extracted from prod) · `toymq` v1.3 + `toykv` v1.0 + `toyraft` in-flight (consensus, 91 commits in 6 days) · `beacon` SDK at **p99 = 6,360 ns** per emit.

**Currently** — Lead architect at [Optimo Capitals](https://optimocapital.in/): OptiView dashboard platform, the 5-service co-lending mesh (sole author of 4 of 5 repos), three AWS Lambda services, AA-consent pipeline. Platform-wide since the resilience-kernel rollout: latency came down hard, DB load came down harder, and uptime moved from "good enough" to "boring" — the shape of the work is open-sourced as [`resilience-kit`](https://github.com/prajwalmahajan101/resilience-kit).

**Previously** — Backend lead at Viamagus on **Quason** (VDA 5050 fleet backbone — 100+ AMRs at ~10k msgs/sec, zero observed message loss in production) and **Synthia** (RAG legal assistant with a Word plugin agent on GPT-4).

#### What I work on

- **Resilience kernels** — circuit breakers, retries with backoff + jitter, idempotency, tiered rate limiting, DLQs
- **Postgres-enforced invariants** — CHECK constraints, BEFORE INSERT/UPDATE triggers, durable-id dedupe, declarative migrations
- **LLM platforms** — RAG pipelines, structured document extraction, Bedrock / Ollama / GPT-4 routing
- **Security at the lowest layer** — SSRF guards, HMAC + nonce webhooks, Fernet field crypto, fail-closed boot, audit logging

#### How it fits together

```mermaid
flowchart TB
    subgraph KERNEL["resilience kernel — the thesis"]
        K["resilience-kit<br/>PyPI v0.1.0"]
    end

    subgraph PRIMITIVES["distributed-systems primitives — from-scratch Go"]
        direction LR
        P1["toymq<br/>broker · v1.3.0"]
        P2["toykv<br/>KV store · v1.0.0"]
        P3["toyraft<br/>consensus · in-flight"]
    end

    subgraph PLATFORMS["platforms"]
        B["beacon<br/>OTel observability<br/>Java SDK · p99 6.36µs"]
    end

    subgraph STARTERS["production starters — consume the kernel"]
        direction LR
        C1["django_boilerplate<br/>v0.1.0"]
        C2["fastapi_boilerplate<br/>v1.0.0"]
    end

    subgraph APPS["applications & services"]
        direction LR
        A1["BookReader<br/>EPUB TUI · v1.0.0"]
        A2["pomban<br/>Pomodoro TUI · v0.3.0"]
        A3["repay_sync<br/>loan-collection API"]
    end

    subgraph DEVTOOLS["developer tooling"]
        T1["claude-skills-pack<br/>sb · code_assist · unabridged"]
    end

    K --> C1
    K --> C2
    P1 -.composes.-> APPS
    P2 -.composes.-> APPS
    P3 -.feeds future toy-messenger.-> APPS

    classDef shipped fill:#1f6f3a,stroke:#0d3a1e,color:#fff;
    classDef active  fill:#b97a00,stroke:#6e4900,color:#fff;
    class K,P1,P2,B,C1,C2,A1,A2,A3,T1 shipped;
    class P3 active;
```

<sub>Green = shipped & stable · amber = in-flight.</sub>

#### Building in public

> _Cadence: episodic — concentrated weekday-evening sessions (Tue / Fri dominant, with occasional full-day pushes), not weekends. The public surface ships in bursts; the day job is full-time. Silent stretches mean shipping elsewhere, not stalled._

**Libraries** *(the thesis — everything else consumes these)*
- [`resilience-kit`](https://github.com/prajwalmahajan101/resilience-kit) — framework-agnostic Python resilience + core-infra kernel · retries, circuit breakers, throttles, cache, SSRF guard, DNS-pinned HTTP client, audit decorators, field crypto · pluggable backends · adapters for Django + FastAPI · stable [`v0.1.0`](https://github.com/prajwalmahajan101/resilience-kit/releases/tag/v0.1.0) on PyPI · [write-up on dev.to](https://dev.to/prajwalmahajan101/building-resilience-kit-a-python-resilience-kernel-forged-in-production-5973)

**Distributed systems learning track** *(building the bottom of the stack from scratch in Go — broker · KV · consensus)*
- [`toymq`](https://github.com/prajwalmahajan101/toymq) — single-node persistent message broker · append-only WAL with CRC framing, per-message fsync, at-least-once delivery, crash recovery · [`v1.3.0`](https://github.com/prajwalmahajan101/toymq/releases/tag/v1.3.0) adds Prometheus + OpenTelemetry observability · [write-up on dev.to](https://dev.to/prajwalmahajan101/building-toymq-a-from-scratch-persistent-message-broker-in-go-ob7)
- [`toykv`](https://github.com/prajwalmahajan101/toykv) — single-node persistent KV store · RESP2 codec, concurrent-safe INCR, AOF persistence with crash recovery, TTL (lazy + sweep) · ships with `toykv-cli` + `toykv-tui` + a chaos harness + goreleaser binaries · stable [`v1.0.0`](https://github.com/prajwalmahajan101/toykv/releases/tag/v1.0.0) · [write-up on dev.to](https://dev.to/prajwalmahajan101/building-toykv-a-from-scratch-persistent-kv-in-go-and-why-i-took-the-opposite-call-from-toymq-5862)
- [`toyraft`](https://github.com/prajwalmahajan101/toyraft) — Raft consensus from the paper, in Go · spec-first (PRD/HLD/LLD + 9 ADRs before code), deterministic test infra (`Fake` clock + `inproc` chaos transport with drop/delay/reorder/partition + seed-split RNG), Figure 7 election-timeout table-driven test, **1000-seed at-most-one-leader-per-term invariant** · phases 1 → 5 closed in 6 days; replication next · `v1.0.0` target Jul 6 (file storage + torn-tail recovery + Porcupine linearizability gate)

**Platforms**
- [`beacon`](https://github.com/prajwalmahajan101/beacon) — self-hosted OpenTelemetry-native observability platform (logs / traces / metrics) · Kafka buffer, polyglot storage (Elasticsearch + wide-column NoSQL + TSDB), React console, Java + Python SDKs · spec-first: JSON Schema + multi-language conformance suite frozen at [`v0.1-m0`](https://github.com/prajwalmahajan101/beacon/releases/tag/v0.1-m0) **before any SDK code shipped** · Java SDK now at M1.7 — production `BeaconLogbackAppender` + Spring Boot auto-config + ReDoS-resistant redactor + OTel Context/MDC propagation + **JMH benchmark: p99 = 6,360 ns per emit** · 12/12 conformance scenarios green · Maven Central release next
- [`BookReader`](https://github.com/prajwalmahajan101/BookReader) — terminal EPUB reader and personal library (Textual, SQLite-backed) · inline kitty / iTerm2 / WezTerm / sixel images, two-page mode, per-book bookmarks + stats, collections + wishlist · stable [`v1.0.0`](https://github.com/prajwalmahajan101/BookReader/releases/tag/v1.0.0) with a [docs site](https://prajwalmahajan101.github.io/BookReader/) · `pipx install bookreader-tui`
- [`pomban`](https://github.com/prajwalmahajan101/pomban) — keyboard-driven Pomodoro TUI with kanban board + stats heatmap, themes, hooks, plugins (Textual) · [`v0.3.0`](https://github.com/prajwalmahajan101/pomban/releases/tag/v0.3.0)

**Starters & services**
- [`fastapi_boilerplate`](https://github.com/prajwalmahajan101/fastapi_boilerplate) — production-shaped FastAPI + async SQLAlchemy starter · consumes `resilience-kit` v0.1.0 · stable [`v1.0.0`](https://github.com/prajwalmahajan101/fastapi_boilerplate/releases/tag/v1.0.0) · Redis-backed resilience, SSRF-safe HTTP, request-id audit log, security middleware, Alembic, Docker
- [`django_boilerplate`](https://github.com/prajwalmahajan101/django_boilerplate) — production-shaped Django 6 + DRF starter · consumes `resilience-kit` v0.1.0 · first tagged [`v0.1.0`](https://github.com/prajwalmahajan101/django_boilerplate/releases/tag/v0.1.0) · typed exceptions, structured response envelopes, JWT + OAuth, Valkey throttles, AWS Secrets Manager overlay, Docker
- [`repay_sync`](https://github.com/prajwalmahajan101/repay_sync) — Django 5 + DRF loan-collection service · audit-logged mutations, agent-officer assignment, call / field-visit interactions with PTP / Refused / Partial dispositions, JWT, MPTT

**Developer tools**
- [`claude-skills-pack`](https://github.com/prajwalmahajan101/claude-skills-pack) — bundle of three [Claude Code](https://claude.com/claude-code) skills, each independently installable · **sb** (persistent second-brain — captures Claude Code conversations into an Obsidian vault, analyzes them into lessons / kanban / topics / cross-project connections; 22 `/sb:*` commands, 5 hooks) · **code_assist** (atomic git commits, stack-aware code reviews, phase-journal entries; 7 commands, 3 subagents) · **unabridged** (forces complete, untruncated output)

**Up next** *(public repos forthcoming — target Q3 2026)*
- `go_boilerplate` — production-shaped Go REST starter; closes the boilerplate trio (Django · FastAPI · Go)
- `toylock` — distributed lock service on `toyraft` (leases + fencing tokens + watches); proves the Raft layer in anger
- `toy-messenger` — TUI-only E2E-encrypted chat composing toymq + toykv into one user-facing artifact
- `resilience-kit-go` — Go port of `resilience-kit` · same kernel (retries, breakers, throttles, SSRF guard, audit decorators) for Go services

<details>
<summary><strong>Personal tooling</strong> — daily-driver dotfiles & editor config (not maintained as products)</summary>

- [`omarchy-abyss-glass`](https://github.com/prajwalmahajan101/omarchy-abyss-glass) — Hyprland dotfiles · glass-morphic waybar, layered window animations, multi-monitor wallpaper engine
- [`nvim_config`](https://github.com/prajwalmahajan101/nvim_config) — LazyVim setup tuned for backend work · ~60ms cold start
- [`VaultTemplate`](https://github.com/prajwalmahajan101/VaultTemplate) — Obsidian vault template for bootstrapping a notes workspace

</details>

#### Writing & web

- Long-form at [dev.to/prajwalmahajan101](https://dev.to/prajwalmahajan101) and [prajwalmahajan101.hashnode.dev](https://prajwalmahajan101.hashnode.dev) — backend, distributed systems, AWS · source markdown lives in [`blog-posts`](https://github.com/prajwalmahajan101/blog-posts) (split into `devto/` and `hashnode/`)
- [`portfolio`](https://github.com/prajwalmahajan101/portfolio) — personal site · [live](https://prajwalmahajan.in)

<sub>_Feed below is injected nightly from dev.to + Hashnode RSS; may go stale between writing bursts._</sub>

<!-- BLOG-POST-LIST:START -->
- 📝 **[Building toykv: a from-scratch persistent KV in Go, and why I took the opposite call from toymq three times](https://dev.to/prajwalmahajan101/building-toykv-a-from-scratch-persistent-kv-in-go-and-why-i-took-the-opposite-call-from-toymq-5862)** <sub>· Jun 17, 2026</sub>
- 📝 **[Building resilience-kit: A Python Resilience Kernel Forged in Production](https://dev.to/prajwalmahajan101/building-resilience-kit-a-python-resilience-kernel-forged-in-production-5973)** <sub>· Jun 11, 2026</sub>
- 📝 **[Building toymq: a from-scratch persistent message broker in Go](https://dev.to/prajwalmahajan101/building-toymq-a-from-scratch-persistent-message-broker-in-go-ob7)** <sub>· Jun 9, 2026</sub>
- 📝 **[Mastering Clean Code: Effective Naming Conventions for Developers](https://prajwalmahajan101.hashnode.dev/mastering-clean-code-effective-naming-conventions-for-developers)** <sub>· Jun 30, 2024</sub>

<!-- BLOG-POST-LIST:END -->

#### Reach me

- Portfolio: https://prajwalmahajan.in
- LinkedIn: https://linkedin.com/in/prajwal-mahajan
- Email: prajwal.mahajan101@gmail.com
