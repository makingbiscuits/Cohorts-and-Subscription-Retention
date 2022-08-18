# Cohorts and Subscription Retention


✨ ✨ Solution for Cohorts and Subscription Retention task for Turing College✨ ✨ 

<a href = 'https://docs.google.com/spreadsheets/d/1gbsgTC0hNnmgPrrrGJfd1R4cnKEOLRse-ae7I9zDfx8/edit?usp=sharing
'> The dashboard with visualisations.</a> It explains the main insights of the analysis for subscription retention and provides a solution for creating a weekly retention cohort.

:rocket: SQL (BigQuery), Excel, Google Sheets, Cohort analysis

### The task:

You got a follow up task from your product manager to give stats on how subscriptions churn looks like from a weekly retention standpoint. Your PM argues that to view retention numbers on a monthly basis takes too long and important insights from data might be missed out.

You remember learning previously that cohorts analysis can be really helpful in such cases. You should provide weekly subscriptions data that would show how many subscribers who started on a particular week remain active in the upcoming 6 weeks. Your end result should show weekly retention cohorts and their retention from week 1 to week 6. Assume that you are doing this analysis on 2021-02-07.

### Main SQL Query:

``` SQL 
WITH t1 AS 
(
  SELECT user_pseudo_id,
  DATE_TRUNC(subscription_start, WEEK) as start_week,
  subscription_end
  FROM `tc-da-1.turing_data_analytics.subscriptions` AS s 
)

SELECT t1.start_week as sub_date,
  COUNT(start_week) as w0,
  SUM(CASE WHEN subscription_end IS NULL OR subscription_end > DATE_ADD(start_week, INTERVAL 1 WEEK) THEN 1 ELSE 0 END) AS w1,
  SUM(CASE WHEN subscription_end IS NULL OR subscription_end > DATE_ADD(start_week, INTERVAL 2 WEEK) THEN 1 ELSE 0 END) AS w2,
  SUM(CASE WHEN subscription_end IS NULL OR subscription_end > DATE_ADD(start_week, INTERVAL 3 WEEK) THEN 1 ELSE 0 END) AS w3,
  SUM(CASE WHEN subscription_end IS NULL OR subscription_end > DATE_ADD(start_week, INTERVAL 4 WEEK) THEN 1 ELSE 0 END) AS w4,
  SUM(CASE WHEN subscription_end IS NULL OR subscription_end > DATE_ADD(start_week, INTERVAL 5 WEEK) THEN 1 ELSE 0 END) AS w5,
  SUM(CASE WHEN subscription_end IS NULL OR subscription_end > DATE_ADD(start_week, INTERVAL 6 WEEK) THEN 1 ELSE 0 END) AS w6
FROM t1
GROUP BY 1
```
