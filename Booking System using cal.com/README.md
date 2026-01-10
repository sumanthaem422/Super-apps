This is a professional, enterprise-grade `README.md` tailored for your **Cal.com Sales Booking Automation**. It emphasizes the lead qualification logic and the "B2B vs. B2C" intelligence of the workflow.

***

# 🚀 Autonomous B2B Sales Scheduler & Lead Qualifier
An intelligent sales operations engine built with **n8n**, **Cal.com**, and **Gmail** to automatically qualify inbound bookings and separate high-value corporate leads from generic prospects.

![n8n](https://img.shields.io/badge/n8n-Orchestration-orange) ![Cal.com](https://img.shields.io/badge/Cal.com-Scheduling-black) ![Gmail](https://img.shields.io/badge/Gmail-Outreach-red) ![JavaScript](https://img.shields.io/badge/Logic-Domain%20Analysis-yellow)

## 📖 Project Overview
In high-volume sales environments, calendars often get cluttered with unqualified leads. This workflow acts as a **smart gatekeeper** between your scheduling tool and your sales pipeline.

It intercepts every booking request in real-time, performs **heuristic domain analysis** to determine if the prospect is using a corporate email (Business) or a generic provider (Gmail/Yahoo/etc.), and dynamically executes downstream actions based on lead quality.

### Key Features
*   **Heuristic Domain Analysis:** Uses custom JavaScript logic to strip email domains and cross-reference them against a "Free Provider" blocklist (Gmail, Outlook, iCloud, etc.).
*   **Automated Lead Scoring:** Instantly tags leads as `isBusiness: true` or `false`, allowing you to prioritize B2B contracts over B2C consultations.
*   **Standardized Data Object:** Transforms raw webhook JSON into a clean "Lead Object" with unique Lead IDs, standardized timestamps, and source tracking—ready for CRM ingestion.
*   **Instant White-Glove Response:** Triggers immediate, personalized confirmation emails to qualified prospects, ensuring zero latency in the sales cycle.

## 🏗️ Workflow Architecture
The system follows a strict "Detect, Decide, Deliver" architecture:

1.  **Ingestion (Webhook):** Listens for the `BOOKING_CREATED` event from Cal.com's API.
2.  **Normalization (Set):** Flattens the complex JSON payload to extract critical fields: Name, Email, Timezone, and Meeting Type.
3.  **Intelligence (JavaScript):** A code node executes the domain parsing logic, determining the lead's professional status.
4.  **Decision Gate (Logic):** A conditional router filters out personal emails (optional) or routes them to a different nurture sequence.
5.  **Execution (Gmail):** High-value business leads receive a formatted confirmation message including their unique Lead ID.

## 🛠️ Built With
*   **[n8n](https://n8n.io/):** The central orchestration layer handling logic and state.
*   **[Cal.com](https://cal.com/):** The frontend booking engine and trigger source.
*   **[Gmail API](https://developers.google.com/gmail/api):** For reliable, authenticated transactional emailing.
*   **Node.js / JavaScript:** Used for the domain splitting and filtering algorithms.

## 📝 Configuration & Setup
To deploy this workflow in your environment:

1.  **Import Workflow:** Copy the provided JSON schema and paste it directly into your n8n editor.
2.  **Webhook Configuration:**
    *   Copy the *Production URL* from the **Cal.com Webhook** node.
    *   Navigate to **Cal.com > Settings > Webhooks**, create a new hook, and paste the URL.
3.  **Credential Mapping:**
    *   Connect your **Gmail OAuth2** credentials to the "Send a message" node.
4.  **Domain Logic:**
    *   Open the **"Detect Business Email"** node.
    *   Review the `const freeDomains` array. Add or remove domains (e.g., `protonmail.com`, `aol.com`) to fit your ideal customer profile (ICP).

## 🎨 Customization Options
*   **CRM Integration:** The "Create Lead" node prepares a perfect JSON object. You can attach a **HubSpot**, **Salesforce**, or **Pipedrive** node immediately after it to sync the lead to your CRM.
*   **Slack Alerts:** Add a Slack node to the "Business Email" path to notify the Sales VP: *"New B2B Lead Detected: [Company Name]"*.
*   **Rejection Logic:** Instead of ending the workflow for non-business emails, you can route them to a "Qualify" form or an automated rejection email.

## 📄 License
This project is open-source and available for modification.

---
*Operational Note: This workflow is configured to generate dummy Lead IDs (`LEAD-YYYYMMDD-XXXX`). For production use, ensure these map to your internal database keys.*