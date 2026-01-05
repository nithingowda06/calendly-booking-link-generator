# Calendly Booking Link Generator (n8n)

This project generates **personalized Calendly booking links** using **n8n webhooks**.

---

## 🚀 Features
- Accepts name & email via webhook
- Generates personalized Calendly booking links
- Supports single-use or parameterized links
- Logs booking data to Google Sheets
- Returns clean JSON response

---

## 🧰 Tech Stack
- n8n (Cloud)
- Calendly API
- Google Sheets
- REST Webhooks

---

## 🔗 Webhook API

**Method:** POST  
**Endpoint:**


/webhook/generate-calendly-link


---
## 🖼 Workflow Overview

![n8n Workflow](Workflow.png)
## 🔄 Workflow Steps

1. **Webhook Trigger** – Receives user name and email  
2. **Set Configuration** – Sets Calendly API and workflow configuration  
3. **Get Current User** – Fetches Calendly user details  
4. **Extract User** – Extracts required user identifiers  
5. **Get Event Types** – Retrieves available Calendly event types  
6. **Select Event Type** – Selects the required meeting type  
7. **Create Single-Use Link** – Generates a Calendly booking link  
8. **Build Personalized Link** – Personalizes the booking link  
9. **Append Row in Google Sheets** – Logs booking details  
10. **Respond to Webhook** – Returns the booking link as JSON response  

---
🧪 Test with curl
```
curl -X POST https://<your-n8n-domain>.app.n8n.cloud/webhook/generate-calendly-link \
  -H "Content-Type: application/json" \
  -d '{
    "name": "<NAME>",
    "email": "<EMAIL>"
  }'
```
---

### 📥 Request Body
```json
{
  "name": "John Doe",
  "email": "john@example.com"
}
```

📤 Response Example

```json
{
  "success": true,
  "recipient": {
    "name": "John Doe",
    "email": "john@example.com"
  },
  "event": {
    "name": "30 Minute Meeting",
    "duration_minutes": 30
  },
  "booking": {
    "url": "https://calendly.com/...",
    "created_at": "2026-01-04T20:06:29Z"
  },
  "status": "CREATED"
}
```

## ⚙️ Setup Instructions

Import Calendly Booking Link Generator.json into n8n

Configure:

Calendly API Token

Google Sheets credentials

Activate the workflow

Use Production Webhook URL

---


