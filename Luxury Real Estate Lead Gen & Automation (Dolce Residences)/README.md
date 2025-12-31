This is a professional, high-impact `README.md` for your GitHub repository. It reflects the premium nature of the **Dolce Residences** project while highlighting the technical sophistication of the automation.

***

# 🏰 Luxury Real Estate Lead Gen & Automation (Dolce Residences)
An institutional-grade lead capture and qualification engine built with **n8n**, **Airtable**, and **Gmail** to sell high-end villas in Tivat, Montenegro.

![n8n](https://img.shields.io/badge/n8n-Workflow-orange) ![Airtable](https://img.shields.io/badge/Airtable-CRM-blue) ![Gmail](https://img.shields.io/badge/Gmail-Notification-red) ![Real Estate](https://img.shields.io/badge/Industry-Luxury%20Real%20Estate-gold)

## 📖 Project Overview
This workflow is designed to move away from "black box" lead generation. It allows real estate developers and agents to own their infrastructure, ensuring that high-net-worth individuals (HNWIs) from the UK and DACH (Germany, Austria, Switzerland) regions receive a premium, instant response while the agent receives enriched lead data.

The system doesn't just collect emails; it **cleanses data, scores lead quality, and triggers instant VIP notifications** via personalized HTML communications.

### Key Features
*   **Data Sovereignty:** Full ownership of the lead flow—no monthly SaaS retainers for "per-lead" systems.
*   **Automated Data Cleansing:** Uses JavaScript to normalize names (Title Case) and phone numbers (E.164) for immediate WhatsApp follow-up.
*   **VIP Qualification Logic:** Automatically flags leads as "High-Value" based on geographical origin (DACH/UK) and investment intent.
*   **Airtable Integration:** Acts as a headless CRM, logging every interaction for a permanent audit trail.
*   **Premium HTML Alerts:** Generates a sophisticated internal notification email featuring "AI-style" insights and recommended follow-up actions.

## 🏗️ Workflow Architecture
The workflow follows a linear, high-integrity path:

1.  **Ingestion (Webhook):** Receives raw data from high-converting front-end forms (Framer, Webflow, or Typeform).
2.  **Transformation (JavaScript):** A code node cleanses the data and generates a `wa_link` (Direct WhatsApp link) so the agent can initiate contact with one click.
3.  **Persistence (Airtable):** Every lead is immediately logged to an Airtable Base before any further processing to prevent data loss.
4.  **Qualification (Filtering):** An logic-gate node separates "Browsers" from "High-Value Investors" using region and intent-based scoring.
5.  **Distribution (Gmail):** Delivers a beautifully formatted HTML dossier notification to the agent/developer, including budget details and specific lead messages.

## 🛠️ Built With
*   **[n8n](https://n8n.io/):** The core engine hosting the logic and API integrations.
*   **[Airtable](https://airtable.com/):** Used as the primary lead database and sales pipeline.
*   **[Gmail API](https://developers.google.com/gmail/api):** For high-deliverability internal and external notifications.
*   **JavaScript:** For custom data formatting and lead scoring logic.

## 📝 Configuration & Setup
To deploy this workflow:
1.  **Import JSON:** Copy the `.json` file from this repository and paste it into your n8n canvas.
2.  **Airtable Setup:** Create an Airtable table with the following fields: `Name`, `Email`, `Phone`, `Country`, `Intent`, `Budget`, and `VIP_Status`. Update the Node ID with your Base and Table ID.
3.  **Gmail OAuth:** Connect your Google Cloud Console credentials to the Gmail node.
4.  **Webhook Mapping:** Point your website's form "Submit" action to the Webhook URL provided by the first node.

## 🎨 Customization
*   **Targeting Logic:** Modify the `Data Cleansing & Logic` node to include different priority countries (e.g., adding "USA" or "UAE").
*   **Lead Scoring:** Adjust the `isHighValue` variable to trigger based on specific budget thresholds (e.g., only leads > €2M).
*   **Styling:** The Gmail node contains an inline CSS template; update colors and logos to match your specific real estate brand.

## 📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

---
*Disclaimer: This workflow is optimized for luxury asset sales. Ensure your data collection methods comply with local GDPR and data privacy regulations.*