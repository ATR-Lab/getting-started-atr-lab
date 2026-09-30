# Codex

> **Read this when** you want to install OpenAI's Codex CLI, use it on a lab repository, or check the lab's rules for AI coding agents.

Codex is OpenAI's coding agent. The Codex CLI runs in your terminal, reads your repository, edits files and runs commands inside a sandbox, asking before it goes outside it; the same agent is also available as an editor extension and as Codex cloud. Codex reads a repository's `AGENTS.md` before it starts work, and lab repositories keep their agent instructions there, so Codex and [Claude Code](claude-code.md) follow the same rules. The one thing to remember: you are the author of everything the agent writes, so read every diff before you commit it, and never give it passwords, keys or identifiable study data.

> [!IMPORTANT]
> **Kent State's guidance comes first.** Kent State's [AI Hub](https://www.kent.edu/ai) lists Microsoft Copilot, Google Gemini and NotebookLM, and Adobe Firefly as sanctioned for university use, and says tools outside that list, naming Claude and ChatGPT, "may be used for personal/non-sensitive work only, do not input university data." Until the director confirms with Kent State Information Security (<security@kent.edu>) which lab work Codex may be used for, use it only on public or non-sensitive code, such as the lab's open-source repositories, and never on student records, study data or other university data.

## Contents

- [Install](#install)
- [First run](#first-run)
- [AGENTS.md](#agentsmd)
- [Sandbox and approvals](#sandbox-and-approvals)
- [Lab rules for AI coding agents](#lab-rules-for-ai-coding-agents)
- [Related](#related)

## Install

From the [Codex CLI docs](https://learn.chatgpt.com/docs/codex/cli) and the [openai/codex README](https://github.com/openai/codex#readme) (checked Sept. 30, 2026; latest release 0.159.2, Apache 2.0 license).

macOS and Linux:

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Windows PowerShell (Codex runs natively on Windows with its own sandbox, or inside WSL):

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

With a package manager instead:

```bash
# npm
npm install -g @openai/codex
# macOS with Homebrew
brew install --cask codex
```

## First run

Open a terminal in the repository you want to work on and start Codex:

```bash
cd ~/src/[repository]
codex
```

Choose **Sign in with ChatGPT** to use a ChatGPT plan that includes Codex, or sign in with an OpenAI API key ([authentication docs](https://learn.chatgpt.com/docs/auth)):

```bash
printenv OPENAI_API_KEY | codex login --with-api-key
```

The lab's arrangement for accounts is [which OpenAI accounts the lab provides, if any: ask lab manager name]. Never paste an API key into a prompt or commit it; keep it in an environment variable.

## AGENTS.md

"Codex reads AGENTS.md files before doing any work" ([AGENTS.md docs](https://learn.chatgpt.com/docs/agent-configuration/agents-md)). It reads, in order:

1. Your personal file in `~/.codex/AGENTS.md` (or `AGENTS.override.md`), for preferences that apply to every project.
2. The `AGENTS.md` at the repository root, then any `AGENTS.md` in the folders between the root and your current folder. Files closer to where you work come later and take precedence.

The combined instructions are capped at 32 KiB by default. In a repository with no `AGENTS.md`, the `/init` command drafts one; for a lab repository, follow the documentation standards in the [dev guidelines](https://github.com/ATR-Lab/dev-guidelines). [AGENTS.md](https://agents.md/) is an open format, now stewarded by the Agentic AI Foundation under the Linux Foundation, and other agents read it too.

## Sandbox and approvals

By default Codex can read files, edit files and run commands inside your workspace, with network access off, and asks before anything outside that boundary ([approvals and security](https://learn.chatgpt.com/docs/agent-approvals-security)). Switch during a session with `/permissions`.

| Setting | What it allows | Use it in the lab |
| --- | --- | --- |
| `--sandbox read-only --ask-for-approval on-request` | Reads and runs read-only commands; asks for anything else | To explore unfamiliar code, and on any computer connected to a robot |
| `--sandbox workspace-write --ask-for-approval on-request` (the default) | Edits and commands inside the workspace, no network | Normal work on your own branch |
| `--dangerously-bypass-approvals-and-sandbox` | Everything, with no sandbox and no approvals; OpenAI marks it "not recommended" | Only inside a disposable container or virtual machine |

## Lab rules for AI coding agents

These rules apply to Codex, [Claude Code](claude-code.md) and every other coding agent. The full policy, with examples, is in the dev guidelines page on [AI-assisted development](https://github.com/ATR-Lab/dev-guidelines/blob/master/docs/ai-assisted-development.md).

1. **Follow Kent State's AI guidance** (above): no university data, student records or study data in any tool Kent State has not sanctioned.
2. **You own the result.** Read every diff before you commit it and run the tests. Be ready to explain any line in review.
3. **Never paste secrets.** No passwords, Kent State credentials, API keys, tokens or SSH keys in a prompt, a file the agent reads or a commit. Keep them in environment variables or a secrets manager, and never commit `.env` files.
4. **Never give an agent identifiable study data**: names, faces, voices, emails or anything else that identifies a study participant, or any data the IRB protocol restricts. Test with synthetic or public sample data instead.
5. **No agent drives a robot unattended.** An agent may write and run code in simulation. A command that makes real hardware move runs only with a person watching, within reach of the emergency stop ([robots in motion](../lab-rules/safety.md#robots-in-motion)).
6. **Keep the sandbox and approvals on** on shared lab machines and on any computer connected to a robot. Bypass them only in a throwaway container.
7. **Disclose AI use** where it matters: in the pull request description, and in papers as the venue's policy requires ([generative AI in research and writing](../research/standards.md#generative-ai-in-research-and-writing)).
8. **Check licenses.** Don't accept code that looks copied from a project whose license the repository can't take.

Codex is named here because lab members use it; this page describes the tool and is not an endorsement by the lab or Kent State University.

## Related

- [Claude Code](claude-code.md)
- [Tech stack](README.md)
- [AI-assisted development](https://github.com/ATR-Lab/dev-guidelines/blob/master/docs/ai-assisted-development.md) in the dev guidelines
- [Codex documentation](https://learn.chatgpt.com/docs/codex/cli)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/codex.md)</sub>
