# Research standards

> **Read this when** you start a research project or a study with people, decide who is an author, store data, post a preprint, use generative AI in your work, or write an acknowledgment.

The standards every project in the Advanced Telerobotics Research Lab follows, from research integrity to the funding line at the end of a paper. Most of them come from Kent State University policy and from the publishers (ACM and IEEE); the lab adds a few practices of its own, labeled as such. The one thing to remember: **any study with people needs Kent State IRB approval before you recruit anyone**, and most human-robot interaction studies are studies with people.

## Contents

- [Research integrity](#research-integrity)
- [Human-subjects research](#human-subjects-research)
- [Authorship and contribution](#authorship-and-contribution)
- [Citations and Zotero](#citations-and-zotero)
- [Data management](#data-management)
- [Reproducibility and artifacts](#reproducibility-and-artifacts)
- [Preprints, embargoes and news timing](#preprints-embargoes-and-news-timing)
- [Generative AI in research and writing](#generative-ai-in-research-and-writing)
- [The lab affiliation line](#the-lab-affiliation-line)
- [Funding acknowledgments](#funding-acknowledgments)
- [Related](#related)

## Research integrity

- **No fabrication, falsification or plagiarism.** Kent State's [policy on misconduct in research and scholarship](https://www.kent.edu/policyreg/university-policy-regarding-misconduct-research-and-scholarship-0) (Policy 10-07) and its [procedures](https://www.kent.edu/policyreg/administrative-policy-and-procedures-regarding-allegations-and-instances-misconduct-0) (Policy 10-07.1) apply to all lab research. How to raise a concern is in the [code of conduct](../lab-rules/code-of-conduct.md#reporting-a-concern).
- **Keep the path from data to claim.** Every number in a paper should trace back to raw data, the code that processed it and the commit that code was at.
- **Report failures and exclusions.** If you drop trials, participants or runs, say which and why.
- **Responsible conduct of research (RCR) training:** students and postdocs must complete RCR training before they work on research funded by the U.S. National Science Foundation (NSF) ([Kent State compliance training](https://www.kent.edu/research/office-research-compliance/compliance-training)). Ask the director whether your project needs it.

## Human-subjects research

"The Kent State Institutional Review Board (IRB) must review research involving human subjects before the research project is implemented" ([Kent State IRB](https://www.kent.edu/research/office-research-compliance/research-human-subjects-irb)). Under the federal definition the IRB uses, research is human-subjects research when you gather data through interaction or intervention with living people, or collect identifiable private information about them, as part of a systematic investigation meant to produce generalizable knowledge.

In human-robot interaction, that usually includes user studies, surveys, interviews, recordings of people with a robot, and field deployments where people's behavior is measured.

> [!WARNING]
> Do not recruit, pilot with or collect data from anyone until the IRB has approved or exempted your study. If you are unsure whether your project counts, submit an **IRB Review Determination Form** and let the Office of Research Compliance decide.

**Steps, in order:**

1. **Complete CITI training.** "All researchers conducting research involving the use of human subjects must complete CITI before the Kent State Institutional Review Board (IRB) will approve a project" ([compliance training](https://www.kent.edu/research/office-research-compliance/compliance-training)). Most lab studies take the **Social & Behavioral Research Investigators** course; biomedical studies take the Biomedical course. Log in to CITI with your FlashLine ID. Training is valid for three years.
2. **Plan the study with the director**: research question, procedure, risks (including robot safety), recruitment, consent, compensation, data storage and who can see the data.
3. **Apply.** Applications go through Kuali, linked from the [IRB forms page](https://www.kent.edu/research/office-research-compliance/irb-forms) (the IRB page also gives <researchcompliance@kent.edu>). The IRB assigns one of three levels: exempt (Level I), expedited (Level II) or full board (Level III).
4. **Wait for approval**, then run the study exactly as approved. Any change (new questions, a different robot behavior, more participants) needs an amendment first.
5. **Minors need more.** Studies with people under 18, including high school interns, need parental permission and extra review, and Kent State's [policy on activities involving minors](https://www.kent.edu/policyreg/university-policy-regarding-campus-activities-involving-minors) (Policy 5-19) applies.

Kent State's human-subjects procedures are Policy [10-02.1](https://www.kent.edu/policyreg/administrative-policy-regarding-research-involving-human-subjects-0). Contact the Office of Research Compliance at 330-672-2704 or <researchcompliance@kent.edu>.

## Authorship and contribution

Agree on authorship early, in writing, and revisit it as the project changes. The director settles disagreements: [lab authorship practice].

| | ACM | IEEE |
| --- | --- | --- |
| Who is an author | An identifiable human who made a substantial intellectual contribution (such as conception, design or analysis), took part in drafting or revising the paper, and takes full responsibility for its content | Someone who made a significant intellectual contribution to theory, system or experiment design, prototype development or the analysis and interpretation of data; helped draft or revise the paper; and approved the final version |
| Not allowed | Gift, guest, ghost and purchased authorship; AI tools as authors | Anyone who does not meet all three criteria is acknowledged, not listed |
| Also required | Every author provides an ORCID iD before ACM's rights process is completed | |
| Source | [ACM policy on authorship](https://www.acm.org/publications/policies/new-acm-policy-on-authorship) (updated May 14, 2026) | [IEEE ethical requirements](https://journals.ieeeauthorcenter.ieee.org/become-an-ieee-journal-author/publishing-ethics/ethical-requirements/) (IEEE PSPB Operations Manual 8.2.1.A) |

**Contribution statements.** [CRediT](https://credit.niso.org/) (Contributor Roles Taxonomy) is a standard list of 14 roles: conceptualization, data curation, formal analysis, funding acquisition, investigation, methodology, project administration, resources, software, supervision, validation, visualization, writing (original draft) and writing (review and editing). ACM's policy recommends CRediT roles when you acknowledge contributors who are not authors. Keep a running CRediT list for every project; it makes authorship conversations easier.

## Citations and Zotero

- Use [Zotero](https://www.zotero.org/) to collect references, with the [Better BibTeX](https://retorque.re/zotero-better-bibtex/) add-on to export a `.bib` file with stable citation keys. Share a group library per project: [lab Zotero group].
- Cite the published version when one exists, with its DOI, and cite software and datasets you used, not just papers.
- **Check every reference exists and says what you claim.** Some venues now desk-reject papers with citations to nonexistent work (for example CoRL and RSS in their current calls for papers), which is a common failure of AI-generated text.
- Follow the venue's reference style; the [LaTeX templates](../templates/latex/README.md) already set IEEE and ACM styles.

## Data management

- **Where data lives:** lab datasets, recordings and models go in [shared data location]. Study data goes only where the IRB protocol says.
- **Not in personal accounts:** Kent State deletes staff and faculty accounts "on a rolling basis shortly after each user's departure" ([Kent State IT](https://www.kent.edu/it/digital-storage-changes-current-staff-and-faculty)), and graduates keep access for two years ([students](https://www.kent.edu/it/digital-storage-changes)). Lab data in a personal OneDrive or Google Drive is lost when you leave. Kent State provides Microsoft 365, including OneDrive ([Kent State IT](https://www.kent.edu/it/o365)).
- **Classify before you store:** Kent State's [data handling policy](https://www.kent.edu/policyreg/university-policy-regarding-data-handling) (Policy 9-04) and [information security policy](https://www.kent.edu/policyreg/administrative-policy-electronic-information-security) (Policy 9-03.1) set how university data must be protected. The classification standards are on Kent State's [Secure IT data pages](https://www.kent.edu/secureit/protecting-data) (FlashLine login required).
- **Study data:** keep consent forms separate from data, replace names with participant codes, keep the key that links codes to names in a separate restricted place, and keep data only as long as the protocol says.
- **No study data in unapproved tools:** Kent State's [AI Hub](https://www.kent.edu/ai) says not to put university data into AI tools outside its sanctioned list, and not to process FERPA-protected student data with any AI tool without IT guidance.
- **No study data on personal laptops or USB drives** unless the IRB protocol allows it, and never in a GitHub repository.

## Reproducibility and artifacts

A reader, a reviewer or a lab member two years from now should be able to rerun your work.

- **Code:** in the lab's GitHub organization, with a README that says how to build and run it, and a Git tag for the exact version behind each paper (for example `icra2027-submission`).
- **Environment:** pin versions: a Dockerfile, a ROSEnv lockfile (`rosenv.lock`), a `requirements.txt` or `uv.lock`, and the ROS 2 distribution and simulator version ([Docker and ROSEnv](../tech-stack/docker.md)).
- **Experiments:** record configuration files, random seeds, hardware and firmware versions, and the number of trials, with the results.
- **Data and models:** publish them with a license and a data or model card when the director and, for study data, the IRB protocol allow it.
- **Videos:** every video of a robot says whether the robot is **teleoperated, autonomous, semi-autonomous or scripted**, and its **playback speed** (for example "2× speed"), in the video itself and in its caption. Label simulation as simulation.
- **Hardware:** name the exact robot model and any modifications the lab made.

## Preprints, embargoes and news timing

- **Talk to the director before anything goes public**: a preprint, a talk, a poster, a video or a post.
- **Preprints are public the moment you post them**, and an embargo cannot be applied afterwards. arXiv licenses are irrevocable once chosen ([arXiv licenses](https://info.arxiv.org/help/license/index.html)).
- **IEEE** does not treat preprints on arXiv or TechRxiv as prior publication. For a conference paper, add a notice on the preprint's first page saying it has been submitted to IEEE for possible publication; after acceptance, replace it with the accepted version and add the DOI and IEEE copyright notice. Don't post the final IEEE Xplore PDF unless the paper is open access ([IEEE: post your paper](https://conferences.ieeeauthorcenter.ieee.org/get-published/post-your-paper/); [author posting policy](https://www.ieee.org/publications/rights/author-posting-policy.html)).
- **ACM** lets authors post preprint, submitted and accepted versions on their own pages, institutional repositories and non-commercial repositories such as arXiv, with the DOI once it exists, but not on commercial sites such as ResearchGate or Academia.edu ([ACM author rights](https://authors.acm.org/author-resources/author-rights)).
- **Double-blind venues** may limit publicity while a paper is under review; check the venue's anonymity policy, including for talks and videos that reveal who you are.
- **Journal embargoes** are set by the publisher. Nothing appears on the lab website or social media before the embargo lifts.
- **News:** publicize a paper only after acceptance is public. For a paper worth a news story, the lab tells Kent State University Communications and Marketing (UCM) four to six weeks before publication (the lab's practice), with a plain-language summary.
- **Inventions:** if the work might be patentable, talk to the director and Kent State's [Office of Technology Commercialization](https://www.kent.edu/research/technology-commercialization) **before** any public reveal, including a preprint.

## Generative AI in research and writing

Publishers now treat AI used in the research differently from AI used to polish the writing. Follow the stricter of the publisher's policy and the venue's call for papers.

| | ACM | IEEE |
| --- | --- | --- |
| AI used to do the research (design, data, code, simulations, analysis, figures the conclusions rely on) | Describe it in detail in the Methods section | Disclose AI-generated content, including text, figures, images and code, in the acknowledgments: name the system, the sections and the level of use |
| AI used only to help write or edit | ACM "no longer requires the disclosure of information regarding the use of AI" | Editing and grammar help need not be disclosed, though IEEE recommends it |
| AI as an author | Not allowed | Not addressed on this page; IEEE Robotics and Automation Society calls for papers (ICRA 2027, IROS 2026) say it is not allowed |
| Reviewing | | Never upload a manuscript under review to a public AI platform: it breaches confidentiality |
| Source | [ACM policy on authorship](https://www.acm.org/publications/policies/new-acm-policy-on-authorship) and [FAQ](https://www.acm.org/publications/policies/frequently-asked-questions) (updated May 14, 2026) | [IEEE submission and peer review policies](https://journals.ieeeauthorcenter.ieee.org/become-an-ieee-journal-author/publishing-ethics/guidelines-and-policies/submission-and-peer-review-policies/) |

Lab practice on top of those rules:

- **Kent State first:** don't put university data, study data or unpublished manuscripts you are reviewing into AI tools Kent State has not sanctioned ([AI Hub](https://www.kent.edu/ai)).
- **Keep a short log** of how you used AI tools in each project, so the disclosure is easy to write.
- **Verify everything** an AI tool gives you: every citation, number and claim. All authors are accountable for what the paper says.
- **Label AI-generated images** as illustrations, and never present them as photos of lab robots, people or results.

## The lab affiliation line

Write the lab's full name and Kent State in every author block, following the venue's format:

```text
Advanced Telerobotics Research Lab, Department of Computer Science, Kent State University, Kent, OH, USA
```

- Spell out the lab's name. "ATR" alone also names a large robotics institute in Kyoto (the Advanced Telecommunications Research Institute International), so reviewers may confuse the two. When you cite work from that institute, name it as "ATR, Kyoto".
- The [LaTeX templates](../templates/latex/README.md) already contain this block.
- In a double-blind submission, the affiliation is hidden with the authors; it returns in the camera-ready version.

## Funding acknowledgments

- Name the funder and award number **exactly as the award record gives them**, and only after the PI confirms which award funded this work. Until then, write `[Sponsor]` and `[Grant No.]`.
- For work funded by the U.S. National Science Foundation, the current NSF award terms use this wording: "This material is based upon work supported by the U.S. National Science Foundation under award No. [Grant No.]" Materials other than journal papers (posters, slides, web pages) also carry NSF's disclaimer; ask the PI for the exact text in the award's terms.
- Acknowledge people who helped but are not authors (with their permission), and study participants as a group, never by name.
- Remove acknowledgments from double-blind submissions; the templates do this automatically in anonymous mode.

## Related

- [Writing papers](writing-papers.md) and the [publishing checklist](publishing-checklist.md)
- [LaTeX templates](../templates/latex/README.md)
- [Code of conduct](../lab-rules/code-of-conduct.md): integrity, privacy and reporting a concern
- [Kent State Office of Research Compliance](https://www.kent.edu/research/office-research-compliance)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/research/standards.md)</sub>
