# QUEST.md

Lives at `docs/quests/<slug>/QUEST.md`. The slug is short and kebab-case (`goal-tunnel`, `newsletter-launch`). It's written section by section as each part is decided; sections still open read `_Pending_`.

## Template

```md
# <Quest name>

> <The vision in one sentence.>

## Expected result

<What exists when the quest is complete. Concrete scenes from the point of view of whoever uses, sees, or buys it.>

**Audience and context**: <who it's for and where they meet it>
**References**: <works, products, campaigns, styles that act as a compass>

## Non-goals

- <What this deliberately is not or does not do.>

## Decisions

- **<Topic>**: <decision> — <why, in one line>. <Link to ADR if one exists.>

## Prerequisites

- ✅ <ready>
- ⚠️ <missing> → <how it gets resolved / mission that covers it>
- ❌ <blocking> → <what's needed to unblock it>

## Risks

- <Risk> → <mitigation or experiment that answers it>

## Missions

### M1 — <name>
**Goal**: <one sentence>
**Done when**: <observable criterion>
**Depends on**: —
**Issue**: <#123, if created>

### M2 — <name>
...

## Open questions

- <Whatever is pending on an experiment or on external information.>
```

## Rules

- The brief says **what** and **why**; the fine-grained **how** is decided in each mission.
- One line per decision. Decisions that meet the ADR criteria link to their ADR.
- "Done when" is always observable: something you can see, measure, or test.
- "Open questions" should be empty when the quest closes, except for what depends on an experiment.
