---
name: invite-your-own-participants
description: Use when the user wants to interview their own customers, users, or contacts in a BYOP study. Triggers on "invite my customers", "send interview invites", "add these people to the study", "reward that participant".
---

When the user wants to invite their own participants:

1. **Confirm the study is BYOP** (`is_panel=false`) via `get_study`. Panel studies recruit from the panel instead.
2. **For each participant, call `create_invite`** with `assistant_id`, `email`, and `name`. By default this SENDS the invitation email immediately — if the user wants to send invites themselves (from their own address), pass `issilent: true` and give them the interview links.
3. **For a shareable link with no email list,** create one invite with `isuniversal: true` — no email required; anyone with the link can participate.
4. **For internal testing,** pass `istest: true` so the dry-run interview is excluded from billing and analysis.
5. **Rewards (BYOP only):** the study needs `is_offering_enabled: true` and an `incentive_amount` ($5–$400), set via `update_study`. After a completed interview, `send_reward` with the `invite_id` pays that participant — it is idempotent, so re-sending cannot double-pay. If `auto_send_reward` is on, completed interviews are rewarded automatically. Only send rewards when the user explicitly asks.
