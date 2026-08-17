---
name: field-a-panel
description: Use when the user wants to recruit respondents from the User Intuition panel for an existing Panel study. Triggers on "recruit from the panel", "field this study", "buy N responses", "launch the panel".
---

When the user wants to field a panel:

1. **Verify the study qualifies.** Call `get_study`: it must be a Panel study (`is_panel=true` — BYOP studies cannot field a panel and `create_panel` will refuse), with `screener_questions` configured and `voice_config.language` matching the intended `language_code`.
2. **Always dry-run first.** Call `create_panel` with `assistant_id`, `target`, `country_code`, `language_code`, and `dry_run: true`. This returns per-response cost, total credits, available balance, `sufficient_credits`, and the card reward-hold (`hold_amount_usd`) — without provisioning or charging.
3. **Show the full cost to the user and wait for an explicit yes.** Lead with the all-in total (credits + reward hold), not the per-unit price. Never launch a panel without confirmation.
4. **Launch** by repeating the call with `dry_run: false`. Confirm what was provisioned back to the user.
5. **To stop spending,** call `stop_panels` with the `assistant_id` — it cancels all active panel recruitment without deleting the study or its completed interviews. Confirm with the user before stopping.
