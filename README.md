# 📱 WhatsApp Automation (n8n Workflow)

This project automates WhatsApp interactions using **n8n**, **OpenAI**, **Google Calendar**, and **Gmail**. It enables users to chat via WhatsApp, automatically process requests through AI, and trigger calendar bookings or email responses — all without manual intervention.

---

## 🚀 Features

- **WhatsApp Trigger:**  
  Automatically receives incoming WhatsApp messages through the Meta Cloud API.

- **AI Agent (LangChain):**  
  Uses an OpenAI model to understand the message and decide the next action (answer, book a meeting, or send an email).

- **Conversation Memory:**  
  Maintains chat context for each WhatsApp user using memory buffer.

- **Google Calendar Integration:**  
  Books meetings or appointments automatically when requested by the user.

- **Gmail Integration:**  
  Sends follow-up or confirmation emails using predefined templates.

- **Conditional Logic:**  
  Filters messages based on sender number before processing through the AI.

---

## 🧠 Workflow Overview

```plaintext
WhatsApp Trigger
      ↓
      IF (Check Sender)
      ↓
AI Agent (LangChain)
 ├── Uses → OpenAI Chat Model
 ├── Uses → Memory Buffer (Session-based)
 ├── Calls → Google Calendar Tool (for booking)
 └── Calls → Gmail Tool (for sending mail)
      ↓
WhatsApp Business Cloud (Sends AI Response)
```

---

## ⚙️ Setup Instructions

### 1. Prerequisites

- An **n8n** instance (self-hosted or cloud)
- Meta **WhatsApp Business Cloud API**
- **OpenAI API key**
- **Google Calendar** and **Gmail OAuth2** credentials

---

### 2. Import Workflow

1. Open your **n8n dashboard**
2. Click **Import → From File**
3. Upload the file: `Whatsapp Automation.json`

---

### 3. Configure Credentials

Under **Credentials** in n8n, connect the following:

| Integration | Credential Name | Purpose |
|--------------|----------------|----------|
| WhatsApp API | `WhatsApp account` | Send automated messages |
| WhatsApp Trigger API | `WhatsApp OAuth account` | Receive incoming messages |
| OpenAI | `manoj_ai_dude` | AI chat responses |
| Google Calendar | `Google Calendar account` | Schedule meetings |
| Gmail | `the_ai_dude_mail` | Send emails |

---

### 4. Activate Workflow

1. Ensure all nodes show a **green checkmark** (credentials connected).  
2. Toggle the **Active** switch at the top-right of the workflow editor.  
3. Send a test message to your WhatsApp number to verify automation.

---

## 💡 Example Usage

**User:** “Can you set up a call with Manoj tomorrow at 5 PM?”  
**AI Agent:**  
✅ Creates Google Calendar event  
✅ Sends Gmail confirmation  
✅ Replies on WhatsApp with:  
> “Meeting with Manoj scheduled for tomorrow at 5 PM. Invite sent to your email.”

---

## 🧩 Nodes Used

| Node | Type | Description |
|------|------|--------------|
| WhatsApp Trigger | `n8n-nodes-base.whatsAppTrigger` | Detects new WhatsApp messages |
| If | `n8n-nodes-base.if` | Filters sender number |
| OpenAI Chat Model | `@n8n/n8n-nodes-langchain.lmChatOpenAi` | AI model (GPT-4o-mini) |
| AI Agent | `@n8n/n8n-nodes-langchain.agent` | Handles AI logic and decisions |
| Simple Memory | `@n8n/n8n-nodes-langchain.memoryBufferWindow` | Stores chat context |
| Appointment Booking | `n8n-nodes-base.googleCalendarTool` | Books meetings |
| Gmail Agent | `n8n-nodes-base.gmailTool` | Sends emails |
| WhatsApp Business Cloud | `n8n-nodes-base.whatsApp` | Sends WhatsApp replies |

---

