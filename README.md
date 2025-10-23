# 🧠 DREAM Phishing Detector

## Overview  
**DREAM Phishing Detector** is an AI-powered phishing triage system designed to detect, analyze, and classify **nation-state–style spear-phishing attacks**.  
Built using **n8n** for orchestration and **MCP (Model Context Protocol)** for AI reasoning and tool use, it automatically enriches incoming emails, evaluates threat indicators, and produces a structured, auditable incident report for security teams.  

This project simulates a real-world SOC workflow for government and defense clients — combining automated enrichment, LLM-driven analysis, and explainable decision logic to reduce analyst workload while maintaining full transparency.  

---

## 🏗️ Architecture  

| Stage | Component | Description |
|-------|------------|-------------|
| 1 | **Email Ingestion** | IMAP or Webhook trigger captures message |
| 2 | **Parsing & Extraction** | n8n extracts IOCs (URLs, domains, hashes) |
| 3 | **Enrichment** | VirusTotal, URLScan, WHOIS, MISP, Passive DNS |
| 4 | **AI Analysis** | MCP Agent (LLM + Tools) scores risk and classifies |
| 5 | **Decision Logic** | Determines Quarantine / Notify / Monitor |
| 6 | **Incident Handling** | Creates JIRA/ServiceNow ticket + Slack alert |
| 7 | **Reporting** | Generates SOC brief (PDF/Markdown) |
| 8 | **Logging** | Database storage + analyst feedback loop |
