---
name: cowork-descriptive-report
description: >
  Generates an institutional-grade company fundamental report as a .docx file.
  Triggers on: "run report for [ticker]", "generate report", "descriptive report for [company]".
  Reads Bloomberg data from local folder, writes report to reports folder,
  records scorecard to scorecard_summary.csv.
---

# Descriptive Report — Cowork Edition

Generates a five-section institutional buy-side fundamental report as a .docx file.

---

## Paths (edit once per machine)

| Purpose          | Path                                                                  |
|------------------|-----------------------------------------------------------------------|
| Bloomberg data   | `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\bloomberg_data\`              |
| Reports output   | `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\reports\`                     |
| Scorecard summary| `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\scorecard_summary.csv`        |
| Section skills   | `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\skills\`                      |

Bloomberg files must be named exactly: `{ticker}.docx` or `{ticker}.txt`

---

## Step 1 — Build the Ticker List

**A. From user message**
Extract any explicitly named tickers from the user's prompt (e.g. `AAPL US`, `700 HK`).

**B. From Bloomberg data folder**
If the user mentions "companies with Bloomberg data" or similar, scan:
`C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\bloomberg_data\`
Add the filename (minus extension) of every `.docx` and `.txt` file found as a ticker.

**C. Merge and deduplicate**
Combine lists A and B, removing any duplicates.

**C2. Filter already-completed tickers**
Before resolving company names, scan:
`C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\reports\`
- If a `.docx` file matching the ticker exists, skip that ticker.
- Inform the user which tickers were skipped and why.

Example:
```
Skipping 1 already-completed ticker:
  - AAPL US  — report found: AAPL_AppleInc_Fundamental_Report_30May2026.docx
```

**D. Resolve company name for each ticker**
For each ticker, web search `"{ticker} stock company name"` to resolve the full
legal company name → `{company_name}`.
- Prefer the primary-listed entity implied by the ticker suffix (e.g. `HK` → HKEX, no suffix → NYSE/NASDAQ).
- Example: ticker `AAPL` → `{company_name}` = `Apple Inc.`
- This is required before proceeding — `{company_name}` is used in the report filename and scorecard.

**E. Confirm before starting**
Print the full list of tickers (with resolved company names) to be processed and wait for user confirmation before proceeding.
Example:
```
Tickers to process (3):
  1. AAPL US   — Apple Inc.          — no Bloomberg file → web search
  2. RKT US    — Rocket Companies    — Bloomberg file found: RKT US.txt
  3. CALX US   — Calix Inc.          — Bloomberg file found: CALX US.txt
```

Then process each ticker sequentially through Steps 2–6.

---

## Step 2 — Resolve Bloomberg Data

- Look for a file at:
  `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\bloomberg_data\{ticker}.docx`
  `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\bloomberg_data\{ticker}.txt`
- If found → read it as the primary data source.
- If not found → use web search for all financial data.

---

## Step 3 — Gather Data

- If a Bloomberg file was found, read it thoroughly first.
- Then search the web for:
  - Latest earnings results and consensus estimates
  - Recent earnings call transcripts
  - Competitive landscape and market data
  - Material news from the last 90 days

**Partial data handling:**
Bloomberg files may not cover the full required period. For any metric where the
Bloomberg file covers only part of the required range:
- Extract the available years from the Bloomberg file.
- Use web search to fill only the missing years.
- Clearly label the source per data point in citations
  (e.g. `"Bloomberg FY2021–2024"`, `"10-K FY2025"`).
- Never discard Bloomberg data in favour of web search for years that are covered.

---

## Step 4 — Write Each Section

Read the corresponding skill file **before** writing each section.
Do not write a section without reading its skill file first.

| Order | Read this skill file                                                                   | Then write              |
|-------|----------------------------------------------------------------------------------------|-------------------------|
| 1     | `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\skills\01_corporation.md`   | CORPORATION             |
| 2     | `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\skills\02_value_driver.md`  | VALUE DRIVER            |
| 3     | `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\skills\03_industry.md`      | INDUSTRY                |
| 4     | `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\skills\04_news.md`          | NEWS                    |
| 5     | `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\skills\05_conclusion.md`    | CONCLUSION + SCORECARD  |

---

## Step 5 — Save the Report

**Do NOT invoke the `docx` skill. Do NOT use multiple bash commands.**
Write and run a single self-contained Python script in one bash call that:
1. Runs `pip install python-docx --quiet` at the top of the script
2. Builds the entire .docx document (all sections, all tables, all formatting) in that same script
3. Saves the file to:
   `C:\Users\JasmineTongYu\OneDrive - Golden Equator Holdings Pte Ltd\Desktop\cowork - descriptive report\reports\`

Filename format:
  `{TICKER}_{CompanyName}_Fundamental_Report_{DDMonthYYYY}.docx`
  Example: `AAPL_Apple_Inc_Fundamental_Report_30May2026.docx`

Everything must happen in one bash call — no splitting across multiple commands.

---

## Step 6 — Record the Scorecard

Scorecard recording is handled directly in `05_conclusion.md` immediately after
the scorecard is finalised — no separate extraction step required.

---

## Formatting Rules (apply across all sections)

- Tables: HTML with `border="1" cellpadding="6"`
- Sub-table headings: always present as a bold italic standalone line immediately above the table (e.g. ***Free Cash Flow — Last 5 Fiscal Years ($M)***). Never embed the heading in a preceding prose sentence.
- Sub-section labels: any named sub-topic within a section (e.g. "Threats of substitutes", "Buyer power") must be presented as a bold italic standalone line, not embedded as a lead-in to a prose paragraph.
- Data presentation: whenever 3 or more comparable data points exist (e.g. pricing tiers, regional metrics, plan features, segment breakdown), always present as an HTML table rather than embedded in prose. Reserve prose for qualitative commentary and observations only.
- Headings: Bold and Italic
- Revenue / FCF: $M, 1 decimal place, comma separators
- Margins / percentages: 1 decimal place; Y/Y change in bps
- Periods: last 5 fiscal years + up to 2 forward estimates
- Year order: always chronological — oldest first, newest last, estimates after actuals. If years are on columns: left-to-right. If years are on rows: top-to-bottom. Example: `2021A → 2022A → 2023A → 2024A → 2025A → 2026E → 2027E`
- Currency (mandatory): All monetary figures in prose and tables must be in USD. For non-US companies, convert every figure using the period-specific average FX rate and note the FX rate used (e.g. annual average for full-year figures, quarter-end for quarterly). Never leave figures in local currency.
- Abbreviations: write for a reader who is not an expert in the target company's industry. On first use of any abbreviation, acronym, or industry/technical term (e.g. ARR, NRR, GLP-1, RAN, TAM, FCF), spell out the full name with the abbreviation in parentheses — e.g. `Annual Recurring Revenue (ARR)` — then the abbreviation alone may be used thereafter. If spelling out inline would clutter a table or prose, instead add a short notation line directly beneath the table or paragraph defining the abbreviation(s), e.g. *Note: NRR = Net Revenue Retention; ARPU = Average Revenue Per User.* Universally known terms (e.g. USD, CEO, IPO, GDP) are exempt.
- Prose style (mandatory for all narrative sections): Write as flowing narrative prose. Integrate figures naturally into sentences rather than chaining facts with semicolons. Avoid data-dump style.
- Citations: source after every data point — e.g. `"10-K FY2024"`, `"Q4 2025 earnings call"`
- Missing data: use `"-"` only after genuinely searching; never fabricate
- Empty tables: if all or the majority of cells would be N/A or N/D, skip the table entirely. Instead, state in one sentence why the data is unavailable and cite the source.
- Page header: Company Name | Fundamental Report | Report Date
- Page footer: Page X of Y | CONFIDENTIAL — For Institutional & Accredited Investor Only
