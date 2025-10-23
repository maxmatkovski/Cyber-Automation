🧠 DREAM Phishing Detector
Overview

DREAM Phishing Detector is an AI-powered phishing triage system designed to detect, analyze, and classify nation-state–style spear-phishing attacks.
Built using n8n for orchestration and MCP (Model Context Protocol) for AI reasoning and tool use, it automatically enriches incoming emails, evaluates threat indicators, and produces a structured, auditable incident report for security teams.

This project simulates a real-world SOC workflow for government and defense clients — combining automated enrichment, LLM-driven analysis, and explainable decision logic to reduce analyst workload while maintaining full transparency.

Architecture
Email (IMAP/Webhook)
    ↓
n8n → Parse Email → Extract IOCs (URLs, domains, hashes)
    ↓
n8n → Enrichment Layer → (VirusTotal, URLScan, WHOIS, MISP, Passive DNS)
    ↓
n8n → Send Enriched Data → MCP Agent
    ↓
MCP Agent → LLM + Tools → Risk Scoring + Nation-State Classification
    ↓
MCP Agent → Return Structured JSON (score, action, summary)
    ↓
n8n → Decision Logic → (Quarantine | Notify | Monitor)
    ↓
n8n → Create Ticket (JIRA/ServiceNow) + Slack/Email Alert
    ↓
n8n → Generate SOC Brief (PDF/Markdown)
    ↓
Database / Log Storage → Analyst Review → Feedback Loop (model + rules tuning)


