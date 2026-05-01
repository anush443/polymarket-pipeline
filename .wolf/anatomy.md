# anatomy.md

> Auto-maintained by OpenWolf. Last scanned: 2026-05-01T15:17:06.484Z
> Files: 23 tracked | Anatomy hits: 0 | Misses: 0

## ./

- `.gitignore` — Git ignore rules (~19 tok)
- `backtest.py` — import: fetch_resolved_markets, run_backtest (~2535 tok)
- `calibrator.py` — import: check_resolutions, get_report (~1334 tok)
- `classifier.py` — import: classify, classify_async (~1147 tok)
- `CLAUDE.md` — Polymarket Pipeline (~709 tok)
- `cli.py` — cmd_watch, cmd_run, cmd_backtest, cmd_calibrate + 6 more (~4698 tok)
- `config.py` (~689 tok)
- `dashboard.py` — PipelineState: run_scan_cycle, make_layout, render_header, render_status + 4 more (~3947 tok)
- `edge.py` — import: detect_edge, detect_edge_v2, size_position (~973 tok)
- `executor.py` — execute_trade, execute_trade_async (~978 tok)
- `logger.py` — init_db, log_trade, log_news_event, log_calibration + 8 more (~2988 tok)
- `market_watcher.py` — class: price_change, get_niche_markets, refresh_markets, run + 3 more (~2050 tok)
- `markets.py` — import: implied_probability, fetch_active_markets, filter_by_categories, get_token_id (~2054 tok)
- `matcher.py` — extract_keywords, match_news_to_markets, match_news_to_markets_broad (~1178 tok)
- `news_stream.py` — class: age_seconds, setup_rules, stream, stream + 3 more (~3302 tok)
- `pipeline.py` — PipelineV2: run, run_pipeline_v2, run_pipeline (~2897 tok)
- `README.md` — Project documentation (~1715 tok)
- `requirements.txt` — Python dependencies (~56 tok)
- `scorer.py` — score_market, filter_news_for_market (~1322 tok)
- `scraper.py` — import: age_hours, scrape_rss, scrape_newsapi, deduplicate + 1 more (~1183 tok)
- `setup.sh` — Polymarket Pipeline V2 — One-Command Setup (~1272 tok)

## .claude/

- `settings.json` (~441 tok)

## .claude/rules/

- `openwolf.md` (~313 tok)
