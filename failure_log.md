# Failure Log

This log records what did not work, what was tried, and what was learned.

---

## 1. Random forest with text features collapsed on the minority class

**What was tried.** Random forest (300 trees, `class_weight="balanced"`) on
TF-IDF text features and on combined text+context features.

**What happened.** On the test set:
- RF text: recall on cyberbullying = 0.041 (found 5 of 121 cases)
- RF combined: recall = 0.050 (found 6 of 121 cases)

Accuracy remained high (0.897 and 0.899), which makes the failure easy to miss
if only accuracy is reported.

**Likely cause (not proven).** Sparse TF-IDF features (up to 10,000 dimensions)
dilute the smaller number of informative context features inside each tree
split. Balanced class weights reweight the loss but do not change how splits
are chosen.

**Decision.** Reported as a genuine negative result. The manuscript flags it
explicitly rather than hiding it. No attempt was made to force RF to work with
text; that would have required feature selection or dimensionality reduction,
which was out of scope for this study.

**What would be tried next.** Feature selection on TF-IDF, using `max_features`
far smaller, or using a linear model in front of RF. See §7 for future work.

---

## 2. `peerness` is missing for ~49% of training conversations

**What was tried.** Median imputation inside a scikit-learn pipeline, fitted on
the training split only.

**What happened.** The context-only and combined models still work, but the
imputation fills half of the `peerness` column with a single constant value.
Any model gain attributed to `peerness` is partly a gain from "is this value
missing or not", which is an unintended artifact.

**Decision.** Disclosed as a limitation. Kept the feature because the notebook
correctly excludes `aggressive_count` and `intent_to_harm` (which would be
direct leakage) and `peerness` is the least-leaky of the label-derived
features. Also noted that CB2's label construction itself uses `peerness`, so
some circularity is unavoidable on this dataset.

**What would be tried next.** Add an explicit missingness indicator for
`peerness`, or model it separately. Test with and without `peerness` to
isolate its contribution.

---

## 3. H3 was only partly supported

**Hypothesis.** For every classifier, combined features outperform context-only
features.

**What happened.**
- LR: 0.590 combined vs. 0.558 context → supported
- SVM: 0.662 combined vs. 0.558 context → supported
- RF: 0.091 combined vs. 0.696 context → **not supported** (huge drop)

The hypothesis holds for linear models but fails badly for random forest, for
the same reason as §1.

**Decision.** Reported as "partly supported" rather than dropping RF from the
analysis. The exception is informative.

**What would be tried next.** Restrict H3's scope to linear models, or run RF
with a smaller, denser text representation.

---

## 4. User-level leakage across splits

**What was tried.** Checked whether user pairs and users overlap across splits.

**What happened.**
- Pairs: 0 overlap (good).
- Users: all 100 users appear in all three splits.

**Decision.** This is a property of CB2 as distributed, not something introduced
by the project. Disclosed as a limitation. Test metrics are optimistic relative
to a strict user-disjoint evaluation. No attempt was made to re-split the data
because that would break comparability with the released benchmark.

**What would be tried next.** A user-disjoint split to measure how much of the
reported performance is user-specific.

---

## 5. Single seed, no hyperparameter tuning

**What was tried.** Default hyperparameters and seed 42 for all models. No
grid search.

**What happened.** Two configurations reached F1 = 0.558 (LR context, SVM
context). Whether the tie is real or an artifact of the single seed is unknown.

**Decision.** Explicitly stated as a limitation. Differences smaller than the
bootstrap CI width ([0.153, 0.284]) are not treated as meaningful.

**What would be tried next.** Repeated runs with multiple seeds; report mean
and standard deviation. A small grid search on `C` for SVM and on
`n_estimators` / `max_features` for RF.

---

## 6. No network features

**What was tried.** Reviewed CB2's columns for a social-graph or interaction
history signal.

**What happened.** CB2 has no network graph — no follower/following structure,
no centrality metrics, no interaction history. The source paper's network
features (degree, closeness, betweenness) could not be reproduced.

**Decision.** Documented in the manuscript. The project compares text vs.
tabular context instead of text vs. network context.

**What would be tried next.** A dataset with a real social graph and repeated
interactions, to test the source paper's network hypothesis directly.

---

## 7. Summary of what the failures taught

1. Random forest is the wrong tool for very sparse text in this setting.
2. Half-missing `peerness` is a real caveat that limits how much of the context
   gain should be attributed to peer similarity itself.
3. H3's failure for RF is the most informative negative result in the study.
4. CB2's split design (pair-disjoint, user-shared) is a benchmark property that
   future work must contend with.
5. Reporting the failures honestly is more useful than hiding them behind a
   single "best model" headline.

---

