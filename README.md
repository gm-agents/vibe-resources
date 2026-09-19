# AI resources

![Repo Status](https://img.shields.io/badge/status-active-success)
![Prompt Types](https://img.shields.io/badge/prompts-multi--tool-blue)
![Built For](https://img.shields.io/badge/built%20for-ChatGPT%20%7C%20Claude%20%7C%20Cursor-purple)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

A curated library of reusable prompts for building apps, generating content, structuring projects, and guiding AI tools through complex tasks.

This repository is built to make prompts easy to **reuse, adapt, version, and share** across tools like **ChatGPT, Claude, and Cursor**.

## Content Rules (Generic)

[`content-rules-generic.md`](./content-rules-generic.md) is a portable set of writing and voice rules for any content you generate with an AI tool. Most AI writing carries the same giveaways: em-dashes everywhere, runs of short choppy sentences, filler like "unlock" and "surface," and openers like "what nobody tells you is..." This file bans those tells and pushes every draft toward plain, clear writing that reads the way a person actually talks. Drop it into any tool and the output stops sounding generated.

**What's inside**

- Voice fundamentals: one consistent voice, no em-dashes, no anthropomorphizing the model.
- A banned-words list (substrate, unlock, "surface" as a verb, "on purpose," and more), with carve-outs for when a word is genuinely correct.
- Banned sentence patterns: fragment runs, colon-aphorisms, rhetorical inversions, "what nobody tells you" reveals, weekday scene-setting, vanity number callouts.
- Clarity rules: say it the way you would say it out loud, never cryptic, name things directly.
- Evidence and structure rules: keep citations out of the prose, vary real examples, lead with what matters, format for scanning.

**How to use it**

Point any AI tool at the file, or paste it into that tool's instructions:

- **Claude Code:** add `@content-rules-generic.md` to your `CLAUDE.md` (global at `~/.claude/CLAUDE.md`, or per project).
- **Claude.ai:** paste it into a custom Style, your personal preferences, or a Project's instructions.
- **ChatGPT:** paste it into Custom Instructions, or a Project's instructions.
- **Cursor:** add it to your rules file (for example `.cursor/rules`).
- **Anything else:** paste it into the system prompt or instructions field.

Keep the file as your single source of truth. When you refine a rule, update it in one place and re-sync anywhere you pasted a copy.

## Budgeting the Bots: an estimation routine for multi-agent tasks

[`estimate-before-you-approve.md`](./estimate-before-you-approve.md) is a budget routine for tasks where an AI coding agent launches other agents, loops, or background work. One of those tasks, described as "a few dozen small calls," once used most of a week's plan allowance and did not finish. The routine is written as instructions the agent follows, so once it sits in your tool's instructions file, the agent estimates, sets a hard cap, pilots one slice, and reports cost after every stage without being asked.

The finding behind it: on one codebase the cost per agent barely moves, because every agent loads the same instructions before it starts. What the estimates get wrong is the number of agents. So the routine estimates in agents, not tokens, and uses a pilot to measure the count before the rest of the job runs.

**What's inside**

- Ten instructions for the agent: ask before acting, estimate in agents, cap at 125 percent as a hard stop, name any stage whose width depends on an earlier stage's output, pilot one slice, report cost after every stage, cut agents rather than quality when the estimate misses, offer priced options at the cap, resume rather than restart after a limit, and keep the per-agent unit current.
- Two fill-in templates: the plan the agent presents for approval, and the cost report it gives after each stage.
- A short checklist for the human side: set the cap in the same message as the approval, read the pilot report before anything else runs, and measure your own tokens per agent.

**How to use it**

Copy the block between the two horizontal rules into the file your tool reads at the start of every session:

- **Claude Code:** `CLAUDE.md` in the project root, or `~/.claude/CLAUDE.md` for every project.
- **OpenAI Codex:** `AGENTS.md`.
- **Cursor:** `.cursor/rules/budget.mdc`, or `.cursorrules`.
- **GitHub Copilot:** `.github/copilot-instructions.md`.
- **Gemini CLI, Windsurf, anything else:** `GEMINI.md`, `.windsurfrules`, or the system prompt.

The routine and the numbers behind it are written up in [Budgeting the Bots](https://girishpm.substack.com/p/my-estimation-process-for-multi-agent) and in the field note [How we budget a fan-out](https://ainativeproductmanager.com/field-notes/how-we-budget-a-fan-out).


## Honors Geometry Tutorial App Prompt Set - Make it your own, modify it for your kid and teach them any subject for any grade

A [structured prompt set](https://github.com/gm-agents/vibe-resources/blob/main/HonorsGeometry_Claude_Prompt.txt) for creating a scalable Honors Geometry tutorial app for 9th grade students. This prompt is designed to help an AI tool generate a brand new project that:
- builds a tutorial app or website for Honors Geometry
- uses teacher-provided PDFs and textbook materials as source inputs AND
- uses any and all internet resources and LLM model knowledge to generate content and problem sets
- organizes content by unit
- creates step-by-step lessons, worked examples, guided practice, challenge problems, and full unit tests
- generates an exam review summary for each unit
- maintains a living build document (`HG-Starter-Prompt.md`) so the project can be recreated or extended later


## Helpful Resources

A few useful public resources for prompt engineering, AI workflows, and learning:

- [Aishwarya Reganti’s awesome GitHub repository and trainings](https://github.com/aishwaryanr/awesome-generative-ai-guide/tree/main)
- [Free Lightning Lessons from Maven](https://maven.com/free-lessons)
- [Claude Code Tutorial by Carl Vellotti](https://ccforeveryone.com/)
- [Microsoft's Generative AI for Beginners](https://github.com/microsoft/generative-ai-for-beginners)
