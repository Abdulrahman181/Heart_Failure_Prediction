# Heart Failure Prediction

This repository contains a reproducible, leakage-aware machine-learning notebook for **Heart Failure Prediction**. It is an educational/research artifact, not a clinical decision system.

## Data

The patient dataset is intentionally not committed (size/licensing and privacy constraints). The notebook requires a CSV named `heart.csv` with these columns:

`Age`, `Sex`, `ChestPainType`, `RestingBP`, `Cholesterol`, `FastingBS`, `RestingECG`, `MaxHR`, `ExerciseAngina`, `Oldpeak`, `ST_Slope`, and binary target `HeartDisease`.

Set `HEART_FAILURE_DATA` to the CSV path before running. Without it, the notebook falls back to `data/heart.csv` and raises a clear error if the file is absent. No data or model metrics are included in this repository.

## Run

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
export HEART_FAILURE_DATA=/absolute/path/to/heart.csv
python validate_repository.py
jupyter notebook Heart_Failure_Prediction.ipynb
```

Run cells from top to bottom. The workflow validates the schema, performs stratified 70/15/15 train/validation/test splits, fits imputation/one-hot encoding/scaling inside a scikit-learn `Pipeline`, selects by validation recall, and evaluates the selected model once on the untouched test set. `artifacts/` is local-only and ignored by git.

## Engineering notes

- `validate_repository.py` performs dependency-free JSON, AST, stale-output, and non-portable-path checks. It does not execute training.
- Randomness is controlled with seed `42`; models with stochastic behavior also receive that seed. Metrics remain dependent on the dataset and package versions.
- XGBoost is optional at notebook runtime so static inspection works without its native dependency; it is listed in `requirements.txt` for a full run.
- A full training run was **not** claimed during this audit because `heart.csv` is absent and the sandbox does not have scikit-learn/XGBoost installed.

## Limitations and cautions

- A single holdout on a small public dataset is not sufficient evidence of clinical performance. Confidence intervals, external validation, calibration, fairness, and prospective evaluation are out of scope.
- Do not interpret predictions as professional medical advice.
