# ds_AbhayKrishna

## Overview
Explore the relationship between trader performance and market sentiment (Fear & Greed Index). The workflow merges trade-level history with daily sentiment, engineers performance metrics, and summarizes how outcomes vary across sentiment regimes.

## What the notebook does
- Load data
	- `csv_files/historical_data.csv` (trades)
	- `csv_files/fear_greed_index.csv` (daily sentiment)
- Time handling & merge
	- Parse `Timestamp IST` with day-first format and normalize to daily `date`.
	- Left-join on `date` to attach sentiment `value` (score) and `classification` (label).
- Cleanup
	- Drop non-analytical fields: `Account`, `Coin`, `Timestamp IST`, `Start Position`, `Transaction Hash`, `Order ID`, `Trade ID`, `Crossed`, `Timestamp`.
	- Keep direction as `Side` (fallback to `Direction` if needed).
- Analysis & metrics
	- By sentiment bucket: trades, win rate, weighted return, average PnL, average size.
	- Daily metrics: trades, total PnL, average sentiment.
	- Stats: Spearman correlation (sentiment vs per-trade return), Mann–Whitney U (Extreme Fear vs Extreme Greed).

## Generated artifacts
- Plots (in `outputs/`)
	- `avg_pnl_by_sentiment.png`
	- `avg_volume_by_sentiment.png`
	- `sentiment_score_vs_pnl.png`
	- `trade_direction_by_sentiment.png`

## Quick start
1) Open `notebook_1.ipynb` and run all cells.
2) Ensure `dayfirst=True` when parsing `Timestamp IST`.
3) After merge, verify coverage (count of non-null `classification`) and inspect missing values.

## Notes
- If your `historical_data.csv` contains multiple assets, keep `Coin` and group by asset before dropping.
- Align timezone if you derive intraday features; here we use normalized daily dates for sentiment alignment.
