# SME Loan Portfolio Health: an early-warning system for a Canadian lender

> Sector: Banking and financial services. Data: illustrative (simulated, Canadian). Tools: SQL (SQLite), Power BI, Datawrapper. Method: credit-risk scoring and early warning.

This project runs on illustrative data. The loan book is simulated, but the risk relationships built into it are real ones, and the analysis is the same I would run on an actual portfolio. How the data was built is documented in `data/DATA_DICTIONARY.md`.

## The problem
A Canadian lender holds 1,200 small-business loans worth $114M across five provinces and six sectors. Its non-performing loan rate is 3.9% and rising. The catch is that the lender only learns a loan has gone bad once it passes 90 days past due, and by then the borrower is usually too far gone to recover and the loss is booked. I set out to build something that flags a loan heading for default while there is still time to act, and to find where the book is leaking so the lender can tighten who it lends to.

## What I found
The risk is not where I first looked. NPL rates by province sit within a few points of each other, so geography is not the story. Loan structure and who wrote the loan are.

By sector, default concentrates in Construction (7.8%) and Transportation (6.4%), while Manufacturing and Professional services stay under 1%. By loan officer the split is sharper. Two officers, LO07 and LO12, run NPL rates of 14.8% and 8.0% against near zero for the best originators, and both write under-secured loans.

The common marker is collateral. The loans that defaulted averaged 0.45 in collateral coverage, meaning the security was worth less than half the loan, and every one of them was under-secured. Performing loans averaged 1.04. A loan that went bad was usually set up that way at origination.

## The early-warning score
I built a score from the markers that are visible at origination: collateral coverage, interest rate, sector, and the officer. It runs from 0 to 100 and uses nothing about whether a loan is already late, so it works on loans that still look fine.

To test it, I compared the score on the loans that defaulted against the rest. Defaulted loans score 76.7 on average, performing loans 33.2. The score separates the two cleanly, which is what lets the lender act on it with confidence.

Pointed at the performing book, the score produces a watch list: the accounts that most resemble the ones that defaulted. Most are LO07 or LO12, in Construction or Transportation, under-secured, and several are already drifting past due.

## The money
Expected loss on the book is about $6.2M. Of that, $2.33M is in loans already past 90 days, where little can be done. The other $3.9M is in loans that have not defaulted yet. That $3.9M is the case for the watch list. Work those accounts now and most of it stays on the book; wait, and it moves quarter by quarter into the pile that is already gone.

## The decision
Three things come out of this for the lender:

- Work the watch list now, starting with the highest scores that are already showing early delinquency.
- Set a minimum collateral coverage at origination, since under-securing is the clearest marker of loss.
- Review LO07 and LO12's files and tighten lending on Construction and Transportation, where the losses concentrate.

## How I built it
I shaped the loan book, built the health baseline and the score in SQLite, one query per question, made the publication charts in Datawrapper, and built the interactive dashboard in Power BI. The queries are in `sql/`, the chart data in `datawrapper/`.

## Limitations
The data is simulated and illustrative, not a real institution's book, and the risk relationships in it are ones I built in, described in the data dictionary. The probability-of-default weights behind the expected-loss figure are assumptions, not a fitted model. A real early-warning system would use each loan's repayment history over time rather than a single snapshot, and would be judged on how its flagged loans actually turn out.
