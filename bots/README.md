# Bot templates

Each folder is a shareable bot template: `PROMPT.md`, two skills (role and getting started) and an installation `README.md`.

| Bot | Import name | Folder |
|---|---|---|
| Profile Bot | "Grok Bot Academy - Profile Bot" | [`profile-bot/`](profile-bot/) |
| Mathbot | "Grok Bot Academy - Mathbot" | [`mathbot/`](mathbot/) |
| Tuxbot | "Grok Bot Academy - Tuxbot" | [`tuxbot/`](tuxbot/) |
| Secbot | "Grok Bot Academy - Secbot" | [`secbot/`](secbot/) |
| Langbot | "Grok Bot Academy - Langbot" | [`langbot/`](langbot/) |
| Builder Bot (optional) | "Grok Bot Academy - Builder Bot" | [`builder-bot/`](builder-bot/) |

## Installing the team
1. Import the Profile Bot first, then the teachers you want (they also work alone, in degraded mode).
2. Create the shared folder `academy/` from `../shared/`.
3. Permissions: only the Profile Bot writes `profile.md` and `profile.json`; teachers read those files and write only in `reports/` (new files).
4. Connect the bots (group channel, inter-agent messaging, or simply the `reports/` folder).
5. Start the diagnostic with the Profile Bot.

## Create your own teacher
The **Builder Bot** (optional) interviews the user and then generates a new teacher (prompt + skills) compatible with the Profile Bot. See `builder-bot/` and the example `../examples/guitarbot/`.

`PROMPT.md` is a copy of `../prompts/`; if you change one, update both (and the role skill).
