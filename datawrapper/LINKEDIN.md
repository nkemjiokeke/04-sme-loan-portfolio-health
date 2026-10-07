# Project 04 - LinkedIn write-up (SME loan early-warning)

## LinkedIn post (connected story, first person)

Lenders usually find out a loan has gone bad only after it crosses 90 days past due, and by then there is little left to do. I wanted to build the thing that catches it earlier, so I took an illustrative book of 1,200 Canadian small-business loans and worked out what separates the loans that default from the ones that hold.

Geography was not it. Default rates across the provinces sat within a few points of each other. The risk was in how the loans were built and who wrote them.

Two loan officers stood out. One ran a 15% default rate and another 8%, against near zero for the best originators, and both had a habit of lending against too little collateral. By sector, Construction and Transportation carried most of the losses while Manufacturing and Professional services barely showed up.

The clearest marker was collateral coverage. The loans that defaulted were secured by less than half their value on average, and every one of them was under-secured. The loans that performed were covered better than one to one. A loan that went bad was usually built that way at the start.

So I turned those markers into a score from 0 to 100, using only what a lender knows the day it writes the loan: coverage, rate, sector, and officer. To check it, I compared the score on the loans that defaulted against the rest. The defaulters averaged 77, the performers 33. The score tells them apart, which is what makes it worth acting on.

Pointed at the loans that are still performing, the score gives the lender a watch list, ranked by how much each account looks like the ones that already failed.

The money is the reason to bother. Expected loss on the book is $6.2M. About $2.3M is in loans already past 90 days, where the outcome is mostly set. The other $3.9M is in loans that have not defaulted yet. Work the watch list and most of that stays on the book; leave it, and it moves into the lost pile a quarter at a time.

I built the analysis in SQL and the dashboard in Power BI, so a credit officer can filter the watch list by officer, sector, and province and open any account.

One note: the data is illustrative, with the risk relationships built in and documented. The point is the method, not the specific loans.

## Carousel slides

1. Can you see a loan going bad before it does? An early-warning system for a small-business lender. Illustrative Canadian loan book, SQL and Power BI.
2. The problem. Lenders learn a loan is bad only after 90 days past due, when the window to act has closed.
3. It is not geography (Chart 1/2). Default rates are flat across provinces. The risk is in loan structure and two loan officers, one at 15% default, another at 8%.
4. The marker (Chart 3). Loans that defaulted were secured by less than half their value, and every one was under-secured. Performing loans were covered above one to one.
5. The score works (Chart 4). Built only on origination markers. Defaulted loans score 77, performing loans 33. It separates them.
6. The watch list (Chart 5 / dashboard). Still-performing loans that look like the ones that failed, ranked by score.
7. The money (Chart 6). $3.9M of expected loss is still in loans that have not defaulted. Act now and most of it stays on the book.
8. The dashboard. Built in Power BI so a credit officer can filter the watch list by officer, sector, and province, and drill into any account. [insert Power BI screenshot]
9. How I built it. Illustrative data with documented risk relationships, measures and score in SQL and DAX, charts in Datawrapper, dashboard in Power BI.
