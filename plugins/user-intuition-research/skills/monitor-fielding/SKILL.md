---
name: monitor-fielding
description: Use when the user wants a read-only status snapshot of User Intuition studies or interviews.
---

When the user asks for fielding status:

1. Call `list_studies`, paginating when necessary. Use response totals rather than counting only the current page.
2. For each study in scope, call `list_interviews` with its `study_id`. Use `status` and `quality` filters when the user asks for a breakdown.
3. Present a compact table with study name, recruiting method, lifecycle status, interview count, and quality distribution when available.
4. Flag stalled recruitment, no completions, or a high Fair/Poor share as observations, not diagnoses.
5. Keep the workflow read-only. Offer `pause_study`, `resume_study`, `stop_study`, or report generation as follow-ups, but do not mutate unless the user explicitly asks.
