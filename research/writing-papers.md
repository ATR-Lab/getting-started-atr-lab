# Writing papers

> **Read this when** you start a paper for an ACM or IEEE venue, need to know which LaTeX template a venue uses, or are preparing a camera-ready version.

How the lab writes papers in LaTeX: the tools, the two publisher classes (IEEEtran and acmart), the templates and review rules of the venues we usually submit to, figures and video, and what happens after acceptance. Venue rules change every year, so the table below records the edition we checked. The one thing to remember: **the current call for papers (CFP) always wins**; read it before you write the first line.

## Contents

- [LaTeX basics for the lab](#latex-basics-for-the-lab)
- [IEEEtran or acmart](#ieeetran-or-acmart)
- [Venues](#venues)
- [Overleaf](#overleaf)
- [Figures and video](#figures-and-video)
- [Camera-ready and copyright forms](#camera-ready-and-copyright-forms)
- [Related](#related)

## LaTeX basics for the lab

LaTeX is a typesetting system: you write plain text with markup, and a compiler turns it into a PDF. ACM and IEEE both publish LaTeX classes, and most robotics and human-robot interaction papers are written in it.

- **Start from a template.** Copy [`templates/latex/ieee-conference`](../templates/latex/ieee-conference/README.md) or [`templates/latex/acm-sigconf`](../templates/latex/acm-sigconf/README.md), or the venue's own template if it has one.
- **Compile locally** with [tectonic](https://tectonic-typesetting.github.io/) (`tectonic main.tex`) or a full [TeX Live](https://tug.org/texlive/) installation (`latexmk -pdf main.tex`), or on [Overleaf](#overleaf).
- **Keep the paper in Git**, in a private repository in the lab's organization: [paper repository naming convention]. Commit the `.tex`, `.bib` and figure sources, never the PDF or build files.
- **Write one sentence per line.** Git diffs and co-author reviews become much easier to read.
- **Suggested layout:**

  ```text
  paper/
    main.tex          preamble, title, authors, \input of each section
    sections/         intro.tex, method.tex, experiments.tex, ...
    figures/          PDF plots, PNG or JPEG photos, and the scripts that make them
    references.bib    exported from Zotero with Better BibTeX
  ```

- **Label everything** with a prefix (`fig:`, `tab:`, `sec:`, `eq:`) and refer to it with `\ref`, never by typing a number.
- **Don't change the class's margins, fonts or spacing** to fit the page limit. Publishers check, and it is grounds for rejection.

## IEEEtran or acmart

| | IEEEtran | acmart |
| --- | --- | --- |
| Publisher | IEEE | ACM |
| Class line for a conference paper | `\documentclass[conference]{IEEEtran}` | `\documentclass[sigconf]{acmart}` |
| Current version on CTAN | [1.8b](https://ctan.org/pkg/ieeetran) | [2.20](https://ctan.org/pkg/acmart) (Aug. 16, 2026) |
| Anonymous review | No built-in switch; remove author details yourself (the lab template adds a switch) | Built in: `review` adds line numbers, `anonymous` hides authors and acknowledgments |
| Metadata it needs | IEEE keywords (`IEEEkeywords`) | CCS concepts (from [dl.acm.org/ccs](https://dl.acm.org/ccs/ccs.cfm)), keywords, and a `\Description` alt text for every figure |
| Reference style | `IEEEtran.bst`: numbered | `ACM-Reference-Format.bst` |
| Official template page | [IEEE conference templates](https://www.ieee.org/conferences/publishing/templates.html) | [ACM primary article template](https://www.acm.org/publications/proceedings-template) |

**IEEE Robotics and Automation Society conferences are a special case.** ICRA, IROS, Humanoids and RO-MAN, and first submissions to RA-L, use the RAS template from PaperCept, the society's submission system: `\documentclass[letterpaper, 10 pt, conference]{ieeeconf}`, from the [PaperCept LaTeX support page](https://ras.papercept.net/conferences/support/tex.php). The body of the lab's IEEE template moves into it unchanged. PaperCept rejects PDFs that contain Type 3 fonts.

**ACM's publishing system (TAPS)** builds the final version from your LaTeX source, so it accepts only acmart with packages on ACM's accepted list and warns that defining your own commands can cause validation errors. ACM recommends compiling with LuaLaTeX on TeX Live 2025 or later ([Preparing your article with LaTeX](https://authors.acm.org/proceedings/production-information/preparing-your-article-with-latex)).

## Venues

The lab's usual venues, checked on Sept. 30, 2026 against each venue's own page. Lengths are for the edition shown; always confirm them, and every deadline, in the current call for papers.

| Venue | Publisher | Template | Review | Length (edition checked) | Author kit |
| --- | --- | --- | --- | --- | --- |
| ACM/IEEE HRI | ACM (open access) | acmart `sigconf`, two columns; not the SIGCHI format | Double-blind | Up to 8 pages excluding references (HRI 2027) | [HRI 2027 full papers](https://humanrobotinteraction.org/2027/full-papers/) |
| ACM CHI | ACM (open access) | acmart single-column for review: `manuscript,review,anonymous`; `sigconf` for the final version | Anonymous | 5,000 to 8,000 words encouraged; over 12,000 desk-rejected (CHI 2027) | [CHI 2027 papers](https://chi2027.acm.org/authors/papers/), [formats](https://chi2027.acm.org/chi-publication-formats/) |
| IEEE ICRA | IEEE Robotics and Automation Society | ICRA two-column format; RAS template (`ieeeconf`) from PaperCept | Double-anonymous | 8 pages including references (ICRA 2027) | [ICRA 2027 call for papers](https://2027.ieee-icra.org/contribute/call-for-icra-2027-papers-now-accepting-submissions/) |
| IEEE/RSJ IROS | IEEE (proceedings on IEEE Xplore) | RAS template (`ieeeconf`) from PaperCept | Double-anonymous | Up to 8 pages including references (IROS 2026; the 2027 call is not out yet) | [IROS 2026 call for papers](https://2026.ieee-iros.org/contribute/call-for-papers/) |
| IEEE RO-MAN | IEEE | RAS template from PaperCept, US letter | Single-blind (authors named) | 6 to 8 pages including references at submission; 6 pages plus up to 2 paid pages in the final version (RO-MAN 2026) | [RO-MAN 2026 submission](https://ro-man2026.org/papersubmission/) |
| IEEE RA-L (journal) | IEEE Robotics and Automation Society | RAS conference format (`ieeeconf`) to submit; RA-L style for the final version | Double-anonymous | 6 pages, plus up to 2 paid pages (maximum 8) | [RA-L information for authors](https://www.ieee-ras.org/publications/ra-l/ra-l-information-for-authors/) |
| IEEE VR | IEEE Computer Society | IEEE VGTC conference format ([template](https://tc.computer.org/vgtc/publications/conference/)); the TVCG journal template for papers accepted to the journal special issue | Double-blind | 4 to 9 pages plus up to 2 pages of references (IEEE VR 2027) | [IEEE VR 2027 papers](https://ieeevr.org/2027/contribute/papers/) |
| CoRL | Proceedings of Machine Learning Research (PMLR) | CoRL LaTeX template, linked from the author instructions | Double-blind; reviews of accepted papers are made public | 8 pages of main text; references and appendix don't count; 9 pages for the camera-ready version (CoRL 2026) | [CoRL instructions for authors](https://www.corl.org/contributions/instruction-for-authors) |
| RSS | RSS Foundation (publisher of the proceedings not stated on the call) | RSS LaTeX or Word template from the conference site | Anonymized | Two stages: a 6-page extended abstract, then at most 8 pages excluding references (RSS 2027) | [RSS 2027 call for papers](https://roboticsconference.org/information/cfp/) |
| IEEE-RAS Humanoids | IEEE (proceedings on IEEE Xplore) | RAS template from PaperCept | Double-anonymous | 8 pages including references, no extra pages (Humanoids 2026) | [Humanoids 2026 call for papers](https://2026.ieee-humanoids.org/call-for-papers/) |

**Double-anonymous rules for RAS venues** (ICRA, IROS, Humanoids, RA-L) are on the [RAS double-anonymous review page](https://www.ieee-ras.org/publications/rules-for-the-double-anonymous-review-process/): cite your own work in the third person ("In previous work [3]"), leave acknowledgments out until acceptance, and remove identifying links; posting a preprint on arXiv is allowed.

## Overleaf

[Overleaf](https://www.overleaf.com/) is a web-based LaTeX editor where co-authors edit the same project. It hosts the official template galleries for [ACM](https://www.overleaf.com/gallery/tagged/acm-official) and [IEEE](https://www.overleaf.com/gallery/tagged/ieee-official).

- **Kent State has no institutional Overleaf license** ([Overleaf](https://www.overleaf.com/edu/kentstate); the [Kent State University Libraries guide](https://libguides.library.kent.edu/c.php?g=278135&p=7508433) says the same). Everyone uses their own account and plan; the lab's arrangement: [lab Overleaf plan, if any].
- **Keep Git as the source of truth.** If you write in Overleaf, sync or copy the project back to the paper's Git repository at every milestone (submission, rebuttal, camera-ready).
- **Check the template's options.** Overleaf's ACM template may default to a different format (for example `manuscript`) than your venue wants; HRI's call for papers points this out.

## Figures and video

- **Plots** go in as vector PDF, with fonts embedded and text no smaller than the caption text. **Photos** go in as PNG or JPEG at 300 dpi or more at their printed size.
- **Readable for everyone:** use color palettes that work for color-blind readers, never carry meaning by color alone (add markers or labels), and write a real caption that says what the reader should notice. ACM papers need a `\Description` (alt text) for every figure.
- **Label robot footage** in every figure and video: teleoperated, autonomous, semi-autonomous or scripted, and the playback speed ([reproducibility](standards.md#reproducibility-and-artifacts)).
- **People in figures and videos** appear only with consent, and study participants only when the IRB consent form covers it. Never show minors' faces without a signed parent or guardian release.
- **Anonymize for double-blind review:** no lab logos, lab names, faces of known lab members, or voices that identify the lab in submission videos, and no links to the lab's GitHub.
- **Video length, size and format limits** are in each venue's call for papers. Add captions to every video with speech.
- **AI-generated images** are labeled as illustrations and follow the venue's AI policy ([generative AI](standards.md#generative-ai-in-research-and-writing)).

## Camera-ready and copyright forms

After acceptance:

1. **Read the reviews with your co-authors** and make the changes you promised in the rebuttal.
2. **De-anonymize:** switch the template out of review mode, restore authors, affiliations, acknowledgments and self-citations, and add the [funding acknowledgment](standards.md#funding-acknowledgments) the PI has confirmed.
3. **Rights and copyright:**
   - **ACM** has been fully open access since Jan. 1, 2026 ([ACM Open](https://www.acm.org/publications/openaccess)). Authors keep copyright and grant ACM a license under CC BY or CC BY-NC-ND ([rights policy](https://www.acm.org/publications/policies/publication-rights-and-licensing-policy)). Only the corresponding author receives the rights form; paste the LaTeX commands it gives you into the paper's rights block. The publication fee depends on whether the corresponding author's institution participates in ACM Open; for 2027 conferences, HRI and CHI list $500 for ACM or SIG members and $750 for non-members. Whether Kent State participates: [ask Kent State University Libraries whether Kent State is an ACM Open institution].
   - **IEEE** conference authors submit the IEEE Electronic Copyright Form (eCF) through the conference; without it, IEEE cannot publish the paper ([IEEE copyright](https://www.ieee.org/publications/rights/copyright-main.html)).
4. **Check the PDF:** conferences that use [IEEE PDF eXpress](https://www.ieee.org/conferences/publishing/pdfexpress.html) require a compatible PDF, RAS conferences check PDFs in PaperCept, and ACM builds the final version in TAPS ([TAPS workflow](https://authors.acm.org/proceedings/production-information/taps-production-workflow)).
5. **Register and present:** most venues require at least one author to register for the paper to appear. Ask the director before you commit travel funds.
6. **Tag the code** used for the camera-ready results, update the preprint as the publisher allows ([preprints](standards.md#preprints-embargoes-and-news-timing)), and tell the director so the lab can list the paper.

Before you submit anything, run the [publishing checklist](publishing-checklist.md).

## Related

- [Research standards](standards.md)
- [Publishing checklist](publishing-checklist.md)
- [LaTeX templates](../templates/latex/README.md)
- [Tech stack](../tech-stack/README.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/research/writing-papers.md)</sub>
