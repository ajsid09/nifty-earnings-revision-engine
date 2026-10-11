# nifty-earnings-revision-engine

Ranks Nifty 50 constituents by the direction and breadth of analyst
EPS estimate revisions. Built on free data (yfinance).

## Result
No detectable predictive power. Spearman rho = -0.17 vs forward 21d
returns, p = 0.275, sign unstable across 5-63d horizons.

With n=48 over a single overlapping period, this is a statement about
the test's power, not about the factor.

## Method
- Consensus FY1 EPS, current vs 7/30/60/90 days ago
- Magnitude: % drift in consensus
- Breadth: (up - down) / (up + down + k), k=8 shrinkage
- Winsorised z-scores, 0.55 / 0.45 weighting
- Signal lagged 30d, tested against forward returns

## Data quality issues found
- Missing estimates returned as 0, not null
- Analyst-panel changes masquerading as revisions (+37% with 0 upgrades)
- Breadth ratios on n=1 ranked alongside n=31
- Ticker drift: TATAMOTORS -> TMPV (demerger), LTIM -> LTM (rebrand)

## Known limitations
Single period, no power. Fiscal-year rollover unhandled (Indian FY ends
March). Survivorship bias from current-day ticker list. Weights unfitted.

## Run it
Open `revision_engine.ipynb` in Colab. No API key required.
