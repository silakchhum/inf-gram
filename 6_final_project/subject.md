# INF-GRAM — Final project

## Objectives

The final project evaluates your ability to build a **complete and defensible machine-learning workflow**.

You should be able to:

1. import and audit an unfamiliar biomedical dataset;
2. perform descriptive analysis;
3. build several classification models;
4. tune models without leaking information from the test set;
5. compare models using appropriate metrics;
6. justify a final choice and discuss its limitations.

## Context

The dataset contains biomechanical measurements related to vertebral-column conditions.

The original three classes are:

- **DH** — Disk Hernia;
- **SL** — Spondylolisthesis;
- **NO** — Normal.

For this project, use a binary target:

- **0 = Normal (NO)**;
- **1 = Abnormal (DH or SL)**.

Keep this coding explicit throughout the notebook.

## Data

Use `column_3C.txt`.

Each patient has six biomechanical predictors:

- pelvic incidence;
- pelvic tilt;
- lumbar lordosis angle;
- sacral slope;
- pelvic radius;
- degree of spondylolisthesis.

The target is the diagnosis class.

---

# Methodological rule: keep the test set untouched

This rule is part of the assessment.

1. Create one stratified train/test split near the beginning.
2. Use **training data only** for:
   - preprocessing;
   - feature scaling;
   - hyperparameter tuning;
   - model selection;
   - threshold selection.
3. Use cross-validation inside the training set.
4. Evaluate the selected models on the test set only after the modeling choices are fixed.

Do not repeatedly modify a model after looking at its test performance.

Use a fixed random seed such as:

```python
SEED = 42
```

---

# Task 1 — Import and data audit

1. Import the required Python libraries.
2. Load `column_3C.txt`.
3. Display:
   - first rows;
   - number of rows and columns;
   - data types;
   - missing-value counts;
   - class counts.
4. Create the binary target:
   - `0 = Normal`;
   - `1 = Abnormal`.
5. Display the class balance as both a table and a graph.
6. Separate predictors `X` and target `y`.

---

# Task 2 — Descriptive analysis

For the six predictors:

1. report mean, standard deviation, median and interquartile range;
2. report these summaries by class;
3. visualize distributions by class;
4. compute and visualize the correlation matrix;
5. identify at least two notable relationships or differences and describe them in words.

The objective is to understand the data **before** fitting a model.

---

# Task 3 — Development / test split

Create a stratified split:

- 80% training;
- 20% test.

Report class proportions in both sets.

From this point, do not inspect the test labels for model development.

---

# Task 4 — Baseline model: logistic regression

Build a scikit-learn `Pipeline` containing:

1. `StandardScaler`;
2. `LogisticRegression`.

Use cross-validation on the training set to select a reasonable value of the
regularization hyperparameter.

Report cross-validation performance.

Do not tune on the test set.

---

# Task 5 — Two additional model families

Choose **two** model families among:

- SVM;
- decision tree;
- random forest;
- gradient boosting;
- k-nearest neighbors;
- another model justified from the course.

For each family:

1. explain why it is a reasonable candidate;
2. create an appropriate pipeline;
3. identify the hyperparameters you will tune;
4. tune them with cross-validation on the training set;
5. report the selected hyperparameters and cross-validation score.

Use the same primary selection metric for all three model families.

---

# Task 6 — Final test-set comparison

After model selection is complete, evaluate the three selected models on the
untouched test set.

Report at least:

- confusion matrix;
- sensitivity / recall for the abnormal class;
- specificity;
- precision;
- F1 score;
- ROC AUC.

Use predicted probabilities or decision scores for ROC AUC.

Create one comparison table with one row per model.

---

# Task 7 — Probability and threshold analysis

For your best probability-producing model:

1. draw the ROC curve;
2. draw the precision-recall curve;
3. inspect at least two possible classification thresholds;
4. explain how changing the threshold changes false positives and false negatives.

You do **not** need to claim a universally optimal threshold.

Explain which error would be more concerning in this clinical context and why.

---

# Task 8 — Final model and limitations

Choose the model you would retain **for this project**.

Your justification should consider:

- test performance;
- sensitivity / specificity trade-off;
- model complexity;
- interpretability;
- stability;
- small sample size.

Then discuss at least three limitations, for example:

- single small dataset;
- no external validation;
- simplified binary target;
- unknown sampling mechanism;
- possible dataset shift;
- no prospective clinical evaluation.

A higher test score alone is not a sufficient argument for clinical deployment.

---

# Submission

Submit one Jupyter notebook on Amétice containing:

- executable code;
- figures and tables;
- Markdown explanations;
- all answers and interpretations.

The notebook must run from top to bottom without manual intervention.

## Oral examination

During the oral examination you may be asked to:

- execute part of the notebook;
- explain the train/test and cross-validation strategy;
- explain one hyperparameter;
- interpret a confusion matrix or ROC curve;
- modify a small piece of code;
- justify your final model choice.

The objective is to assess understanding, not only whether the notebook produces a high score.
