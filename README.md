# Cyberbullying Detection Using Machine Learning
A controlled comparison of three classifiers (logistic regression, linear SVM,
random forest) across three feature configurations (text, context, combined)
for conversation-level cyberbullying detection.

---

## Research question

Does adding contextual user and conversation features to message text improve
cyberbullying detection compared with text alone?

## Key result

Adding context raised the linear SVM's cyberbullying F1 from **0.444** to
**0.662** (95% bootstrap CI [0.153, 0.284]; exact McNemar p = 2.99 × 10⁻¹¹).
Context-only models outperformed text-only models for every classifier, and
random forest on context alone gave the highest F1 (**0.696**).

---

## Repository structure

```
.
├── README.md
├── requirements.txt
├── cyberbullyingmodel.ipynb          # the experiment
├── figure_1_class_distribution.png
├── figure_2_f1_comparison.png
├── figure_3_precision_recall.png
├── figure_4a_svm_text_confusion_matrix.png
├── figure_4b_svm_combined_confusion_matrix.png
├── figure_5_methodology_pipeline.png
├── table_statistical_comparison.csv
├── docs/
│   ├── data_card.md
│   ├── model_card.md
│   ├── literature_matrix.md
│   ├── ethics_statement.md
│   ├── ai_use_disclosure.md
│   ├── failure_log.md
│   └── reproducibility_checklist.md
└── metrics/
    ├── results.csv
    └── table_statistical_comparison.csv
```

---

## Models

| Classifier | Configuration |
|---|---|
| Logistic Regression | `max_iter=1000`, `class_weight="balanced"`, seed 42 |
| Linear SVM | `LinearSVC`, `class_weight="balanced"`, seed 42 |
| Random Forest | `n_estimators=300`, `class_weight="balanced"`, seed 42 |

## Feature configurations

- **Text:** TF-IDF, `max_features=10000`, `ngram_range=(1, 2)`
- **Context:** `total_messages`, `peerness`, `user1_age`, `user1_grade`,
  `user2_age`, `user2_grade`, `user1_gender`, `user2_gender`
- **Combined:** text and context concatenated

---

## Results (test set, n = 1189, 121 positives)

| Classifier | Features | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|---|
| Random Forest | Context | 0.943 | 0.757 | 0.645 | **0.696** |
| Linear SVM | Combined | 0.919 | 0.577 | 0.777 | **0.662** |
| Logistic Regression | Combined | 0.881 | 0.453 | 0.843 | 0.590 |
| Logistic Regression | Context | 0.854 | 0.403 | 0.909 | 0.558 |
| Linear SVM | Context | 0.854 | 0.404 | 0.901 | 0.558 |
| Logistic Regression | Text | 0.826 | 0.342 | 0.769 | 0.473 |
| Linear SVM | Text | 0.857 | 0.368 | 0.562 | 0.444 |
| Random Forest | Combined | 0.899 | 0.545 | 0.050 | 0.091 |
| Random Forest | Text | 0.897 | 0.417 | 0.041 | 0.075 |

---

## Figures

| Figure | File |
|---|---|
| Figure 1 — Pipeline | [`figure_5_methodology_pipeline.png`](figure_5_methodology_pipeline.png) |
| Figure 2 — Class distribution | [`figure_1_class_distribution.png`](figure_1_class_distribution.png) |
| Figure 3 — F1 by classifier and features | [`figure_2_f1_comparison.png`](figure_2_f1_comparison.png) |
| Figure 4 — Precision–recall trade-off | [`figure_3_precision_recall.png`](figure_3_precision_recall.png) |
| Figure 5a — SVM text confusion matrix | [`figure_4a_svm_text_confusion_matrix.png`](figure_4a_svm_text_confusion_matrix.png) |
| Figure 5b — SVM combined confusion matrix | [`figure_4b_svm_combined_confusion_matrix.png`](figure_4b_svm_combined_confusion_matrix.png) |

---

## Reproduce

```bash
git clone https://github.com/amoakoantwimaaafia2-0/cyberbullying-detection-ml
cd cyberbullying-detection-ml
pip install -r requirements.txt
# Place the three CB2 .parquet files in this directory
jupyter notebook cyberbullyingmodel.ipynb
```

Full procedure and verification checks:
[`docs/reproducibility_checklist.md`](docs/reproducibility_checklist.md)

---

## Data

The CB2 dataset is **not redistributed** here. Source: Ejaz, Choudhury &
Razi (2023, 2024). Message text from Elsafoury (2020). The dataset is
semi-synthetic: text is real, user attributes are generated. See
[`docs/data_card.md`](docs/data_card.md).

## Ethics

See [`docs/ethics_statement.md`](docs/ethics_statement.md). In short:
identifiers are pseudonymised, the dataset is not redistributed, and this
project is **not suitable for deployment** — models are not calibrated, the
data is semi-synthetic, and all 100 users appear in every split.

## AI use

See [`docs/ai_use_disclosure.md`](docs/ai_use_disclosure.md).

## Limitations and failures

See [`docs/failure_log.md`](docs/failure_log.md) and
[`docs/model_card.md`](docs/model_card.md). Notable failures: random forest
collapses on text features (recall < 0.05), `peerness` is missing ~49% of the
time, and all 100 users appear in every split.

---

## References

- Ejaz, N., Choudhury, S. & Razi, F. (2023). *Towards comprehensive
  cyberbullying detection*. Computers in Human Behavior, 108123.
- Ejaz, N., Choudhury, S. & Razi, F. (2024). *A multi-faceted semi-synthetic
  dataset for automated cyberbullying detection*. arXiv:2402.10231.
- Elsafoury (2020). *Cyberbullying datasets*. Mendeley Data.
- Tahmasbi, N. & Rastegari, E. (2018). *A socio-contextual approach in
  automated detection of cyberbullying*. HICSS-51.

Full list in [`docs/literature_matrix.md`](docs/literature_matrix.md).

---

## Contact

Maa Afia Amoako-Antwi — Student ID 22049822
