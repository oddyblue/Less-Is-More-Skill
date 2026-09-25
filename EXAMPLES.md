# Examples

Short examples showing what `Less Is More` changes in practice.

## 1. Hesitation Triggers Better Diagnosis

**User request:** "Fix the sync bug."

Wrong move:

- patch the nearest failing method
- add retries and extra logging
- hope the symptom disappears

Better move:

- trace the sync path end to end to where the state is decided
- identify where source of truth diverges
- compare whether the bug is caused by stale cache, wrong ownership, or a lifecycle race
- fix the real owner, then verify the regression with a focused check

## 2. The First Plausible Fix Is Not Automatically The Right Fix

**User request:** "Clean up this auth flow."

Wrong move:

- introduce an `AuthManager`, `SessionCoordinator`, and wrapper helpers
- spread the same responsibility across more files
- call it architecture

Better move:

- identify the current owner of auth state
- remove duplicate state and stale compatibility branches
- keep each rule next to the code that enforces it
- prefer one obvious path over multiple coordinating layers

## 3. One Rule Per Symptom Is Not A Fix

**User request:** "Turkish users say the coach keeps starting replies with 'As an AI…'. Fix it."

Wrong move:

- add Turkish phrases to the banned-phrase filter
- add German ones while you're there

Better move:

- find where the behavior is decided: the "never mention being an AI" instruction was sent only to English users
- send it to every language
- notice the phrase filter is never called by the app, and delete it instead of growing it

## 4. The Diff Gets A Final Pass

**User request:** "Add the export feature."

Wrong move:

- tests pass, hand it back
- leave debug prints, a comment narrating each change, two unused parameters, and a formatting helper that duplicates one three files away

Better move:

- re-read the complete diff as a skeptical reviewer
- delete scaffolding, narrating comments, and anything that doesn't trace to the task
- replace any duplicate introduced by the feature with the existing helper
- report separate cleanup opportunities without expanding the feature diff
