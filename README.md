# Less Is More

An architecture-first, reduction-first skill for coding agents — Claude Code, Codex, Cursor, and anything that reads `AGENTS.md` or the [Agent Skills](https://agentskills.io) format.

Less accidental complexity. More evidence. More ownership clarity.

The skill makes an agent earn its diff:

- start from the real repo state, not memory
- verify drift-prone facts against current primary sources, as of the actual date
- trace the owning code path before editing — never patch the diff window
- reuse what the codebase already provides before writing anything new
- choose the clearest justified outcome: deletion, consolidation, a narrow addition, or no edit
- sweep the finished diff until every hunk earns its place

## The problem

Coding agents fail in predictable ways:

- they patch the nearest symptom instead of the owning code path
- they re-implement helpers the codebase already has
- they trust stale framework knowledge and old examples
- they add speculative abstraction before it is earned — or repeat themselves instead of naming the repetition
- they stop at "tests pass," leaving scaffolding in the diff: narrating comments, unused parameters, debug output, drive-by churn

## The idea

*Less* means less accidental complexity, duplication, and confused ownership — never less rigor, less verification, or fewer lines for their own sake. The aim is the best professional solution the problem justifies, leaving a codebase that stays fast to understand as it compounds.

One bar governs every change:

> The gate is proof, not permission.

Evidence of a clearly better outcome licenses a complete fix — including improvements discovered beyond the ask — and forbids expanding scope on a hunch. The bar cuts both ways: it blocks timid half-measures as firmly as reckless sprawl.

The workflow in one breath: trace the owning path → audit the shape → reuse before writing → weigh the strongest options → verify → then a final pass over the diff, because a diff that works is not yet a diff that is finished.

## Layout

- [`skills/less-is-more/SKILL.md`](./skills/less-is-more/SKILL.md) — canonical text, the single source of truth
- [`AGENTS.md`](./AGENTS.md) — the same text as a cross-agent root instruction file
- [`.cursor/rules/less-is-more.mdc`](./.cursor/rules/less-is-more.mdc) — the same text as a Cursor project rule
- [`skills/less-is-more/agents/openai.yaml`](./skills/less-is-more/agents/openai.yaml) — Codex skill interface metadata
- [`EXAMPLES.md`](./EXAMPLES.md) — the workflow in practice

If you change the skill, edit `SKILL.md` first, then mirror the body into `AGENTS.md` and the Cursor rule.

## Install

### Claude Code

Copy the skill folder into your user skills directory:

```bash
cp -r skills/less-is-more ~/.claude/skills/
```

Claude Code triggers it automatically from the description, or invoke it explicitly with `/less-is-more`.

### Codex

```bash
cp -r skills/less-is-more ~/.codex/skills/
```

### Skills CLI

```bash
npx skills add oddyblue/less-is-more-skill --skill less-is-more
```

### Cursor

Copy [`.cursor/rules/less-is-more.mdc`](./.cursor/rules/less-is-more.mdc) into your project's `.cursor/rules/` directory.

### Any other agent

Copy [`AGENTS.md`](./AGENTS.md) into the project root, or merge it with an existing `AGENTS.md`.

## How to know it's working

- fixes land in the real owner instead of a nearby symptom
- new code extends existing helpers instead of forking near-duplicates
- decisions on unstable facts are current and source-backed
- diffs arrive swept: no scaffolding, no narrating comments, no drive-by churn
- deeper investigation happens before mistakes, not after them

## Honest calibration

On top-tier models, much of this workflow is close to default behavior — the gains concentrate in the parts models actually skip: the reuse check before writing new code, and the final pass over the finished diff. The rest pins the bar in writing so behavior stays consistent across tasks, sessions, and models. Weaker or faster models benefit more broadly.

## Tradeoff

Rigor over speed on non-trivial work — by design. The skill itself tells the agent to match effort to the task and never turn a small mechanical edit into process theater.

## License

[MIT](./LICENSE)
