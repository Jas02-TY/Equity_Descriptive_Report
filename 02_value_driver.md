# Section: Value Driver

Six subsections. All comparison tables: company in row 1, then 5 peers.
All tables HTML with `border="1" cellpadding="6"`.

**Table completeness gate (apply before writing every table in this section):**
For every time-series table, use Bloomberg as the primary source and web-search to fill only the missing years. Before building any table, check whether Bloomberg covers the full required window for every row (subject company and all peers). If any row falls short, search for the missing year(s) and label the source per data point (e.g. `"Annual Report FY2025"`, `"StockAnalysis FY2025"`). Do not publish a table with uneven year coverage across rows.
Year order for all time-series tables: always chronological — oldest first, newest last, estimates after actuals. If years are on columns: left-to-right. If years are on rows: top-to-bottom. Example: `2021A → 2022A → 2023A → 2024A → 2025A → 2026E → 2027E`

---

## 1. Sales Productivity
- Price premium analysis: innovation, brand, customer lock-in, price discipline.
- Price/volume mix decomposition if disclosed in filings.
- HTML table: Revenue Y/Y growth (%) — company vs. 5 peers — last 5 years.
- HTML table: Product-wise ASP if available.
- HTML table: Gross margin (%) — company vs. 5 peers — last 5 years.

## 2. Cost Productivity
Three separate HTML tables (company row 1, 5 peers, last 5 years):
- Operating margin (%)
- R&D expense as % of revenue
- SG&A expense as % of revenue

Assessment: innovative business methods, unique resources, economies of scale,
scalable product/process.

## 3. Intangible Asset Analysis
Intangibles excl. goodwill (patents, IP, trademarks, licenses):
- Size as % of total assets
- Relationship between R&D spend and asset development
- Role in competitive moat

Goodwill:
- Size as % of total assets
- Whether acquisitions appear value-creating or potentially overpriced

## 4. Competitive Moat Assessment
Moat sources: assess each using an HTML table:
Moat Source | Assessment | Trajectory (Widening / Stable / Narrowing) | Evidence
Cover: cost advantages · switching costs · network effect · efficient scale · intangible assets.
One row per source. Evidence must cite a specific figure or source.

Replication barrier: Identify 2–3 structural advantages that a well-funded competitor could not replicate within 12–24 months. 
For each, explain the specific barrier (e.g. proprietary data, regulatory licence, network density, accumulated switching costs). 
Present as an HTML table: Advantage | Barrier to Replication | Estimated Timeframe to Copy

Vulnerability map: top 3–5 realistic scenarios where the moat gets destroyed.

## 5. Financial Perspective
- HTML table: FCF ($M) and Y/Y growth — last 5 completed fiscal years
- HTML table: Revenue by business segment — last 8 completed fiscal quarters.
  Columns: Segment | QX 20XXA | QX 20XXA | ... (chronological, oldest left)
  Rows per segment: Revenue ($M) · Q/Q growth (%) · Y/Y growth (%)
- HTML table: Profitability by business segment — last 8 completed fiscal quarters.
  Use the most granular metric disclosed (in order of preference: segment operating income,
  segment EBIT, segment gross profit). Label the metric used explicitly.
  Columns: Segment | QX 20XXA | QX 20XXA | ... (chronological, oldest left)
  Rows per segment: metric ($M) · margin (%)
- HTML table: ROIC (%) and ROE (%) — last 5 years; include prosperity
  insight and basic volatility analysis

## 6. Ownership & Governance / Managerial Strategy
 
**Ownership:**
- HTML table: Top 5 institutional holders (Name | Shares | % Outstanding | Filing Date)
- HTML table: Top 5 insider holders (Name | Shares | % Outstanding | Role | Filing Date)
- Free float %; shareholding structure and control mechanism; 
  group structure (parent entity, subsidiaries, strategic holding)

**Organisation Health & Management Quality:**

HTML table for board composition (quick-scan stats):
Columns: Metric | Value | Notes
Rows: Independent directors (%) · Board size · Female directors (%) · Average tenure (years) · Key committees present

Then prose for the following (logic and context matter here):
- Management changes and succession: key members with name, role, start date/tenure
- Capital allocation track record: M&A, buybacks, dividends — assess whether ROIC/ROA improved post-deployment
- Guidance accuracy and execution consistency: cite specific instances where management beat, met, or missed guidance

**Future Growth Outlook (from earnings calls / investor days):**
- Strategic positioning
- AI strategy, opportunities, and management commentary on AI risks
- Forward guidance highlights

---
Source citation format: `"Company 10-K FY2024"`, `"Bloomberg BQL"`, `"Q3 2025 earnings call"`
