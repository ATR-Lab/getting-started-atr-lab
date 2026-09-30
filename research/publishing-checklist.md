# Publishing checklist

> **Read this when** a paper deadline is a week or two away, and again the day you submit or post a preprint.

Every check to run before a paper leaves the lab, in the order you usually meet them. Copy the list into the paper's repository or issue tracker and tick items off with your co-authors. The details behind each item are in [research standards](standards.md) and [writing papers](writing-papers.md). The one thing to remember: the director reviews every submission before it goes out, so leave time for that review.

## Contents

- [Weeks before the deadline](#weeks-before-the-deadline)
- [Claims and content](#claims-and-content)
- [Format](#format)
- [References](#references)
- [Anonymity (double-blind venues)](#anonymity-double-blind-venues)
- [Disclosures and acknowledgments](#disclosures-and-acknowledgments)
- [Video and supplementary material](#video-and-supplementary-material)
- [Approvals](#approvals)
- [Submitting](#submitting)
- [Preprints and after submission](#preprints-and-after-submission)
- [Related](#related)

## Weeks before the deadline

- [ ] You have read the **current call for papers**: format, page or word limit, anonymity rules, supplementary material, AI policy and every deadline (abstract, paper, video).
- [ ] The paper uses the **venue's template**, or the lab template moved into it, unmodified ([templates](../templates/latex/README.md)).
- [ ] **Authorship and author order** are agreed with every co-author and the director, and each author meets the publisher's criteria ([authorship](standards.md#authorship-and-contribution)).
- [ ] Any **study with people** ran under an approved or exempt IRB protocol, and the paper reports it as the protocol allows ([human-subjects research](standards.md#human-subjects-research)).
- [ ] The director has a date in the calendar to review the full draft: [how many days before the deadline the director needs the draft].

## Claims and content

- [ ] Every claim is backed by a result in the paper or a citation, and keeps its conditions ("in simulation", "with [N] participants", "at walking speed").
- [ ] Every robot result says whether the robot was **teleoperated, autonomous, semi-autonomous or scripted**, and simulation results are labeled as simulation.
- [ ] Numbers in the text, tables and figures agree, and each can be traced to data and code at a known commit ([reproducibility](standards.md#reproducibility-and-artifacts)).
- [ ] Excluded trials or participants are reported with the reason.
- [ ] There is a **limitations** paragraph.
- [ ] Words like "first", "only", "novel" and "state of the art" are either backed by a citation or removed.

## Format

- [ ] Within the page or word limit, counted the way the call for papers counts it (with or without references and appendices).
- [ ] Margins, fonts and spacing are the template's own; nothing was squeezed.
- [ ] All fonts are embedded. For PaperCept (ICRA, IROS, RO-MAN, Humanoids, RA-L), the PDF contains **no Type 3 fonts**; check with `pdffonts main.pdf`.
- [ ] Figures are readable in print and in grayscale, with legible labels, units on every axis and captions that say what to notice.
- [ ] **ACM papers:** CCS concepts and keywords are set, and every figure has a `\Description`.
- [ ] **IEEE papers:** IEEE keywords are set.
- [ ] The PDF opens without errors, and no `[placeholder]`, `??` (a broken reference) or leftover to-do note remains. Search the PDF for `[` and `??`.

## References

- [ ] Every reference exists and says what you cite it for. Check each one that an AI tool suggested or that you did not read yourself.
- [ ] Published works cite the published version with its DOI, not only the preprint.
- [ ] Software, datasets and robot models you used are cited.
- [ ] The bibliography follows the venue's style (the templates set it).

## Anonymity (double-blind venues)

- [ ] Author names, affiliations, emails and ORCID iDs are hidden (the lab templates' anonymous switch).
- [ ] The acknowledgment and funding lines are removed.
- [ ] Self-citations are in the third person ("In previous work, Smith et al. [3]"), as the venue's rules say.
- [ ] No links to the lab's GitHub, website or YouTube; use an anonymized link if the venue allows one.
- [ ] Figures, photos and videos show no lab logos, lab names, name badges, recognizable lab members or identifying voices.
- [ ] The PDF metadata (author and title fields) doesn't name you; check with `pdfinfo main.pdf`.

## Disclosures and acknowledgments

- [ ] **Generative AI use** is described as the publisher and venue require: in the Methods section for AI used in the research (ACM), in the acknowledgments for AI-generated content (IEEE), or as the call for papers says ([generative AI](standards.md#generative-ai-in-research-and-writing)).
- [ ] **Funding:** the funder and award number were confirmed by the PI and match the award record; no `[Grant No.]` placeholder remains in the camera-ready version ([funding acknowledgments](standards.md#funding-acknowledgments)).
- [ ] **Conflicts of interest** are declared in the submission system and, if the venue asks, in the paper.
- [ ] People thanked in the acknowledgments agreed to be named; study participants are thanked as a group, never by name.
- [ ] The affiliation is the lab's full line: Advanced Telerobotics Research Lab, Department of Computer Science, Kent State University ([affiliation line](standards.md#the-lab-affiliation-line)).

## Video and supplementary material

- [ ] The video states **teleoperated, autonomous, semi-autonomous or scripted** and the **playback speed** on screen.
- [ ] Everyone who appears in it consented, and study footage is covered by the consent form. No minors without a signed parent or guardian release.
- [ ] Speech is captioned, and there is no music you don't have rights to.
- [ ] Length, file size and format meet the call for papers, and the video is anonymized for double-blind review.
- [ ] Supplementary code and data are anonymized where needed and contain no passwords, keys, tokens or identifiable study data.

## Approvals

- [ ] The director has reviewed and approved the final version.
- [ ] Every co-author has read and approved the final version (IEEE's authorship criteria require it).
- [ ] If the work is sponsored, any prepublication review the sponsor agreement requires is done (ask the director; agreements run through Kent State's Office of Sponsored Programs).
- [ ] If anything in the paper might be patentable, the invention disclosure was filed with Kent State's [Office of Technology Commercialization](https://www.kent.edu/research/technology-commercialization) before submission or posting.

## Submitting

- [ ] Every author has an account in the submission system (PCS, PaperCept, OpenReview) with the right email address, and is entered in the right order.
- [ ] Topic areas, keywords and conflicts of interest are filled in the submission system.
- [ ] You submitted at least a few hours before the deadline, and checked the PDF the system stored.
- [ ] The confirmation email is saved, and the director has the paper ID: [where the lab tracks submissions].

## Preprints and after submission

- [ ] A preprint goes up only after the director agrees, and only as the venue and publisher allow; an IEEE conference preprint carries the "submitted to IEEE" notice ([preprints](standards.md#preprints-embargoes-and-news-timing)).
- [ ] The code and data behind the submission are tagged in Git (for example `hri2027-submission`).
- [ ] Nothing about the paper goes on the lab website or social media until acceptance is public.
- [ ] For the camera-ready version, follow [camera-ready and copyright forms](writing-papers.md#camera-ready-and-copyright-forms).

## Related

- [Writing papers](writing-papers.md)
- [Research standards](standards.md)
- [LaTeX templates](../templates/latex/README.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/research/publishing-checklist.md)</sub>
