# Claude Code

> **Read this when** you want to install Claude Code, use it on a lab repository, or check the lab's rules for AI coding agents.

Claude Code is Anthropic's coding agent: it runs in your terminal (and in editors and a desktop app), reads your repository, edits files and runs commands after you approve them. Lab repositories keep their agent instructions in `AGENTS.md`, with a one-line `CLAUDE.md` that imports it, so Claude Code and [Codex](codex.md) follow the same rules. The one thing to remember: you are the author of everything the agent writes, so read every diff before you commit it, and never give it passwords, keys or identifiable study data.

> [!IMPORTANT]
> **Kent State's guidance comes first.** Kent State's [AI Hub](https://www.kent.edu/ai) lists Microsoft Copilot, Google Gemini and NotebookLM, and Adobe Firefly as sanctioned for university use, and says tools outside that list, naming Claude and ChatGPT, "may be used for personal/non-sensitive work only, do not input university data." Until the director confirms with Kent State Information Security (<security@kent.edu>) which lab work Claude Code may be used for, use it only on public or non-sensitive code, such as the lab's open-source repositories, and never on student records, study data or other university data.

## Contents

- [Install](#install)
- [First run](#first-run)
- [AGENTS.md and CLAUDE.md](#agentsmd-and-claudemd)
- [Permission modes](#permission-modes)
- [Lab rules for AI coding agents](#lab-rules-for-ai-coding-agents)
- [Related](#related)

## Install

From Anthropic's [setup guide](https://code.claude.com/docs/en/setup) (checked Sept. 30, 2026). Claude Code runs on macOS 13 or later, Ubuntu 20.04 or later, Debian 10 or later and Windows 10 1809 or later, with at least 4 GB of RAM.

macOS, Linux and WSL (the native installer, which updates itself):

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Windows PowerShell:

```powershell
irm https://claude.ai/install.ps1 | iex
```

macOS with Homebrew (does not update itself; run `brew upgrade claude-code`):

```bash
brew install --cask claude-code
```

The guide also lists WinGet, npm (Node.js 22 or later) and signed apt, dnf and apk repositories. Check the install:

```bash
claude --version
claude doctor
```

## First run

Open a terminal in the repository you want to work on and start a session:

```bash
cd ~/src/[repository]
claude
```

The first run opens a browser to sign in. Claude Code needs a Claude Pro, Max, Team or Enterprise plan or an Anthropic Console (API) account; the free Claude plan does not include it ([setup guide](https://code.claude.com/docs/en/setup#authenticate)). The lab's arrangement for accounts is [which Claude accounts the lab provides, if any: ask lab manager name]. Type `/login` to switch accounts and `/help` for commands.

Good first prompts on a lab repository:

- "Read AGENTS.md and summarize the rules for this repo."
- "Explain how this package is built and tested. Don't change anything yet."

## AGENTS.md and CLAUDE.md

Claude Code reads project instructions from `CLAUDE.md` files at the start of every session. [AGENTS.md](https://agents.md/) is an open format for the same purpose, read by Codex and other agents. Lab repositories keep the instructions in `AGENTS.md` and add a `CLAUDE.md` containing one line:

```text
@AGENTS.md
```

The `@` imports the file, so Claude Code reads exactly what other agents read. Recent versions of Claude Code (v2.1.277 or later) also read `AGENTS.md` directly when a repository has no `CLAUDE.md`, but the import works in every version and setup ([memory docs](https://code.claude.com/docs/en/memory#agentsmd)). Run `/context` in a session to see which instruction files loaded.

In a repository with no instructions yet, `/init` drafts a `CLAUDE.md` from the code. For a lab repository, move what it writes into `AGENTS.md` and follow the documentation standards in the [dev guidelines](https://github.com/ATR-Lab/dev-guidelines).

## Permission modes

A permission mode decides what Claude Code may do without asking you first ([permission modes](https://code.claude.com/docs/en/permission-modes)). Recent versions (v2.1.283 or later) start terminal and VS Code sessions in **auto** mode, where a second model reviews each action instead of you. Press Shift+Tab to change mode during a session, or start in a chosen mode with `claude --permission-mode manual`.

| Mode | What runs without asking | Use it in the lab |
| --- | --- | --- |
| Manual (`default`) | Reads only; asks before edits, commands and network access | On shared lab machines, on any computer connected to a robot, and for sensitive work |
| Plan (`plan`) | Reads; proposes a plan and changes nothing | To explore unfamiliar code or plan a change |
| Accept edits (`acceptEdits`) | Reads, file edits and common file commands | On a branch you will review before merging |
| Auto (`auto`) | Everything, with background safety checks | Your own machine, in a repository with no secrets or study data |
| Bypass permissions (`bypassPermissions`) | Everything | Only inside a disposable container or virtual machine |

To make Manual your own default, add `"permissions": {"defaultMode": "manual"}` to `~/.claude/settings.json`.

## Lab rules for AI coding agents

These rules apply to Claude Code, [Codex](codex.md) and every other coding agent. The full policy, with examples, is in the dev guidelines page on [AI-assisted development](https://github.com/ATR-Lab/dev-guidelines/blob/master/docs/ai-assisted-development.md).

1. **Follow Kent State's AI guidance** (above): no university data, student records or study data in any tool Kent State has not sanctioned.
2. **You own the result.** Read every diff before you commit it and run the tests. Be ready to explain any line in review.
3. **Never paste secrets.** No passwords, Kent State credentials, API keys, tokens or SSH keys in a prompt, a file the agent reads or a commit. Keep them in environment variables or a secrets manager, and never commit `.env` files.
4. **Never give an agent identifiable study data**: names, faces, voices, emails or anything else that identifies a study participant, or any data the IRB protocol restricts. Test with synthetic or public sample data instead.
5. **No agent drives a robot unattended.** An agent may write and run code in simulation. A command that makes real hardware move runs only with a person watching, within reach of the emergency stop ([robots in motion](../lab-rules/safety.md#robots-in-motion)).
6. **Use Manual mode on shared lab machines** and on any computer connected to a robot. Use a bypass mode only in a throwaway container.
7. **Disclose AI use** where it matters: in the pull request description, and in papers as the venue's policy requires ([generative AI in research and writing](../research/standards.md#generative-ai-in-research-and-writing)).
8. **Check licenses.** Don't accept code that looks copied from a project whose license the repository can't take.

Claude Code is named here because lab members use it; this page describes the tool and is not an endorsement by the lab or Kent State University.

## Related

- [Codex](codex.md)
- [Tech stack](README.md)
- [AI-assisted development](https://github.com/ATR-Lab/dev-guidelines/blob/master/docs/ai-assisted-development.md) in the dev guidelines
- [Claude Code documentation](https://code.claude.com/docs/en/overview)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/claude-code.md)</sub>
