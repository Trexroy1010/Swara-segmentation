# Thesis LaTeX Project

## Structure
```
thesis/
├── main.tex                  # Master document (compile this)
├── references.bib            # Bibliography (see notes below)
├── figures/                  # Put all figure image files here (.png/.pdf/.jpg)
└── chapters/
    ├── abstract.tex
    ├── acknowledgments.tex
    ├── chapter1_introduction.tex
    ├── chapter2_literature_review.tex
    ├── chapter3_dataset.tex
    ├── chapter4_methodology.tex
    ├── chapter5_results.tex
    ├── chapter6_limitations.tex
    ├── chapter7_future_work.tex
    └── chapter8_conclusion.tex
```

## How to compile
Requires a standard TeX Live / MiKTeX install with `natbib`.

```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

Or with `latexmk`:
```bash
latexmk -pdf main.tex
```

## Figures — action needed
All figures from the original document (folder structure diagram, dataset
distribution plots, MFCC/Log-Mel/Pitch/RMS/CQT visualizations, methodology
diagram, attention mechanism diagram, per-experiment training curves, and
end-to-end pipeline visualizations) were **not** available as separate image
files, so each has been replaced with a placeholder box:

```
\figplaceholder{suggested_filename.png}{Caption text}{fig:label}
```

To finish the document:
1. Export/crop each figure from your original notebooks/plots.
2. Save it into `figures/` using the suggested filename (or any name you like).
3. Replace the corresponding `\figplaceholder{...}` call with:
   ```latex
   \begin{figure}[H]
     \centering
     \includegraphics[width=0.8\textwidth]{figures/suggested_filename.png}
     \caption{Caption text}
     \label{fig:label}
   \end{figure}
   ```

All tables that already contained data in the source PDF (dataset stats,
model architecture tables, training configs, per-experiment metrics, the
overall comparison table) have been fully typeset in LaTeX — no placeholders
needed there.

## References — action needed
The original thesis PDF you uploaded contains **only in-text citation
markers** ([1]–[39]) — the actual reference list page was not included in
the file. `references.bib` was reconstructed from the author names and
topics mentioned in the literature review text:

- Entries marked `% VERIFY` are well-known, easily identifiable papers
  (e.g., YIN, pYIN, SWIPE, Onsets and Frames, the CQT toolbox paper, Slakh).
  These are very likely correct but you should double-check
  year/volume/pages against the actual paper before submitting.
- Entries marked `% FIXME` only had partial information recoverable from
  context (author surname(s) + rough topic). **You must locate the actual
  paper and fill in the venue, year, volume, and page numbers** — the title
  wording is also a paraphrase from context, not necessarily the exact
  published title.

Once `references.bib` is complete, `\cite{ref1}` … `\cite{ref39}` in
`chapters/chapter2_literature_review.tex` will resolve automatically.

## Notes
- `\figplaceholder` is a helper macro defined in `main.tex`; you can delete
  it once all figures are inserted for real.
- Title page fields (`[Your Name]`, co-authors) are placeholders — fill in
  your actual name(s) in `main.tex`.
- Table VII in Chapter 5 (overall comparison) has a footnote flagging that
  the source PDF did not explicitly report Segmentation Precision/Recall/F1
  and end-to-end percentages consistently for row E6 (CQT) — verify against
  your experiment logs.
