# Examples

Short examples of what `Less Is More` changes in practice.

## 1. Fix It Where It's Decided

**User request:** "Fix the sync bug."

Wrong move:

- patch the nearest failing method
- add retries and extra logging
- hope the symptom disappears

Better move:

- follow the data end to end to the place that decides it
- find which cause it really is: a stale cache, two places changing the same data, or a timing problem
- fix it there, then confirm the bug is gone with one focused check

## 2. A Cleanup Comes Out Smaller

**User request:** "Clean up this auth flow."

Wrong move:

- introduce an `AuthManager`, `SessionCoordinator`, and wrapper helpers
- spread the same responsibility across more files
- call it architecture

Better move:

- find the one place that should hold the signed-in state
- delete the duplicate copies of that state and old branches nothing uses anymore
- keep each rule next to the code that enforces it
- end with one obvious path and fewer files than before

## 3. One Rule Per Symptom Is Not A Fix

**User request:** "Users who chat in other languages say the coach keeps starting replies with 'As an AI…'. Fix it."

Wrong move:

- add the phrase in each language to the banned-phrase filter

Better move:

- find where the behavior is decided: the "never mention being an AI" instruction was sent only in English
- send it in every language
- notice the phrase filter is never called by the app, and delete it instead of growing it

## 4. Finish By Subtracting

**User request:** "Add the export feature."

Wrong move:

- tests pass, hand it back
- leave debug prints, a comment narrating each change, two unused parameters, and a formatting helper that duplicates one three files away

Better move:

- check the net size, and ask of each addition what would break without it
- delete the debug prints, narrating comments, and unused parameters
- use the existing formatting helper instead of the new copy
