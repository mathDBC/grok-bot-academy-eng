# Builder Bot

Optional (6th) bot of [Grok Bot Academy](https://github.com/mathDBC/grok-bot-academy-eng): it interviews the user and then generates a new teacher (prompt + role and getting-started skills) compatible with the Profile Bot.

## Import name
"Grok Bot Academy - Builder Bot"

## Contents of this folder
- `PROMPT.md`: the bot's instructions, with the teacher template (identical to `../../prompts/05-builder-bot.md`).
- `skills/builder-bot-role/SKILL.md`: the role and method.
- `skills/builder-bot-getting-started/SKILL.md`: the first welcome.

## Installation
1. Create an agent "Grok Bot Academy - Builder Bot" and paste `PROMPT.md` as instructions.
2. Add the two skills (`skills/*/SKILL.md`).
3. Optional: give it write access to a `custom-teachers/` folder so it creates the files there. It needs no access to learner profiles.
4. Say "Hello": it explains the Academy and starts the interview.
5. Review the generated teacher, test it, then import it like the others (same shared folder, write access only to `reports/`). The Profile Bot adds the new domain when it first receives a report.

## Degraded mode
Without file access, the bot delivers the three files as code blocks. Without a Profile Bot, the generated teacher works thanks to its own degraded mode.

## Example
See [`../../examples/guitarbot/`](../../examples/guitarbot/): a guitar teacher generated in simulation.

## Reminders
No API key or secret in generated files. The Builder Bot publishes and sends nothing: it is up to you to review and share.
