# 💳 SME Loan Portfolio Health Dashboard

> **Sector:** Banking & Financial Services | **Tools:** SQL · Power BI | **Phase:** 1

**A development finance institution managing 1,200 SME loans is seeing NPL ratios creep up — but by the time a loan hits the NPL bucket, the intervention window has already closed. This dashboard surfaces the warning signals 60–90 days earlier.**

---

## Business Problem

A development finance institution's NPL ratios have risen for three consecutive quarters but the risk team lacks a centralized view distinguishing early-stage stress from confirmed default. This dashboard surfaces payment pattern shifts, sector clustering, and borrower size concentration that precede default — giving the risk committee time to intervene.

## Key Questions

1. Which borrower segments show early signs of payment stress?
2. Is the NPL increase driven by a specific origination cohort or broadly distributed?
3. Are there geographic clusters suggesting an external shock rather than individual credit risk?
4. What is the projected NPL rate in 90 days if current trends hold?
5. Which account officers have the highest concentration of watch-list accounts?

## Dataset

Simulated loan portfolio data modeled on CBN SME lending guidelines and IFC MSME Finance Gap benchmarks.
- 1,200 loan records · 18 months repayment history · 12 risk variables
- File: `data/sme_loan_portfolio_simulated.csv`
- ⚠️ *Clearly labeled as simulated throughout*

## Methodology

1. `sql/01_data_cleaning.sql` — Standardize loan IDs, calculate days past due, flag restructured loans
2. `sql/02_cohort_analysis.sql` — Segment loans by origination quarter, track performance over time
3. `sql/03_risk_tier_segmentation.sql` — Assign watch / substandard / doubtful flags by DPD and sector
4. `sql/04_npl_projection.sql` — 90-day forward NPL estimate based on current trend line
5. Power BI dashboard — Portfolio health heatmap, NPL trend, watchlist, sector concentration

## Key Findings

*(To be updated when built)*

## Dashboard Preview

![Portfolio Health Overview](assets/01_overview.png)
![NPL Trend and Watchlist](assets/02_watchlist.png)

## Folder Guide

| Folder | Contents |
|---|---|
| `/data` | Simulated loan portfolio CSV |
| `/sql` | Cohort, risk tier, and projection queries |
| `/dashboard` | Power BI file (.pbix) + PDF export |
| `/assets` | Dashboard screenshots |

## Insight Summary

The NPL problem is not random — it is concentrated in one origination cohort and one sector. Catching it now costs the institution a fraction of what catching it in 90 days will.

---
*Part of a 20-project data analytics portfolio. [View all projects →](https://github.com/YOUR_USERNAME)*
