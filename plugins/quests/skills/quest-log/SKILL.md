---
name: quest-log
description: Record a multi-session idea as a quest: brief, decisions, ADRs, and missions, plus optional GitHub issues. Use when planning work that spans several sessions, or when writing or editing a QUEST.md or an ADR.
---

Keep a written log of a quest while it's being defined, so the goal, the expected result, and the work ahead survive the session. Write as decisions settle, not at the end.

## Where it lives

```
docs/
├── quests/
│   └── <slug>/
│       └── QUEST.md
└── adr/
    ├── 0001-<slug>.md
    └── 0002-<slug>.md
```

Relative to the current project directory. If the current directory isn't a project (no repo, no clear root), ask the user where the quest should live.

Create files lazily: only when there is something to write. If `QUEST.md` or `docs/adr/` already exist, read them first: the quest may continue an earlier one.

## QUEST.md

The quest brief: vision, expected result, non-goals, decisions, prerequisites, risks, missions. Update the matching section the moment something settles. Format in [QUEST-FORMAT.md](./QUEST-FORMAT.md).

## ADRs

Every decision gets one line under "Decisions" in `QUEST.md`. Offer a full ADR in `docs/adr/` only for decisions that are hard to reverse, surprising without context, and the result of a real trade-off. Criteria and format in [ADR-FORMAT.md](./ADR-FORMAT.md).

## Missions

Split the quest into missions and write them into `QUEST.md`:

- **Each mission fits in one session** and produces a tangible, checkable result (a running prototype, a published page, a draft, a validated assumption), not a loose layer of work.
- Each mission has a goal, an observable "done when", and dependencies (`depends on: M2`).
- Experiments that could change the plan go first.
- Order by dependencies, then by what proves the vision soonest.
- If a mission doesn't fit in one session, split it. If it's trivial, merge it.

Validate the list with the user, with a `preview` showing the mission map.

## Issues

If the project has a GitHub remote (`gh repo view`), offer to create one epic issue with the vision and expected result, and one issue per mission with its goal, "done when", and linked dependencies. Check existing labels first and don't invent labels without asking. Record the issue numbers in `QUEST.md`.

Don't commit the documents unless the user asks.
