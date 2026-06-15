# 🤖 Automated Audio Meeting Report Generator (n8n Workflow)

This repository contains an **n8n workflow** designed to automate the process of transcribing an audio file (like a recorded meeting) and generating a structured business summary using AI.

It leverages **AssemblyAI** for high-quality audio transcription and **OpenAI's GPT-4o-mini** model for intelligent report generation.

---

## ✨ Features

* **Form-Triggered:** Starts automatically upon submission of an audio file and user email via a public n8n form.
* **Audio Transcription:** Uploads and transcribes the audio, including support for **speaker labels**.
* **AI Summarization:** Uses a custom system prompt to force the AI to generate a structured report with specific sections.
* **Structured Output:** The final report includes:
    * **Key Decisions Made**
    * **Action Items** (with owners and due dates if mentioned)
    * **General Discussion Summary**
* **Email Delivery:** Converts the final report into a text file and automatically emails it as an attachment to the submitting user.

---

## 🚀 Prerequisites

To run this workflow, you will need:

1.  An **n8n Instance** (cloud or self-hosted).
2.  An **AssemblyAI API Key** (for transcription and audio upload).
3.  An **OpenAI API Key** (for the AI summarization).
4.  An **SMTP Account** configured in n8n (for sending the final email).

---

## 🛠️ Setup Instructions

### 1. Import the Workflow

1.  Copy the JSON content from the workflow file (`assembly_ai_report_generator.json`) in this repository.
2.  Open your n8n editor.
3.  Click **New** and then select **Import from JSON**.
4.  Paste the workflow JSON and click **Import**.

### 2. Configure Credentials

The workflow relies on secure credentials for external services. You must update these in the n8n interface:

| Node | Credential Type | Action Required |
| :--- | :--- | :--- |
| **HTTP Request** (and **1**, **2**) | Custom Header `Authorization` | **Replace** the placeholder value `***************` with your **actual AssemblyAI API Key**. |
| **OpenAI Chat Model** | **OpenAiApi** | **Replace** the linked credential with your **OpenAI API Key**. |
| **Send Email** | **SMTP** | **Replace** the linked credential with your working **SMTP Account** credentials. |

### 3. Final Checks

* **Form URL:** After activating the workflow, open the **On form submission** node and copy the **Public URL**. This is the link you will share to start the process.
* **Sender Email:** Update the `fromEmail` field in the **Send Email** node (`selva@digimabble.com`) to your desired sender address.

---

## 🧪 Testing the Workflow

1.  Ensure all API keys and SMTP settings are correct.
2.  **Activate** the workflow.
3.  Open the **Form URL** in your browser.
4.  Fill in a test name and a valid email address you can check.
5.  Upload a short audio file (e.g., an MP3 or WAV of a mock meeting).
6.  Submit the form.

The workflow will run, wait 60 seconds for transcription, generate the report, and you should receive the summary via email shortly after!
