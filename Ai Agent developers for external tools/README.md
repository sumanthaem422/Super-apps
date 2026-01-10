### Part 2: README.md File
Below is the markdown content, ready to be pasted into your repository.

# 🎙️ Groq + n8n Voice Agent Orchestrator

An ultra-low latency AI conversation backend built with **n8n**, **Groq (Llama 3.3)**, and **LangChain**.

[![n8n](https://img.shields.io/badge/n8n-Workflow-FF6D5A?style=flat&logo=n8n)](https://n8n.io/)
[![Groq](https://img.shields.io/badge/AI-Groq--Llama3.3-orange?style=flat)](https://groq.com/)
[![LangChain](https://img.shields.io/badge/Agent-LangChain-1C3C3C?style=flat&logo=langchain)](https://langchain.com/)

## 📖 Project Overview
This workflow functions as the "brain" for voice assistants (like Vapi, Twilio, or Retell AI). It accepts voice transcripts via webhook, processes the conversation using **Groq's fast inference API**, maintains conversation history via memory buffers, and returns a natural language response in milliseconds.

### **Key Features**
- **⚡ Real-Time Speeds:** Uses **Groq (Llama 3.3-70b)** for lightning-fast inference, essential for voice interfaces to prevent "awkward silence."
- **🧠 Contextual Memory:** Includes a **Window Buffer Memory** node so the AI remembers the conversation flow (names, previous questions, etc.).
- **🔌 Universal Integration:** Accepts standard JSON payloads via Webhook, making it compatible with any frontend or telephony provider.
- **🛠️ Structured Logic:** Pre-processes input data with JavaScript to ensure the AI Agent receives clean `transcript`, `sessionId`, and `customerName` variables.

---

## 🏗️ Workflow Architecture

The workflow executes in a linear pipeline with parallel agentic resources:

1.  **Webhook Trigger:** Listens for POST requests at `/voice-agent-orchestrator`.
2.  **Data Formatting:** A Code node extracts the raw transcript and session details from the incoming JSON body.
3.  **AI Agent:** The core logic engine. It combines:
    *   **System Prompt:** Defines the persona (e.g., "Helpful Assistant").
    *   **Memory:** Retains the last $N$ exchanges.
    *   **Model:** Queries Groq for the response.
4.  **Response:** Sends the generated text back to the voice provider to be spoken (TTS).

---

## 🛠️ Built With
- **[n8n](https://n8n.io/)** - For orchestrating the logic flow.
- **[Groq](https://groq.com/)** - Providing the Llama 3.3-70b-versatile model.
- **[LangChain](https://langchain.com/)** - Managing the agent loop and conversation memory.

---

## 🚀 Setup & Configuration

### 1. Prerequisites
*   An n8n instance (Self-hosted or Cloud).
*   A **Groq API Key** (Get one [here](https://console.groq.com/keys)).

### 2. Import the Workflow
Download the `workflow.json` from this repository and import it into your n8n editor.

### 3. Configure Credentials
*   Double-click the **Groq Chat Model** node.
*   Select "Create New Credential" and paste your Groq API Key.

### 4. Input Payload Format
The workflow expects your Voice Provider to send a JSON body similar to this structure (defined in the *Format for Agent* node):

```json
{
  "body": {
    "message": {
      "transcript": "Hello, can I make a reservation?",
      "call": {
        "id": "session-12345",
        "customer": {
          "name": "Roger"
        }
      }
    }
  }
}
```

*Note: If your provider (e.g., Twilio) sends a different structure, modify the JavaScript in the **Format for Agent** node.*

---

## 📝 Customization
- **Change Personality:** Open the **AI Agent** node and edit the `System Message`.
  - *Example:* "You are a sarcastic receptionist at a futuristic hotel."
- **Adjust Memory:** Open the **Window Buffer Memory** node to change the "Window Size" (how many messages back the AI remembers).
- **Swap Models:** You can easily swap the **Groq Chat Model** node for OpenAI or Anthropic if speed is less critical than reasoning capability.

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
**Disclaimer:** *This project is designed for low-latency interactions. Ensure your n8n instance is hosted in a region close to your users/voice provider for best performance.*