# ADR

ADRs (decision records) live in `docs/adr/` with sequential numbering: `0001-slug.md`, `0002-slug.md`. Find the highest existing number and add one. Create the folder only when the first ADR is needed.

## When to offer one

Only when all three are true:

1. **Hard to reverse**: changing your mind later has a real cost.
2. **Surprising without context**: someone looking at the result months later will wonder "why this way?".
3. **The result of a real trade-off**: there were genuine alternatives and one was picked for specific reasons.

If any is missing, no ADR: the line under "Decisions" in `QUEST.md` is enough.

What usually qualifies:

- **Foundational choices with lock-in**: platform, engine, stack, vendor, pricing model, legal structure.
- **Scope and boundary calls**: "v1 only targets Mexico", "no mobile app", "no user accounts". The explicit no's are as valuable as the yes's.
- **Deliberate deviations from the obvious path**: anything a reasonable person would assume the opposite of. These stop someone from "fixing" what was intentional.
- **Constraints not visible in the result**: "must run offline at the venue", "budget capped at X", "the partner requires Y".
- **Rejected alternatives when the rejection isn't obvious**: so nobody proposes them again in six months.

## Template

```md
# <Short title of the decision>

<1-3 sentences: context, what was decided, and why.>
```

An ADR can be a single paragraph. Add sections only when they add value:

- **Status** (`proposed | accepted | deprecated | superseded by ADR-NNNN`), when the decision gets revisited.
- **Considered options**, when the rejected alternatives are worth remembering.
- **Consequences**, when there are non-obvious effects.
