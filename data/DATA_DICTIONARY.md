# Data dictionary - SME Loan Portfolio (illustrative, Canadian)

`sme_loan_portfolio_canada.csv` - 1,200 small-business loans held by a Canadian lender (a credit union or business bank). Data is simulated for illustration; it is modelled on how a Canadian small-business loan book behaves, not drawn from a real institution. Labelled illustrative throughout.

| Column | Meaning |
|---|---|
| `loan_id` | Unique loan identifier. |
| `sector` | Borrower's industry: Retail trade, Construction, Agriculture, Transportation & warehousing, Manufacturing, Professional services. |
| `principal_cad` | Original loan amount, Canadian dollars. |
| `tenure_months` | Loan term in months. |
| `interest_rate_pct` | Annual interest rate on the loan. |
| `disbursement_date` | Date the loan was advanced. |
| `maturity_date` | Scheduled final payment date. |
| `days_past_due` | Days the loan is currently past due (0 = current). |
| `dpd_bucket` | Delinquency band: Current, 1-30 DPD, 31-60 DPD, 61-90 DPD, NPL (>90). |
| `collateral_type` | Security pledged: Equipment, Land, Invoice, Guarantee, None. |
| `collateral_coverage_ratio` | Collateral value / outstanding principal. Below 1.0 means under-secured. |
| `loan_officer_id` | Officer who originated the loan (LO01-LO15). |
| `province` | Province the borrower operates in. |

Key idea: a loan becomes **non-performing (NPL)** once it passes 90 days past due, and by then the recovery options are mostly gone. The buckets before that (1-30, 31-60, 61-90 DPD) are the early-warning signal.

## How the illustrative data was built (transparency)
The data is simulated with realistic credit-risk relationships built in, so the analysis reflects how a real book behaves. Default (NPL) is driven by: low collateral coverage (the strongest driver), higher interest rate, riskier sectors (Construction and Transportation highest; Manufacturing and Professional services lowest), longer tenure, and two weaker loan officers (LO07, LO12), plus random noise. Province has no built-in effect. The resulting book runs about a 3.9% NPL rate. These relationships are assumptions for illustration, not a fitted model; a real system would learn them from repayment history.
