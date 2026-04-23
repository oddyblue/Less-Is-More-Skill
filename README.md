# Less Is More

An architecture-first instruction set for coding agents.

Less accidental complexity. More evidence. More ownership clarity.

`Less Is More` helps agents make safer, cleaner, more current code changes by forcing a stronger workflow before they edit:

- inspect the real local baseline
- verify unstable facts from current primary sources
- trace the owning code path before proposing a fix
- treat hesitation as a signal to investigate further
- compare nearby explanations and realistic fixes
- choose the clearest justified outcome, not the first workable patch

## The Problem

Coding agents often fail in predictable ways:

- they make silent assumptions and code past uncertainty
- they patch the nearest symptom instead of the owning code path
- they trust stale framework knowledge or old examples
- they add abstractions, helpers, or "flexibility" before it is earned
- they produce plausible changes that are harder to explain than the problem itself

## The Approach

`Less Is More` is not "write fewer lines no matter what."

It means:

- less accidental complexity
- less duplicate state
- less confused ownership
- less speculative abstraction
- fewer changes made on weak evidence

The goal is a system that is easier to inspect, explain, change, and trust.

## What Makes It Different

Many instruction files focus on behavior in the abstract. `Less Is More` is a workflow.

It pushes the agent to:

- start from the real repo state instead of memory
- verify time-sensitive facts against current primary sources
- look for the real owner of the behavior before editing
- challenge the leading diagnosis when confidence is incomplete
- prefer deletion, consolidation, or reshaping when those produce a stronger result
- stop when evidence is weak instead of forcing motion

The key idea is simple:

> Treat hesitation as a signal, not a speed bump.

If the diagnosis is still soft, the answer is usually not a bigger patch. The answer is better investigation.

## Files

- [`skills/less-is-more/SKILL.md`](./skills/less-is-more/SKILL.md): installable skill
- [`CLAUDE.md`](./CLAUDE.md): portable root instruction file
- [`.cursor/rules/less-is-more.mdc`](./.cursor/rules/less-is-more.mdc): Cursor project rule
- [`EXAMPLES.md`](./EXAMPLES.md): short examples of the workflow in practice

## Install

### Skills CLI

After this repo is published, install it with:

```bash
npx skills add https://github.com/YOUR_NAME/less-is-more --skill less-is-more
```

Replace `YOUR_NAME` with the GitHub owner you publish under.

### Codex

Copy [`skills/less-is-more`](./skills/less-is-more) into your Codex skills directory, typically:

```text
~/.codex/skills/less-is-more
```

### Claude Code

Copy or merge [`CLAUDE.md`](./CLAUDE.md) into your project instruction file.

### Cursor

Copy [`.cursor/rules/less-is-more.mdc`](./.cursor/rules/less-is-more.mdc) into your project's `.cursor/rules/` directory.

## How To Know It's Working

These guidelines are working if you see:

- fewer speculative abstractions and fewer drive-by edits
- more fixes landing in the real owner instead of a nearby symptom
- more current, source-backed decisions on unstable facts
- smaller diffs that are easier to defend
- clarifying questions or deeper investigation before mistakes, not after them

## Tradeoff

`Less Is More` biases toward rigor over speed on non-trivial work.

That is intentional. It should reduce expensive mistakes, not slow down obvious one-line edits with unnecessary ceremony.

## Examples

See [`EXAMPLES.md`](./EXAMPLES.md) for concrete before-and-after behavior.

## License

[MIT](./LICENSE)
