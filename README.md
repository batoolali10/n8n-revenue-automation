# Daily Revenue Automation & Alerting System

An automated data pipeline built with **n8n** to fetch, filter, and summarize daily sales data from Google Sheets, send beautifully formatted HTML reports to the sales manager, and trigger escalation alerts to the CEO if daily targets are not met.

## ⚙️ Workflow Architecture & Logic
1. **Schedule Trigger:** Runs automatically every day at 23:59 to process the full day's data.
2. **Data Ingestion (Google Sheets):** Fetches recent transaction logs and revenue data.
3. **Time-Based Filtering:** Filters rows dynamically to match only the current date (`$now.toFormat('MM/d/y')`).
4. **Data Aggregation:** Summarizes and calculates the total `sum_Revenue` for the day.
5. **Manager Reporting (Gmail):** Sends an automated, styled HTML/CSS email report showing the total daily revenue.
6. **Conditional Escalation (IF Logic):** Checks if the total revenue is less than **$1,500**. If true, it triggers an immediate email notification to the CEO alerting them that the daily target was missed.
7. **Error Handling & Retry:** Includes a "Wait & Retry" loop mechanism to re-fetch data from Google Sheets if the initial request fails.

## 🛠️ Tech Stack & Tools
* **Automation Platform:** n8n
* **Data Source:** Google Sheets API
* **Communication & Alerting:** Gmail API (OAuth2)
* **Frontend/Formatting:** HTML5 & CSS3 (For structured email templates)
* **Expression Language:** JavaScript / n8n Expressions
