# Machine Failure Prediction — Project Report

## Objective
Build a binary classifier to identify machine failures from operating measurements in the AI4I 2020 Predictive Maintenance dataset.

## Data preparation
- Remove identifier columns: `UDI` and `Product ID`.
- Exclude `TWF`, `HDF`, `PWF`, `OSF`, and `RNF` because they encode failure reasons and may leak target information.
- Preserve `Type` as a categorical feature.
- Use a stratified 80/20 train/test split.

## Modeling
Two pipelines are compared:
1. Logistic Regression with degree-two polynomial numeric features, standardization, and one-hot encoding.
2. Random Forest with degree-two polynomial numeric features and one-hot encoding.

Preprocessing is included in each pipeline to avoid fitting transformations outside the training folds.

## Evaluation strategy
The target is imbalanced. Precision, recall, F1-score, ROC-AUC, PR-AUC, and confusion matrices are therefore reported rather than relying on accuracy alone. Five-fold stratified cross-validation is performed on the training set. The decision threshold is selected from training out-of-fold probabilities and then applied to the held-out test set.

## Selected observations
Previously recorded Random Forest results on the held-out split:
- At threshold 0.50: precision 0.941, recall 0.706, F1 0.807.
- At a tuned threshold around 0.44: precision 0.895, recall 0.750, F1 0.816.

These figures are historical notebook outputs and should be reproduced by running the notebook in the specified environment before being treated as final.

## Limitations
Threshold selection should reflect the relative operational cost of missed failures and false alarms. Results are dataset- and split-specific and require external validation before industrial deployment. Impurity-based feature importance is exploratory, not causal. Torque and tool-wear relationships do not independently validate a physical failure mechanism.

## Reproducibility
Download the AI4I 2020 CSV separately and place it at `data/ai4i2020.csv`. Install the packages listed in `requirements.txt`, then run the notebook from top to bottom.
