<!-- Synced from skills/less-is-more/SKILL.md — edit there first, then mirror the body here and into .cursor/rules/less-is-more.mdc. -->

# Less Is More

Make changes that leave the system easier to inspect, explain, change, and trust. *Less* means less accidental complexity, duplication, and confused ownership — never less rigor, less verification, or fewer lines for their own sake. The aim is the best professional solution the problem justifies — often reached by subtraction, sometimes by a narrow addition, sometimes by no edit yet — leaving a codebase that stays fast to understand as it compounds over time.

## The bar for changing code

Change code when there is evidence of a clearly better outcome — then change it fully and well: a complete fix, not a timid half-measure. The same bar covers improvements you discover beyond the ask: investigate deeply, check against the strongest alternatives, and once certain something is genuinely better, fix it too. The gate is proof, not permission — it licenses real betterment and forbids expanding scope on a hunch. When the evidence isn't there, keep diagnosing or leave the code alone. And the bar cuts both ways: small but weak code (tangled ownership, a violated invariant) still justifies change even when the fix is larger.

If the request is ambiguous or self-contradictory and the risk is material, ask one sharp question; otherwise state the narrowest safe assumption and proceed.

## Work the owning path, not the diff window

1. **Start from real state.** The actual files, dependency versions, config, and current worktree — not memory or assumption.
2. **Verify what can drift.** Framework and library APIs, platform rules, and time-sensitive facts: confirm against current primary sources, as of today's actual date, before relying on them.
3. **Trace ownership.** Follow inputs, state, side effects, and the surrounding call sites until you can see where the behavior actually lives and how the end-to-end flow works.
4. **Audit the shape before editing.** The problem is often the wrong code being present, not code missing. Look for duplicate state, a second source of truth, abandoned migrations, dead or disabled branches, stale compatibility code, and abstraction with a single caller that guards no real boundary. Before removing code that only looks dead, confirm it is truly unreachable — no live call site, no reachable state, no path it quietly protects.
5. **Reuse before writing.** Find what already does the job — the codebase's own helper, pattern, or idiom first, then a built-in platform or library primitive — and extend the existing owner rather than fork a near-duplicate. Re-implementing a capability the system already has is the most common way good diffs go bad.
6. **Weigh the options, then choose.** Compare the strongest realistic paths — more diagnosis, deletion, consolidation, reuse, or a narrow addition — and the competing explanations for the cause, not just the fixes. Pick the smallest change that fully solves the problem and leaves the owning path most auditable: fewer sources of truth, fewer branches, clearer ownership, logic kept with its existing owner, in the project's idiom unless the idiom is the problem. Once you can say why it beats the alternatives, act — don't ritualize the comparison.
7. **Verify your result.** Focused tests for logic changes (including updating or removing tests that pinned the old behavior); targeted local validation for UI, lifecycle, concurrency, storage, or integration behavior — done yourself before handing back. Confirm any simplification cut clutter without erasing useful behavior or product character.

## Where complexity hides

Look hardest where simplification tends to go wrong: state ownership and synchronization; concurrency, async lifetimes, and cancellation; navigation, lifecycle, and scheduling; storage schemas, migrations, and caching; configuration and environment-specific branches; permissions and external integrations.

## Altitude

Altitude — the level of abstraction the code sits at — fails in both directions. Too high: speculative generality — layers, options, and parameters with one real caller, abstraction added to feel architectural, complexity moved around instead of removed, one responsibility split across several owners. Too low: repetition that wants a name, hand-rolled machinery that reimplements a built-in primitive. Adding structure is right when it enforces a real boundary, preserves an invariant, or contains complexity better than a flatter shape would — when you add, say why it beats deletion or consolidation, not just that it works. Naming is a cheap probe: a thing you can't name honestly is usually the wrong shape. Keep the clear shape efficient: no gratuitous recomputation, repeated I/O, or quadratic passes over unbounded input — and never contort readable code for an unmeasured micro-win.

## The final pass

Working is not done. Re-read the complete diff as a skeptical reviewer: leftover scaffolding and debug output; comments that narrate the change or the process instead of stating a constraint the code can't show; unused parameters, imports, and guards for impossible states; a near-duplicate of something that already existed; churn — renames, reformatting, drive-by edits — that doesn't trace to the task or a verified improvement. Then look once more at the shape: the working version often reveals a simplification the plan couldn't see, and folding it in now is cheap. Every hunk should earn its place; this pass is what separates a diff that works from one that is finished.

## Don't force it

Don't edit on a hunch, and don't impose a generic best-practice pattern over the system's documented and actual behavior. If you can't name the owning path, verify the fact, or explain why your change beats the strongest alternative, keep investigating instead of patching. And don't over-work a task whose path is already clear — match effort to the task, and don't turn a small mechanical edit into process theater.

## Report

Before a non-trivial edit, give a short read: the concrete problem, the local evidence, the chosen path, the main risk, and how you'll check it. After, state what changed, what you verified, and any residual risk — including adjacent improvements you confirmed and made, and anything you spotted but couldn't fully verify, surfaced for a decision rather than left unsaid. Compress to a line for tiny edits.
