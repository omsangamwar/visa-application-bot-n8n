# Visa Application Automation (n8n)

An end-to-end automation that lets applicants apply for a visa, upload documents, and track their status — entirely over WhatsApp.

## 🎥 Demo Video
https://drive.google.com/file/d/1JRBDy5YMRmSNsUY507yeWt6G5czoACGe/view?usp=sharing

## What it does

- Applicants message a WhatsApp number to start or continue their visa application
- New users are automatically registered and welcomed; returning users are routed based on their current status
- Uploaded documents (like passports) are automatically parsed and analyzed using AI
- Application state is tracked in real time and updated automatically
- Clients get instant WhatsApp notifications whenever their status changes

The one exception is payment confirmation — kept as a human-in-the-loop step so no automated guess is ever made on something that involves real money.

## Tech Stack

- **n8n** – workflow orchestration
- **Twilio** – WhatsApp messaging
- **Google Sheets** – application data & state tracking
- **LlamaIndex** – document parsing
- **Groq** – LLM-based analysis of parsed data

## How it works

1. A Twilio webhook receives the inbound WhatsApp message
2. The payload is normalized to extract phone number, name, message text, and any media
3. Google Sheets is checked to see if the sender is a new or existing applicant
4. New users are added and welcomed; existing users are routed based on their current application stage
5. If a document is sent, it's downloaded, uploaded to LlamaIndex for parsing, and the extracted text is analyzed by Groq
6. Results are saved to Google Sheets, updating the applicant's state
7. A Google Sheets trigger fires a WhatsApp update whenever the state changes

## Setup

1. Import the workflow JSON into your n8n instance
2. Add credentials for:
   - Twilio (Account SID + Auth Token)
   - Google Sheets OAuth2
   - LlamaIndex API key
   - Groq API key
3. Replace placeholder values (Sheet ID, phone number, API keys) with your own
