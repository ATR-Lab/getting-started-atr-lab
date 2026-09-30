# AGENTS.md: getting-started-atr-lab

This repository is the onboarding handbook for new members of the Advanced Telerobotics Research Lab (Department of Computer Science, Kent State University): research standards, LaTeX paper templates for ACM and IEEE venues, the lab's tech stack by layer, the lab's rules and conduct, and one page per piece of lab hardware. It is read by new students and by coding agents such as Claude Code and Codex. It is **not** the lab's public profile (that is `ATR-Lab/about`), not a coding style guide (`ATR-Lab/dev-guidelines`) and not a ROS 2 tutorial (`ATR-Lab/all-things-ros2`). It is plain Markdown plus two LaTeX templates; there is no application code.

## Repo map

| Path | What it is |
| --- | --- |
| `README.md` | Landing page: banner, "Start here" card grid, first-week checklist, repo map, license |
| `AGENTS.md` | This file: the agent index |
| `CLAUDE.md` | One line, `@AGENTS.md`, so Claude Code reads this file |
| `LICENSE` | MIT License, 2017-2026 |
| `.gitignore` | OS and editor files, LaTeX build output, PDFs under `templates/` |
| `.markdownlint.jsonc` | markdownlint rules shared by the lab's docs repos |
| `.lycheeignore` | Sites that block automated link checkers (ACM, Autodesk, IEEE, Meta); check those links by hand |
| `.github/workflows/docs.yml` | CI: markdownlint on every push and pull request; lychee checks local links on pull requests and every link after merge and weekly |
| `.github/assets/header.png`, `social-preview.png` | Banner and GitHub social preview (don't regenerate) |
| `.github/assets/icons/` | 96 px navy icon badges used in the README card grid and the hardware index |
| `research/README.md` | Index of the research pages |
| `research/standards.md` | Research integrity, IRB and CITI, authorship (ACM, IEEE, CRediT), Zotero, data management, reproducibility, preprints and embargoes, generative AI policies, affiliation line, funding acknowledgments |
| `research/writing-papers.md` | LaTeX basics, IEEEtran vs acmart, the venue table (HRI, CHI, ICRA, IROS, RO-MAN, RA-L, IEEE VR, CoRL, RSS, Humanoids), Overleaf, figures and video, camera-ready and copyright forms |
| `research/publishing-checklist.md` | Pre-submission checklist |
| `templates/latex/README.md` | Index of the LaTeX templates and how to build them |
| `templates/latex/ieee-conference/` | `main.tex`, `references.bib`, `README.md`: IEEEtran conference skeleton with an anonymous switch |
| `templates/latex/acm-sigconf/` | `main.tex`, `references.bib`, `README.md`: acmart sigconf skeleton with review and anonymous options, CCS concepts and keywords |
| `tech-stack/README.md` | The stack by layer: Mermaid diagram, layer table, versions at a glance |
| `tech-stack/ros2.md` | Pointer to `ATR-Lab/all-things-ros2` and what to read first |
| `tech-stack/isaac-sim.md` | NVIDIA Isaac Sim and Isaac Lab: versions, requirements, install, ROS 2 bridge, robot assets |
| `tech-stack/mujoco.md` | MuJoCo, MJX, MuJoCo Warp, Menagerie models of lab robots |
| `tech-stack/gazebo.md` | Gazebo releases, ROS 2 pairing table, `ros_gz` |
| `tech-stack/lerobot.md` | Hugging Face LeRobot: install, workflow, datasets and privacy, policies |
| `tech-stack/autodesk.md` | Autodesk Fusion and Inventor: education licenses, export to PreForm, CAD to URDF |
| `tech-stack/unity.md` | Unity 6 for XR teleoperation, Meta Quest setup, ROS 2 connection options |
| `tech-stack/docker.md` | Docker Engine vs Desktop, NVIDIA Container Toolkit, GUI apps, Compose, ROSEnv |
| `tech-stack/claude-code.md` | Claude Code: install, AGENTS.md and CLAUDE.md, permission modes, lab rules for AI coding agents |
| `tech-stack/codex.md` | Codex CLI: install, AGENTS.md, sandbox and approvals, lab rules for AI coding agents |
| `lab-rules/README.md` | Index of the lab rules |
| `lab-rules/code-of-conduct.md` | Code of conduct (draft until the director approves), extending Kent State's Code of Student Conduct |
| `lab-rules/safety.md` | Safety rules: emergencies, injuries, benches and soldering, robots in motion, batteries, resin, lasers, attire |
| `lab-rules/best-practices.md` | Everyday habits: Slack, calendar, `[ATR]` email tag, checkout, meetings, shared GPUs, storage, leaving the lab |
| `hardware/README.md` | Hardware index and inventory table (maintained separately; see its own open items) |
| `hardware/unitree-go2.md` | Unitree Go2 quadruped |
| `hardware/booster-k1.md` | Booster K1 humanoid |
| `hardware/openmanipulator-x.md` | ROBOTIS OpenManipulator-X arm |
| `hardware/lerobot-so-101.md` | LeRobot SO-101 arm |
| `hardware/jetson-agx-thor.md` | NVIDIA Jetson AGX Thor |
| `hardware/raspberry-pi-5.md` | Raspberry Pi 5 |
| `hardware/rosmaster-x3.md` | Yahboom ROSMASTER X3 |
| `hardware/formlabs-form-3.md` | Formlabs Form 3 resin printer |

## Sources of truth

- **Lab facts** (names, director, contacts, handles, projects, platforms, achievements and their exact wording, the "never print" list) come only from `references/brand-foundation.md` in the ATR Lab design skill ([ATR-Lab/atr-lab-design-skill](https://github.com/ATR-Lab/atr-lab-design-skill)), or from the lab lead.
- **Kent State rules** come from kent.edu pages and the Policy Register (kent.edu/policyreg), linked next to each fact.
- **Publisher and venue rules** come from acm.org, ieee.org, ieee-ras.org, ctan.org and each venue's current call for papers.
- **Technical facts** (versions, requirements, commands, EOL dates) come from the vendor's or project's own docs, GitHub releases or package index, checked on the date in the page footer, with the source linked next to the fact.
- **Never invent names, rooms, phone lines, results, versions, page limits or dates.** Anything only the lab can supply stays a `[bracketed placeholder]` and is listed under [Open items](#open-items). If you cannot verify a technical fact, say so in the text ("check the current call for papers") or leave it out.
- Third-party tools are named as facts, never as endorsements by the lab or Kent State.

## Writing rules

- **Voice:** precise, curious, hands-on, welcoming, grounded. Write for a smart first-year student; define jargon on first use.
- **Kent State style:** sentence-case headings; no Oxford comma in a simple series; "and", not "&"; one through nine spelled out, 10 and up as numerals, numerals with units and versions; dates like "Sept. 30, 2026"; times like "9 a.m."; phones like "330-672-9980".
- **Names:** "Advanced Telerobotics Research Lab" on first reference, then "the lab"; "ATR Lab" only in display type and always with Kent State nearby; never "ATR" alone or "KSU" in running copy. Director: "Jong-Hoon Kim, associate professor of computer science". Never print the nonexistent social handle, the director's office room or phone as the lab's, or the college's former name: the exact strings are on the "Never print" list in `brand-foundation.md` §11, and `brand_check.py` flags them.
- **Words:** ROS 2 (never "ROS2" in prose), teleoperation, telepresence, tele-embodiment, Physical AI, human-robot interaction, open-source (adjective), real-world (adjective), advisor, leader-follower. Robots are "it".
- **Cut hype:** cutting-edge, state-of-the-art, revolutionary, groundbreaking, world-class, innovative, novel, leverage, utilize, seamless, robust, holistic, transformative, pivotal, delve, furthermore, moreover.
- **AI and robots:** label every robot demo as teleoperated, autonomous, semi-autonomous or scripted, with playback speed; concrete verbs, no "understands" or "thinks".
- **Page shape:** `# Title`, a "> **Read this when**" line, two to four sentences, `## Contents` when there are five or more sections, then sections, `## Related`, and the `<sub>Last reviewed ...</sub>` footer. README, AGENTS and CLAUDE files are exempt.
- **Commands:** fenced blocks tagged `bash` (or the right language), one command per line, no `$` prompts, with the OS and version stated.
- **Callouts:** GitHub alerts (`> [!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]`, `[!CAUTION]`), sparingly; safety rules in WARNING or CAUTION.
- **Mermaid:** start every diagram with the brand theme line used in `tech-stack/README.md`. When edges carry labels, add `linkStyle default color:#1B2533` at the end of the diagram so the labels stay readable. Don't set a font in the theme line: a custom `fontFamily` makes node text clip.
- **Files and links:** lowercase kebab-case names; relative links inside this repo; full `https://github.com/ATR-Lab/<repo>/blob/<branch>/<path>` links across repos (`master` for dev-guidelines, about and this repo; `main` for all-things-ros2 and .github). Link only public ATR-Lab repositories.
- **Repo-specific:** the code of conduct stays marked "Draft until the director approves" until he does. Don't commit PDFs. Keep the anchors other pages link to (`#safety` on hardware pages, `#human-subjects-research`, `#data-management`, `#robots-in-motion` and the rest) stable, or update every link.

## How to check your work

Run from the repository root:

```bash
# 1. Brand, facts and Kent State style (exit 0 = no errors); README files must be named explicitly
PYTHONDONTWRITEBYTECODE=1 ~/.claude/skills/atr-lab-design/.venv/bin/python ~/.claude/skills/atr-lab-design/scripts/brand_check.py $(git ls-files --others --cached --exclude-standard '*.md')

# 2. Markdown structure
npx --yes markdownlint-cli2 "**/*.md"

# 3. Hype words and "ROS2" in prose (review each hit; slugs, URLs and code are fine)
grep -rnE -i "cutting-edge|state-of-the-art|revolutionary|groundbreaking|world-class|innovative|novel|leverag|utiliz|seamless|robust|holistic|transformative|pivotal|delve|furthermore|moreover|ROS2" --include='*.md' .

# 4. Both LaTeX templates compile (tectonic downloads IEEEtran and acmart on first use)
(cd templates/latex/ieee-conference && tectonic main.tex)
(cd templates/latex/acm-sigconf && tectonic main.tex)

# 5. Links (the same check CI runs; it skips the domains in .lycheeignore)
lychee --no-progress --accept 200,206,429 "**/*.md"
```

Brand-check warnings for intentional `[placeholders]` are expected; fix every other warning or explain it in the pull request. Delete the compiled PDFs before you commit (they are ignored by Git anyway).

## Open items

Every placeholder in this repository, by file, with who can fill it. Agents must not fill these by guessing.

**Hardware pages:** see [hardware/README.md#open-items](hardware/README.md#open-items).

| File | Placeholder | Who fills it |
| --- | --- | --- |
| `README.md` | `[who sends GitHub organization invitations]`, `[Slack workspace]`, `[main lab channel]`, `[lab calendar]` | Lab manager |
| `README.md` | `[lab safety contact]` | Director |
| `README.md` | `[mentor name]` | Director, per new member |
| `lab-rules/code-of-conduct.md` | Approval of the whole draft | Director (Jong-Hoon Kim) |
| `lab-rules/code-of-conduct.md` | `[designated break area]`, `[lab door rules: ...]`, `[visitor rules: ...]`, `[after-hours rules, ...]`, `[lab policy on personal use of equipment and printers]` | Director and lab manager |
| `lab-rules/code-of-conduct.md` | `[purchase request procedure]`, `[reimbursement procedure]` | Director, with the department office |
| `lab-rules/code-of-conduct.md` | `[lab social media administrators]`, `[lab password manager]`, `[lab manager name]`, `[lab contact for concerns]` | Director |
| `lab-rules/code-of-conduct.md` | `[Department of Computer Science chair]` | Lab manager (from the department website; name the role if the person changes) |
| `lab-rules/code-of-conduct.md` | `[where students check assistantship and employment terms]` | Lab manager, with the Graduate College |
| `lab-rules/safety.md` | `[lab safety contact]`, `[how sign-offs are recorded]`, `[how the lab marks a robot test area]` | Director |
| `lab-rules/safety.md` | `[first aid kit location]`, `[fire extinguisher location]`, `[eyewash location]`, `[evacuation route and assembly point]` | Lab safety contact (walk the lab and building) |
| `lab-rules/safety.md` | `[battery charging location]`, `[battery storage location]`, `[SDS location]`, `[lab resin and IPA waste procedure]` | Lab safety contact, with Kent State EHS |
| `lab-rules/best-practices.md` | `[Slack workspace]`, `[main lab channel]`, `[lab calendar tool]`, `[equipment checkout log or system]`, `[machine administrator]`, `[GPU booking method]` | Lab manager |
| `lab-rules/best-practices.md` | `[day, time and place of the lab meeting]`, `[where: ...]`, `[day and time]`, `[update format, ...]`, `[how often and how to book]` | Director |
| `lab-rules/best-practices.md` | `[shared data location]`, `[Overleaf or shared drive]`, `[CAD file location]`, `[private or public by default: confirm]` | Director and lab manager |
| `lab-rules/best-practices.md` | `[ATR]` | Not a placeholder: the lab's email subject tag |
| `research/standards.md` | `[lab authorship practice]`, `[lab Zotero group]`, `[shared data location]` | Director |
| `research/standards.md` | `[Grant No.]` | PI, per paper |
| `research/writing-papers.md` | `[paper repository naming convention]`, `[lab Overleaf plan, if any]` | Director |
| `research/writing-papers.md` | `[ask Kent State University Libraries whether Kent State is an ACM Open institution]` | Lab manager, with Kent State University Libraries |
| `research/publishing-checklist.md` | `[how many days before the deadline the director needs the draft]`, `[where the lab tracks submissions]` | Director |
| `templates/latex/*/main.tex` | Author names, emails, ORCID iDs, `[Sponsor]`, `[Grant No.]`, venue metadata | Each paper's authors and the PI |
| `tech-stack/isaac-sim.md` | `[list of lab workstations with RTX GPUs]`, `[GPU booking method]`, `[shared asset location]` | Lab manager |
| `tech-stack/mujoco.md` | `[location of lab MuJoCo models]` | Lab manager |
| `tech-stack/lerobot.md` | `[lab Hugging Face organization]` | Director |
| `tech-stack/autodesk.md` | `[Fusion or Inventor: lab decision]`, `[CAD file location]` | Director |
| `tech-stack/unity.md` | `[which Unity license lab machines use]`, `[Meta Quest headsets and location]` | Lab manager |
| `tech-stack/claude-code.md`, `tech-stack/codex.md` | Which AI coding agent accounts the lab provides, and which lab work they may be used for under Kent State's AI guidance | Director, with Kent State Information Security (<security@kent.edu>) |
| `tech-stack/docker.md` | `[lab manager name]` (Docker Desktop license question), `[machine administrator]` | Lab manager |

Lab decisions these pages raise (not placeholders, but open): whether the lab needs a paid Docker Desktop plan under Docker's public-sector terms (`tech-stack/docker.md`); which lab repositories AI coding agents may be used on, given Kent State's AI Hub guidance (`tech-stack/claude-code.md`, `tech-stack/codex.md`).

## Related repos

| Repo | The question it answers |
| --- | --- |
| [ATR-Lab/.github](https://github.com/ATR-Lab/.github) | What is in the ATR-Lab organization, and which repo do I open? |
| [ATR-Lab/about](https://github.com/ATR-Lab/about) | Who is the lab, what does it work on, and what can we say about it? |
| [ATR-Lab/getting-started-atr-lab](https://github.com/ATR-Lab/getting-started-atr-lab) | I just joined: what are the rules, standards, tools and robots? (this repo) |
| [ATR-Lab/dev-guidelines](https://github.com/ATR-Lab/dev-guidelines) | How do we write, format, review and version code? |
| [ATR-Lab/all-things-ros2](https://github.com/ATR-Lab/all-things-ros2) | How do I install, use and debug ROS 2 on lab robots? |
