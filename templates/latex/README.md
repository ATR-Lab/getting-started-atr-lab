# LaTeX templates

> **Read this when** you start a new paper and want a skeleton that already has the lab's affiliation block, an acknowledgment line and a sample figure.

Two skeletons, one per publisher, both compiled with `tectonic` on Sept. 30, 2026. Copy the folder, rename it for your paper, and replace every `[bracketed placeholder]`. If the venue publishes its own template (many IEEE Robotics and Automation Society conferences do), start from the venue's file and move this body into it; the venue's template always wins.

| Template | Class | Use it for | Compiled against |
| --- | --- | --- | --- |
| [`ieee-conference/`](ieee-conference/README.md) | `IEEEtran` (`conference` option) | IEEE conferences that use IEEE's standard conference template. Robotics and Automation Society venues (ICRA, IROS, RO-MAN, Humanoids, RA-L) use their own PaperCept template: move this body into it (see the [venue table](../../research/writing-papers.md#venues)) | IEEEtran V1.8b (2015/08/26), the current release on [CTAN](https://ctan.org/pkg/ieeetran) |
| [`acm-sigconf/`](acm-sigconf/README.md) | `acmart` (`sigconf` format) | ACM conferences such as HRI and CHI | acmart v1.83 (2022/02/19) from tectonic's bundle; ACM's current release on [CTAN](https://ctan.org/pkg/acmart) is v2.20 (Aug. 16, 2026) |

## Build a template

With [tectonic](https://tectonic-typesetting.github.io/) (a self-contained LaTeX engine that downloads packages as it needs them; it also runs BibTeX for you):

```bash
# macOS; on Ubuntu, see the tectonic website for install options
brew install tectonic
cd templates/latex/ieee-conference
tectonic main.tex
```

With a full TeX Live 2026 installation, `latexmk -pdf main.tex` works too. On [Overleaf](https://www.overleaf.com/), upload `main.tex` and `references.bib` to a new blank project. Details and the venue table are in [writing papers](../../research/writing-papers.md).

> [!NOTE]
> Compiled PDFs and LaTeX build files are ignored by Git (see `.gitignore`). Commit the `.tex`, `.bib` and figure sources, never the PDF.

## What every template includes

- The lab's affiliation block: Advanced Telerobotics Research Lab, Department of Computer Science, Kent State University, Kent, OH, USA ([why this wording](../../research/standards.md#the-lab-affiliation-line)).
- A review toggle for double-blind venues that hides authors and acknowledgments.
- An acknowledgment with `[Sponsor]` and `[Grant No.]`, to fill only after the PI confirms which award funded the work.
- A sample figure with a caption, a sample table and three sample references checked against Crossref.

## Related

- [Writing papers](../../research/writing-papers.md)
- [Publishing checklist](../../research/publishing-checklist.md)
- [Research standards](../../research/standards.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/templates/latex/README.md)</sub>
