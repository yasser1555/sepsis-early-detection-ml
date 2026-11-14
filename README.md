<div align="center">

# Early Detection of Sepsis in ICU Patients

**Machine Learning · Imbalanced Classification · Healthcare Analytics**

An academic machine-learning study comparing classification models on ICU records, with a focus on detecting the minority sepsis class.

[View Notebook](notebooks/Sepsis_Early_Detection.ipynb) · [Results](#results-from-the-saved-experiment) · [Dataset Source](https://physionet.org/content/challenge-2019/1.0.0/training/) · [Developer Portfolio](https://yasser-alassad-portfolio.vercel.app/)

</div>

---

## Overview

Sepsis is a serious condition for which timely recognition matters. For this **CS4082 Machine Learning** course assignment at **Effat University (Spring 2026)**, I independently implemented a workflow to study class imbalance in ICU data and compare machine-learning approaches using patient-level features constructed from hourly clinical measurements. The assignment was formally submitted as group coursework.

> **Scope:** The saved experiment predicts **whether a patient was labeled with sepsis over their recorded ICU stay** using aggregates computed from the **entire stay**. It is **not a prospectively validated early-warning model** and should not be used for diagnosis or clinical decisions.

## Dataset at a Glance

| Property | Saved experiment |
|---|---:|
| Source | PhysioNet / CinC Challenge 2019 |
| Hourly observations | 1,552,210 |
| Patients | 40,336 |
| Patients with sepsis | 2,932 (7.27%) |
| Patients without sepsis | 37,404 (92.73%) |
| Train / test | 32,268 / 8,068 patients |
| Patient-level input features | 34 after engineering |

The workflow aggregates vital signs (e.g., heart rate, oxygen saturation, temperature, blood pressure and respiratory rate) into summary statistics such as mean, standard deviation, minimum and maximum. It then applies imputation, feature scaling and **SMOTE** to address the underrepresented positive class.

![Sepsis class distribution before and after SMOTE](figures/smote_class_balance.png)

## Methods

- **Feature engineering:** Patient-level summaries from hourly measurements.
- **Preprocessing:** Median imputation and standardization.
- **Imbalance handling:** SMOTE applied to the training data; selected classifiers use class weights.
- **Models compared:** Logistic Regression, Decision Tree, Random Forest, SVM, KNN, Naive Bayes and Gradient Boosting. Additional ensemble experiments include voting, bagging and AdaBoost.
- **Evaluation:** Held-out patient-level test split, ROC-AUC, class-specific F1 and macro-averaged metrics.

## Results from the Saved Experiment

The following results are **transcribed from the notebook's saved outputs**. They were not independently rerun or audited as part of preparing this repository.

| Model | ROC-AUC | F1 (sepsis) | F1 (macro) |
|---|---:|---:|---:|
| **Random Forest** | **0.8644** | **0.5088** | **0.7296** |
| SVM | 0.8323 | 0.4010 | 0.6658 |
| Gradient Boosting | 0.8074 | 0.1428 | 0.1354 |
| Naive Bayes | 0.7597 | 0.2900 | 0.5787 |
| KNN | 0.7505 | 0.2968 | 0.5894 |
| Logistic Regression | 0.7491 | 0.2594 | 0.5472 |
| Decision Tree | 0.6310 | 0.1970 | 0.4724 |

For the saved Random Forest evaluation, the **sepsis class** has precision ≈ **0.42** and recall ≈ **0.64** on the reported test split. These are much more informative than raw accuracy alone in an imbalanced medical classification task.

### Visual Results

**ROC curves**

![ROC curves of model predictions](figures/roc_curves.png)

**Confusion matrices**

![Confusion matrices for classifiers](figures/confusion_matrices.png)

**Feature importance (Random Forest)**

![Random Forest feature importance](figures/feature_importance.png)

[See precision–recall curves](figures/precision_recall_curves.png).

## Reproducibility

The notebook was originally developed in **Google Colab** and prompts you to upload a CSV dataset. The repository deliberately excludes the two large CSV exports and generated model checkpoints.

1. Obtain the project's **preprocessed** `Dataset.csv` (see [data instructions](data/README.md)). It is not the same format as the raw downloaded PhysioNet `.psv` files.
2. Open [`notebooks/Sepsis_Early_Detection.ipynb`](notebooks/Sepsis_Early_Detection.ipynb) in Google Colab.
3. Upload `Dataset.csv` when prompted in the first data-loading cell.
4. Run the cells in order; some model-training steps (particularly SVM and cross-validation) can be computationally expensive.

Dependencies are in [`requirements.txt`](requirements.txt). The **original notebook code and saved results are preserved**, aside from the GitHub publication note at the top and a clearer filename.

## Limitations and Research Integrity

These limitations matter when interpreting the saved performance metrics:

- **Look-ahead bias:** Features summarize patients' *complete* ICU stays, including observations that would not have been available at an earlier decision time. This prevents a claim of validated real-time sepsis prediction.
- **Optimistic cross-validation:** Parts of the notebook apply SMOTE before cross-validation; synthetic observations may influence different folds. A robust follow-up should put preprocessing and resampling **inside each training fold**.
- **Test-set reuse:** One experimental section selects a tuned model using test-set accuracy. That section is exploratory and should not be treated as an unbiased final assessment.
- **Limited clinical validation:** Models were evaluated on the provided retrospective dataset, not prospectively or on a new external clinical cohort.

The saved results should be treated as **academic, exploratory findings**, not production or medical performance guarantees.

## Repository Contents

```text
README.md
notebooks/
  Sepsis_Early_Detection.ipynb
figures/
  smote_class_balance.png
  roc_curves.png
  confusion_matrices.png
  precision_recall_curves.png
  feature_importance.png
data/
  README.md
requirements.txt
.gitignore
```

## Project Implementation & Academic Context

**Developer: Yasser Alassad** — Independently completed the project's technical implementation, including data preparation, exploratory analysis, feature engineering, class-imbalance handling, model training and tuning, evaluation, and visualizations.

**Academic context:** This work was submitted as part of a group-assigned **CS4082 Machine Learning** course project at **Effat University (Spring 2026)**. The group submission format does not represent a division of the implementation work.

The implementation attribution above reflects the developer's firsthand account. The notebook's original model outputs are preserved; see [Limitations and Research Integrity](#limitations-and-research-integrity).

## Dataset Attribution

Data derived from: **Reyna et al., "Early Prediction of Sepsis from Clinical Data: The PhysioNet/Computing in Cardiology Challenge 2019."**

- [PhysioNet dataset / challenge page](https://physionet.org/content/challenge-2019/1.0.0/training/)
- DOI: [10.13026/v64v-d857](https://doi.org/10.13026/v64v-d857)
- Source dataset license: [CC BY 4.0](https://physionet.org/content/challenge-2019/view-license/1.0.0/)

## About the Developer

**Yasser Alassad** — B.Sc. Computer Science student, Artificial Intelligence specialization, Effat University.

[GitHub](https://github.com/yasser1555) · [LinkedIn](https://www.linkedin.com/in/yasser-alassad/) · [Portfolio](https://yasser-alassad-portfolio.vercel.app/)
