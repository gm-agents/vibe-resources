# Ask for the estimate before you approve the plan

A budget routine for tasks where an AI coding agent launches other agents, loops, or background work. It is written as instructions the agent follows, so once it sits in the file your tool reads at the start of every session, the agent estimates, caps, pilots, and reports cost on every large task without being asked.

The finding behind it: on one codebase the cost per agent barely moves, because every agent loads the same instructions before it starts. What the estimates get wrong is the number of agents. So the routine estimates in agents, not tokens, and uses a pilot to measure the count before the rest of the job runs.

## Where to put it

| Tool | File |
| --- | --- |
| Claude Code | `CLAUDE.md` in the project root, or `~/.claude/CLAUDE.md` for every project |
| OpenAI Codex | `AGENTS.md` |
| Cursor | `.cursor/rules/budget.mdc`, or `.cursorrules` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| Gemini CLI | `GEMINI.md` |
| Windsurf | `.windsurfrules` |
| Anything else | The system prompt, or the first message of the session |

Copy everything between the two rules below.

---

## Budget routine for any task that launches agents, loops, or background work

An **agent** is one model run with its own context (a subagent, a worker in a fleet, one iteration of a loop). A **cap** is a spending level at which you stop.

1. **Ask before you act.** Before any task that will run more than a handful of agent calls, present the plan below and stop for approval. Mark the per-agent figure as measured on this codebase or as unmeasured; never present a guess as a measurement.
2. **Estimate in agents, not tokens.** Total = agents × tokens per agent, summed across stages. The agent count is the number most likely to be wrong, so show how you arrived at it.
3. **Propose a hard cap in the same message,** at 125 percent of the estimate. When spending reaches it, stop and report. Do not finish the stage first.
4. **Name any stage whose width you cannot know yet.** If a stage's agent count depends on what an earlier stage produces (one verifier per finding, before the findings exist), give the cost as a range and cap the count. Never launch an unbounded stage on a fixed estimate.
5. **Pilot one slice first.** Run one subtask through the full pipeline and report its agent count and tokens per agent against the estimate. Nothing else runs until that report has been approved.
6. **Report cost after every stage,** in the format below, whether or not anyone asked.
7. **When the estimate misses, cut agents, not quality.** Fewer agents in parallel, one verifier per batch instead of one per item, no duplicate passes. Refresh the estimate and pilot again before running the rest.
8. **When the projection crosses the cap, stop and offer priced options:** raise the cap from a fresh estimate, hold it by cutting scope you name and price, or pause. Never raise the cap on your own or continue quietly.
9. **When a limit interrupts a run, resume rather than restart.** Replay what the tool cached, run only what did not finish, and read the resumed output before trusting it. If the allowance ends with work left, finish it sequentially, without a fleet.
10. **Keep the unit current.** After every run, record tokens per agent by kind of work so the next estimate starts from a measurement.

### The plan to present

```text
Budget for:        <task>
Stages:            <stage 1> → <stage 2> → <stage 3>
Agents per stage:  <n1> / <n2> / <"depends on stage 2 output; capped at N">
Tokens per agent:  ~<x>k (measured on this repo, <date>)  or  unmeasured
Estimate:          ~<total> tokens
Hard cap:          <1.25 × total> tokens, a stop, not a target
Pilot:             <one slice> runs first; the rest waits for its cost report
Lean option:       <what it drops> at ~<total>, cap <1.25 × total>
Reply with: approve, change the cap, or take the lean option.
```

### The cost report after each stage

```text
Cost report:       <stage>
Actual / estimate: <tokens> / <tokens>
Agents:            <n> run, <m> planned, ~<x>k tokens each
Running total:     <spent> of <cap> (<percent> used)
Why the gap:       <one sentence naming the cause>
Next:              <what runs next, or "stopping: cap reached", with options>
```

---

## What you do

- Say yes and set the cap in the same message, so the two cannot drift apart.
- Read the pilot report before anything else runs, and every cost report after that. The reason for the gap is the part that teaches you something.
- When the projection crosses the cap, decide from the options. Raising it is a fine decision when the extra work is worth more than the margin; the point is that you make it with a price in front of you.
- Measure your own tokens per agent: one run's total divided by its agent count. Ours sat between about 70,000 and 90,000 for text-audit agents in September 2026; yours will differ, which is why you measure rather than borrow it.

## Sources

- [Budgeting the Bots: An Estimation Process for Multi-Agent Orchestration in AI tools](https://girishpm.substack.com/p/my-estimation-process-for-multi-agent), the post that walks through the routine.
- [How we budget a fan-out](https://ainativeproductmanager.com/field-notes/how-we-budget-a-fan-out), the field note with the cost ledger of one run, closed at 18.3 million tokens against a 19 million cap.
- [How we spent a week's tokens on a great idea](https://ainativeproductmanager.com/field-notes/fable-5-lessons), the incident the routine came out of.

## License

MIT, the same as the repository this file lives in. See [LICENSE](./LICENSE).
