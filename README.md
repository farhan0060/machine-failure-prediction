# Machine Failure Prediction — AI4I 2020

A machine-failure classification project using the AI4I 2020 Predictive Maintenance Dataset. The notebook compares Logistic Regression and Random Forest, evaluates imbalanced-class performance, selects a decision threshold using training-only out-of-fold predictions, and explores feature importance and operating measurements.

## Project Structure
- `data/`: dataset instructions (the CSV is not included)
- `notebooks/Machine_Failure_Prediction.ipynb`: complete analysis
- `reports/Machine_Failure_Prediction.pdf`: project report
- `requirements.txt`: Python dependencies

## Dataset
Download the AI4I 2020 Predictive Maintenance dataset and place the CSV at `data/ai4i2020.csv`. See [data/README.md](data/README.md). The dataset is not bundled with this repository.

## Methods
- Remove `UDI` and `Product ID`.
- Exclude `TWF`, `HDF`, `PWF`, `OSF`, and `RNF` to reduce target leakage.
- Use a stratified train/test split.
- Apply polynomial numeric features and one-hot encoding for `Type`.
- Train Logistic Regression and Random Forest classifiers.
- Evaluate with stratified five-fold cross-validation.
- Select an F1-oriented threshold from training out-of-fold predictions.
- Evaluate on the held-out test set.
- Inspect feature importance and torque/tool-wear relationships.

## Run
1. Clone this repository.
2. Install dependencies: `pip install -r requirements.txt`.
3. Download the dataset and place `ai4i2020.csv` in `data/`.
4. Open `notebooks/Machine_Failure_Prediction.ipynb` in Jupyter.
5. Run the notebook from top to bottom.

## Evaluation
The notebook reports precision, recall, F1-score, ROC-AUC, PR-AUC, and confusion matrices. Accuracy is not treated as the only measure because failures are rare.

## Limitations
Threshold selection is based on training OOF predictions, not the test set. Results are specific to this dataset and split and do not guarantee performance on another factory or time period. Impurity-based feature importance is exploratory and does not imply causality. Torque and tool wear are exploratory proxies, not validated failure mechanisms.

## License
No license is specified. Add a license file if you want to define reuse permissions.
