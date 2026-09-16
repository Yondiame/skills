---
name: search-research
description: Use when the user wants to find existing User Intuition findings or participant responses across authorized studies before deciding whether more qualitative research is needed.
---

1. Turn the user's information need into a query. Use any supplied study, audience, date, or content-type constraints. Do not impose extra filters without a reason grounded in the request.
2. Discover the current research-search operation and input schema from the connected server or published API reference. Use only supported fields and enum values. If search is not exposed in the connected release, report that limitation; do not invent a tool name or silently substitute a different operation.
3. Search authorized findings and participant-response summaries. Use the service's supported keyword/semantic matching; do not promise a particular ranking algorithm or matching mode unless the released schema provides it. Search retrieves existing evidence and does not launch research.
4. Read coverage and result context: study identity, audience, research dates, content type, text kind, freshness, references, and report version when available. Search of report sections does not imply full-transcript search, and zero matches do not prove a topic was absent from every interview.
5. Follow pagination with the same query and filters when the task needs more coverage. State when results are partial or only the first page was inspected. Do not interpret relevance scores as statistical confidence or population prevalence.
6. Fetch the relevant report or source interview through the discovered read operations before citing a load-bearing claim or quoting a passage. Resolve references using the returned identifiers. A finding summary is not a verbatim quote; repeated matches from one interview are not independent supporting participants.
7. Return relevant evidence, source links/identifiers, coverage, contradictions, and remaining uncertainty. Distinguish empty results from failed requests. Keep recommended next steps labeled as proposals and include them only when relevant to the user's request.

Do not create studies, regenerate reports, invite people, or incur recruitment costs as a side effect of searching. The calling agent decides whether the evidence answers the question and whether a separate research task is needed.

The illustrative [search example](https://github.com/user-intuition/examples/tree/main/examples/search-research) requires reconciliation with the released C1 contract before live use. [API reference](https://docs.userintuition.ai/api-reference/introduction).
