# Prompt Log — Abdoul Sawadogo

**Project:** Security Alert Triage Bot
**Team:** Justin Quinones, Alexander Lustig, Ujjwal Singh, Abdoul Sawadogo
**My Component:** Monitoring (Dashboard)
**AI Tools Used:** GitHub Copilot

---

## How to Use This Log
Add an entry for each significant AI interaction:
- Copilot Chat conversations where you asked it to generate, explain, or debug something
- Moments where Copilot was wrong and you had to fix it (these are the most valuable entries)
- Cases where you refined a prompt to get a better result


---

## 2026-05-01 — Generating a README for the Monitoring Dashboard component

**Context:** Working in VS Code with copilot-instructions.md open. My dashboard 
was already built and connected to my teammates' Airtable data. I just needed 
to actually document it properly.

**Prompt:**
> Using the project context from .github/copilot-instructions.md, write a complete 
> README for my Monitoring component. Include:
> - What it does (2-3 sentences)
> - How it connects to other components (inputs and outputs)
> - Setup instructions (what accounts/keys are needed, what to configure in Streamlit/Airtable)
> - How to test it (specific steps)
> - Known limitations

**Result:** Copilot generated a full README covering everything I asked for. It 
pulled the actual Airtable field names from the context file which was nice, things 
like alert_id, severity, status, and analyzed_at showed up correctly instead of 
generic placeholders.

**Evaluation:** Overall it was solid. The structure matched what the assignment 
wanted and the component connections were described accurately. The one thing that 
needed updating was the Streamlit deployment section since that detail wasn't fully 
in the context file yet.

**What I changed:** Left a note to update the Airtable API key section once we 
configure it for real. Also flagged the clone URL as a placeholder to fix later.

**What I learned:** The more specific your context file is, the better the output. 
Copilot actually used our real field names because they were in copilot-instructions.md. 
Next time I want to do something like this I will make sure the schema section is 
completely filled in first.

---

## 2026-05-01 — Running the Checkpoint 2 readiness audit

**Context:** It was Checkpoint 2 week and I wanted to get a clear picture of where 
things stood before submitting. I had copilot-instructions.md open and ran the 
audit prompt from the Week 8 lab again.

**Prompt:**
> Using the context in .github/copilot-instructions.md, perform a Checkpoint 2 
> readiness assessment for my capstone project. Answer these 10 questions based 
> on the current project state. For each question give a status: Ready / At Risk / Blocked.
> Then provide a prioritized fix list based on the gaps found.

**Result:** Copilot flagged 4 blockers: the Airtable schema not being finalized, 
the Specialist trigger not firing, status field transitions not working, and no 
confirmed standalone demos for all components.

**Evaluation:** It was pretty accurate. Those 4 things matched exactly what we 
found during the actual end-to-end test. The only thing off was it marked the 
dashboard as At Risk when it was actually fully working, but that was because 
the context file had not been updated yet to reflect that.

**What I changed:** After the audit I went and updated the Current State section 
in copilot-instructions.md so the dashboard shows as working. That way future 
prompts will be more accurate.

**What I learned:** The audit is only as good as what is in the context file. 
If copilot-instructions.md is outdated the results will be off too. Keeping 
that file current is more important than I originally thought.

---

## 2026-05-01 — Generating the Checkpoint 2 results document

**Context:** We had just finished the end-to-end test. I had screenshots from 
Airtable and the live dashboard and needed to write up checkpoint2-results.md 
to submit with everything else.

**Prompt:**
> Based on our end-to-end test results, write a checkpoint2-results.md file 
> documenting what happened at each component stage. The test record was alert-007, 
> a brute force attack. Ingestion and AI Core worked. Specialist partially worked 
> because the status field stayed None and GitHub Issue creation was not confirmed. 
> Dashboard is fully live showing all 6 records.

**Result:** It produced a full results document with a component-by-component 
breakdown, a gaps section, and a prioritized fix plan. The structure covered 
everything the assignment asked for.

**Evaluation:** The content was accurate but the writing style was way too formal. 
It sounded like a generated report rather than something a student actually wrote 
after running a real test. I had to go back and ask for a rewrite.

**What I changed:** Asked Copilot to humanize the tone and make it sound more 
natural. The second version was a lot better. It was honest about where things 
broke without sounding robotic about it.

**What I learned:** Always check the tone, not just the facts. Copilot got the 
details right but the voice was off. A simple follow-up prompt asking it to 
rewrite in a more natural way fixed it pretty quickly.

---

## 2026-05-01 — Comparing Week 8 vs Week 9 audit results

**Context:** I had the new Checkpoint 2 audit done and wanted to put it side 
by side with the Week 8 version to see how much had actually changed.

**Prompt:**
> Compare the Week 8 and Week 9 audit results side by side. Show what improved, 
> what is still blocked, and what the team should focus on before Week 10.

**Result:** Copilot made a comparison table showing Ingestion, AI Core, and the 
Dashboard all moved from At Risk to Ready since Week 8. The Specialist trigger 
and status transitions were still blocked. Overall project status went from 
At Risk to Partial.

**Evaluation:** This was actually really useful. Seeing it laid out clearly made 
it obvious that real progress happened in one week even if it did not feel like 
it during the test. Three components improving in a week is not bad at all.

**What I changed:** Added a short paragraph below the table to explain what the 
changes actually meant for the team going forward. The table alone felt a bit 
incomplete without some context around it.

**What I learned:** Running the same audit prompt at different checkpoints and 
comparing them is a genuinely good way to track progress. I am going to do this 
again at Checkpoint 3.

---

## 2026-05-01 — Updating copilot-instructions.md after Checkpoint 2

**Context:** After the end-to-end test it was clear the context file was pretty 
outdated. The dashboard was live, Ingestion was working, and the schema had 
changed. The Current State section still said we were in Weeks 4-6.

**Prompt:**
> Update the Current State section of copilot-instructions.md to reflect where 
> the project is after Checkpoint 2. What is working: Ingestion, AI Core, Dashboard. 
> What is in progress: Specialist trigger fix, schema finalization. Known issues: 
> status field not advancing, missing raw_payload on alert-007, response time 
> metrics are estimated until resolved_at timestamps come in.

**Result:** Copilot rewrote the section cleanly with accurate bullets for each 
category. It also caught that the Repository Structure section needed updating 
since we added the docs/ folder and it fixed that too without me asking.

**Evaluation:** No real issues with this one. The prompt was specific enough that 
there was not much room to guess wrong. The output was accurate on the first try.

**What I changed:** Just small wording tweaks here and there to match how we 
actually talk about the project as a team.

**What I learned:** Updating the context file right after a milestone is the 
right move. If I had waited a week I would have forgotten half the details from 
the test. The file works best when it actually reflects where things are right now.