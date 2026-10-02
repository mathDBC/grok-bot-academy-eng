# Mathbot

Public bot template of [Grok Bot Academy](https://github.com/mathDBC/grok-bot-academy-eng).

## Import name
"Grok Bot Academy - Mathbot"

## Contents of this folder
- `PROMPT.md`: the bot's instructions (identical to `../../prompts/01-mathbot.md`).
- `skills/mathbot-role/SKILL.md`: the bot's role and method.
- `skills/mathbot-getting-started/SKILL.md`: the first conversation with a new learner.

## Installation
1. Create an agent and name it "Grok Bot Academy - Mathbot".
2. Paste the content of `PROMPT.md` as the agent's instructions.
3. Add the two skills (`skills/*/SKILL.md`) to the agent, using your platform's skill import feature. Otherwise, paste their content after the instructions.
4. Create a shared folder `academy/` accessible to the 5 bots, with a copy of `../../shared/` (`profile.md`, `profile.json`, `reports/`).
   - Permissions: read `profile.md` and `profile.json`, write only in `reports/` (creating new files).
   - No special tool is needed.
5. Messaging: put the 5 bots in the same group channel, or enable inter-agent messaging, so teachers send their reports to the Profile Bot.
6. Test: say "Hello" to the bot; it should introduce itself, explain the loop and ask its starting questions one by one.

## Degraded mode
- Profile Bot absent or shared folder not found: the bot asks the learner for their level and notes it as "declared".
- Messaging unavailable: the report is given to the learner (or dropped in `reports/`) to be passed to the Profile Bot.
- Another bot absent: the others carry on, only the missing subject is unavailable.

## Reminders
No API key, password or secret in prompts, skills or reports. Never publish a real learner profile.
