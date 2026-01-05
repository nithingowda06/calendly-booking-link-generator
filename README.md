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

1. Webhook Trigger
Receives the user’s name and email via a POST request to start the workflow.

2. Set Configuration
Sets up required configuration values such as Calendly API token and workflow parameters.

3. Get Current User
Fetches the authenticated Calendly user account details.

4. Extract User
Extracts and formats required user identifiers (user URI, organization data).

5. Get Event Types
Retrieves all available Calendly event types for the user.

6. Select Event Type
Selects the required event type (e.g., 30-Minute Meeting).

7. Create Single-Use Link
Generates a single-use Calendly booking link for the selected event.

8. Build Personalized Link
Personalizes the booking link using the user’s name and email.

9. Append Row in Google Sheets
Logs booking details (name, email, event type, link, timestamp, status) to Google Sheets.

10. Respond to Webhook
Returns a clean JSON response containing the booking link and booking status.

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

⚙️ Setup Instructions

Import Calendly Booking Link Generator.json into n8n

Configure:

Calendly API Token

Google Sheets credentials

Activate the workflow

Use Production Webhook URL

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


