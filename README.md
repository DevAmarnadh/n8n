# 🚀 Lead-to-Support Automation (n8n)

## 📌 Overview

This project implements an **n8n automation workflow** that converts inbound leads into a structured support pipeline. It includes validation, enrichment, routing, storage, notifications, and daily summaries.

---

## ⚙️ Features

* Webhook-based lead ingestion
* Input validation and spam detection
* Lead enrichment (company inference from email domain)
* Idempotency (prevents duplicate entries using unique hash key)
* Data storage in Google Sheets or Airtable
* Routing logic:

  * High urgency → Slack alert + Jira/Trello ticket
  * Normal → Email confirmation + status update
* Daily digest summary at 6 PM
* Error handling with retries and dead-letter logging

---

## 🔧 Setup Instructions

### 1. Install n8n

```bash
npm install -g n8n
n8n start
```

---

### 2. Import Workflow

* Open n8n UI
* Go to Workflows → Import
* Upload the provided workflow JSON

---

### 3. Configure Credentials

Set up the following services inside n8n:

* Google Sheets or Airtable
* Slack Webhook
* Email (SMTP or Gmail)
* Jira or Trello

---

### 4. Environment Variables

Create a `.env` file and configure:

```env
SLACK_WEBHOOK_URL=your_slack_webhook
GOOGLE_SHEET_ID=your_sheet_id
SMTP_USER=your_email
SMTP_PASS=your_password
JIRA_API_KEY=your_key
```

---

## ▶️ Running the Workflow

1. Activate the workflow in n8n
2. Send a POST request to the webhook endpoint with JSON data

Example:

```json
{
  "name": "John Doe",
  "email": "john@company.com",
  "company": "",
  "message": "Need urgent help with API",
  "urgency": "high",
  "product": "API"
}
```

---

## 🧪 Validation Rules

* Required fields must be present
* Email must be valid format
* Spam messages are filtered using keyword checks

---

## 🔁 Idempotency

* A unique key is generated using input data
* Duplicate webhook retries do not create multiple records
* Verified by sending the same payload multiple times

---

## 🔀 Routing Logic

### High Urgency

* Sends alert to Slack
* Creates ticket in Jira or Trello

### Normal

* Sends confirmation email
* Updates status in storage

---

## ⚠️ Error Handling

* Automatic retries for external services
* Failures are logged with error details
* Invalid or failed payloads are stored separately (dead-letter handling)

---

## 📊 Daily Digest

* Runs automatically at 6 PM
* Provides:

  * Count by urgency
  * Count by product
  * Top 5 recent leads

---

## 📸 Outputs

The workflow execution demonstrates:

* High urgency routing
* Normal lead handling
* Error handling and failure logging
* Daily summary generation

---

## ✅ Final Checklist

* Workflow JSON provided
* Sample payloads included
* Screenshots demonstrating execution
* Setup and run steps documented
* Outputs are reproducible

---

## 👨‍💻 Author

Your Name
