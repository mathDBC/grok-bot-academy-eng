# Grok Bot Academy: a small agentic tutoring loop

Grok Bot Academy is a prototype of AI-agent tutoring. A **Profile Bot** measures your level in
each subject, and **teacher bots** teach you. After every session, each teacher sends a report
to the Profile Bot, which updates the profile. Teachers read that profile to adapt the next session.

It is a prototype, not a finished product. Try it, break it, improve it.

## The loop

```mermaid
flowchart LR
    U[Learner] -->|starting diagnostic| P[Profile Bot]
    P -->|writes| F[(profile.md / profile.json)]
    F -->|read-only| M[Mathbot]
    F -->|read-only| T[Tuxbot]
    F -->|read-only| S[Secbot]
    F -->|read-only| L[Langbot]
    U <-->|sessions| M
    U <-->|sessions| T
    U <-->|sessions| S
    U <-->|sessions| L
    M -->|report| P
    T -->|report| P
    S -->|report| P
    L -->|report| P
```

1. **First interaction**: the Profile Bot asks questions, one subject at a time, and assigns a starting level.
2. **Session**: the teacher reads the profile, then runs a goal, a short explanation, exercises, a correction and a takeaway.
3. **Verification by exercise**: every session ends with an unaided exercise. Its result validates the learning or not. Never validate on an explanation alone.
4. **Report**: the teacher sends the Profile Bot a short summary (topics covered, exercise and result, decision validated / to review, recurring mistakes, difficulties, estimated level, next step).
5. **Update**: the Profile Bot confirms level changes and rewrites the profile. Only it writes to the profile.

## Repository contents

- `ARCHITECTURE.md`: roles, rules and design choices.
- `prompts/`: generic prompts for the 5 bots (Profile, Mathbot, Tuxbot, Secbot, Langbot), plus the Builder Bot one.
- `bots/`: one shareable template per bot (`PROMPT.md`, role and getting-started skills, installation `README.md`), including the optional **Builder Bot** that generates your own teacher.
- `examples/guitarbot/`: a guitar teacher generated in simulation by the Builder Bot.
- `shared/`: shared profile format (`profile.example.json`, `profile.example.md`) and a `reports/` folder with an example report.
- `CONTRIBUTING.md`: how to propose an improvement.

## Set it up yourself

The concept is platform-independent: you only need several LLM agents that share a folder and can message each other.

1. Create 5 agents named "Grok Bot Academy - Profile Bot", "- Mathbot", "- Tuxbot", "- Secbot" and "- Langbot", following the `README.md` in each folder of `bots/` (prompt + 2 skills).
2. Set up a shared folder readable by all (for example `academy/`), with a copy of `shared/` (rename `profile.example.*` to `profile.md` and `profile.json`).
3. Give only the Profile Bot write access to `profile.md` and `profile.json`; teachers may only create files in `reports/`.
4. Let teachers message the Profile Bot (inter-agent messaging, a queue, a webhook, or simply a file dropped in `reports/`, named `YYYY-MM-DD-<bot>-<topic>.md`, that it reads). Degraded mode: if a bot or messaging is missing, the others carry on and the report is given to the learner.
5. Start with the Profile Bot's diagnostic, then run a session with a teacher.

## Create your own teacher

The optional **Builder Bot** interviews you (subject, audience, level, language, tone, validation exercises), then generates a teacher prompt and two skills compatible with the Profile Bot. See `bots/builder-bot/` and the example `examples/guitarbot/`.

## Key design choices

- **Single writer** for the profile, to avoid contradictions.
- **Verification by exercise**: a level only goes up after a successful unaided exercise.
- **No invention**: a level or result exists only if it comes from a real answer or report.
- **Free models first**: the concept is designed to run on free quotas.
- **Defensive security**: the cybersecurity teacher teaches offensive practice only on legal environments (labs, CTFs, test machines). Never scan or attack third-party systems.
- **Sandbox** for command exercises (Linux), never on the learner's own machine.

## Ideas for improvement

- Finer level scale and sub-skills per domain.
- Spaced repetition: the Profile Bot schedules reviews.
- New teachers (code, finance, sciences): the loop is the same.
- Automatic quality evaluation of corrections.
- A light web interface on top of the shared profile.

## License

MIT. See `LICENSE`.
