---
name: invite-your-own-participants
description: Use when the user wants to add, invite, update, or reward their own participants in a BYOP study.
---

When the user supplies participants:

1. Call `get_study` and verify `recruiting_method` is `byop` and `provisioning_status` is `provisioned`.
2. Return the complete current persisted study plan in a readable form with its audience, screeners, concepts, and interview settings. Obtain explicit approval of that exact version before creating participants; approval to create or customize the study does not count.
3. Normalize and deduplicate email addresses case-insensitively. `create_participants` accepts 1–100 participants per request.
4. Explain that invitations send by default. Use `silent: true` for each participant when the user wants records created without sending email.
5. Call `create_participants` with `study_id` and the batch only after provisioning and exact-version plan approval are confirmed.
6. Use `list_participants` to verify the batch. Call `get_participant` before `update_participant`.
7. `send_participant_reward` has a financial side effect and is BYOP-only. Confirm the exact participant and require an explicit request before sending. The backend prevents a duplicate reward for an already-paid participant.
8. Participant deletion is not available through the public MCP surface. Do not promise to delete a participant.
