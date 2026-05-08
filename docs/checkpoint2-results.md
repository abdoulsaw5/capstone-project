# Checkpoint 2 Results

**Date:** 2026-05-01
**Team:** Justin Quinones, Alexander Lustig, Ujjwal Singh, Abdoul Sawadogo
**Test record:** alert-007 — a brute force attack flagged by Suricata, showing 47 
failed SSH login attempts from external IP 185.220.101.45 targeting 10.0.0.12, 
classified as High severity.

## End-to-End Status: PARTIAL

## Component-by-Component Results

### Ingestion
- **Status:** Working
- **What happened:** Justin's ingestion workflow picked up alert-007 without issues. 
The record landed in Airtable. All the key fields were there: alert type, 
description, source and destination IPs, timestamp, severity, and source tool. 
No normalization errors.
- **Screenshot:** screenshots/ingestion-airtable.png

### AI Core
- **Status:** Working
- **What happened:** Alexander's multi-agent system processed the alert and filled 
in the recommendation, analyst notes, and researcher notes. For alert-007 it 
correctly identified the threat as worth escalating, which lines up with what 
we'd expect from a confirmed brute force attempt. The reasoning looked solid.
- **Screenshot:** screenshots/aicore-airtable.png

### Specialist (Action)
- **Status:** Partially Working
- **What happened:** This is where the pipeline stalled a bit. alert-007's status 
field is showing "None" instead of updating to something like "escalated" after 
Ujjwal's workflow runs. We haven't confirmed a GitHub Issue was created for this 
record either. The workflow may not be triggering correctly on the AI Core output.
- **Screenshot:** screenshots/specialist-airtable.png

### Integration Dashboard
- **Status:** Working
- **What happened:** This part honestly exceeded expectations. The SOC Command 
Center is pulling all 6 records from Airtable in real time and displaying them 
correctly. severity breakdown, source distribution, alert type charts, response 
time estimates, and the full alert feed with recommendations. It updates 
dynamically when new data comes in.
- **Screenshot:** screenshots/dashboard-working.png

## Gaps Found
- The status field isn't advancing after the Specialist runs — records stay stuck 
on "New" or "None" instead of moving to "escalated" or "resolved". This breaks 
the handoff signal the dashboard relies on for accurate metrics.
- alert-007 is missing its raw_payload, which suggests something in the ingestion 
step didn't fire fully for that record.
- We haven't confirmed a GitHub Issue ticket was actually created for any 
High/Critical alert yet this needs to be verified.
- Response time metrics on the dashboard are estimated right now because we don't 
have real resolved_at timestamps yet. Once the Action component starts writing 
those, the numbers will be accurate.

## Fix Plan
1. Ujjwal — fix the n8n workflow trigger so it picks up records after AI Core 
finishes and updates the status field correctly. This is the top priority because 
everything downstream depends on it.
2. Justin — check why alert-007 didn't get a raw_payload written and make sure 
all future records include it.
3. Ujjwal — verify that GitHub Issues ticket creation is actually firing for 
High and Critical alerts, not just running silently.
4. Once resolved_at timestamps are flowing in, the dashboard response time 
metrics will automatically become accurate no code changes needed on my end.
5. Aboul- I will update the dashboard accordingly. I am not sure if anything 
will break once the group members updadte their parts.