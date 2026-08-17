---
name: design-screeners
description: Use when the user wants to control who qualifies for an existing study — by role, behavior, demographics, or product usage. Triggers on "add screeners", "only interview people who X", "screen for Y", "filter participants".
---

When the user wants screeners on a study:

1. **Read before writing.** Call `get_study` with `include: ['screener_questions']` — the default summary truncates option lists, and `update_study.screener_questions` REPLACES the full list. Writing back a truncated array silently destroys screeners.
2. **Prefer PANEL questions for standard attributes.** Call `list_available_panel_questions` (a catalog of 180+ standard demographic/behavioral questions), then `get_panel_question` on candidates to see their answer options. Panel questions carry `is_panel_question: true` and a `qualification_id` — never invent a `qualification_id`.
3. **Write CUSTOM questions only for study-specific criteria.** Close-ended, 3–5 options, and always at least one disqualifying option so the screener doesn't lead the witness.
4. **Never add consent questions.** "Do you consent to being recorded?" and similar are handled outside screeners — adding one is a UX bug.
5. **Show the full proposed screener list to the user before saving.** Over-tight screeners slow recruitment; each disqualification costs fielding time.
6. **Call `update_study`** with the COMPLETE list — existing questions (both kinds) plus the new ones, ordered via the `order` field.
7. **If the study will field a panel,** remind the user that the panel recruits against these screeners — geo targeting is set by `country_code` at panel launch, not by a screener question, so never add a country screener.
