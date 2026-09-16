---
name: retrieve-study-results
description: Use when the user wants to fetch an existing User Intuition study report, inspect its four sections, or follow a finding or participant response to supporting interview evidence without regenerating analysis.
---

1. Use the supplied study ID. If only a name is supplied, resolve it with `list_studies` and disambiguate matches. Fetch `get_study` for audience and study context when needed.
2. Discover the current schema for `get_study_report` and retrieve the existing report. This is a read workflow: do not call `generate_report`, create a study, invite participants, or launch recruitment merely to fulfill retrieval.
3. Inspect the returned sections: Study Findings, Participant Responses, Participant Profiles, and Recommended Next Steps. Preserve missing, partial, or unavailable sections as such. Findings and response summaries are generated research outputs; profiles describe the sample; next steps are proposals rather than observed outcomes.
4. Preserve study ID, report version or generation time, coverage, freshness, and source references when provided. Missing freshness is unknown, not fresh. Report-eligible interviews, completed interviews, and the target sample are different counts.
5. Resolve each reference using the returned reference map and identifiers. Keep respondent labels scoped to the study/report. Do not assume a response label is a participant ID or a reference ID is an interview ID. Follow interview references with `get_interview`; retain message or passage identifiers if present.
6. Before presenting an exact quotation or treating a finding as verified, inspect the original supporting passage. Do not invent finer citation precision than the response provides. Distinguish multiple quotes from one interview from independent participants.
7. Return the requested evidence and limitations. Distinguish a missing report, stale report, empty section, access failure, and transport error. If new analysis is needed, explain that it is a separate operation and follow the user's scope.

The calling agent interprets the evidence in its wider context. The illustrative [results example](https://github.com/user-intuition/examples/tree/main/examples/retrieve-study-results) shows the intended B2 shape; verify it against the released schema before live use. [API reference](https://docs.userintuition.ai/api-reference/introduction).
