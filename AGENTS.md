<!-- Synced from skills/less-is-more/SKILL.md — edit there first, then mirror the body here and into .cursor/rules/less-is-more.mdc. -->


# Less Is More

Leave the system easier to inspect, explain, change, and trust.

Prefer, in order: **no edit, deletion, consolidation, replacement, then a narrow addition**. This is a decision order, not a checklist to perform or narrate. Correctness, explicit product requirements, user data, and useful product character outrank line count. The target is less accidental complexity: fewer competing owners, sources of truth, states, branches, fallbacks, abstractions, dependencies, and things that must change together.

## Establish the real problem

For non-trivial work, decide whether the request is an audit, bug fix, feature, simplification, or a mix. Do not call new product behavior simplification, and do not turn classification into ceremony. If the request is materially ambiguous, contradictory, destructive, or likely to affect user data, ask one precise question; otherwise state the narrowest safe assumption and proceed.

1. **Start from real state.** Read the applicable repository instructions, current files, configuration, dependencies, tests, generated sources, and working tree. Protect unrelated user changes. Do not reason from memory when the current system can be inspected.
2. **Name the invariant and owner.** State what must be true, which component enforces it, what state and side effects it owns, and what success and failure mean. If the invariant or owner is unclear, keep investigating.
3. **Verify what can drift.** Confirm framework behavior, platform rules, external APIs, dependencies, and other time-sensitive facts against current primary sources. Say `unknown` when evidence is unavailable.
4. **Trace end to end.** Follow inputs, state, persistence, concurrency, cancellation, lifecycle, side effects, callers, and downstream consumers. Work from the ownership boundary, not only the reported symptom or diff window.
5. **Audit the shape before writing.** Look for duplicate state, competing owners, second sources of truth, obsolete branches, abandoned migrations, unsupported compatibility, unacceptable fallbacks, unused configuration, hand-edited generated output, and abstractions that guard no real boundary. Before deleting apparently dead code, check reachable callers, supported clients, persisted data, migrations, and deployment paths.
6. **Choose the smallest coherent operation.** Consider no edit, deletion, consolidation, and direct replacement before addition. Reuse the project's existing owner, idiom, helper, or platform primitive before creating another. For non-trivial work, be able to say briefly why the choice beats the strongest realistic alternative; do not produce a ritual options table.
7. **Verify the real outcome.** Use focused regression tests where behavior changed, remove tests that preserve obsolete behavior, and run the relevant broader checks. Match verification to the claim: an internal event is not proof of audible playback, visible rendering, durable persistence, delivered data, or completed teardown. Use real integration, lifecycle, device, or human checks when software tests cannot establish the result.

## Replace; do not layer

When a requirement makes behavior obsolete, remove or replace that behavior at its owner. Do not retain it behind another boolean, mode, guard, wrapper, suppression condition, retry layer, or configuration option unless a current supported consumer, persisted format, deployment boundary, or explicit product requirement demonstrably needs both paths. Compatibility requires a named supported client, format, or deployment boundary and a concrete failure without it; hypothetical future use is insufficient. Keep necessary compatibility at one boundary rather than spreading it through the core.

A fallback is additional product behavior, not free reliability. Keep one only when its degraded behavior is acceptable, preserves the product's invariant and identity, has one owner, cannot compete with the primary path, and can be tested. If a fallback is unacceptable, delete it or narrow its boundary; do not preserve it and add selective suppression. When no acceptable fallback exists, prefer an explicit failure over silently doing the wrong thing.

## Keep shape and scope small

Do not implement an adjacent improvement merely because it is valid. Include adjacent work only when necessary to preserve the invariant, remove duplication created by the requested change, delete behavior the change made obsolete, or keep the owning path coherent. Report other opportunities without modifying them. Avoid unrelated renaming, formatting, file movement, comment rewriting, abstraction, observability, hardening, and drive-by cleanup.

In bug fixes and simplification work, treat every new state, runtime branch, fallback, abstraction, public API, protocol requirement, configuration option, dependency, or source of truth as a cost. First ask whether deletion, consolidation, or replacement makes it unnecessary. Feature work may require new behavior, but it should live with the existing owner and remove paths it supersedes.

Derive state instead of mirroring it. Keep one owner for each side effect and policy with the code that enforces it. Do not extract a helper, protocol, wrapper, manager, or strategy merely to shorten one function. A one-caller abstraction should enforce a real boundary, isolate an external dependency, remove meaningful duplication, or make an important invariant directly testable. Do not compress readable code or remove useful checks to reduce line count.

Keep comments only when they explain an enduring constraint, non-obvious invariant, external requirement, or why a simpler-looking implementation is wrong. Delete comments that narrate the change, preserve bug history, repeat the code, or describe scaffolding that no longer exists. History belongs in commits and regression tests.

## Finish subtractively, then stop

After the change works, review the complete affected diff. The final pass is subtractive: delete scaffolding, debug output, redundant guards, unused state, parameters, imports, configuration, obsolete tests, narrative comments, near-duplicates, and unrelated churn; inline or consolidate where that leaves the owner clearer. It must not introduce a new capability, fallback, abstraction, compatibility path, configuration option, or unrelated fix. If review exposes a correctness problem in the requested invariant, return to the owning-path workflow; otherwise report separate opportunities and leave them untouched.

Stop when the invariant holds, relevant verification passes, behavior made obsolete by the change is removed or retained with evidence, no competing owner or duplicate source of truth was introduced, and the diff contains no unrelated work.

Do not edit on a hunch or impose a generic best practice over the system's documented constraints and actual behavior. A verified no-edit result is successful. If you cannot name the owner, verify the premise, or explain why the change beats the strongest alternative, continue diagnosing instead of patching. Report unavailable evidence as `unknown` rather than guessing.

## Report

Before a non-trivial edit, give a short read: the problem, evidence, chosen operation, main risk, and verification plan. Afterward, state what changed; what was deleted, replaced, or consolidated; what was verified; and what remains unknown or intentionally unchanged. Compress tiny changes to one or two lines.
