# Architecture

## Roles

| Bot | Role | Writes to the profile? |
|---|---|---|
| Profile Bot | Starting diagnostic, level per domain, history, validation of progress | Yes (only one) |
| Mathbot | Mathematics | No, sends a report |
| Tuxbot | Linux (hands-on in a sandbox) | No, sends a report |
| Secbot | Cybersecurity (defensive and educational) | No, sends a report |
| Langbot | Languages (CEFR A1 to C2) | No, sends a report |

## Shared data

- `profile.json`: structured data (level and evidence per domain, history).
- `profile.md`: readable summary, read by teachers before each session.

The starter format is in `shared/`. It is deliberately simple: add fields (sub-skills, review dates, goals) as needed.

## Report template (teacher to Profile Bot)

```
Date:
Domain / language:
Topics covered:
Successes:
Recurring mistakes:
Difficulties:
Verification exercise given:
Actual result (passed or failed, with the exact mistake):
Decision (validated / to review):
Estimated level:
Next step:
```

Delivery: the file `reports/YYYY-MM-DD-<bot>-<topic>.md` is the reference; inter-agent messaging is used to notify the Profile Bot (see `shared/reports/example-report.md`).

## Shared folder permissions

- Profile Bot: writes `profile.md` and `profile.json`, reads `reports/`.
- Teachers: read `profile.md` and `profile.json`, create new files in `reports/` (no other write access).

## Evidence and levels

Scale 0 to 5 (languages: CEFR). A level is "declared", "estimated" or "validated". One piece of evidence: `{"date", "source", "point", "result", "decision", "mistake"}`. A level goes up one step after two "validated" reports from different sessions. The Profile Bot records the processed file in the history so it never processes it twice.

## Bot templates

The `bots/` folder holds one shareable template per bot: `PROMPT.md` (copy of the file in `prompts/`), two skills (role and getting started) and an installation `README.md`. Import names: "Grok Bot Academy - Profile Bot", "- Mathbot", "- Tuxbot", "- Secbot", "- Langbot".

## Builder Bot (optional)

A 6th bot, outside the learning loop, helps create your own teacher: it interviews the user then generates a prompt and two skills in the same format, compatible with the Profile Bot (see `bots/builder-bot/` and `examples/guitarbot/`). The Profile Bot adds the new domain when it first receives a report.

## Degraded mode

Every bot works even if the team is incomplete: without the Profile Bot, the teacher estimates the level with a few questions (noted "declared"); without messaging or a shared folder, the report is given to the learner; without another teacher, that subject is simply unavailable.

## Cross-cutting rules

- **Verification by exercise**: a teacher always validates or not the learning with a verification exercise, with no solution given. No successful exercise, no validation. The report states the exercise, the result and the decision (validated / to review), and the Profile Bot raises a level only on that basis.
- Never invent a level, a result or a piece of evidence.
- Teachers do not give the solution of an exercise in progress: they guide.
- Sessions follow the same pattern: goal, short explanation, exercises, correction, takeaway.
- No API key, password or secret appears in prompts or reports.
- Personal data: the profile stays local to the learner. Never publish a real profile.
