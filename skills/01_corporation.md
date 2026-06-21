# Section: Corporation

Write seven subsections in order. All tables in HTML with `border="1" cellpadding="6"`.

**Table completeness gate (apply before writing every table in this section):**
For every time-series table, use Bloomberg as the primary source and web-search to fill only the missing years. Before building any table, check whether Bloomberg covers the full required window for every row. If any row falls short, search for the missing year(s) and label the source per data point (e.g. `"Annual Report FY2025"`, `"StockAnalysis FY2025"`). Do not publish a table with uneven year coverage across rows.Year order for all time-series tables: always chronological — oldest first, newest last, estimates after actuals. If years are on columns: left-to-right. If years are on rows: top-to-bottom. Example: `2021A → 2022A → 2023A → 2024A → 2025A → 2026E → 2027E`

---

## 1. Company Fact Sheet
One HTML table, one item per row:
HQ · IPO date · Sector · BICS classification · Reporting currency ·
Stock exchange · Index memberships · ETF memberships

## 2. Company Overview
200–300 words. Structure as short sub-paragraphs, with no bold lead-ins, no sub-paragraph labels, and no bullet points. Weave these topics naturally across paragraphs:
- Business model: core product, service, and monetisation mechanism
- Scale & reach: size, geographic footprint, customer base
- Segments & regions: how the business is organised and reported
- Strategic positioning: key competitive differentiators and strategic priorities
- Key revenue drivers: the 2–3 factors most likely to move revenue and margins

## 3. Revenue & Profitability
HTML table columns: last 5 completed fiscal years + up to 2 forward estimates.

Rows:
- Revenue ($M) · Y/Y growth (%) · 3-yr CAGR (%)
- Gross margin (%) · Y/Y change (bps)
- Operating margin (%) · Y/Y change (bps)
- Net margin (%) · Y/Y change (bps)

Observations (bullet points, each citing a specific figure or year):
- (a) Revenue trajectory: trends, inflection points, forward outlook
- (b) Margin patterns: expansion/compression drivers per margin type
- (c) Revenue quality: recurring vs. one-time revenue breakdown

## 4. Revenue by Business Segment
HTML table: Segment | Revenue $M | % of total | Y/Y% | 3-yr CAGR
Periods: last 5 years + 2 forward. Include a total row.
Break down sub-segments where disclosed.
Observations: brief intro per segment; identify the main growth engine.

## 5. Manufacturing Analysis
*(Optional — include only if the company operates physical manufacturing or fabrication facilities, e.g. semiconductor fabs, auto plants, factories. Skip for pure software, services, or asset-light businesses.)*

**(1) Manufacturing Facilities**
HTML table: Facility Location | Type | Capacity | Ownership (Owned / Leased / JV) | Geopolitical Risk Notes
List all major facilities. Where data is not publicly disclosed, note explicitly and provide qualitative assessment based on earnings call commentary or analyst reports.

**(2) Internal Business Perspective**
- Manufacturing excellence: cycle time, unit cost, yield
- Design productivity: silicon efficiency and engineering efficiency
- New product introduction: actual schedule vs. plan
Where metrics are not publicly disclosed, note explicitly and provide qualitative assessment based on earnings call commentary or analyst reports.

**(3) Innovation & Learning Perspective**
- Technology leadership: time to develop next generation
- Manufacturing learning: process time to maturity
- Product focus: percentage of products that equal 80% of sales
- Time to market: new product introduction vs. competition
Where metrics are not publicly disclosed, note explicitly and provide qualitative assessment based on earnings call commentary or analyst reports.

## 6. Revenue by Geographic Market
HTML table: Region | Revenue $M | % of total | Y/Y% | 3-yr CAGR
Periods: last 5 years + 2 forward. Include a total row.
Observations: largest current contributor + fastest-growing region.

## 7. Peer Group
BICS Level 5 preferred; fall back to BICS Level 4 or GICS Level 4.
HTML table: Company | Ticker | Market Cap | Classification | Rationale
Select 5 peers under same BICS/GICS classification, with comparable scale and business model.

---
Source citation format: `"Company 10-K FY2024"`, `"Bloomberg consensus"`, `"Q4 2025 earnings call"`
