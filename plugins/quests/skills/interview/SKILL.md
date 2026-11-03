---
name: interview
description: Interview the user relentlessly about an idea, plan, or decision, one round of questions at a time, until it is concrete and actionable. Use when the user wants to sharpen, refine, or stress-test an idea of any kind.
---

Interview the user until you reach a shared understanding of the idea: what it is, why it matters, what the expected result looks like, what it takes to get there, and how you'll both know it's done. The idea can be anything: code, a product, a business, a campaign, a piece of art.

Act as a sharp collaborator, not a form: propose, give opinions, recommend. The decisions belong to the user.

## How to ask

Always use the agent's native question tool: `AskUserQuestion` in Claude Code, `request_user_input` in Codex. Only if neither exists, ask in plain text with numbered questions and your recommendation under each.

- **Up to 4 questions per call**, each with 2-4 concrete options. The user can always type their own answer.
- **Your recommended option goes first** and its label ends with `(Recommended)`. Actually recommend, with judgment, instead of listing neutral options.
- **Use `preview`** whenever options are easier to compare by seeing them: mockups, snippets, copy variants, diagrams, tables, structures.
- Each question must stand on its own: the user may only see the dialog. If it depends on something you found, say so in the question.

## Facts are yours, decisions are theirs

Never ask the user for a fact you can find yourself: in the files, the code, the docs, the web. Before the first question, look around for context (project files, `AGENTS.md`/`CLAUDE.md`, existing notes). When finding a fact is expensive, dispatch a sub-agent and keep asking whatever doesn't depend on its answer.

When the user states how something is or works, check it against the sources when you can, and surface contradictions.

## Rounds over a decision tree

Model the idea as a **decision tree**: every decision opens the decisions that hang off it. The **frontier** is every decision whose prerequisites are already settled. Each round, ask only the frontier (max 4 per call; if there are more, start with the ones that unblock the most branches). A question whose answer depends on another still-open question belongs to a later round. Every answer moves the frontier: recompute it before the next round.

Branches most ideas have (a checklist, not a script; skip what doesn't apply, add what the idea needs):

- **Goal and why**: what this is in one sentence, and what changes if it exists.
- **Audience**: who it is for, who sees or uses it, in what context.
- **Expected result**: what exists when it's done. Ask for concrete scenes: "someone opens it and…".
- **Non-goals**: what it deliberately isn't. Ask explicitly; it keeps scope from growing on its own.
- **Shape**: the main choices of how (medium, channel, stack, format, structure, tone).
- **Constraints**: time, budget, tools, skills, rules it must respect.
- **Done when**: observable criteria to know it worked.

Sharpen language as you go: when the user uses a vague or overloaded word ("engaging", "fast", "simple", "users"), propose a precise meaning. Stress-test boundaries with invented concrete scenarios.

When a decision can't be settled with words (it depends on seeing, feeling, or testing it), propose a **cheap experiment**: a throwaway sketch, prototype, mock, or draft that answers the question, and leave the decision pending on it.

## Prerequisites

Before closing, list everything the idea needs to happen, verify what you can yourself, and present it as a checklist (✅ ready / ⚠️ missing / ❌ blocking): tools, dependencies, accounts, assets, access, data, knowledge, people, money. Each ⚠️ and ❌ becomes a question (get it, cut scope, or plan for it).

## Done

The interview is done when the frontier is empty: every branch visited, nothing silently assumed, prerequisites resolved or planned for. Don't act on the idea until the user confirms you've reached a shared understanding.
