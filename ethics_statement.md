# Ethics Statement
---

## 1. Purpose and Scope

This project is coursework for DCIT 316. It compares three classical machine
learning classifiers (logistic regression, linear SVM, random forest) across
three feature configurations (text, context, combined) for conversation-level
cyberbullying detection. It is a research exercise, not a deployed system.

---

## 2. Data Ethics

### 2.1 Source

The CB2 dataset is semi-synthetic. Message text comes from a publicly released
cyberbullying corpus (Elsafoury, 2020); user attributes are generated
(Ejaz et al., 2023, 2024). No new data was collected. No human participants
were recruited. No interaction with real people occurred.

### 2.2 Privacy

- **Participant identifiers are already pseudonymised** as integers 1–100. No
  names, emails, handles, or other direct identifiers are present.
- **The dataset is not redistributed** in this repository. Only the code that
  reads the Parquet files is published. This respects the dataset authors'
  terms and prevents accidental re-identification.
- **Notebook outputs** that would have echoed raw conversation text were cleared
  before the final commit. The manuscript masks or paraphrases illustrative
  examples rather than quoting harmful language verbatim.

### 2.3 Sensitive Content

The conversation texts contain slurs, profanity, threats, and personal attacks.
Handling:

- No raw text appears in any published figure or table.
- The manuscript quotes only masked fragments where necessary to illustrate a
  point.
- Any reviewer reading the code understands in advance that the data contains
  harmful language.

### 2.4 No Credentials

No passwords, API keys, tokens, or personal access credentials are stored in
the repository or in the manuscript.

---

## 3. Fairness and Responsible Use

### 3.1 Sensitive Attributes as Features

The context and combined models use `user1_age`, `user1_grade`,
`user1_gender`, `user2_age`, `user2_grade`, and `user2_gender` as inputs.
This is defensible for research into *how context affects detection*, but it
must not be taken as an endorsement of using demographic attributes to make
decisions about people.

Any real system that flags individuals based on age, gender, or grade raises
serious fairness concerns — particularly when those individuals are minors,
as in CB2.

### 3.2 Non-Deployment

Predictions from these models are not explanations and must not be presented as
evidence that a specific person bullied another. The models have:

- Low precision on the positive class (0.34–0.76 across configurations).
- Known data limitations (semi-synthetic construction, user-level leakage,
  heavy class imbalance).
- No calibration guarantees.

They are unsuitable for content moderation, disciplinary action, or any
decision affecting real users.

### 3.3 Label Construction

CB2 labels are derived from thresholds on `peerness`, `intent_to_harm`, and
`aggressive_count` (Ejaz et al., 2024). Context features used in this project
overlap with those rules. This is disclosed in the manuscript and model card,
because it means the measured benefit of context is partly circular and may
not transfer to real conversations.

---

## 4. Research Integrity

- The notebook reports exactly the results it produces. No metrics are
  adjusted or selected post hoc.
- The nine-model grid (3 classifiers × 3 feature sets) is reported in full,
  including weak models (random forest with text: F1 0.075).
- Hypotheses H1, H2, H3 were stated before results were interpreted. H3 was
  reported as *partly* supported because random forest contradicts it.
- The gain from context (SVM text → combined) is reported with a bootstrap
  interval and an exact McNemar p-value, not as a bare number.
- Limitation section acknowledges the risk that the reported gain reflects
  label construction rather than a general property of context.

---

## 5. AI Use

Large language model assistance was used for documentation drafting and code
review. The full disclosure is in `docs/ai_use_disclosure.md`.

---
