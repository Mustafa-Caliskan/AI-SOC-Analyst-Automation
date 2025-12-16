# 🛡️ AI-Powered SOC Analyst Automation

> **Automated Incident Response System** powered by **n8n**, **Splunk**, **Google Gemini**, and **Llama 3**.

![n8n](https://img.shields.io/badge/Orchestration-n8n-ff6c37?style=flat&logo=n8n)
![Splunk](https://img.shields.io/badge/SIEM-Splunk-000000?style=flat&logo=splunk)
![AI](https://img.shields.io/badge/AI-Gemini%20%2F%20Llama3-blue)
![Security](https://img.shields.io/badge/Security-SOAR-red)

This project is an intelligent security automation workflow designed to combat **Alert Fatigue** in SOC (Security Operations Center) environments. It acts as a **Tier 1 SOC Analyst** by automatically capturing alerts from Splunk, enriching them with threat intelligence, analyzing the intent using a "Dual-Engine" AI approach, and generating professional incident reports.

![Workflow Diagram](workflow-diagram.png)

---

## 🚀 Key Features

* **⚡ Real-time Event Capture:** Listens for HTTP Webhooks triggered by **Splunk** alerts.
* **🕵️ Threat Intelligence Enrichment:** Automatically scans suspicious IP addresses using the **VirusTotal API** to check for reputation and malware history.
* **🧠 Dual-Engine AI Analysis:**
    * **Analyst Engine (Google Gemini):** Deeply analyzes raw logs and threat data to determine attack type (e.g., SQL Injection, Brute Force) and MITRE ATT&CK techniques.
    * **Editor Engine (Llama 3 via Groq):** Formats the analysis into a standardized report and handles logic tasks like **Timezone Conversion (UTC to Local Time)**.
* **📝 Automated Reporting:** Sends a clean, action-oriented email report to the security team, ready for review.

---

## ⚙️ Architecture & Workflow

1.  **Trigger:** Splunk detects a suspicious pattern (e.g., SQLi attempt) and sends a JSON payload via Webhook.
2.  **Enrich:** n8n extracts the `src_ip` and queries **VirusTotal**.
3.  **Analyze:** The raw log + VirusTotal data is sent to **Google Gemini** with a specific "SOC Analyst" system prompt.
4.  **Refine:** The analysis is passed to **Llama 3 (Groq)** to format the text and calculate the correct local time (e.g., `UTC +3`).
5.  **Act:** An HTML/Text email is sent via SMTP containing the final report.

---

## 📊 Sample Report Output

The system generates a human-readable report without any manual intervention:

![Sample Report](sample-report.png)

---

## 🛠️ Splunk Configuration

To trigger this automation, create a **Correlation Search** or **Alert** in Splunk. Here is the SPL (Search Processing Language) query used for this project (focused on SQL Injection):

```splunk
index=web_logs sourcetype=access_combined
| regex uri_query="(?i)(union\s+select|select\s+.*\s+from|insert\s+into|update\s+.*\s+set|OR\s+1=1)"
| stats count by src_ip, uri_query, user_agent, _time
| rename uri_query as message
```

**Trigger Action:** Select **Webhook** and paste your n8n production URL.

---

## 🔧 Installation & Setup

### Prerequisites

* **n8n** (Self-hosted or Cloud)
* **Splunk** Enterprise / Cloud
* **API Keys** for:
    * Google Gemini (PaLM)
    * Groq (for Llama 3)
    * VirusTotal
* **SMTP** (Gmail or other provider)

### Steps

1. **Clone/Download:** Download the `AI-SOC-Analyst-Automation.json` file from this repository.
2. **Import:** Open your n8n dashboard, go to **Workflows > Import from File**, and select the JSON file.
3. **Credentials:** Double-click on the nodes to configure your credentials:
    * **VirusTotal** → Header Auth
    * **Google Gemini** → Google PaLM API
    * **Groq** → Groq API
    * **Send Email** → SMTP Credentials
4. **Activate:** Toggle the **Active** switch in n8n.
5. **Test:** Trigger a test alert from Splunk or send a mock JSON to the Webhook URL.

---

## 📂 Project Structure

```
├── AI-SOC-Analyst-Automation.json    # n8n workflow file
├── workflow-diagram.png               # Architecture diagram
├── sample-report.png                  # Example output report
└── README.md                          # This file
```

---

## 🎯 Use Cases

* **Alert Triage:** Automatically classify and prioritize security alerts.
* **Threat Hunting:** Enrich indicators with external intelligence sources.
* **Compliance Reporting:** Generate audit-ready incident reports.
* **Training:** Demonstrate AI-driven automation in cybersecurity education.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a **Pull Request** or open an **Issue** for suggestions and improvements.

---

## 📜 License

This project is open-source and available under the **MIT License**.

---

**Developed to demonstrate the power of Low-Code Automation and Generative AI in Cybersecurity.**

