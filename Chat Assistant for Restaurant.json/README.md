Here is a professional, high-impact `README.md` tailored for the **Spice Haven Bistro RAG** workflow provided in your JSON.

***

# 🍽️ AI-Powered Hospitality Concierge & RAG Knowledge Base
An enterprise-grade **Retrieval-Augmented Generation (RAG)** system built with **n8n**, **Pinecone**, and **Groq**. Designed for **Spice Haven Bistro**, this workflow automates knowledge ingestion from Google Drive and powers a high-speed, context-aware customer support agent.

![n8n](https://img.shields.io/badge/n8n-LangChain-orange) ![Pinecone](https://img.shields.io/badge/Pinecone-Vector%20DB-blue) ![Groq](https://img.shields.io/badge/Groq-Llama3-purple) ![HuggingFace](https://img.shields.io/badge/HuggingFace-Embeddings-yellow)

## 📖 Project Overview
In the fast-paced hospitality industry, static FAQ pages are obsolete. This project implements a **dual-pipeline AI architecture** that ensures your guest assistant always has the latest information regarding menus, pricing, hours, and policies.

The system performs two critical functions:
1.  **Knowledge Sync:** Automatically crawls specific Google Drive folders, vectorizes restaurant documents, and indexes them.
2.  **Intelligent Concierge:** A conversational AI agent that retrieves this specific data to answer guest queries with hallucination-free accuracy using Llama 3.

### Key Features
*   **Dynamic Knowledge Base:** "Black-box" knowledge is eliminated. Simply upload a PDF or Doc to Google Drive, and the AI learns it instantly.
*   **High-Speed Inference:** Utilizes **Groq** running `llama-3.3-70b-versatile` for near-instant responses, crucial for retaining website visitors.
*   **Vector Search Retrieval:** Uses **Pinecone** to perform semantic searches, ensuring the AI cites actual restaurant policies rather than guessing.
*   **Memory Management:** Includes Window Buffer Memory to maintain context throughout a multi-turn conversation with a guest.
*   **Cost-Effective Embeddings:** leverages **HuggingFace Inference** for generating high-quality vector embeddings without high operational costs.

## 🏗️ Workflow Architecture
The system is divided into two distinct operational flows within a single canvas:

### 1. The Ingestion Pipeline (Database Update)
*   **Trigger:** Manual execution (or scheduled).
*   **Extraction:** Scans a designated Google Drive folder (e.g., "Spice Haven Docs") and downloads all files.
*   **Transformation:** Uses a recursive character text splitter to chunk documents into digestible pieces.
*   **Embedding & Loading:** Converts text to vectors via HuggingFace and upserts them into the Pinecone index (`sample`).

### 2. The Inference Pipeline (Guest Chat)
*   **Interaction:** A guest asks a question via the chat interface.
*   **Agent Reasoning:** The AI Agent determines if it needs external knowledge.
*   **Retrieval:** Queries the Pinecone Vector Store for the top 14 relevant document chunks.
*   **Synthesis:** The Groq LLM synthesizes the retrieved context into a polite, helpful response for the guest.

## 🛠️ Built With
*   **[n8n](https://n8n.io/):** The orchestration layer utilizing advanced LangChain nodes.
*   **[Pinecone](https://www.pinecone.io/):** Long-term vector memory for the AI.
*   **[Groq](https://groq.com/):** The inference engine powering the Llama 3 model.
*   **[HuggingFace](https://huggingface.co/):** Provides the embedding models.
*   **[Google Drive](https://www.google.com/drive/):** The CMS (Content Management System) for raw documents.

## 📝 Configuration & Setup
To deploy this workflow:

1.  **Import JSON:** Copy the `.json` file from this repository and paste it into your n8n canvas.
2.  **Credential Setup:** You will need API keys for:
    *   Google Drive (OAuth2)
    *   Pinecone
    *   Groq
    *   HuggingFace
3.  **Vector Database:** Create a Pinecone index named `sample` with dimensions matching your HuggingFace model (usually 384 or 768).
4.  **Google Drive Mapping:** Replace the folder ID in the "Search files and folders" node with the ID of your own document folder.
5.  **Run Ingestion:** Click "Test Workflow" once to populate your database before chatting.

## 🎨 Customization
*   **Brand Voice:** Edit the `System Message` in the **AI Agent** node to change the persona from "Spice Haven Bistro Assistant" to your own brand.
*   **Model Swapping:** The workflow uses `llama-3.3-70b-versatile`. You can swap this in the **Groq Chat Model** node for smaller/larger models depending on complexity needs.
*   **Retrieval Depth:** Adjust the `Top K` value in the **Pinecone Vector Store (Retrieve)** node to control how much context the AI reads (currently set to 14 documents).

## 📄 License
This project is licensed under the MIT License.

---
*Note: This workflow requires the n8n LangChain node set. Ensure your n8n instance is updated to the latest version to support AI Agents.*