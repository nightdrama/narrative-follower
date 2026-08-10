# narrative-follower

Every day, a scheduled Claude Code cloud agent pulls and summarizes the main
**bull / bear debates from X (formerly Twitter)** for a portfolio of AI-supply-chain
stocks, and commits the brief to this repo.

## What's here
- **`portfolio.txt`** — the watchlist (source of truth). US-listed names grouped into
  sections, format `TICKER | Company` (blank lines and `#`-comments ignored;
  `# --- SECTION ---` lines mark the groups). 112 names sourced from a TradingView
  "AI Supply Chain" watchlist (foreign local listings, OTC ADRs, ETFs, and duplicate
  share classes removed).
- **`prompts/cloud_daily_brief.md`** — the exact instructions the daily agent follows.
- **`reports/<DATE>_narratives.md`** — the daily deliverable.

## How the daily run works
A routine at [claude.ai/code/routines](https://claude.ai/code/routines) runs each day at
**11:00 UTC (7 AM ET)**. It:
1. Reads `portfolio.txt`.
2. For each section, makes one **xAI Grok live-search** call over X (last 2 days).
3. Synthesizes the results into a **theme-first** brief — top cross-cutting bull/bear
   debates, then a per-section pulse — and commits `reports/<DATE>_narratives.md`.

Requires `XAI_API_KEY` in the cloud environment; falls back to web search (and labels
itself as such) if the key is missing.

## Editing the portfolio
Edit `portfolio.txt` here and commit — the next run picks it up automatically.

_Output is research, not investment advice._
