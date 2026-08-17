---
name: run-a-concept-test
description: Use when the user wants reactions to a concept, prototype, design, or landing page — anything participants should look at during the interview. Triggers on "concept test", "test this prototype", "get reactions to this page", "show participants this design".
---

When the user wants a concept test:

1. **Create the study with `is_concept_test: true`** — follow the create-study-from-brief flow, but draft the moderator guide from the concept-test template (the study-type row loaded via `get_study_type`, or the `get_concept_test_planning_prompt` / `get_concept_test_chat_planning_prompt` tool as fallback).
2. **Attach the stimulus with `upload_concept_link`** (`assistant_id`, `url`, `label`). Prefer this over writing `concept_link` via `update_study` — it dedups by label and preserves IDs, so re-uploading a corrected URL replaces the old link in place without breaking live interviews.
3. **The URL must be publicly reachable** — participants open it in a new tab mid-interview. Prototype links (e.g. a shared prototype or staging page) must not require login. Verify the link loads in an incognito context before fielding.
4. **Structure the guide around the reveal:** context questions BEFORE showing the concept (unprimed expectations), then reaction, comprehension, and value questions after. Ladder from what they noticed → what it means to them → whether they'd use it.
5. **Field as usual** — panel via field-a-panel, or your own participants via invite-your-own-participants.
