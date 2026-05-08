# proposal-review — 方案讨论 Skill for Claude Code

> A Claude Code skill that turns Claude into an opinionated thinking partner — one that challenges assumptions, seeks visual references, and keeps both sides accurately understood.

---

## What it does

`proposal-review` changes how Claude participates in design and product discussions. Instead of enthusiastically completing whatever you describe, Claude acts as a **thinking partner with a stance**:

- Challenges assumptions before helping you refine them
- Searches for visual references when words can't align a direction
- Tracks decisions, rejections, and open questions across the conversation
- Issues structured task lists for things you need to do in external tools (Figma, user testing, etc.)

The core principle: **bidirectional fidelity** — what you say doesn't get misunderstood, and what Claude says can be verified, not just trusted.

---

## When to use it

| Situation | Example trigger |
|-----------|----------------|
| Discussing a product idea | "我有个想法" / "let's discuss this"  |
| Reviewing a design direction | "帮我想想这个方案" / "design review" |
| Choosing between approaches | "我在考虑两种方案" / "help me think through" |
| Aligning on a visual style | "怎么看这个设计方向" / "proposal review" |

---

## Installation

### Option A: Copy skill file into your project

```bash
mkdir -p .claude/skills/proposal-review
cp SKILL.md .claude/skills/proposal-review/SKILL.md
```

Then reference it in your project's `CLAUDE.md`:

```
@.claude/skills/proposal-review/SKILL.md
```

### Option B: Reference directly (if you cloned this repo)

Add to your project's `CLAUDE.md`:

```
@/path/to/proposal-review/SKILL.md
```

### Option C: Sync to global skills (all projects)

```bash
mkdir -p ~/.claude/skills/proposal-review
cp SKILL.md ~/.claude/skills/proposal-review/SKILL.md
```

---

## How it works

### Step 1 — Entry ritual (every session)

Before any discussion, Claude asks 3 questions:

- **Background**: What's the project/context?
- **Goal**: What specific outcome do you want from this discussion?
- **Constraints**: What's already decided and can't change?

If Claude has project memory, it reads it first and explicitly asks: *"I see X from before — is that still accurate?"*

### Step 2 — Dynamic mode switching

Claude switches between three modes based on conversation state, and **announces the switch**:

| Mode | Trigger | What Claude does |
|------|---------|-----------------|
| **Explore / Challenge** | Direction is vague, assumptions untested | Questions the premise before helping refine |
| **Focus / Evaluate** | Options have surfaced, user is comparing | Structured comparison, pushes toward a decision |
| **Refine / Execute** | Direction is decided | Fills in details, flags execution risks |

### Step 3 — Visual reference workflow

When words can't align a visual direction, Claude pauses and says so explicitly:

> "I think we've hit the limit of what text can align here. I want to find some reference images. Here's the direction I'm looking for: [X]. Does that sound right?"

Claude then runs a web search and returns:
- Positive references with specific callouts ("the part worth looking at here is X")
- Counterexamples ("this is what failure looks like in this direction")
- A follow-up question to keep the discussion grounded

### Step 4 — Task delegation

When something is faster for you to do in an external tool, Claude issues a structured task:

```
[Task for you]

Task: [one-sentence description]

Steps:
1. [specific action]
2. [specific action]

Done when: Send me [screenshot / file / specific output] and I'll [verify X / continue to Y]

Estimated time: ~X min
```

### Step 5 — Summary

At the end of any converged discussion, Claude produces a structured summary:

- Decisions made (with reasoning)
- Options rejected (with reasons)
- Open questions (with what's needed to resolve them)
- Visual anchors (reference URLs, if any)
- Your action items

---

## Anti-patterns this skill prevents

| What Claude normally does | What it does with this skill |
|---------------------------|------------------------------|
| "Great idea! Let me help you refine it…" | Asks what assumption this is based on first |
| Gives three parallel options and asks you to pick | States Claude's recommendation with reasoning |
| Stops pushing back when you insist | Records the disagreement explicitly and explains why |
| Uses vivid language to describe a visual direction | Searches for actual reference images |
| Ends the conversation without summarizing | Proactively offers to document what was decided |

---

## Skill file

| File | Description |
|------|-------------|
| [`SKILL.md`](SKILL.md) | Full skill instructions (load this into Claude) |

---

## Compatibility

- **Claude Code** (CLI, desktop app, VS Code / JetBrains extension)
- Works best with models that have web search access (for visual reference workflow)
- Language: primarily Chinese with full English support

---

## Related skills

- [market-research](../market-research/) — research the competitive landscape before a proposal discussion
- [frontend-design](../frontend-design/) — execute UI decisions made during the discussion
