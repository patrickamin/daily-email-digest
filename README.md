# 📧 Daily Email Digest Automation

An automated workflow that searches your Gmail inbox daily, summarizes emails using AI, and sends you one clean digest every morning at 8am Cairo time. Zero manual work — runs 24/7.

---

## ✨ What It Does

1. **Searches Gmail** — Finds all emails from the past 24 hours
2. **Summarizes with AI** — Uses Gemini AI to create concise summaries
3. **Groups by sender** — One combined email showing all summaries organized by person
4. **Sends automatically** — Arrives in your inbox at 8am Cairo time every day

**Result:** Instead of checking 50 emails, you read one digest with the key info from each sender.

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| Automation Platform | Make.com |
| Gmail Integration | Gmail API (OAuth) |
| AI Summarization | Google Gemini AI |
| Scheduling | Make.com Scheduler (cron) |
| Email Delivery | Gmail SMTP |

---

## 📋 Workflow Steps

This is built entirely in **Make.com** (no code). Here's the flow:

```
[Daily Trigger 8:00 AM] 
    ↓
[Gmail Search Module] — Find emails from last 24 hours
    ↓
[Iterate Module] — Loop through each email
    ↓
[Gemini AI Module] — Summarize each email
    ↓
[Text Aggregator] — Combine all summaries
    ↓
[Gmail Send Module] — Email you the digest
```

### Detailed Setup

**1. Trigger**
- Module: **Trigger → Schedule → Date and time**
- Time: `08:00` (8am)
- Repeat: Every day
- Timezone: `Africa/Cairo`

**2. Gmail Search**
- Module: **Gmail → Search Emails**
- Query: `newer_than:1d` (past 24 hours)
- Limit: 50 emails

**3. Iterator**
- Module: **Flow Control → Iterator**
- Array: Results from Gmail Search

**4. Gemini AI Summarization**
- Module: **Google Gemini → Generate content**
- Prompt: 
```
Summarize this email in 1-2 sentences, keep it factual:

Subject: {email_subject}
From: {sender_name}
Body: {email_body}
```

**5. Text Aggregator**
- Module: **Text Aggregator**
- Input: Summaries from Gemini
- Format: Join with line breaks
- **Important:** Add sender name before each summary:
```
From: {sender_name}
{summary}
---
```

**6. Gmail Send**
- Module: **Gmail → Send Email**
- To: Your email address
- Subject: `Daily Digest — {date}`
- Body: Output from Text Aggregator

---

## ⚙️ Configuration

**Gmail API Setup:**
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project
3. Enable Gmail API
4. Create OAuth 2.0 credentials (Desktop application)
5. In Make.com, connect your Gmail account with these credentials

**Gemini API Key:**
1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Generate an API key
3. Add it to Make.com as a connection

**Timezone:**
Make sure Make.com account is set to `Africa/Cairo` so 8am triggers correctly.

---

## 📊 Current Status

✅ **Working:** Email search, AI summarization, daily delivery  
🔧 **To improve:**
- Add sender name consistently to each summary (Text Aggregator formatting)
- Show English date format in each email entry
- Note: Gemini quota resets daily — fully functional

---

## 💡 Use Cases

- **Busy professionals** — Read 50 emails in 2 minutes
- **Multiple email addresses** — Forward to one inbox and get one digest
- **Project managers** — Track all client updates in one email
- **Founders** — Monitor all partner/investor emails daily

---

## 🔗 How to Clone This Workflow

1. Go to Make.com → **Templates**
2. Create a new scenario
3. Copy the module structure above
4. Connect your Gmail + Gemini accounts
5. Test it → Activate it
6. Set timezone to Cairo (or your timezone)

**Estimated setup time:** 15 minutes

---

## 💼 Business Angle

This workflow is **sellable** to:
- **Busy professionals** — $10–20/month subscription
- **Agencies** — White-label for client email monitoring
- **Enterprises** — Deploy for team email summaries (each team member gets their own digest)

Can be adapted to:
- Slack summaries instead of email
- Weekly instead of daily
- Filter by specific senders/labels
- Include AI-powered action items ("what do I need to do?")

---

## 📁 Project Files

This repo documents the Make.com workflow setup. The actual automation runs on Make.com servers (no local code).

- `README.md` — This guide
- `workflow-screenshots/` — Screenshots of each Make.com module (optional, for reference)

---

## 🔄 Next Improvements

- [ ] Add sender display name before each summary
- [ ] Format dates in English (ISO 8601)
- [ ] Filter out marketing emails automatically
- [ ] Add action items extraction ("reply needed", "follow-up", etc.)
- [ ] Support multiple digest times (morning + evening)

---

## 👤 Author

**Patrick Amin** — AI Automation Developer  
[github.com/patrickamin](https://github.com/patrickamin)

Part of my AI automation agency portfolio. Built to demo Make.com + Gemini AI integration for Egyptian businesses.
