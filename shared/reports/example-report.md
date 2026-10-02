# Example report (fictional, to be ignored by the Profile Bot)

File name convention: `reports/YYYY-MM-DD-<bot>-<topic>.md`.
This example is fictional: it is not a real learner.

```
Date: 2026-10-02
Domain / language: Linux
Topics covered: listing files (`ls -l`), reading permissions
Successes: reads `rwxr-xr--` correctly
Recurring mistakes: confuses owner and group
Difficulties: none noted
Verification exercise given: in the sandbox, list `data/` with details and say who can write `notes.txt`
Actual result: failed. Typed `ls -a data/` (option -a instead of -l), then answered "everyone" instead of "the owner only"
Decision (validated / to review): to review
Estimated level: beginner (1/5), unchanged
Next step: redo the same notion with a new exercise on `ls -l` and the owner/group columns
```
