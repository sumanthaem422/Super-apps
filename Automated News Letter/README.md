This is a professional, comprehensive `README.md` file tailored for your GitHub repository. It explains the project clearly for developers and users who might want to fork or use your workflow.

***

# 🏔️ AI-Powered Denver Daily Newsletter
An automated "Digital Newspaper Factory" built with **n8n**, **Groq AI**, and **Gmail**.

[![n8n](https://img.shields.io/badge/n8n-Automation-FF6D5A?style=flat&logo=n8n)](https://n8n.io/)
[![Groq](https://img.shields.io/badge/AI-Groq--Llama3.3-orange?style=flat)](https://groq.com/)
[![Gmail](https://img.shields.io/badge/Email-Gmail-D14836?style=flat&logo=gmail)](https://gmail.com/)

## 📖 Project Overview
This project is a fully automated workflow that sources, curates, and distributes a hyper-local daily newsletter for Denver, Colorado. Every morning, the system fetches real-time data, uses Large Language Models (LLMs) to summarize the most important stories, and sends a professionally designed HTML email to subscribers.

### **Key Features**
- **Real-Time Sourcing:** Automatically pulls news from `Denverite` and local event calendars via RSS.
- **Live Weather:** Integrates with the `Open-Meteo` API for accurate local forecasts.
- **AI-Powered Curation:** Uses **Groq (Llama 3.3)** to act as an "Editor-in-Chief," writing catchy intros and concise 2-sentence summaries.
- **Responsive Design:** Generates a beautiful, mobile-friendly HTML newsletter template.
- **Zero-Maintenance:** Runs entirely on a schedule (Triggered daily at 7:00 AM).

---

## 🏗️ Workflow Architecture

The workflow is divided into five logical stages:

1.  **Trigger & Config:** A `Daily Schedule` node starts the process, while a `Configuration` node stores URLs and recipient details.
2.  **Sourcing:** Parallel nodes fetch News (RSS), Events (RSS), and Weather (JSON API).
3.  **Preparation:** Data is cleaned, standardized, and aggregated into a single text block.
4.  **AI Analysis:** The `Groq LLM` processes the data and outputs structured JSON containing summaries and titles.
5.  **Distribution:** The `HTML Generator` creates the visual layout, and the `Gmail` node sends the final email.

---


## 🛠️ Built With
- **[n8n](https://n8n.io/)** - Workflow automation platform.
- **[Groq](https://groq.com/)** - Ultra-fast AI inference engine.
- **[Denverite RSS](https://denverite.com/)** - Real-time local news source.
- **[Open-Meteo](https://open-meteo.com/)** - Public weather API (No-key required).

---

## 📝 Customization
- **Change Cities:** Update the coordinates in the Weather API node and the RSS URLs in the Configuration node to adapt this for any city.
- **Adjust AI Tone:** Modify the `System Message` in the **Newsletter Content Generator** node to change the personality of the newsletter (e.g., more humorous, more professional, or purely factual).
- **Styling:** Edit the CSS in the **Generate HTML Newsletter** node to match your personal branding.

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
**Disclaimer:** *This project is for educational purposes. Ensure you comply with the Terms of Service of the RSS feeds and APIs you utilize.*