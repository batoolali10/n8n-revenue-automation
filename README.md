# Daily Revenue Automation & Alerting System

An automated data pipeline built with **n8n** to fetch, filter, and summarize daily sales data from Google Sheets, send beautifully formatted HTML reports to the sales manager, and trigger escalation alerts to the CEO if daily targets are not met.
![n8n Workflow](workflow.png)

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

---

## 📌 Project 2: AI-Powered Smart Helpdesk & Ticketing System

An intelligent, automated ticketing system that handles incoming internal support forms, archives them in Google Sheets, and utilizes **Gemini 2.5 Flash LLM (via LangChain)** to dynamically analyze, classify, prioritize, and route the issues.

![Project 2 Workflow](ticket_system.png)

### ⚙️ Workflow Architecture & Logic
1. **Form Trigger:** Captures incoming employee complaints/tickets (Name, Email, Problem Description).
2. **Data Logging:** Appends the raw ticket details immediately into Google Sheets for historical archiving.
3. **AI Analysis (Basic LLM Chain):** Passes the problem description to **Gemini 2.5 Flash** using LangChain. 
4. **Smart Classification & Prioritization:** The LLM executes custom prompt engineering logic to classify the ticket department (**IT Department** vs. **HR Department**), determine severity levels, and calculate a dynamic resolution deadline.
5. **Dynamic HTML Generation:** The LLM formats the final output into a responsive, styled HTML alert template.
6. **Human-in-the-Loop Routing:** Sends the generated HTML alert via Gmail to the responsible team and utilizes the **Send Message & Wait for Response** node to hold for an internal human action (e.g., assigning a specific HR member via a dropdown menu).

### 🛠️ Tech Stack & Tools
* **Automation Platform:** n8n
* **AI Orchestration:** LangChain Nodes inside n8n
* **LLM Engine:** Google Gemini 2.5 Flash Chat Model
* **Data Logging:** Google Sheets API
* **Notification & Interaction:** Gmail API (with Wait-for-Response Webhooks)
