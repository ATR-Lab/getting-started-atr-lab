# ACM sigconf template

> **Read this when** you start a paper for an ACM conference, such as HRI or CHI, that uses the `acmart` class.

A compilable skeleton on ACM's `acmart` class in the `sigconf` format, with the lab's affiliation block, review and anonymous switches, sample CCS concepts and keywords, a figure with a `\Description` (alt text), a table, an acknowledgment with `[Grant No.]` and ACM-style references.

> [!NOTE]
> **Class version.** Compiled with tectonic 0.17.0 on Sept. 30, 2026 against **acmart v1.83 (2022/02/19)**, the version in tectonic's default bundle. ACM's current release is **v2.20 (Aug. 16, 2026)** on [CTAN](https://ctan.org/pkg/acmart). The skeleton uses only commands that v2.20 still documents (checked against the class source on GitHub), but ACM's publishing system builds your final paper with its own current copy, so do a last check on Overleaf or a TeX Live 2026 installation before you submit. ACM recommends LuaLaTeX with TeX Live 2025 or later ([ACM LaTeX guide](https://authors.acm.org/proceedings/production-information/preparing-your-article-with-latex)).

## Files

| File | What it is |
| --- | --- |
| `main.tex` | The paper. Search it for `[` to find every placeholder |
| `references.bib` | Sample BibTeX entries checked against Crossref; replace them with yours |

## Build

```bash
cd templates/latex/acm-sigconf
tectonic main.tex
```

`latexmk -pdf main.tex` works with TeX Live, and the two files upload to Overleaf as they are.

## Switches and placeholders

Pick one `\documentclass` line at the top of `main.tex`:

| Line | Use it for |
| --- | --- |
| `\documentclass[sigconf,review,anonymous]{acmart}` | Double-blind submission: line numbers, authors and acknowledgments hidden (the default in the template) |
| `\documentclass[sigconf,review]{acmart}` | Single-blind submission: line numbers, authors shown |
| `\documentclass[sigconf]{acmart}` | Camera-ready, after acceptance |
| `\documentclass[manuscript,review,anonymous]{acmart}` | Venues that ask for the single-column review format, such as CHI 2027; check the call for papers |

- **Rights block:** `\setcopyright`, `\acmDOI`, `\acmISBN` and `\acmConference` hold sample values. After acceptance, ACM's rights form (sent to the corresponding author) gives you the exact commands for your paper; paste them in place of the whole block. ACM has been fully open access since Jan. 1, 2026, so expect a Creative Commons license in those commands ([writing papers](../../../research/writing-papers.md#camera-ready-and-copyright-forms)).
- **Authors:** each author has an `\affiliation` with `\department[0]{Advanced Telerobotics Research Lab}` inside `\department[1]{Department of Computer Science}`, so the lab is recorded as part of the department. Replace the placeholder ORCID iD with each author's own.
- **CCS concepts and keywords:** the two sample concepts are real ACM Computing Classification System entries, but choose your own with the tool at [dl.acm.org/ccs](https://dl.acm.org/ccs/ccs.cfm) and paste both the `CCSXML` block and the `\ccsdesc` lines it gives you.
- **Figures:** every figure needs `\Description{...}`, its alt text for screen readers. Describe what the figure shows, not just its title.
- **Acknowledgment:** the `acks` environment is hidden automatically in anonymous mode. `[Sponsor]` and `[Grant No.]` stay as brackets until the PI confirms the award.
- **Generative AI:** ACM's policy (updated May 14, 2026) asks you to describe AI used to do the research in the Methods section; AI used only to help write needs no disclosure. The venue may ask for more; see [generative AI](../../../research/standards.md#generative-ai-in-research-and-writing).

## Related

- [LaTeX templates](../README.md)
- [IEEE conference template](../ieee-conference/README.md)
- [Writing papers](../../../research/writing-papers.md)
- [ACM primary article template](https://www.acm.org/publications/proceedings-template)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/templates/latex/acm-sigconf/README.md)</sub>
