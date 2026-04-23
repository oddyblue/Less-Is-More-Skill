# Examples

Short examples showing what `Less Is More` changes in practice.

## 1. Hesitation Triggers Better Diagnosis

**User request:** "Fix the sync bug."

Wrong move:

- patch the nearest failing method
- add retries and extra logging
- hope the symptom disappears

Better move:

- trace the owning sync path end to end
- identify where source of truth diverges
- compare whether the bug is caused by stale cache, wrong ownership, or a lifecycle race
- fix the real owner, then verify the regression with a focused check

## 2. Time-Sensitive Facts Get Verified Live

**User request:** "Update this code for the latest framework API."

Wrong move:

- rely on remembered syntax
- copy an older snippet from memory
- patch call sites before checking release notes or current docs

Better move:

- use the actual current date
- verify the current API in official docs or release notes
- confirm whether the framework changed behavior, naming, defaults, or migration guidance
- only then choose the narrowest correct update

## 3. The First Plausible Fix Is Not Automatically The Right Fix

**User request:** "Clean up this auth flow."

Wrong move:

- introduce an `AuthManager`, `SessionCoordinator`, and wrapper helpers
- spread the same responsibility across more files
- call it architecture

Better move:

- identify the current owner of auth state
- remove duplicate state and stale compatibility branches
- move invariants closer to their owner
- prefer one obvious path over multiple coordinating layers

## 4. Research Narrows Uncertainty Instead Of Becoming Theater

**User request:** "Why is this endpoint slow in production?"

Wrong move:

- browse broadly
- repeat generic performance advice
- produce a long memo without proving anything about this code path

Better move:

- inspect the local implementation and surrounding call sites
- identify the strongest realistic causes
- research only the unstable facts that could change the diagnosis
- choose the fix only after the bottleneck is defensible with evidence
