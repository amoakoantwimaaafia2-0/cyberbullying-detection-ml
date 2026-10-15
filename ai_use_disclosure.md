# AI Use Disclosure

This disclosure follows the DCIT 316 requirement to state what AI assistance
was used and how it was verified.

---

## 1. Tools Used

- **[Chat-based large language model, e.g. ChatGPT / Claude]** — used for
  drafting and reviewing documentation files (`README.md`, data card, model
  card, ethics statement, this disclosure, reproducibility checklist) and for
  code review suggestions.

No AI tool was used to generate research results, fabricate data, or produce
citations that were not independently verified.

---

## 2. What AI Was Used For

| Area | Use | Verified by |
|---|---|---|
| Documentation drafting | Structure and phrasing of Markdown docs in `docs/` | Read, edited, and corrected by me against the notebook and report |
| Code review | Reading `cyberbullyingmodel.ipynb` and pointing out potential issues (e.g. clearing sensitive outputs, pinning versions) | I inspected the notebook and confirmed each suggestion |
| Reference formatting | Formatting of citations in the literature matrix | Each citation was checked against the source paper's title, authors, and venue |
| Statistical-method explanation | Describing McNemar and bootstrap procedures | Cross-checked against Dietterich (1998) and Efron & Tibshirani (1993) |

---

## 3. What AI Was NOT Used For

- Generating the dataset or any labels.
- Writing the model code (all classifiers, pipelines, and preprocessing were
  written and run by me in the notebook).
- Producing the reported metrics, confusion matrices, or figures.
- Running the McNemar test or the bootstrap — both were executed in code with
  fixed seeds and the outputs are visible in the notebook.
- Generating any citation without verification. Each reference in
  `docs/literature_matrix.md` and the manuscript's References section was
  looked up to confirm title, authors, and year.

---

## 4. Verification Approach

For every AI-assisted artifact:

1. **I read it against the notebook.** Numbers, model names, features, and
   metrics were checked line by line.
2. **I checked references** by searching each title on Google Scholar and the
   publisher's site.
3. **I rewrote or removed anything** that did not match what the code actually
   does. Several placeholder claims in early drafts (e.g. vague dataset
   provenance) were replaced with the exact CB2 source from Ejaz et al.
4. **I take full responsibility** for every claim, figure, and metric in the
   submission. If a number or citation is wrong, it is my error, not the
   tool's.

---

## 5. Honest Limitations of This Disclosure

- I cannot prove a negative — I can only state what I used and how I verified
  it.
- The AI tool may have suggested phrasings I did not fully notice were
  awkward; I reviewed all text before committing.
- Where the AI drafted text that did not match the code, I corrected the text,
  not the code.

---
