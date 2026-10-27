---
name: room-results
description: Report how a WZRD room is doing — visits, visitor questions, outcomes and recent activity — and suggest improvements. Use when the user asks about a room's traffic, engagement, who visited, what visitors asked, or how to improve a room. Requires a connected WZRD account.
---

# Room results

These tools need a **connected WZRD account**. If they return `auth_required`, ask the user to Connect WZRD, then retry.

1. **Find the room** with `rooms_search` or `rooms_list`.
2. **Get the numbers.**
   - Visitor counts and outcomes: `analytics_get` and `outcomes_get`.
   - Recent visits and actions: `rooms_activity_get`.
   - Themes in what visitors asked: `insights_get`.
3. **Summarize.** Lead with the figures the user asked about and the time period they cover. Keep it short, and don't paste raw event lists. Do not invent metrics.
4. **Suggest next steps.** If the user wants improvements, call `suggestions_generate` and present the suggestions. Apply one with `suggestions_decide` only when the user picks it.

To answer a question from the room's own content, use `knowledge_search`.
