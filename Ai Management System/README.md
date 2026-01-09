Here is a professional, high-quality `README.md` file tailored to your workflow. I have analyzed your JSON to accurately describe the logic (Ingestion vs. Querying) and added the specific Twilio integration details you requested.

***

# 🧠 AI-Powered Executive SMS Knowledge Assistant
**An automated "Second Brain" for meetings built with n8n, Groq, Supabase, and Twilio.**

![n8n](https://img.shields.io/badge/n8n-workflow-ff6b6b?style=flat-square) ![Groq](https://img.shields.io/badge/AI-Groq-orange?style=flat-square) ![Supabase](https://img.shields.io/badge/Database-Supabase-green?style=flat-square) ![Twilio](https://img.shields.io/badge/SMS-Twilio-red?style=flat-square)

## 📖 Project Overview
This project is a two-part automation system designed to act as an **Executive Assistant** that never forgets a detail. 

1.  **Ingestion:** It automatically receives meeting transcripts (via Retell AI or similar voice tools), uses AI to summarize them into key action items and decisions, and stores them in a database.
2.  **Retrieval:** It allows the user to send a text message (SMS/WhatsApp) asking a question. An AI Agent searches the database, synthesizes information across multiple past meetings, and replies with the answer.

## ✨ Key Features
*   **Automated Knowledge Entry:** Ingests raw transcripts via webhook, cleans the data, and tags it by project.
*   **AI Summarization:** Uses **Groq (Llama 3.3)** to distill long transcripts into:
    *   Key discussion points
    *   Decisions made
    *   Action items
    *   Deadlines
*   **Long-Term Memory:** Stores all summaries and raw text in **Supabase** for persistent storage.
*   **SMS/WhatsApp Interface:** Integrates with **Twilio** so you can query your knowledge base on the go (e.g., *"What did we decide about the Q3 budget last Friday?"*).
*   **Context-Aware Agent:** The AI doesn't just keyword match; it analyzes all relevant records to provide a synthesized, human-like answer.

## 🏗️ Workflow Architecture
The workflow functions via two distinct pipelines within a single n8n canvas:

### 1. The Ingestion Pipeline
*   **Trigger (Retell/Voice):** Receives the transcript and project name via Webhook.
*   **AI Processing:** Groq (Llama 3.3) summarizes the content into a structured format (under 300 words).
*   **Storage:** The summary and raw text are inserted into a **Supabase** table.

### 2. The Query Pipeline
*   **Trigger (Twilio):** Receives an incoming SMS or WhatsApp message.
*   **AI Agent (RAG):**
    *   The Agent utilizes a **Supabase Tool** to search the database.
    *   It retrieves relevant meeting notes based on the user's question.
    *   It synthesizes the answer using the Groq Chat Model.
*   **Response:** The answer is generated for the user.

## 🛠️ Built With
*   **n8n** - Workflow automation platform.
*   **Groq** - Ultra-fast AI inference (Llama 3.3-70b-versatile).
*   **Supabase** - Postgres database for storing meeting knowledge.
*   **Twilio** - SMS and WhatsApp messaging provider.
*   **Retell AI** (Optional) - Source for voice-to-text transcripts.

## 📱 Twilio Integration Setup
To enable the SMS/WhatsApp functionality, you must configure Twilio to talk to your n8n instance.

1.  **Get a Twilio Number:** Sign up for Twilio and purchase a phone number.
2.  **Configure the Webhook:**
    *   Go to your n8n workflow and open the `Trigger: WhatsApp/SMS (Twilio)` node.
    *   Copy the **Production URL**.
    *   In your Twilio Console, go to **Phone Numbers > Manage > Active Numbers**.
    *   Click on your number and scroll to the **Messaging** section.
    *   Paste your n8n URL into the field: **"A Message Comes In" (Webhook)**.
    *   Set the method to `POST`.
3.  **Sending Replies:**
    *   *Note:* The current JSON processes the query. To send the reply back to the user, ensure your AI Agent's output is connected to a **Twilio Node (Send SMS)** at the end of the flow, utilizing the `From` number provided in the trigger data.

## ⚙️ Configuration & Database

### Supabase Table Setup
Create a table in Supabase (e.g., named `test_table` or `meeting_notes`) with the following columns to match the workflow:
*   `id` (int8, primary key)
*   `created_at` (timestamptz)
*   `text` (text) - *Stores the summary/transcript*
*   `project_name` (text, optional) - *For categorization*

### n8n Credentials
You will need to set up the following credentials in n8n:
1.  **Groq API:** Get your API key from [console.groq.com](https://console.groq.com).
2.  **Supabase API:** Requires your Project URL and Service Role Key.
3.  **Twilio API:** Requires your Account SID and Auth Token.

## 📄 License
This project is open-source. Feel free to modify and adapt it to your specific business needs.

***
*Disclaimer: This workflow uses Large Language Models. Always verify critical dates and financial decisions found in AI summaries against the original transcripts.*