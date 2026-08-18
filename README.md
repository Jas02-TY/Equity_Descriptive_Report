# Equity Descriptive Report

A [Claude Cowork](https://claude.com) skill that generates institutional-grade, five-section equity fundamental research reports as Word documents — automatically sourced from local Bloomberg exports and live web research.

## What it does

Given one or more stock tickers, this skill produces a polished `.docx` fundamental report per company, covering company overview, value drivers, industry dynamics, recent material news, and an investment conclusion with a scored recommendation — all formatted to a consistent institutional house style (HTML tables, chronological time series, cited sources, USD-normalized figures).

**Trigger phrases:** `run report for [ticker]`, `generate report`, `descriptive report for [company]`

## Repository structure

```
.
├── Macro_Skill_updated.md   # Entry point — orchestrates the full report pipeline
├── skills/
│   ├── 01_corporation.md    # Section 1: Corporation
│   ├── 02_value_driver.md   # Section 2: Value Driver
│   ├── 03_industry.md       # Section 3: Industry
│   ├── 04_news.md           # Section 4: News (material events)
│   └── 05_conclusion.md     # Section 5: Conclusion + Scorecard
└── .gitignore                # Excludes generated reports, Bloomberg data, and scorecard CSV
```

## How the pipeline works

1. **Build the ticker list** — extracts tickers from the user's request and/or scans the local Bloomberg data folder, deduplicates, and skips tickers that already have a completed report. Resolves each ticker to a full company name via web search, then asks for confirmation before proceeding.
2. **Resolve Bloomberg data** — looks for a matching `{ticker}.docx` or `{ticker}.txt` file in the Bloomberg data folder as the primary data source.
3. **Gather data** — reads any available Bloomberg file first, then fills gaps (and captures recent earnings, transcripts, competitive data, and news) via web search. Every data point is source-labeled, and Bloomberg data is never discarded in favor of web search where it already covers the required period.
4. **Write each section** — reads the corresponding skill file in `skills/` before drafting that section, in order:

   | Order | Skill file | Section |
   |-------|-----------|---------|
   | 1 | `01_corporation.md` | Corporation — fact sheet, overview, revenue & profitability, segment/geographic breakdowns, peer group (and manufacturing analysis where applicable) |
   | 2 | `02_value_driver.md` | Value Driver — sales/cost productivity, intangible assets, competitive moat, financials, ownership & governance |
   | 3 | `03_industry.md` | Industry — market sizing (TAM/SAM/SOM), competitive forces (Porter's Five Forces style), disruption threat assessment |
   | 4 | `04_news.md` | News — material events from the last 90 days, grouped by category, each tagged Positive/Negative/Neutral |
   | 5 | `05_conclusion.md` | Conclusion — investment thesis, strengths, financial sustainability, growth outlook, risks, qualitative valuation, and a 6-row scorecard |

5. **Save the report** — a single self-contained Python script (using `python-docx`) builds and saves the complete document in one step, named `{TICKER}_{CompanyName}_Fundamental_Report_{DDMonthYYYY}.docx`.
6. **Record the scorecard** — appends the finalized scorecard as one row to `scorecard_summary.csv`, without overwriting prior entries.

## Report format standards

Applied consistently across all five sections:

- **Tables:** HTML (`border="1" cellpadding="6"`), used whenever 3+ comparable data points exist; prose reserved for qualitative commentary
- **Time series:** last 5 fiscal years + up to 2 forward estimates, always chronological (oldest → newest → estimates)
- **Currency:** all monetary figures normalized to USD using period-specific FX rates, with the rate cited
- **Units:** revenue/FCF in $M (1 decimal, comma separators); margins in % (1 decimal); Y/Y margin change in bps
- **Abbreviations:** spelled out on first use (e.g. `Annual Recurring Revenue (ARR)`)
- **Citations:** every data point sourced (e.g. `"10-K FY2024"`, `"Q4 2025 earnings call"`)
- **Missing data:** marked `"-"` only after a genuine search; tables that would be mostly empty are skipped in favor of a one-line explanation
- **Document chrome:** header `Company Name | Fundamental Report | Report Date`; footer `Page X of Y | CONFIDENTIAL — For Institutional & Accredited Investor Only`

## Scoring model

The conclusion section produces a 6-row scorecard (Competitive Moat, Financial Health, Growth Outlook, Risk Assessment, Valuation, Overall View), each rated 1–5 stars. The five dimension scores sum to a total out of 25, which maps to an Overall View label:

| Total score | Rating | Overall View |
|---|---|---|
| 21–25 | ★★★★★ | Strong Buy |
| 17–20 | ★★★★☆ | Buy |
| 13–16 | ★★★☆☆ | Hold |
| 9–12 | ★★☆☆☆ | Sell |
| 5–8 | ★☆☆☆☆ | Strong Sell |

## Setup

The skill's paths are currently hard-coded to a single local machine and must be edited at the top of `Macro_Skill_updated.md` before use elsewhere:

| Purpose | Path |
|---|---|
| Bloomberg data | `.../cowork - descriptive report/bloomberg_data/` |
| Reports output | `.../cowork - descriptive report/reports/` |
| Scorecard summary | `.../cowork - descriptive report/scorecard_summary.csv` |
| Section skills | `.../cowork - descriptive report/skills/` |

Bloomberg source files must be named exactly `{ticker}.docx` or `{ticker}.txt`.

Generated reports, Bloomberg data, and the scorecard CSV are excluded from version control via `.gitignore`.

## Disclaimer

Reports produced by this skill are for institutional and accredited-investor use and do not constitute investment advice. All figures should be independently verified against primary sources before use.
