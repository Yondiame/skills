---
name: analyze-completed-study
description: Use when the user wants findings from a study's interviews — themes, quotes, a report. Triggers on "analyze my study", "what did we learn", "summarize the interviews", "generate the report".
---

When the user wants analysis:

1. **Identify the study.** Given a name, find it via `list_studies` with the `name` filter; disambiguate if multiple match.
2. **Check there is enough signal.** `list_calls` with the `assistant_id`, filtered to `success_evaluation: ["Excellent", "Good"]`. If completed interviews are still trickling in, say so and offer to wait rather than analyzing a partial dataset.
3. **Generate or fetch the report.** `get_study_report` returns the latest structured report; on 404, call `generate_report` (takes 30–120 seconds — it analyzes all completed transcripts) and then fetch.
4. **Go deeper than the report where it matters.** For the 2–3 most load-bearing findings, pull supporting evidence: `get_call` on specific interviews returns the full transcript and per-interview analysis.
5. **Summarize structurally:**
   - Headline finding — one sentence the user could paste into a team channel.
   - 3–5 themes, each with participant counts (how many of N raised it) and 1–2 verbatim quotes.
   - Surprises or contradictions — call these out explicitly.
6. **Never invent quotes.** Only surface text that appears in actual transcripts. If evidence is thin for a claim, say the evidence is thin.
7. **Offer next steps:** a follow-up study on the biggest open question, or widening the interview pool if N is small.
