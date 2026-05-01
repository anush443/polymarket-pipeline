# Polymarket Pipeline

AI-powered breaking-news detector that classifies events against Polymarket prediction markets and trades automatically when it finds edge. Python, asyncio-based, single-process.

## Entry Point

All commands route through `cli.py`:

- `watch` — V2 event-driven pipeline (real-time streams → classify → trade)
- `run` — V1 synchronous pipeline (RSS scan → score → log)
- `dashboard` — live terminal dashboard
- `backtest` / `calibrate` / `verify` / `niche` / `markets` / `trades` / `stats` / `scrape`

V2 (`watch`) is the recommended path. V1 (`run`) is kept for comparison/backtesting.

## Module Map

**V2 event pipeline** — `pipeline.py` orchestrates async via `news_stream.py` (Twitter/Telegram/RSS) → `matcher.py` (keyword match to niche markets) → `classifier.py` (Claude bullish/bearish/neutral + materiality) → `edge.py` (Kelly sizing) → `executor.py` (CLOB order or dry-run).

**Market data** — `markets.py` (REST: active markets, token IDs, implied prob), `market_watcher.py` (WebSocket: live prices, niche filter, momentum).

**Shared infra** — `logger.py` (SQLite: trades, news events, calibration, latency), `config.py` (env vars + thresholds), `dashboard.py` (rich-based TUI).

**V1 / analytics** — `scraper.py` (RSS), `scorer.py` (per-market scoring), `calibrator.py` (accuracy report), `backtest.py` (historical replay).

## Key Conventions

- **Models**: `CLASSIFICATION_MODEL = claude-haiku-4-5-20251001`, `SCORING_MODEL = claude-sonnet-4-6-20250514`. Don't change without updating `config.py`.
- **LLM task framing**: Claude does *classification* (bullish/bearish/neutral + materiality 0–1), not probability estimation. This is the V2 thesis — keep that contract when modifying `classifier.py` or prompts.
- **Niche markets only**: V2 filters to `MIN_VOLUME_USD < volume < MAX_VOLUME_USD` (default $1K–$500K). Don't widen this without an explicit reason — it's the moat.
- **Safety defaults**: `DRY_RUN=true`, `MAX_BET_USD=25`, `DAILY_LOSS_LIMIT_USD=100`, quarter-Kelly sizing. Never disable these silently.
- **Async everywhere in V2**: `news_stream`, `market_watcher`, `classifier.classify_async`, `executor.execute_trade_async`. V1 paths stay sync.
- **All config via env / `config.py`** — no magic numbers in business logic. New tunables go in `config.py` with an env override.
- **Persistence**: SQLite via `logger.py`. New tables/columns require a migration helper there.

## Setup / Verify

`bash setup.sh` then `python cli.py verify`. See `README.md` for env keys (only `ANTHROPIC_API_KEY` is required; Twitter/Telegram/Polymarket are optional).

---

# OpenWolf

@.wolf/OPENWOLF.md

This project uses OpenWolf for context management. Read and follow `.wolf/OPENWOLF.md` every session. Check `.wolf/cerebrum.md` before generating code. Check `.wolf/anatomy.md` before reading files.
