# proposal-review

A Claude Code skill for thinking through ideas together — without Claude just telling you what you want to hear.

---

## The problem this solves

When you describe an idea to Claude, it usually tries to help you execute it. It'll refine your wording, fill in the details, and generally be enthusiastic about whatever direction you're heading.

That's fine for execution tasks. But when you're still figuring out *whether* the idea is good — that behavior is actively unhelpful.

This skill changes Claude's default mode in discussions. Instead of completing your thoughts, it asks what assumptions your thinking is based on. Instead of describing a visual direction in flowery prose, it goes and finds actual reference images. And when something is better done by you (in Figma, in a user interview, on your phone), it writes you a task list instead of pretending it can do it.

The guiding principle is **bidirectional fidelity** — you shouldn't have to wonder if Claude misunderstood you, and Claude shouldn't say things you can only trust, not verify.

---

## When to use it

Anytime you're in the "figuring it out" stage of something:

- You have a product idea and want to pressure-test it before building
- You're choosing between two design directions and can't quite articulate why one feels wrong
- You're about to make a technical decision and want a second opinion that might push back
- You need to align on a visual style but words keep failing you

**Trigger phrases:** `讨论一下` / `方案讨论` / `我有个想法` / `帮我想想` / `design review` / `let's discuss` / `help me think through`

---

## What it actually does

**At the start of every discussion**, Claude asks three things before jumping in: what's the context, what do you want to walk away with, and what constraints are already fixed. If Claude has project memory, it checks whether that's still accurate rather than silently assuming it is.

**During the discussion**, Claude shifts between modes depending on where things are:

- *Early / fuzzy* — it challenges assumptions and asks what's behind them, rather than helping you polish ideas that might be wrong
- *Options on the table* — it helps you compare systematically and pushes you toward an actual decision instead of leaving it open-ended
- *Direction decided* — it switches to collaborative mode, helps fill in details, and flags risks without second-guessing the direction anymore

It announces when it's switching modes, so you always know what role it's playing.

**When words aren't working** (usually for visual/aesthetic directions), Claude stops and says so — then searches for reference images instead of continuing to describe things. It comes back with specific callouts on what's worth looking at, counterexamples of what failure looks like, and a follow-up question.

**When you need to do something outside the conversation** — run a user test, open Figma, check something on your phone — Claude writes you a structured task with steps and a clear "done when" condition, rather than approximating the thing it can't actually do.

**At the end**, Claude summarizes what was decided, what was ruled out and why, what's still open, and what you need to do next.

---

## Installation

The simplest approach: copy `SKILL.md` into your project and reference it from `CLAUDE.md`.

```bash
mkdir -p .claude/skills/proposal-review
cp SKILL.md .claude/skills/proposal-review/SKILL.md
```

Then add this line to your project's `CLAUDE.md`:

```
@.claude/skills/proposal-review/SKILL.md
```

If you want it available across all your projects, put it in your global skills folder instead:

```bash
mkdir -p ~/.claude/skills/proposal-review
cp SKILL.md ~/.claude/skills/proposal-review/SKILL.md
```

---

## Compatibility

Works with Claude Code (CLI, desktop app, VS Code / JetBrains extension). The visual reference step requires web search access. Primarily written in Chinese but fully functional in English.
