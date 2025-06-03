# 🎯 User Monetization Metrics – SQL Project

This mini-project analyzes user payment data to generate key monetization metrics such as ARPU, ARPPU, Total Revenue, and Conversion Rate using SQL.

## 🗂️ Dataset
Simulated or real `user_payments` table with fields:
- `user_id`
- `payment_date`
- `revenue_amount`
- `country`

## 📊 Metrics Calculated
- **Total Users** – number of unique users per month
- **Paying Users** – number of users who generated revenue
- **Total Revenue** – sum of all revenue amounts
- **ARPU** – Average Revenue per User
- **ARPPU** – Average Revenue per Paying User
- **Conversion Rate** – Paying Users / Total Users

## 🧠 Sample SQL Query
```sql
SELECT
  country,
  DATE_TRUNC('month', payment_date) AS month,
  COUNT(DISTINCT user_id) AS total_users,
  COUNT(DISTINCT CASE WHEN revenue_amount > 0 THEN user_id END) AS paying_users,
  SUM(revenue_amount) AS total_revenue,
  SUM(revenue_amount) * 1.0 / COUNT(DISTINCT user_id) AS arpu,
  CASE 
    WHEN COUNT(DISTINCT CASE WHEN revenue_amount > 0 THEN user_id END) = 0 THEN NULL
    ELSE SUM(revenue_amount) * 1.0 / COUNT(DISTINCT CASE WHEN revenue_amount > 0 THEN user_id END)
  END AS arppu,
  COUNT(DISTINCT CASE WHEN revenue_amount > 0 THEN user_id END) * 1.0 
    / COUNT(DISTINCT user_id) AS conversion_rate
FROM user_payments
GROUP BY country, month
ORDER BY country, month;

🔧 Tools
SQL (PostgreSQL syntax)

BigQuery / PostgreSQL-compatible environment

💬 Goal
To track and compare user monetization performance across countries and time.
This type of query is commonly used in SaaS, mobile apps, and e-commerce analytics.

📬 Let's connect
Open to feedback and ideas — feel free to fork or contribute!
