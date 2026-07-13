# Less Is More

An architecture-first, reduction-first skill for coding agents — Claude Code, Codex, Cursor, and anything that reads `AGENTS.md` or the [Agent Skills](https://agentskills.io) format.

Less accidental complexity. More evidence. More ownership clarity.

The skill makes an agent earn its diff:

- start from the real repo state, not memory
- verify drift-prone facts against current primary sources, as of the actual date
- trace the owning code path before editing — never patch the diff window
- prefer no edit, deletion, consolidation, and replacement before addition
- remove obsolete behavior instead of preserving it behind another layer
- keep adjacent scope closed
- finish with a subtractive pass over the affected diff

## The problem

Coding agents fail in predictable ways:

- they patch the nearest symptom instead of the owning code path
- they re-implement helpers the codebase already has
- they trust stale framework knowledge and old examples
- they add speculative abstraction before it is earned — or repeat themselves instead of naming the repetition
- they preserve obsolete behavior behind more guards, modes, and fallbacks
- they expand into valid but unrelated improvements
- they stop at "tests pass," leaving scaffolding in the diff: narrating comments, unused parameters, debug output, drive-by churn

## The idea

*Less* means fewer competing owners, sources of truth, states, branches, fallbacks, abstractions, dependencies, and things that must change together — never less rigor, less verification, or fewer lines for their own sake.

The decision order is:

> No edit → delete → consolidate → replace → add narrowly.

When requirements change, remove behavior they make obsolete instead of preserving it behind another layer. Keep adjacent improvements out unless they are necessary to preserve the requested invariant or keep its owning path coherent.

The workflow in one breath: name the invariant → trace its owner → audit the shape → choose the smallest coherent operation → verify the real outcome → finish subtractively → stop.

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
- obsolete behavior is removed instead of hidden behind another condition
- new code extends existing owners instead of creating competing paths
- decisions on unstable facts are current and source-backed
- adjacent opportunities are reported rather than silently added
- final diffs contain no scaffolding, narrating comments, or drive-by churn
- deeper investigation happens before mistakes, not after them

## Honest calibration

On top-tier models, much of this workflow is close to default behavior. The gains concentrate where models still drift: checking no-edit and subtraction before addition, replacing obsolete paths instead of layering around them, keeping adjacent scope closed, and finishing subtractively. The rest keeps that behavior consistent across tasks, sessions, and models. Weaker or faster models benefit more broadly.

## Tradeoff

Rigor over speed on non-trivial work — by design. The skill itself tells the agent to match effort to the task and never turn a small mechanical edit into process theater.

## License

[MIT](./LICENSE)
