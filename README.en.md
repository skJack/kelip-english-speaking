# kelip-english-speaking

[简体中文](README.md) | **English**

Practise spoken English with AI, and turn every day into an English journal entry along the way — two birds with one stone.

This is a skill: hand the repo to your AI agent and it sets the whole workflow up for you. The core is two prompts; if you don't want a system, just copy them.

```
Start prompt ─▶ ChatGPT voice (GPT Live), four parts ─▶ End prompt ─▶ one Markdown journal entry
                                                                     │ send it to your agent: "save it"
                                                                     ▼
       filed by date · new expressions deduplicated into a word bank · review cards during the day · one evening reminder
```

## The two prompts

| | Where to paste | What it does |
|---|---|---|
| [Start prompt](prompts/start-prompt.md) | A new ChatGPT chat every day, then turn on voice | Makes it your speaking coach: the same four parts every day (what I did / a daily check-in / my biggest progress / my reflection). It waits until you finish a whole part, polishes the whole answer, lets you say it again in your own words, and then points out only one or two things |
| [End prompt](prompts/end-prompt.md) | After you exit voice mode, **in the same chat** | Turns the conversation into a Markdown journal: the four polished parts, a correction table, the words and patterns you genuinely learned, and a speaking rating |

Design choices, kept after months of daily use:

- **No interruptions while you speak.** Feedback comes after a whole part, so you keep talking.
- **Polish the whole part, then retell it.** You learn a connected way of saying it, not scattered one-line fixes, and you produce it right away.
- **Only one or two corrections.** Ten at once means none stick.
- **No interview.** It doesn't keep asking follow-up questions.
- **Ask for help anytime**, in your own language ("How do I say…?"), then carry on.
- **Nothing invented.** Every line of the journal comes from what you said; topics you skipped are marked "Not discussed".
- **Only genuinely new language** goes into the vocabulary table, with its preposition or pattern (`be proud of`, not `proud`).

Part 2 defaults to a health check-in (food, drinks, exercise, sleep). Swap it for anything you want to track daily, such as study or music practice: see [references/customize.md](references/customize.md). The default prompts give explanations in Chinese; the same file shows how to switch to your own language.

## Two ways to use it

**Just the prompts**: copy the code blocks from the two files above. Every day: new chat → paste the start prompt → speak the four parts in voice mode → exit voice → paste the end prompt in the same chat → save the Markdown it produces.

**Let an agent build the whole thing**: no idea how to install a skill? Just send this GitHub link to your agent and let it install the skill itself, then say "help me set up an English speaking practice system". You can send both at once:

```
Install this skill for me: https://github.com/skJack/kelip-english-speaking
Then help me set up an English speaking practice system.
```

It asks a few questions in one go (where to keep the workspace, morning or evening practice, what to track in part 2, when to send review cards…), then:

- writes your own two prompts from your answers;
- creates a workspace: a journal folder, a word bank, and an `AGENTS.md` with every rule, so any agent can take over later;
- schedules a review card every 2 hours during the day (3 items each), and a check at 18:00 that reminds you once if yesterday's journal is missing.

After each session, send the end prompt's output to the agent and say "save it": the entry is filed by date, new expressions are deduplicated into the bank, and you get today's rating and what you learned.

Review cards ask first and answer below. Reply with your own sentences; the agent corrects them and schedules the next review at 1 → 3 → 7 → 14 → 30 days, or tomorrow if you missed it.

## Install

Easiest: send this repo's link to your agent and say "install this skill for me"; it will follow the steps below.

**Claude Code**:

```bash
git clone https://github.com/skJack/kelip-english-speaking.git ~/.claude/skills/kelip-english-speaking
```

Then say "help me set up an English speaking practice system".

**Codex / Cursor / other agents**: clone the repo and ask the agent to read `SKILL.md` and follow it. Agents that read `AGENTS.md` automatically need nothing else.

**A cloud personal agent** (I use a bot in Grok Bot): send it the repo URL and ask it to read `SKILL.md` and set things up in its cloud workspace. Review cards and reminders keep coming even when your laptop is closed.

No dependencies.

## Privacy

The repo contains only the workflow and the prompts — **no one's journal**. Your entries, word bank and check-in data stay in your own workspace; its `.gitignore` excludes all of them, and the agent is told never to send them anywhere public. If you track health, the personal context you give the coach stays in your own copy of the prompts.

## Files

| Path | What it is |
|---|---|
| `SKILL.md` | For the agent: first-time setup and how to route everyday requests |
| `AGENTS.md` | One-page pointer for agents that read it automatically |
| `prompts/start-prompt.md` | Start prompt + what each block does |
| `prompts/end-prompt.md` | End prompt + output format |
| `references/customize.md` | Change the part 2 topic, add personal context, morning practice about yesterday, time zone, native language |
| `references/dashboard.md` | (Optional) a local dashboard: pages and approach |
| `templates/AGENTS.md` | Everyday rules copied into your workspace: saving entries, word bank, review cards, reminders, weekly reviews |
| `templates/language-bank.md` | Empty word bank |
| `templates/speaking.json` | Default settings |
| `templates/gitignore` | The workspace `.gitignore` |
| `examples/journal-example.md` | What a journal entry from the end prompt looks like (made up) |

## Related

- [kelip-slide](https://github.com/skJack/kelip-slide): single-file HTML slides for explainer videos
- [kelip-paper-reading](https://github.com/skJack/kelip-paper-reading): let an AI agent walk you through a paper

## License

MIT
