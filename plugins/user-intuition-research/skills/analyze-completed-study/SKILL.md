---
name: analyze-completed-study
description: Use when the user wants findings, themes, evidence, or a report from completed User Intuition interviews.
---

When the user asks for analysis:

1. Identify the study with `list_studies`; disambiguate similar names. Call `get_study` for full context.
2. Call `list_interviews` with the `study_id` and check whether enough completed, usable interviews exist. Say when evidence is still thin.
3. Call `get_study_report`. If no report exists or it is stale and the user asked for fresh analysis, call `generate_report`, then fetch the report again.
4. For load-bearing findings, call `get_interview` on the supporting interview IDs and verify evidence in the returned messages. Never invent quotes or attribute a claim to an interview you did not fetch.
5. Summarize the headline, 3–5 themes, participant counts when supported, evidence, contradictions, and open questions.
6. Distinguish direct evidence from inference. Offer a follow-up study when the biggest uncertainty cannot be answered from the current interviews.
