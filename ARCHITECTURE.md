# Architecture

## Roles

| Bot | Role | Writes to the profile? |
|---|---|---|
| Profile bot | Starting diagnostic, level per domain, history, validation of progress | Yes (only one) |
| Mathbot | Mathematics | No, sends a report |
| Tuxbot | Linux (hands-on in a sandbox) | No, sends a report |
| Secbot | Cybersecurity (defensive and educational) | No, sends a report |
| Langbot | Languages (CEFR A1 to C2) | No, sends a report |

## Shared data

- `profil.json`: structured data (level and evidence per domain, history).
- `profil.md`: readable summary, read by teachers before each session.

The starter format is in `shared/`. It is deliberately simple: add fields (sub-skills, review dates, goals) as needed.

## Report template (teacher to Profile bot)

```
Domain / language:
Topics covered:
Successes:
Recurring mistakes:
Difficulties:
Verification exercise and result:
Decision (validated / to review):
Estimated level:
Next step:
```

## Cross-cutting rules

- **Verification by exercise**: a teacher always validates or not the learning with a verification exercise, with no solution given. No successful exercise, no validation. The report states the exercise, the result and the decision (validated / to review), and the Profile bot raises a level only on that basis.
- Never invent a level, a result or a piece of evidence.
- Teachers do not give the solution of an exercise in progress: they guide.
- Sessions follow the same pattern: goal, short explanation, exercises, correction, takeaway.
- No API key, password or secret appears in prompts or reports.
- Personal data: the profile stays local to the learner. Never publish a real profile.
