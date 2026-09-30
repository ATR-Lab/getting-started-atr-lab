# Best practices

> **Read this when** you are new to the lab, or you want to know the everyday habits that keep a shared space working for everyone.

These are the lab's everyday habits: how we talk to each other, schedule, share machines, store files and leave. They are courtesy rules, not university policy; the binding rules are in the [code of conduct](code-of-conduct.md) and the [safety rules](safety.md). The one thing to remember: the lab is shared, so leave people, machines and benches the way you would want to find them.

## Contents

- [Working alongside other people](#working-alongside-other-people)
- [Communication](#communication)
- [Keep a clean workspace](#keep-a-clean-workspace)
- [Equipment checkout](#equipment-checkout)
- [Meetings and weekly updates](#meetings-and-weekly-updates)
- [Shared machines and GPUs](#shared-machines-and-gpus)
- [File storage and backups](#file-storage-and-backups)
- [Leaving the lab](#leaving-the-lab)
- [Related](#related)

## Working alongside other people

### Be courteous to people who are working

Try not to interrupt someone who looks busy. If it can wait, send a message instead and let them answer when they reach a stopping point.

### Respect people wearing headphones

Someone wearing headphones is usually concentrating and would rather not be disturbed. Keep interruptions to things that matter now, such as safety or a deadline. If you must interrupt, get their attention from the front, not by tapping them from behind.

### Do not move other people's property

If it looks like someone owns or is using something (a laptop, a robot mid-experiment, parts laid out on a bench), do not touch or move it without their permission. A half-built setup can take hours to rebuild, and a robot that looks idle may be powered on.

## Communication

### Be present on Slack

The lab talks on [Slack workspace]. Check it during your lab hours and keep notifications on for direct messages and [main lab channel].

- Message someone who looks busy before walking over to them, so you don't break their focus.
- Ask questions in the channel for the project, not in a direct message, so the answer helps the next person too.
- Set your status when you are away for more than a day.

### Use formal calendar invitations

When you set up a meeting, send a calendar invitation from [lab calendar tool] to everyone who should attend, with the place or video link in the invitation. A message that says "let's meet Tuesday" is not a meeting until it is on the calendar.

### Use the `[ATR]` subject tag in lab email

Start the subject line of internal lab email with `[ATR]` so people can filter it. For example:

```text
[ATR] Who can help clean the lab on Friday?
```

The tag is an internal filter label. In email to people outside the lab, write the lab's full name, Advanced Telerobotics Research Lab, in the message itself.

## Keep a clean workspace

Clean up the area you work in, while you work and before you leave. A clean bench:

- prevents lost or misplaced parts and tools
- shows the lab well to visitors
- keeps you from disturbing the people around you
- is safer: loose cables, solder scraps and batteries cause accidents (see [safety rules](safety.md#cleanliness))

Put tools back where they belong, label anything you leave overnight with your name, the date and the project, and throw away scraps.

## Equipment checkout

Robots, sensors, laptops and tools leave their shelf only through the checkout process:

1. Check that you are trained and allowed to use the device (ask [lab manager name]).
2. Record the checkout in [equipment checkout log or system]: device, your name, date, where it will be and when it comes back.
3. Return it charged, complete (cables, batteries, controllers) and clean, and record the return.
4. Report anything missing, damaged or not working right away, and tag the device "out of order".

Device-by-device notes, including where each robot lives and who looks after it, are in the [hardware pages](../hardware/README.md).

## Meetings and weekly updates

- **Lab meetings:** [day, time and place of the lab meeting]. Come prepared to give your update.
- **Weekly updates:** send your update to [where: channel, document or email] by [day and time], in this format: [update format, for example "done, next, blocked"].
- **One-on-one meetings** with your advisor: [how often and how to book].
- Bring slides for research updates on the lab's template (ask [lab manager name] for the current one).

## Shared machines and GPUs

Lab workstations and GPU servers are shared. To keep them usable for everyone:

- Book GPU time through [GPU booking method] before you start a long job, and do not start work on a GPU someone else has booked.
- Check what is already running before you start (`nvidia-smi` shows GPU jobs) and name your jobs or containers so people know whose they are.
- Run your work in your own user account and, where you can, in a container ([Docker guide](../tech-stack/docker.md)), so you don't change the machine for everyone else.
- Ask [machine administrator] before installing system-wide packages, drivers or CUDA versions, or before upgrading the operating system.
- Clean up: delete large datasets, checkpoints and Docker images you no longer need, and keep your data in [shared data location], not the system disk.
- Log out or lock the screen when you leave. Never leave a machine signed in to your Kent State account.

## File storage and backups

| What | Where | Notes |
| --- | --- | --- |
| Code | The lab's GitHub organization, [ATR-Lab](https://github.com/ATR-Lab) | Ask [lab manager name] to create a repository. New repositories are [private or public by default: confirm]. Follow the [dev guidelines](https://github.com/ATR-Lab/dev-guidelines) |
| Papers and figures | [Overleaf or shared drive] | One project per paper; see [writing papers](../research/writing-papers.md) |
| Datasets, recordings and models | [shared data location] | Record where each dataset came from and its license |
| Human-subjects study data | Only where the IRB protocol says | See [data management](../research/standards.md#data-management) |
| CAD and fabrication files | [CAD file location] | See [Autodesk Fusion and Inventor](../tech-stack/autodesk.md) |

Back up anything you cannot recreate. A common rule is three copies, on two kinds of storage, with one copy somewhere else. A laptop's disk alone is not a backup, and never store passwords, keys or identifiable study data in a GitHub repository.

## Leaving the lab

When you graduate, finish a project or leave the lab, hand everything over before your last day:

- [ ] Return every device you checked out, and record the returns.
- [ ] Return keys, access cards and anything else issued to you ([lab manager name]).
- [ ] Push all code to the lab's GitHub organization, with a README that says how to build and run it.
- [ ] Move datasets, recordings, models and CAD files to [shared data location], with a short note on what each one is.
- [ ] Hand study data over as the IRB protocol requires, and tell the PI.
- [ ] Write a short handover note for whoever continues the work: what works, what doesn't and where things are.
- [ ] Clear your bench and shelf space.
- [ ] Remove your files and accounts from shared machines, and ask [machine administrator] to close lab accounts.
- [ ] Tell [lab manager name] where you can be reached, if you would like to stay in touch.

## Related

- [Lab rules](README.md): the index of this folder
- [Code of conduct](code-of-conduct.md)
- [Safety rules](safety.md)
- [Hardware](../hardware/README.md): device pages and checkout notes
- [Tech stack](../tech-stack/README.md)
- [Dev guidelines](https://github.com/ATR-Lab/dev-guidelines): code style, Git and reviews

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/lab-rules/best-practices.md)</sub>
