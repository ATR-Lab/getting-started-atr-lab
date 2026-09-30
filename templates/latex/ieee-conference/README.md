# IEEE conference template

> **Read this when** you start a paper for an IEEE conference or letter and the venue does not supply its own LaTeX file.

A compilable skeleton on IEEE's `IEEEtran` class with the `conference` option, the lab's affiliation block, a double-blind toggle, a sample figure and table, an acknowledgment with `[Grant No.]` and IEEE-style references. Compiled with tectonic 0.17.0 against **IEEEtran V1.8b (2015/08/26)** and IEEEtran.bst 1.14 on Sept. 30, 2026; V1.8b is still the current release on [CTAN](https://ctan.org/pkg/ieeetran).

## Files

| File | What it is |
| --- | --- |
| `main.tex` | The paper. Search it for `[` to find every placeholder |
| `references.bib` | Sample BibTeX entries checked against Crossref; replace them with yours |

## Build

```bash
cd templates/latex/ieee-conference
tectonic main.tex
```

`latexmk -pdf main.tex` works with TeX Live, and the two files upload to Overleaf as they are.

## Switches and placeholders

- **Double-blind review:** change `\anonymousfalse` to `\anonymoustrue`. Authors become "Anonymous Author(s)" and the acknowledgment disappears. Also remove self-citations in the first person, repository links and anything else that identifies the lab, as the venue's anonymity policy says.
- **Fonts:** IEEE papers are set in Times. pdfLaTeX gets it from IEEEtran; under XeLaTeX, LuaLaTeX and tectonic the template loads TeX Gyre Termes, a free Times clone.
- **Authors:** keep the lab and department lines exactly as written; they match the lab's [affiliation line](../../../research/standards.md#the-lab-affiliation-line). Add or remove `\and` blocks for more authors.
- **Acknowledgment:** `[Sponsor]` and `[Grant No.]` stay as brackets until the PI confirms which award funded the work. IEEE asks authors to disclose AI-generated content in the acknowledgments; see [generative AI](../../../research/standards.md#generative-ai-in-research-and-writing).
- **Figures:** replace the `\fbox` placeholder with `\includegraphics`. Use PDF for plots and diagrams, and PNG or JPEG at 300 dpi or more for photos.

## Venue templates that replace this one

IEEE Robotics and Automation Society venues (ICRA, IROS, RO-MAN and Humanoids, plus first submissions to RA-L) use the RAS template (`ieeeconf.cls`) from [PaperCept](https://ras.papercept.net/conferences/support/tex.php), and IEEE VR uses the IEEE Computer Society VGTC template. The [venue table](../../../research/writing-papers.md#venues) says which. If the venue has its own file, copy this body into it and keep the venue's preamble.

## Related

- [LaTeX templates](../README.md)
- [ACM sigconf template](../acm-sigconf/README.md)
- [Writing papers](../../../research/writing-papers.md)
- [IEEE conference templates](https://www.ieee.org/conferences/publishing/templates.html)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/templates/latex/ieee-conference/README.md)</sub>
