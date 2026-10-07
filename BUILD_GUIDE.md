# Project 04 - SME Loan Portfolio Health: an early-warning system for a Canadian lender

### Build guide (illustrative data; you build it, this is the map)

Goal: give a lender a way to see which small-business loans are heading for default 60 to 90 days before they get there, while something can still be done about it, and to show where the book is leaking so origination can be tightened. Built on an illustrative 1,200-loan Canadian portfolio. Data is simulated and labelled as such.

## 1. The situation
A Canadian lender holds 1,200 small-business loans across five provinces and six sectors. Its non-performing loan (NPL) rate is creeping up, but the current reporting only tells leadership a loan has gone bad once it crosses 90 days past due. By then the borrower is usually too far gone to recover, and the loss is booked. The lender needs to act earlier, on loans that are still performing or only lightly delinquent but carry the markers of the loans that later default.

**The one-sentence problem:** we find out a loan is bad only after the window to save it has closed, and we cannot say which sectors, provinces, officers, or loan features are driving the losses.

## 2. Decision-maker
- **Primary:** the **Head of Credit Risk** who sets provisioning and decides which accounts get worked out early.
- **Secondary:** the **Chief Lending Officer** (origination policy: which sectors and collateral types to tighten) and the **portfolio managers** who make the calls on individual accounts.

They want two things: a ranked list of accounts to intervene on now, and a clear read on where the book is structurally weak.

## 3. Problem statement
The NPL rate is rising and the lender cannot see it coming. This project builds a portfolio-health baseline (where the risk sits), an early-warning score that flags performing and lightly delinquent loans likely to migrate to NPL, and an origination read on which sectors, provinces, officers, and collateral profiles produce the most loss.

## 4. Key questions
1. How big is the problem? Overall NPL rate and portfolio-at-risk (PAR30, PAR90), in dollars and share of book.
2. Where does the risk concentrate? NPL and PAR by sector, province, loan officer, and collateral type.
3. What are the markers of a loan that goes bad? How do collateral coverage, interest rate, sector, and loan size differ between performing and non-performing loans?
4. Which performing or early-DPD loans look most like the loans that later defaulted? (the early-warning score)
5. What is the expected loss on the book, and how much of it sits in the accounts we could still act on?
6. Where should origination tighten to stop the leak at the source?

## 5. Data model
One table at loan grain: `data/sme_loan_portfolio_canada.csv` (1,200 rows). See `data/DATA_DICTIONARY.md`.

Derived fields to build early:
| Field | Definition |
|---|---|
| `is_npl` | 1 if dpd_bucket = NPL (>90) else 0 |
| `at_risk_30` | 1 if days_past_due > 30 |
| `under_secured` | 1 if collateral_coverage_ratio < 1.0 |
| `pd_bucket` | probability-of-default weight by DPD bucket (Current low -> NPL high) |
| `expected_loss` | principal_cad x pd_bucket x (1 - min(coverage,1)) |
| `early_warning_score` | 0-100 from DPD stage, coverage, sector risk, and rate |

## 6. KPIs
| KPI | Definition | Why it matters |
|---|---|---|
| NPL rate | NPL principal / total principal | Headline credit quality. |
| PAR30 / PAR90 | principal past 30 / 90 days / total | The risk already in motion. |
| Expected loss | sum of per-loan expected loss | The dollars at stake. |
| Recoverable share | expected loss in performing + early-DPD / total expected loss | The prize still on the table. |
| Origination loss rate | NPL rate by officer / sector / collateral | Where to tighten the tap. |

Always convert rates into dollars. "An 13% NPL rate" only lands once it reads as dollars of principal the lender may not get back.

## 7. Build it - step by step
- **Excel/Power Query:** load the CSV, add the derived fields, first cut of NPL and PAR by sector and province.
- **SQL (SQLite):** the KPI engine. One query per key question - portfolio health, concentration, the performing-vs-NPL profile, the early-warning score, expected loss.
- **Python:** if you want, a simple model to rank early-warning loans (logistic regression of is_npl on coverage, rate, sector, size) and validate the score.
- **Datawrapper / Power BI:** the health dashboard and the charts.

## 8. Charts (Datawrapper / Power BI)
| Question | Chart |
|---|---|
| How bad, and moving which way | NPL rate and PAR, headline numbers |
| Where risk concentrates | NPL rate by sector and province (bar / heat map) |
| Markers of a bad loan | coverage and rate, performing vs NPL (grouped bar) |
| Early-warning list | top flagged accounts (table) |
| Where to tighten | expected loss by officer / collateral (bar) |

## 9. Recommendation and impact
A ranked intervention list (the accounts to work now), a provisioning read (expected loss and how much is still recoverable), and an origination change (which sectors, collateral types, or officers to tighten), each tied to dollars.

## 10. Limitations
Data is simulated and illustrative, not a real institution's book. The probability-of-default weights are assumptions, not a fitted model, unless you fit one in Python. A real early-warning system would use repayment history over time, not a single snapshot, and would be validated on outcomes.
