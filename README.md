# SentinelAI — Network Intrusion Detection

A machine-learning project that classifies NSL-KDD network connection records as `normal` or `attack`.

## Current scope
- Dataset: NSL-KDD (`KDDTrain+` and `KDDTest+`)
- Binary classification: normal vs attack
- Random Forest with hyperparameter tuning and in-pipeline feature selection
- Logistic Regression baseline
- Class-weighted Random Forest
- Optional SMOTENC experiment
- Validation-based threshold selection
- Final evaluation on the official test set
- Confusion matrix, ROC curve, precision-recall curve, feature importance
- Saved model pipeline, threshold, and test metrics

## Important
This is an **offline benchmark ML experiment**, not yet a real-time intrusion detection system. NSL-KDD is an older dataset and benchmark performance does not guarantee performance on modern live network traffic. Do not claim production readiness until the feature extraction pipeline and real-traffic evaluation are implemented.

## Setup (Windows PowerShell)

```powershell
# From the project folder:
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install pandas numpy matplotlib seaborn scikit-learn requests joblib jupyter
python -m pip install imbalanced-learn
```

If PowerShell blocks activation, run this in the current PowerShell session:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
.\.venv\Scripts\Activate.ps1
```

Open and run `SentinelAI_NSL_KDD_Final.ipynb` in VS Code or Jupyter. The notebook downloads the data from GitHub, so internet access is needed on the first run.

## Files to commit to GitHub
Recommended initial repository layout:

```text
SentinelAI/
├── README.md
├── .gitignore
├── notebooks/
│   └── SentinelAI_NSL_KDD_Final.ipynb
├── requirements.txt
└── .github/                 # optional, later
```

Do not commit the generated `.venv/`, cache folders, or large generated model files unless you intentionally want to version them. For a student portfolio, commit the notebook and README first; optionally commit a small metrics CSV and figures after running the notebook. The model `.joblib` file can be large and should usually be ignored or stored with Git LFS if needed.

## Git commands

Run from the root of your local project:

```powershell
git init
git add README.md .gitignore requirements.txt notebooks/SentinelAI_NSL_KDD_Final.ipynb
git commit -m "Add leakage-safe NSL-KDD intrusion detection ML pipeline"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/SentinelAI.git
git push -u origin main
```

If the repository already exists and has a remote, do not repeat `git init` or `git remote add origin`. Check with:

```powershell
git status
git remote -v
```

## Suggested next milestones
1. Run the notebook end-to-end and record the real final test metrics.
2. Add a `src/` module that loads the saved pipeline and predicts from new feature records.
3. Create a Flask/FastAPI prediction endpoint.
4. Build a dashboard for alerts and model metrics.
5. Add traffic feature extraction from authorized PCAP captures and test it against the exact training schema.
6. Evaluate on more recent, representative traffic before making real-time/production claims.
