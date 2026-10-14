# Results

Include this template in each handoff, in the requesting user's language. Specify the report path, limit report-area edits to the assigned file, prohibit completion notices, and explain save-failure handling.

```markdown
# <Task title>
Status: <In progress / Completed / Partially completed / Needs attention / Stopped>
Updated: <date, time, and time zone>

- Result and deliverables: <what changed, work performed, and deliverable links>
- Checks: <passed, unperformed, failed; reasons and uncertainties>
- Remaining: <unresolved work or decisions; omit if none>
```

- Keep this order when saving and presenting results; one line per item is enough. Mark completed only when scope and required checks are satisfied. Read back status, uncertainties, and links. Use relative links for deliverables that move together; resolve others for the display surface.
- Prefer the user's path; otherwise choose a unique `local/reports/<date>-<task>.md` under the originating project. Pass its base/actual path or a verified shared location and confirm write access.
- The origin creates an in-progress placeholder where possible and links it from `local/reports/README.md`. Uncreated reports are planned, without clickable report links. Shared index/ledger updates belong to the origin.
- If saving fails, leave the reason, actual location, and result in an authorized alternative or the destination's final answer. When requested, the origin checks the destination for missing/stale/unknown reports and repairs references. Follow-ups update the same report's scope, status, and time.
- After confirmed delivery, show title → short description → report link → separate destination-chat link; use the same layout in the index and result view. Reflect confirmed outcomes and state failed/uncertain delivery explicitly.
- Use `codex://threads/<thread-id>` only with a verified ID and confirmed chat title ([specification](https://learn.chatgpt.com/docs/app/commands#deep-links)). Elsewhere use a confirmed supported link, or show the title and mark the link unverified. No callback or public share is needed.
