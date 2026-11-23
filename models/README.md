# Model artifacts

Run the notebook from the repository root to train and save the fitted scikit-learn pipelines in this folder.

Generated files:

- `stroke_logistic_model.joblib`
- `stroke_random_forest_model.joblib`

Model files are excluded from Git by `.gitignore`. They can be recreated by running the notebook after installing `requirements.txt` and placing the dataset at `data/raw/healthcare-dataset-stroke-data.csv`.

These models are educational artifacts and are not suitable for medical diagnosis or clinical decisions.