# Stroke Prediction System

A machine-learning project that explores patient health and demographic data and compares classification models for predicting the stroke label in a public healthcare dataset.

> **Important:** This is an educational data-science project, not a medical device or clinical decision-support system. Predictions must not be used to diagnose, screen, or make treatment decisions.

## Project objectives

- Inspect and clean the healthcare dataset.
- Explore demographic and health-related patterns in the data.
- Prepare numerical and categorical features for machine learning.
- Train and compare Logistic Regression and Random Forest classifiers.
- Evaluate performance with metrics suited to an imbalanced classification problem.
- Save trained pipelines for reproducibility.

## Dataset

The project uses the **Healthcare Dataset Stroke Data** CSV file, commonly distributed as `healthcare-dataset-stroke-data.csv`.

The dataset is not included in this repository. Obtain it from the source where you accessed it, then place the CSV at:

```text
data/raw/healthcare-dataset-stroke-data.csv
```

The notebook expects that exact path. Do not upload patient-level data unless you have confirmed that its license and privacy terms allow redistribution.

## Repository structure

```text
Stroke-Prediction-system/
├── data/
│   └── raw/                 # Place the dataset here (not committed)
├── models/                  # Saved model pipelines (created when notebook runs)
├── visualizations/          # Charts exported by the notebook
├── notebooks/
│   └── stroke_prediction.ipynb
├── .gitignore
├── README.md
└── requirements.txt
```

## Tools and libraries

- Python
- Pandas and NumPy
- Matplotlib and Seaborn
- Scikit-learn
- Joblib
- Jupyter Notebook

## How to run

1. Clone this repository:
   ```bash
   git clone https://github.com/gaurikotwal/Stroke-Prediction-system.git
   cd Stroke-Prediction-system
   ```
2. Create and activate a virtual environment (recommended).
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Put the CSV dataset at `data/raw/healthcare-dataset-stroke-data.csv`.
5. Launch Jupyter:
   ```bash
   jupyter notebook
   ```
6. Open `notebooks/stroke_prediction.ipynb` and run the cells from top to bottom.

## Dataset overview

In the run shared during project development:

- Total records: **5,110**
- Stroke-positive records: **249**
- Stroke-negative records: **4,861**
- Mean age: **43.23**
- Mean average glucose level: **106.15**
- Mean BMI after mean imputation: **28.89**

The target is highly imbalanced: approximately **4.87%** of records are stroke-positive. Accuracy alone is therefore not a sufficient measure of model quality.

## Model results

The following are the metrics reported from the project's 80/20 stratified train/test split (random state 42):

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC | PR-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Logistic Regression | 74.56% | 13.79% | 80.00% | 23.53% | 0.8437 | 0.2682 |
| Random Forest | 91.39% | 14.81% | 16.00% | 15.38% | 0.7978 | 0.1719 |

### Interpretation

- Random Forest achieved higher accuracy, but detected a much smaller share of the stroke-positive test examples.
- Logistic Regression achieved higher recall, F1-score, ROC-AUC and PR-AUC in this run.
- The low precision of both models means many positive predictions were false positives.
- Given the class imbalance, precision-recall performance and the confusion matrix should be considered alongside accuracy.

These figures are the results supplied from the development run. Re-running the notebook with a different library version or dataset copy may produce slightly different results.

## Methodology

1. Load and inspect the dataset.
2. Remove duplicate rows and exclude the identifier column from model features.
3. Impute missing numerical values using the median and categorical values using the most frequent category.
4. Standardize numerical features and one-hot encode categorical features within a scikit-learn preprocessing pipeline.
5. Use a stratified train/test split.
6. Train Logistic Regression and Random Forest models with class weighting.
7. Compare accuracy, precision, recall, F1-score, ROC-AUC and average precision (PR-AUC).
8. Plot confusion matrices, ROC curves and permutation feature importance.
9. Save the fitted pipelines with Joblib.

## Limitations and future improvements

- The dataset is imbalanced and may not represent the population where a model would be used.
- The models are not clinically validated and are not suitable for real-world medical decisions.
- The current reported evaluation uses a single holdout split. Cross-validation and an independent external test set would provide stronger evidence.
- Threshold selection should be performed using validation data, not by repeatedly tuning against the test set.
- Further work could include calibration, subgroup/fairness analysis, confidence intervals and careful external validation.

## Author

**Gauri Kotwal**

GitHub: [@gaurikotwal](https://github.com/gaurikotwal)
