---
name: curate-interview-quality
description: Use when the user wants to review interview quality or exclude low-quality interviews from analysis. Triggers on "check interview quality", "hide the bad interviews", "review the Poor calls", "clean up the data".
---

When the user wants to curate quality:

1. **Pull the distribution.** `list_calls` defaults to 5 rows per page, so never count returned rows — for each label, call `list_calls` with `success_evaluation: ["<label>"]` and `page_size: 1`, and read the envelope's `total_count`. Report the four counts.
2. **Review the low end.** For Fair/Poor interviews, call `get_call` with `include: ["transcript"]` — the default response is only a ~6-turn excerpt — and summarize in one line each WHY it scored low (short answers, off-topic, technical issues).
3. **Recommend, then act on confirmation.** For interviews the user agrees are unusable, `update_call` with `is_visible: false` hides them from the dashboard without deleting — reversible. Only delete (`delete_call`) if the user explicitly asks; prefer hiding.
4. **Overrides:** if the user disagrees with a label after reading a transcript, `update_call` accepts a `success_evaluation` override.
5. **Report the after-state:** how many interviews remain visible, and whether that's still enough signal for analysis (flag if the usable N dropped sharply).
6. **Never hide or delete in bulk without a per-study confirmation,** and never touch calls the user hasn't reviewed.
