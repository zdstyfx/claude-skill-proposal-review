# proposal-review

[English](#english) | [中文](#中文)

---

## 中文

一个 Claude Code skill，用来和 Claude 一起想清楚问题——而不是让它顺着你说。

### 这个 skill 解决什么问题

你跟 Claude 描述一个想法，它通常会帮你执行：帮你完善表述、填充细节、对你的方向充满热情。

执行任务时这没问题。但当你还在判断「这个想法到底对不对」的时候，这种默认行为反而是有害的。

这个 skill 改变了 Claude 在讨论中的默认角色。它不再帮你补全想法，而是先问你的判断基于什么假设；不再用华丽的文字描述视觉方向，而是去找真实的参考图；当某件事在对话里做不到（比如 Figma 操作、用户访谈），它会给你一份任务清单，而不是用文字描述来凑合。

核心原则是**双向信息保真**——你不用担心 Claude 误解了你，Claude 说的东西也应该是可以被验证的，而不只是被信任的。

### 什么时候用

适合「还在想清楚」阶段：

- 你有一个产品想法，想在动手之前先压力测试一下
- 你在两个设计方向之间纠结，说不清楚哪里感觉不对
- 你要做一个技术决策，想要一个可能会反对你的第二意见
- 你需要对齐视觉风格，但文字一直描述不准

**触发词：** `讨论一下` / `方案讨论` / `我有个想法` / `帮我想想` / `怎么看这个方案` / `我在考虑`

### 它具体做什么

**每次讨论开始时**，Claude 先问三件事再进入讨论：背景是什么、你希望讨论结束时得到什么、有哪些前提是不能动的。如果 Claude 有项目记忆，它会先确认那些信息是否还准确，而不是默默当作既成事实。

**讨论过程中**，Claude 根据对话状态切换模式：

- *方向模糊时* — 质疑假设，问清楚判断背后的逻辑，而不是帮你把模糊的想法写得更好听
- *选项浮现时* — 系统性对比各个方向，推动你做出实际决策，不让讨论无限延伸
- *方向确定后* — 切换成协作模式，补充细节、指出执行风险，不再质疑已经确定的方向

模式切换时 Claude 会明确说出来，你随时知道它在扮演什么角色。

**当文字对齐不了**（通常是视觉/审美方向），Claude 会暂停并说清楚，然后去搜参考图——附上具体的「值得看哪里」说明、失败案例的反例，以及一个有针对性的追问。

**当你需要在对话外完成某件事**（在 Figma 里操作、做用户测试、在手机上截图），Claude 会发一份结构化任务，包含步骤和明确的验收条件，而不是用它做不到的方式凑合。

**讨论收敛时**，Claude 整理总结：决定了什么、否决了什么及原因、还有什么待定、你接下来要做什么。

### 安装

把 `SKILL.md` 复制到项目里，然后在 `CLAUDE.md` 里引用它：

```bash
mkdir -p .claude/skills/proposal-review
cp SKILL.md .claude/skills/proposal-review/SKILL.md
```

在项目的 `CLAUDE.md` 里加一行：

```
@.claude/skills/proposal-review/SKILL.md
```

想在所有项目里都能用，放到全局 skills 目录：

```bash
mkdir -p ~/.claude/skills/proposal-review
cp SKILL.md ~/.claude/skills/proposal-review/SKILL.md
```

### 兼容性

适用于 Claude Code（CLI、桌面端、VS Code / JetBrains 插件）。视觉参考步骤需要联网搜索。主要用中文写成，完整支持英文。

---

## English

A Claude Code skill for thinking through ideas together — without Claude just telling you what you want to hear.

### The problem this solves

When you describe an idea to Claude, it usually tries to help you execute it. It'll refine your wording, fill in the details, and generally be enthusiastic about whatever direction you're heading.

That's fine for execution tasks. But when you're still figuring out *whether* the idea is good — that behavior is actively unhelpful.

This skill changes Claude's default mode in discussions. Instead of completing your thoughts, it asks what assumptions your thinking is based on. Instead of describing a visual direction in flowery prose, it goes and finds actual reference images. And when something is better done by you (in Figma, in a user interview, on your phone), it writes you a task list instead of pretending it can do it.

The guiding principle is **bidirectional fidelity** — you shouldn't have to wonder if Claude misunderstood you, and Claude shouldn't say things you can only trust, not verify.

### When to use it

Anytime you're in the "figuring it out" stage of something:

- You have a product idea and want to pressure-test it before building
- You're choosing between two design directions and can't quite articulate why one feels wrong
- You're about to make a technical decision and want a second opinion that might push back
- You need to align on a visual style but words keep failing you

**Trigger phrases:** `design review` / `proposal review` / `let's discuss` / `help me think through` / `what do you think about this`

### What it actually does

**At the start of every discussion**, Claude asks three things before jumping in: what's the context, what do you want to walk away with, and what constraints are already fixed. If Claude has project memory, it checks whether that's still accurate rather than silently assuming it is.

**During the discussion**, Claude shifts between modes depending on where things are:

- *Early / fuzzy* — it challenges assumptions and asks what's behind them, rather than helping you polish ideas that might be wrong
- *Options on the table* — it helps you compare systematically and pushes you toward an actual decision instead of leaving it open-ended
- *Direction decided* — it switches to collaborative mode, helps fill in details, and flags risks without second-guessing the direction anymore

It announces when it's switching modes, so you always know what role it's playing.

**When words aren't working** (usually for visual/aesthetic directions), Claude stops and says so — then searches for reference images instead. It comes back with specific callouts on what's worth looking at, counterexamples of what failure looks like, and a follow-up question.

**When you need to do something outside the conversation** — run a user test, open Figma, check something on your phone — Claude writes you a structured task with steps and a clear "done when" condition, rather than approximating the thing it can't actually do.

**At the end**, Claude summarizes what was decided, what was ruled out and why, what's still open, and what you need to do next.

### Installation

Copy `SKILL.md` into your project and reference it from `CLAUDE.md`:

```bash
mkdir -p .claude/skills/proposal-review
cp SKILL.md .claude/skills/proposal-review/SKILL.md
```

Add this line to your project's `CLAUDE.md`:

```
@.claude/skills/proposal-review/SKILL.md
```

To make it available across all your projects, put it in your global skills folder:

```bash
mkdir -p ~/.claude/skills/proposal-review
cp SKILL.md ~/.claude/skills/proposal-review/SKILL.md
```

### Compatibility

Works with Claude Code (CLI, desktop app, VS Code / JetBrains extension). The visual reference step requires web search access. Primarily written in Chinese but fully functional in English.
