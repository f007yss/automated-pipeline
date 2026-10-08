# Automated Analysis Pipeline Exploration

HSE 751 Week 3. Jeremy Childress.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/11eI2sKGsSCtdYD1Swevn5DaMhfaR4Tjr?usp=sharing)

## Purpose

This notebook runs an automated analysis pipeline on the Pima Indians Diabetes data. It covers data ingestion, missing-value handling, exploratory analysis, inferential tests, and classification models for the diabetes outcome. The notebook explains how the pipeline's conditional logic makes decisions and adds four modifications.

1. Automated choice between Welch's t-test and Mann-Whitney U for each predictor, based on skewness, with a Bonferroni correction
2. An `ANALYSIS_GOAL` setting that controls the decision tree tuning metric (F2 or F1) and the logistic regression cutoff (80% sensitivity target or Youden's J)
3. Automatic class weighting when the minority class is under 40% of the training data
4. A random forest added to the model comparison, plus one ROC plot for all models

## Files

- `Automated_Analysis_Pipeline_Childress.ipynb` is the notebook
- `Example Dataset_Diabetes.csv` is the dataset (CSV is the original format)

## How to Run

1. Open the notebook in Colab with the badge above.
2. Runtime > Run all.
3. Upload `Example Dataset_Diabetes.csv` when the upload button appears in the ingestion cell.

The settings cell near the top controls the seed, alpha, analysis goal, and cutoffs. Setting `ANALYSIS_GOAL = "balanced"` reproduces the original notebook's ML results.

## Requirements

Tested in Google Colab. Uses pandas, numpy, matplotlib, seaborn, scipy, statsmodels, scikit-learn, and phik. Everything except phik is preinstalled on Colab, and the notebook installs phik itself.

## Assumptions and Limitations

- Zeros in Glucose, D_BP, Skin_Thickness, Insulin, and BMI are treated as missing and filled with training-set medians inside each model pipeline. Insulin and Skin_Thickness are missing for a large share of patients.
- The split is 70/30, stratified, with seed 42. The test set has 231 patients, so metrics would shift somewhat with a different split.
- The 1.0 skewness cutoff and the 0.40 class-share rule are judgment calls, not standard values.
- The sample is female, Pima Indian heritage, age 21+, and results may not generalize.
- Results are associations, not causes. For instructional use only.
