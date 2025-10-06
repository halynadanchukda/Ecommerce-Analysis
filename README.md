# User Acquisition & Email Performance 

## Tools
- **SQL (BigQuery)**


## Purpose: 
Consolidate daily metrics by accounts and email campaigns, calculate country totals, and rank the top 10 countries by accounts created and emails sent.

## Business questions:
Which countries generate the most new accounts?
Where do we send the most emails and how does this correlate with account activity?
What do the daily metrics (accounts / sent / open / visit) look like in terms of account attributes (verification, unsubscribe, send interval)?

## What the query does:
account_data — daily unique accounts by country and attributes.
emails_data — daily unique emails (sent/open/visit) by country and attributes.
union_data — joins both sources via UNION DISTINCT, aligns columns.
union_group — aggregates metrics after UNION at the level (date, country, attributes).
total_cnt — adds country totals using window SUM.
total_rank — ranks countries by two summary metrics.
Final SELECT — returns all daily rows for countries in the top 10 for either ranking.

## Important notes:
- The field sent_date stores not an absolute date, but an offset in days from the session date (session.date).  DATE_ADD is used to calculate the actual email sent date.
- Rankings are calculated on the entire dataset; the final filter includes all daily rows for countries in the top 10 by either indicator.
