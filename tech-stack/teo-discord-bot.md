# Teo, the lab's Discord bot

> **Read this when** you join the lab's Discord server, want help from Teo, or need to know what happens to what you send it.

Teo (short for "teleoperator") is the assistant bot on the lab's [Discord server](https://discord.gg/NvwsANWEuw). It answers questions about robotics, code, ROS 2, lab safety and the lab's documentation. It writes its answers with Anthropic's Claude and reads this handbook, the [about](https://github.com/ATR-Lab/about) repo and the [dev guidelines](https://github.com/ATR-Lab/dev-guidelines) before it answers questions about the lab. Teo is also the lab's mascot: its avatar and the server's `:teo_*:` emoji show it.

> [!IMPORTANT]
> **Teo is an AI tool.** It sends your message, and any file you attach, to Anthropic's API to write an answer, so the lab's rule for AI tools applies: public or non-sensitive work only ([Claude Code](claude-code.md)). Never give it passwords, keys, tokens, study data, participants' information or unpublished results.

## Contents

- [Ask Teo](#ask-teo)
- [What Teo can do](#what-teo-can-do)
- [What Teo won't do](#what-teo-wont-do)
- [Research project channels](#research-project-channels)
- [Limits and privacy](#limits-and-privacy)
- [Improve Teo](#improve-teo)
- [Related](#related)

## Ask Teo

| How | What happens |
| --- | --- |
| Mention `@Teo`, or reply to one of its messages | Teo answers in that channel. It reads the reply chain and the last 12 messages in the channel for context |
| `/ask` | Ask a question directly. Set `private` to `True` for an answer only you see, and use `file` to attach a file |
| A new post in **#❓・help-desk** | Teo writes the first reply |
| A direct message | Teo points you back to the server; it doesn't answer in DMs |
| `/about-teo` | What Teo is and how it handles your messages |

Good questions get good answers: say what you are trying to do, what you tried and what happened, and paste the exact error or attach the log.

## What Teo can do

- **Answer questions** about robotics, code, ROS 2 and the lab's rules and how-tos, linking the lab page it used. Outside the research project channels it can also search the web, and it links official docs when it does.
- **Read your files.** Text, code, logs, images and PDFs it reads directly. Other formats (Office files, archives, NumPy arrays, ROS bags, very large logs) it opens with code in a temporary sandbox. Up to six files, 25 MB each; files in a message you reply to count too.
- **Remind you.** "@Teo remind me to submit the HRI paper next Friday at 5 p.m." sets a reminder in lab time (Eastern), and Teo pings you in the same channel when it's due. It understands Anywhere on Earth (AoE) deadlines. Reminders are only for the person asking: up to 25 at a time, up to a year ahead. `/reminders` lists yours and `/reminder-cancel` removes one.
- **Create server events**, for members with Discord's event permission or one of the lab roles that allow it: "@Teo create an event: Lab social, Nov. 6, 4-6 p.m., Student Center Ballroom." It asks for the place or time instead of guessing, and it can list upcoming events.

## What Teo won't do

- **Graded work.** For coursework Teo explains the concept, points to the bug or asks a guiding question, but it won't write a full graded solution. Kent State's academic integrity rules and your instructor's policy apply.
- **Move a robot.** Teo only talks. Its advice for robot code follows the [safety rules](../lab-rules/safety.md): simulation first, and a person watching the robot with the emergency stop in reach.
- **Speak for the lab.** It makes no commitments about admissions, positions, funding, grades, equipment or building access, and it points reporters to the director.
- **Make up lab facts.** When the lab hasn't confirmed something, Teo says so and tells you where to ask.
- **Handle emergencies.** For a fire, an injury or smoke from a battery, call 911 first, then tell the [lab safety contact](../lab-rules/safety.md).

## Research project channels

In the channels under 🤖 Research projects, Teo works in question-only mode: it sees only the message that mentions it and its own earlier replies, not the rest of the conversation, and web search is off. Put the context it needs in your message, in general terms. Never paste unpublished results, datasets, participants' information or a collaborator's material there.

## Limits and privacy

- **Limits:** 20 questions per person per hour and 500 a day for the whole server.
- **What is kept:** the bot doesn't store your message text; its logs keep token counts and a scrambled (hashed) user ID only. Files it opens in the sandbox are deleted after it answers. Reminders are stored until they are sent or cancelled.
- **Young members:** some people on the server are middle and high school students in the lab's programs. Teo keeps those conversations in the server, and so should you (rule 6 of the server rules).

## Improve Teo

Teo's code is in the private repository `ATR-Lab/Teo-Discord-Bot`; ask the lab manager for access. Its persona, rules and lab facts are in `teo/prompt.md`, which holds only facts verified in the [about](https://github.com/ATR-Lab/about) repo. Branch from `main` and open a pull request: merging to `main` deploys to the live bot, so follow the repository's README and the [dev guidelines](https://github.com/ATR-Lab/dev-guidelines).

## Related

- [Claude Code](claude-code.md) and [Codex](codex.md), the lab's AI coding agents
- [Tech stack](README.md)
- [Code of conduct](../lab-rules/code-of-conduct.md) and [safety rules](../lab-rules/safety.md)
- The mascot's design rules: [ATR Lab design skill](https://github.com/ATR-Lab/atr-lab-design-skill)

<sub>Last reviewed: Nov. 5, 2026 · Checked against Teo-Discord-Bot `main` on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/teo-discord-bot.md)</sub>
