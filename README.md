# Less Is More

A reduction-first skill for coding agents — Claude Code, Codex, Cursor, and anything that reads `AGENTS.md` or the [Agent Skills](https://agentskills.io) format.

Coding agents add. Every session leaves a little more code, a few more rules, another fallback — and the project gets slower and costlier for every agent that follows. This skill makes subtraction the default move:

- fix problems where they start, not with a special case per symptom
- prefer no edit, deleting, merging, and replacing before adding
- remove replaced behavior instead of hiding it behind a flag or fallback
- do everything asked, and nothing the app doesn't need
- finish by checking the net size and removing what the change doesn't need

## The idea

*Less* means fewer moving parts first — separate paths doing the same job, copies of the same state, special cases, fallbacks, flags, layers, dependencies — and fewer lines too, in code and in the instructions and docs around it. Deleting large chunks is often the best change available. Never less verification, and never squeezed code.

> No edit → delete → merge → replace → add the smallest thing that fully works.

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

### Always-on companion (recommended)

Agents rarely load a skill on their own, and bloat happens in ordinary sessions. Put this short rule in your global `CLAUDE.md` or `AGENTS.md` so every session gets the core idea, and the skill handles deliberate cleanup:

```text
Keep the project small: code and the text around it. Before adding anything, check whether deleting, merging, or reusing what exists solves the task. Fix problems where they start, not with a special case per symptom. When new behavior replaces old, remove the old path; don't keep it behind a flag, fallback, or special case. Do everything asked, fully, and add no features, options, or layers the app didn't ask for. Fix real bugs you find when you're sure of the problem and the fix; otherwise report them. A cleanup should come out smaller. Before finishing, remove anything the task would still work without. For cleanups, refactors, and larger changes, use the less-is-more skill.
```

## How to know it's working

- cleanups come out smaller, and reports state the net size
- replaced behavior is deleted, not hidden behind another condition
- bugs are fixed where they start, not patched per case
- nothing the app didn't ask for shows up in the diff

## Honest calibration

Top models already delete obvious dead code. The gains are in the places they still drift: patching each symptom with a new rule, keeping replaced behavior as a fallback, and approving their own additions. A small self-built smoke test on an earlier draft (Opus 5.5, one run per variant) found no over-deletion and nothing broken; treat it as a sanity check, not proof. The skill scales to the task: a typo fix needs none of it.

## License

[MIT](./LICENSE)
