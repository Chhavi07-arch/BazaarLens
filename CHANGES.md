# BazaarLens — Changelog

All significant changes to the codebase are documented here.  
Format: `[version] — date — phase/branch — description`

---

## [Unreleased] — Pre-build Planning

### 2026-06-13 — `main` — Initial repository setup

#### Added
- `CLAUDE.md` — Full architecture reference and project memory for all Claude Code sessions
- `README.md` — Project overview and getting started guide
- `docs/api.md` — Complete API contract specification for all 11 backend endpoints
- `docs/blueprint.md` — 30-hour engineering blueprint with milestone dependency chart
- `implementation.md` — Phased implementation plan (7 phases, branch-per-phase, commit-per-subtask)
- `CHANGES.md` — This file
- `.gitignore` — Node, Python, Rust, environment, and OS artifact exclusions
- `.claude/memory/MEMORY.md` — Claude Code memory index (persists across sessions)
- `.claude/memory/project_context.md` — Hackathon context, judging weights, team constraints
- `.claude/memory/tech_decisions.md` — LLM model choices, auth strategy, push notification constraints

#### Architecture Decisions Recorded
- **Backend:** Rust + Axum + Tokio (replaced original FastAPI plan)
- **Database:** SQLite (embedded in Rust backend, volume-mounted on Railway) — replaced Supabase for full code ownership
- **Frontend:** Next.js 14 (App Router) + TypeScript + TailwindCSS + shadcn/ui
- **PWA library:** `@ducanh2912/next-pwa` (replaces `next-pwa` v5 — incompatible with App Router)
- **Barcode scanner:** `@zxing/browser` (BarcodeDetector API not supported in Safari)
- **LLM:** DeepSeek V4 via OpenRouter (primary), Minimax M3 (vision fallback)
- **Auth:** None — `device_id = crypto.randomUUID()` in localStorage, passed as `X-Device-Id` header
- **Monorepo:** `frontend/` + `backend/` in single repo, Cargo workspace at root
- **Principles:** SOLID enforced across all phases, conventional commits, well-commented code

#### Repository
- Remote: `https://github.com/sanaa-duhh/BazaarLens`
- Local: `/Users/sanaaara/Codes/bazaarlens` (renamed from `IQOOhackathon`)
- Branch: `main`

---

## Upcoming — Phase 1 (`feat/phase-1-foundation`)

> Not yet started. Will be recorded here after merge.

### Expected Changes
- Rust/Axum backend scaffold with all dependencies
- SQLite schema (5 tables, indexes, migrations via sqlx)
- `AppError` unified error type
- `/health` endpoint
- Next.js 14 frontend scaffold with Tailwind + shadcn/ui
- PWA configuration
- Root layout with dark theme and bottom navigation shell
- `types/index.ts`, `lib/utils.ts`, `lib/api.ts` stubs

---

## Upcoming — Phase 2 (`feat/phase-2-scanning`)

> Blocked on Phase 1.

### Expected Changes
- `ProductSource` trait + `OpenFoodFacts` + `UpcItemDb` implementations
- `LlmService` (OpenRouter client with vision support)
- `POST /api/scan/barcode` and `POST /api/scan/image` routes
- `useScanner` hook (ZXing)
- `BarcodeScanner`, `ImageUpload`, `ScanResult`, `CameraPermissionDenied` components
- `/scan` page with full state machine

---

## Upcoming — Phase 3 (`feat/phase-3-intelligence`)

> Blocked on Phase 2.

### Expected Changes
- Intelligence card prompt template
- `POST /api/intelligence` route with SQLite cache
- `IntelligenceCard` with stagger animation
- `RecommendationBadge`, `PricingInsight`, `ReviewInsight`, `MarketInsight` components
- `/product/[id]` page

---

## Upcoming — Phase 4 (`feat/phase-4-watchlist`)

> Blocked on Phase 3.

### Expected Changes
- `POST`, `GET`, `DELETE /api/watchlist` routes
- `useWatchlist` hook with SWR
- `WatchlistCard`, `EmptyWatchlist` components
- `BottomNav` persistent navigation
- `/watchlist` page

---

## Upcoming — Phase 5 (`feat/phase-5-push`)

> Blocked on Phase 4.

### Expected Changes
- `PushService` with VAPID, 410 handling, SQLite cleanup
- `POST`, `DELETE /api/push/subscribe` routes
- `manifest.json` (PWA, `display: standalone`)
- Service worker push + notificationclick handlers
- `usePushNotifications` hook with iOS standalone guard
- `AddToHomeScreenModal`, `EnableAlertsCard` components

---

## Upcoming — Phase 6 (`feat/phase-6-strategy`)

> Blocked on Phase 5.

### Expected Changes
- Strategy prompt template (4-section multi-perspective)
- `event_simulator` background task service
- `POST /api/events/simulate` (returns immediately, background push + strategy)
- `POST /api/strategy` with SQLite cache
- `EventBanner`, `AIOpinionCard`, `FinalDecisionCard`, `StrategyLoadingState` components
- `/strategy/[eventId]` page with sequential reveal animation
- `/admin` page (demo trigger, key-guarded)

---

## Upcoming — Phase 7 (`feat/phase-7-polish`)

> Blocked on Phase 6.

### Expected Changes
- PWA icons (192, 512, maskable, badge-72)
- Error boundaries on all pages
- Haptic feedback on product identified + watchlist add
- Lighthouse PWA score ≥ 90
- Demo rehearsal checklist in `docs/demo-flow.md`
- Final audit: no `console.log`, no TypeScript errors, no Rust warnings
