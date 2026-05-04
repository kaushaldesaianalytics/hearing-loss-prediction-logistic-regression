# Hearing Loss Prediction
## Logistic Regression Classification

Can a patient's age and physical health score reliably predict whether they will pass a hearing test? This project builds a binary logistic regression classifier on a clinical dataset of 5,000 participants, with full evaluation including coefficient interpretation, confusion matrix analysis, and ROC/AUC scoring.

---

## Overview

Logistic regression models the probability that an observation belongs to a class by applying a sigmoid function to a linear combination of features. Unlike linear regression, the output is bounded between 0 and 1 and interpreted as a probability. Coefficients are expressed as log-odds, which can be converted to odds ratios for direct clinical interpretation.

This project demonstrates the end-to-end logistic regression workflow: exploratory data analysis, feature scaling, model fitting, coefficient interpretation, and threshold analysis via precision-recall and ROC curves.

---

## Dataset

The dataset contains records from a study of 5,000 participants, tracking age, a composite physical health score, and the binary outcome of a standardized hearing test.

| Feature | Description |
|---|---|
| age | Patient age in years |
| physical_score | Composite physical health score |
| test_result | Binary target: 1 = pass, 0 = fail |

---

## Workflow

**1. Exploratory Data Analysis**
Distribution analysis, correlation heatmap, and feature-vs-outcome visualizations establish the baseline relationships between age, physical score, and hearing test outcome. Boxplots show both features differ meaningfully across outcome classes, confirming their predictive signal.

**2. Train/Test Split and Scaling**
A 90/10 train/test split preserves a meaningful held-out evaluation set. StandardScaler normalizes both features to zero mean and unit variance, improving logistic regression convergence and making coefficients more directly comparable.

**3. Model Fitting**
A logistic regression model is fit on the scaled training data. Coefficients are reported as both raw log-odds and exponentiated odds ratios, providing a clinically interpretable view of how each unit increase in age or physical score shifts the odds of passing.

**4. Model Evaluation**
Performance is assessed via accuracy, a confusion matrix, and a full classification report. The confusion matrix breaks down true and false positives and negatives, which is more informative than accuracy alone when the cost of false negatives (missed hearing loss) differs from false positives.

**5. Threshold Analysis**
The precision-recall curve shows the tradeoff between catching more positive cases (higher recall) and maintaining prediction confidence (higher precision). The ROC curve and AUC score summarize the model's ability to discriminate between classes across all possible decision thresholds.

---

## Results

| Metric | Value |
|---|---|
| Accuracy | ~92% |
| AUC | ~0.97 |

The model achieves strong discrimination between pass and fail outcomes, with AUC close to 1.0 indicating robust class separation across thresholds.

---

## Key Concepts

**Log-Odds and Odds Ratios:** Logistic regression outputs log-odds, which are difficult to interpret directly. Exponentiating a coefficient gives the odds ratio, showing how much the odds of a positive outcome multiply per one-unit increase in that feature.

**Precision vs. Recall Tradeoff:** In a clinical context, missing a patient who will fail the hearing test (false negative) may carry a higher cost than an unnecessary follow-up (false positive). The precision-recall curve allows selecting a threshold that reflects this asymmetry.

**AUC as a Threshold-Independent Metric:** Unlike accuracy, AUC does not depend on a fixed 0.5 decision threshold. It measures how well the model ranks positive cases above negative ones across all thresholds.

---

## Stack

- Python 3
- Pandas, NumPy
- Matplotlib, Seaborn, mpl_toolkits (3D scatter)
- scikit-learn (LogisticRegression, StandardScaler, ConfusionMatrixDisplay, PrecisionRecallDisplay, RocCurveDisplay)

---

## File Structure

```
hearing-loss-logistic-regression/
├── logistic_regression_hearing.ipynb   # Main project notebook
├── hearing_test.csv                    # Dataset
└── README.md
```

---

## How to Run

1. Clone the repository
2. Install dependencies: `pip install pandas numpy matplotlib seaborn scikit-learn`
3. Open `logistic_regression_hearing.ipynb` in Jupyter and run all cells
