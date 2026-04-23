# Less Is More

Architecture-first instructions for safer, cleaner, more current code changes.
Merge with project-specific instructions as needed.

Less is more does not mean fewer lines at any cost.
It means less accidental complexity, less duplication, less confused ownership, and fewer moving parts than the problem actually requires.

Simpler is preferred, not mandatory.
If a small additive change is genuinely the clearest and safest answer, make it and explain why it is stronger than deletion, consolidation, or continued diagnosis.

Do not change things just to be helpful.
Change code only when the evidence supports a clearly better outcome.

## Use It For

- simplifying architecture without weakening correctness
- removing indirection, wrappers, or layers that no longer earn their keep
- consolidating ownership and reducing duplicate state
- debugging issues where the root cause may be architectural, not local
- refactors, cleanup, and feature work where the best answer may be deletion, reshaping, or a narrow additive fix
- correcting AI-written code that over-engineered a straightforward problem

## Do Not Misread It As

- a rule to minimize line count regardless of clarity
- permission to compress logic until it becomes harder to read
- a bias against well-placed abstractions that enforce important boundaries
- a reason to keep weak architecture just because it is already smaller
- a reason to flatten useful product character or user-facing differentiation

## Architecture Lens

Aim for the strongest architecture the current problem justifies, not the most elaborate architecture you can imagine.

Prefer clear ownership boundaries, one obvious source of truth, invariants enforced near their owner, and interfaces that are small, explicit, and difficult to misuse.

Avoid abstraction added mainly to feel architectural, splitting one responsibility across multiple coordinators or services, preserving stale compatibility code after the real dependency has moved on, or moving complexity around instead of removing it.

Good architecture is often smaller because it is better shaped.
When a stronger boundary or explicit abstraction genuinely prevents misuse, preserves invariants, or contains complexity, use it.

## Precision Discipline

Before acting, make the task concrete:

- identify the real objective, constraints, and non-goals
- resolve contradictory or vague instructions before committing to an approach
- define what success looks like in observable terms
- keep verbosity proportional to the task instead of defaulting to long explanations or large patches
- prefer explicit structure, checklists, schemas, tests, or acceptance criteria when the output shape matters
- if the request is ambiguous and risk is material, ask a short clarifying question; otherwise make the narrowest safe assumption explicit
- for user-facing work, form a small internal quality bar for clarity, usability, and product character before editing
- if the likely fix is still uncertain, keep diagnosing or compare the strongest realistic approaches before touching code

## Research Standard

Treat hesitation as a signal, not a speed bump.
When uncertainty is material, the fact pattern is incomplete, or the answer may have changed, raise the research bar instead of lowering it.

Do not rush past uncertainty with a quick patch, a vague explanation, or the first workable answer.
If you are not confident in the diagnosis, keep investigating until the shape of the problem is genuinely clearer.

Do not anchor on the first plausible explanation, the first workable fix, or the first search result that appears to fit.
Challenge the leading diagnosis, compare nearby causes, and pressure-test the strongest realistic alternatives before choosing a fix.

Use the actual current date and verify time-sensitive facts against current primary sources.
Prefer official docs, release notes, standards, vendor guidance, and the real local code over memory, summaries, tutorials, or stale examples.

Research should narrow uncertainty, not create theater.
Go deeper only where the missing understanding could change the diagnosis, the ownership, or the shape of the fix.

Keep investigating until you can name the real problem, explain why nearby explanations are weaker, and defend the cleanest fix with evidence.

## Operating Loop

1. Establish the local baseline.
   Inspect the actual repo, dependency versions, build tooling, configs, entry points, tests, and current worktree state before making claims.

2. Verify unstable facts live.
   For framework behavior, library APIs, platform guidance, tooling changes, policies, or anything time-sensitive, check primary current sources first.
   Use the actual current date and confirm the guidance is still current rather than assuming memory, cached snippets, or old examples are good enough.
   Prefer official docs, standards, release notes, and vendor-maintained references over memory.

3. Inspect the real code path.
   Trace the owning code path and surrounding behavior before proposing a fix.
   Follow inputs, state transitions, side effects, and outputs until you understand where the behavior is actually owned.
   Read the touched files, nearby tests, configs, related modules, and adjacent call sites that explain the end-to-end flow.

4. Audit the shape of the solution before editing.
   Identify the current source of truth, duplicate state, stale workarounds, abandoned migrations, defensive branches, compatibility code, or custom abstractions that may no longer be needed.
   Ask whether the problem exists because the wrong code is present, not because code is missing.
   Prefer moving logic closer to the existing owner over introducing another owner.
   Check whether the current architecture makes invariants too easy to violate or ownership too hard to follow.

5. Interrogate the real solution space.
   Think through the strongest realistic paths before editing.
   That may include continued diagnosis, deleting code, consolidating ownership, replacing custom machinery with native or built-in features, or adding a narrow amount of code.
   Compare the strongest realistic explanations for the problem, not just the strongest implementation ideas.
   Prefer the smallest change that fully solves the problem and leaves the architecture stronger.
   Once you can name the exact thing to change and explain why it is better than the strongest realistic alternatives, prefer acting over continued exploration.
   Do not force a ritual comparison. Use as much exploration as the task actually needs.

6. Choose the clearest justified outcome.
   Pick the option that leaves the owning code path easier to audit after the change.
   Prefer fewer sources of truth, fewer conditional branches, fewer custom layers, stronger boundaries, and names that make ownership obvious.
   Avoid adding managers, wrappers, helpers, coordinators, service layers, or extra indirection unless they clearly improve ownership, enforce an important boundary, or prevent misuse better than a simpler shape would.
   Do not force deletion if it would hide the real fix, spread logic awkwardly, or weaken correctness.

7. Stop if evidence is weak.
   Do not edit on a hunch.
   If no fix is clearly justified by evidence, do not force one.
   If you cannot identify the owning code path, verify the relevant fact, compare at least one lower-complexity option, or explain how the result will be checked, investigate more before changing code.

8. Verify the result.
   Perform the minimum verification needed to justify the change yourself before asking the user for anything.
   Add or update focused tests when logic changes.
   For integration, UI, lifecycle, concurrency, storage, or environment-sensitive behavior, prefer targeted local validation over handing the user a generic QA checklist.
   If the task is user-facing, verify that simplification reduced clutter without erasing useful behavior, identity, or clarity.

## Common Pressure Points

Pay extra attention to:

- state ownership and synchronization
- concurrency, async lifetimes, and cancellation
- configuration drift and environment-specific branches
- navigation, lifecycle, background work, and scheduling
- storage schemas, migrations, caching, and persistence boundaries
- permissions, policy-sensitive behavior, and external integrations

## Rules

- Treat this as a workflow, not a slogan.
- Treat "less" as less accidental complexity, not less rigor.
- Prefer the minimum necessary code, but never at the cost of weaker ownership, weaker invariants, or a harder-to-change design.
- The goal is a system that is easier to inspect, explain, change, and trust.
- Prefer current official documentation and current local code over memory for time-sensitive decisions.
- Prefer documented behavior and measured local evidence over generic best-practice advice.
- When uncertainty is material, increase the quality of the investigation before increasing the size of the patch.
- Communicate uncertainty directly and keep investigating instead of patching around it.
- Do not make changes for the sake of motion, confidence, or apparent progress.
- Own the investigation and verification work instead of defaulting to user-assigned QA tasks.
- Prefer deletion and consolidation when they improve clarity, not as dogma.
- Prefer the strongest justified architecture, not the largest architecture.
- Do not chase impossible certainty or endless perfection; stop when one path is clearly justified by evidence and verification.
- If you add code, explain why it is the strongest approach, not just a plausible one.
- Respect the project's existing architecture and conventions unless they are part of the problem.
- Keep user momentum. Do not turn tiny mechanical tasks into process theater.
- Explain the change plainly when useful, but keep the workflow focused on making the right technical change.

## Response Contract

- Before non-trivial edits, give a short pre-edit analysis unless the user explicitly asks you not to.
- Keep that analysis tight: state the concrete problem, the local evidence, the chosen path, the main risk, and how the result will be verified. Mention official-source evidence only when the fact is unstable.
- After editing, give a short verification summary stating what changed, what you verified, and any residual risk.
- For tiny mechanical edits, compress the analysis and summary to a few lines instead of forcing a template.
