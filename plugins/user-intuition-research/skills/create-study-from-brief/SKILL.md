---
name: create-study-from-brief
description: Use when the user wants to create a new User Intuition interview study from a research brief, goal, or idea. Triggers on "create a study", "set up interviews about X", "I want to interview people about Y", "turn this brief into a study".
---

When the user asks to create a study:

1. **Call `list_study_types` FIRST** — always, before anything else. Pick the row matching the user's goal (Win/Loss, Churn, NPS+CSAT, Onboarding, Brand Health, etc.). If the user's goal is ambiguous between two types, ask. The catalog is lightweight — prompt fields are stripped — so after picking a row, **call `get_study_type` with the row's slug** to load its full `chat_prompt`.
2. **Ask Panel vs BYOP.** `is_panel` is required and must come from the user: Panel (`is_panel=true`) recruits respondents from the User Intuition panel; BYOP (`is_panel=false`) means the user invites their own participants. Never guess.
3. **Ask the mode** if unstated: voice (default — both flags false), chat (`enable_chat=true`), or video (`enable_video_recording=true`). Chat and video are mutually exclusive.
4. **Draft the moderator guide** using the `chat_prompt` from the `get_study_type` response as your template — each study type's prompt structure is materially different. Show the draft to the user before creating.
5. **Call `create_study`** with `name`, `is_panel`, `system_prompt`, `study_type: "standard"` (the literal string — never the row's slug), the catalog row's `id` as `study_id`, and the mode flags. For non-English studies build the **complete** `voice_config`: call `list_voices` and set `name` and `voiceId` BOTH to the chosen voice id plus `provider` from the same row, and `language` to an ISO code from `list_available_languages` — a bare `{language}` object sends an empty voice configuration into provisioning.
6. **Do NOT add `screener_questions` at creation** — only add them later (via the design-screeners flow) if the user explicitly asks. Never add consent or "willing to participate" questions.
7. **Share the returned `dashboard_url`** — always. It takes the user straight to the study in the dashboard to review and launch.
