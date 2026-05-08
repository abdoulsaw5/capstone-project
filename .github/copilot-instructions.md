# Capstone Project Context

## Project
- **Name:** Security Alert Triage Bot
- **Team:** 
  - Justin Quinones (Ingestion)
  - Alexander Lustig (Analysis/AI Core)
  - Ujjwal Singh (Action/Specialist)
  - Abdoul Sawadogo (Monitoring/Dashboard — my component)
- **What it does:** An AI-powered system that ingests raw security alerts via webhook, 
uses a multi-agent AI system to triage and classify them, automatically creates tickets 
for high-priority threats, and displays everything on a real-time dashboard. SOC analysts 
and Security Managers benefit by spending time only on verified, high-impact incidents.
- **Project type:** Security Alert Triage Bot

## Architecture
- **Ingestion:** Justin's component — n8n webhook receives raw JSON alerts from 
simulated security tools (Firewalls, EDR), normalizes them into a common schema, 
and writes standardized records to Airtable.
- **AI Core:** Alexander's component — CrewAI/LangGraph multi-agent system 
(analyst, researcher, recommender) reads normalized alerts from Airtable, performs 
deep reasoning, and outputs a triage recommendation (True/False Positive) with a 
reasoning trace back to Airtable.
- **Specialist:** Ujjwal's component — n8n workflow reads triage recommendations 
from Airtable, creates tickets in GitHub Issues for high-severity alerts, and writes 
resolution notes for closed alerts back to Airtable.
- **Integration:** My component — Streamlit dashboard reads all processed Airtable 
records and timestamps, displays real-time charts for triage volume, severity 
distribution, and response time metrics in a "Command Center" view for SOC managers.

## Tech Stack
- Streamlit (dashboard UI — my component)
- Airtable (shared central database "Source of Truth" for all components)
- n8n Cloud (workflow automation Ingestion and Action components)
- CrewAI / LangGraph (multi-agent reasoning — Analysis component)
- Groq API (LLM inference LLaMA 3)
- GitHub Issues (automated ticket creation Action component)
- GitHub (repo, documentation, portfolio)

## Airtable Schema
[Update with real field names once team finalizes below is the expected structure]

### Alerts Table
| Field | Type | Written By | Status Values |
|-------|------|-----------|---------------|
| alert_id | text | Ingestion | |
| alert_type | text | Ingestion | brute_force, sql_injection, unauthorized_login |
| severity | select | Ingestion | low, medium, high, critical |
| raw_payload | long text | Ingestion | |
| normalized_at | datetime | Ingestion | |
| is_true_positive | boolean | Analysis | |
| reasoning_trace | long text | Analysis | |
| triage_recommendation | text | Analysis | |
| analyzed_at | datetime | Analysis | |
| status | select | Action | pending, triaged, escalated, resolved |
| ticket_url | url | Action | |
| resolved_at | datetime | Action | |
| is_escalated | boolean | Action | |

## Conventions
- Field names: snake_case
- Status values: lowercase
- Date fields end in _at
- Boolean fields use is_ prefix

## Current State
- **What's working:** 
  - Ingestion is live, alerts are being written to Airtable correctly via n8n webhook
  - AI Core is processing alerts recommendation, analyst_notes, and researcher_notes 
  are being populated automatically
  - Dashboard (my component) is fully live — SOC Command Center displays real-time 
  charts, severity distribution, alert feed, and response time metrics from Airtable
  - End-to-end flow is 3/4 complete. Ingestion → AI Core → Dashboard all connected

- **What's in progress:** 
  - Specialist/Action component trigger fix — status field not advancing after 
  Ujjwal's n8n workflow runs
  - GitHub Issues ticket creation not yet confirmed for High/Critical alerts
  - Airtable schema still needs to be fully finalized across all components

- **Known issues:** 
  - Status field stuck on "New" or "None" after Specialist runs — breaks handoff 
  signal between components
  - alert-007 missing raw_payload field - Justin fixing on Ingestion side
  - Response time metrics on dashboard are estimated until resolved_at timestamps 
  start flowing in from the Action component

- **Next milestone:** Week 10 — fix Specialist trigger, confirm full end-to-end 
record with all 4 components, finalize Airtable schema

## Repository Structure
capstone-project/
└── .github/
    └── copilot-instructions.md
└── dashboard/
    └── app.py (Streamlit dashboard — my component)
└── docs/
    └── checkpoint2-results.md
    └── checkpoint2-audit.md
└── screenshots/
    └── copilot-instructions.png
└── README.md
