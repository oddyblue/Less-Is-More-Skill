---
name: less-is-more
description: Reduction-first coding for every change, whether building, fixing, refactoring, or cleaning up. Delete, merge, or replace before adding, so the project ends up smaller and simpler without losing anything the app needs, in code and in the text around it. Matters most for cleanups, refactors, and larger changes.
---

# Less Is More

A way of working for every change, not a cleanup mode: leave the project smaller and simpler than it would otherwise be, without losing anything the app needs. This applies to code and to the text around it: instructions, rules, docs, notes, and reports. Everything the project keeps is read and paid for in every later session; a small project keeps agents fast, cheap, and smart.

Measure in moving parts first, then lines. Moving parts are separate paths doing the same job, copies of the same state, special cases, fallbacks, flags and options, layers, dependencies, and things that must change together. Deleting large chunks of code or text is often the best change available, and a larger edit that removes a moving part beats a small patch that adds one. Fewer lines is a real gain; just never squeeze readable code or drop real checks to get there.

Scale the steps to the task, never the principle: a typo fix needs none; a refactor needs all.

## Before editing

Find where the behavior is actually decided and work there, not where the symptom shows up. Most unnecessary code comes from fixing the wrong thing, so try once to prove your diagnosis wrong before acting on it. Where logs or recorded data exist, look at what actually happened instead of reasoning about it.

Then consider, in order: no edit, delete, merge, replace, and only then add the smallest thing that fully works. Look for what already does the job — an existing function, pattern, or platform feature — before writing a new one. A verified "no change needed" is a good result.

For a replacement or cleanup, name exactly what will go: the functions, branches, files, or settings. Afterward, check that they are actually gone.

## While editing

Replace; don't layer. When new behavior supersedes old behavior, delete the old path. Don't keep it behind a flag, mode, guard, fallback, or wrapper unless something real still depends on it — a named client, a saved data format, an app or server version still in use — and then keep it in one place.

A fallback is extra behavior, not free safety. Keep one only if its degraded result is acceptable and testable; otherwise fail clearly.

Don't fix bad behavior by adding a rule per bad case — another banned phrase, keyword check, or special case for the one input that failed. Fix or remove what produces the bad cases. If an old rule never really worked, deleting it is the fix.

Store each piece of state once and derive the rest. Don't add a helper, wrapper, manager, or layer to shorten one function or for a future that isn't here. Do add structure when it removes real duplication or lets a behavior be changed without reading unrelated code.

Before deleting code that looks unused, check callers, saved data, configuration, and anything loaded by name — in apps: stored settings keys, database models and migrations, Info.plist and entitlement entries, asset names, intents, and notification categories. A search with no hits is not proof. Prompts, thresholds, and heuristics tuned against a measurement are trimmed by re-measuring, not by taste.

## Scope

Do everything the request asks, completely: less code is never a reason to deliver less. Don't add features, options, or behavior the app didn't ask for, and don't build for imagined needs: future-proof means easy to change later, which usually means less code. When the request is ambiguous, build the most direct reading and say so; don't build for several readings at once. If a wrong reading could lose people's data or be hard to undo, ask one question first.

For real problems you find along the way — bugs, dead code, outdated text, duplicate paths — investigate until you are sure the problem is real and you know the best fix. If the fix is clearly better for the app, make it and say so. If you are not sure, report it instead.

## Finish by subtracting

When it works, review the whole change for things to remove:

- Check the net size: lines added and removed, and new files. A cleanup, refactor, or reduction should come out smaller; if it doesn't, say why before finishing. Other work may grow, but only by what it needs.
- For each new function, file, branch, flag, fallback, option, dependency, or test, ask what would break without it. If nothing the task needs, remove it; when that's cheap to test, actually remove it and re-run the check.
- Remove leftovers: debug output, scaffolding, unused parameters and imports, comments that narrate the change, near-duplicates of existing code.
- Tests are code too. Keep about one focused test per changed behavior where the project keeps tests, delete tests for behavior you removed, and trust a new test only after seeing it fail without the fix.
- For a large change, get fresh eyes: a reviewer who didn't write it, looking only for what to delete. Approving your own additions is the known weak spot.

Then stop; this pass starts no new work.

## Report

Lead with the result in plain words: the net size (+added / −removed), what was removed or merged, what you checked and how, anything you fixed beyond the request, and anything still uncertain. Claim only what the check shows: a passing test doesn't prove that sound played, the screen shows it, or data was saved. One or two lines for a small change. Don't narrate this workflow.
