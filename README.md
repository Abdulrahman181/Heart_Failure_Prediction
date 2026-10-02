# Heart Failure Prediction

This repository contains an exploratory heart-disease classification notebook. It does **not** include the dataset, and no model results have been independently validated as part of this maintenance change.

## Dataset

Provide a CSV with the columns referenced by the notebook: `Age`, `Sex`, `ChestPainType`, `RestingBP`, `Cholesterol`, `FastingBS`, `RestingECG`, `MaxHR`, `ExerciseAngina`, `Oldpeak`, `ST_Slope`, and the target column `HeartDisease`. The dataset is intentionally not copied into this repository; obtain it from its authorized source and review any applicable license and privacy requirements.

By default, the notebook looks for `heart.csv` in its current working directory. To use another file, set `HEART_DATA_PATH` to its path before starting Jupyter:

```bash
export HEART_DATA_PATH=/path/to/heart.csv
jupyter notebook Heart_Failure_Prediction.ipynb
```

On PowerShell, use `$env:HEART_DATA_PATH = "C:\path\to\heart.csv"` before launching Jupyter. If the file is missing, the first data-loading cell reports the expected path.

## Environment and run

Use Python 3.10 or newer, create a virtual environment, and install the declared dependencies:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
jupyter notebook Heart_Failure_Prediction.ipynb
```

The dependency file gives compatibility ranges, not an exact lockfile. For a fully reproducible environment, resolve and record a platform-specific lockfile after testing with the authorized dataset. The notebook saves fitted encoders, a scaler, and models as pickle files under `artifacts/`; treat these files as trusted local outputs only. **Do not unpickle files from untrusted sources.**

## Security and limitations

Notebook cell outputs and execution counts were cleared to avoid committing stale results or embedded data. This does not erase earlier versions from GitHub history or other clones. Never commit datasets, generated model files, or API credentials. If a Kaggle API credential was exposed in this repository or in a published clone, revoke the old key and generate a replacement in Kaggle; this repository change cannot perform that account-level action. If a credential appeared in a prior Git revision, also follow GitHub's sensitive-data remediation guidance—the credential should be considered compromised even if the current file is clean.

The notebook performs exploratory preprocessing and model comparison. Its reported metrics are not a clinical assessment, evidence of generalization, or medical advice. Preprocessing and model-selection methodology should be reviewed before using any results for research or decisions.
