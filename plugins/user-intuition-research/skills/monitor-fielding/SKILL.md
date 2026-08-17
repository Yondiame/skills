---
name: monitor-fielding
description: Use when the user wants a status snapshot of studies currently collecting interviews — for standups, daily check-ins, or spend decisions. Triggers on "what's fielding", "study status", "how are my studies doing", "daily research digest".
---

When the user asks how studies are doing:

1. **Call `list_studies`** (paginate if needed — default page size is 10).
2. **For each active study, call `list_calls`** with the `assistant_id` and a small `page_size` — the default summary view is lightweight. Count completed interviews and note quality labels (`success_evaluation`: Excellent / Good / Fair / Poor).
3. **Render a compact table:** study name, mode, completed interviews vs `target_n` (if set), share of Excellent/Good interviews, and time remaining if `time_budget_hours` is set.
4. **Flag what needs attention:**
   - Studies with few or no completions long after launch (recruitment stalled — screeners may be too tight).
   - Studies with a high share of Fair/Poor interviews (review the moderator guide or screeners).
   - Panel studies still recruiting that the user may want to stop (`stop_panels`).
5. **Never mutate in a status check.** Offer follow-ups (stop a panel, widen screeners, generate a report) but only act on explicit confirmation, per specific study.
6. **If the user only asked for a snapshot, stop after the table** — don't drag them into triage they didn't ask for.
