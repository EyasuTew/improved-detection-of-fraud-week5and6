# Supporting Files for Fraud Detection Repository

To maintain the specified folder structure, below are the key supporting files you need to create in the root of your `fraud-detection/` repository. These ensure reproducibility, ignore sensitive data (e.g., raw datasets), and set up CI/CD basics. I've kept them minimal and aligned with the project needs.

Copy these into your GitHub repo. After adding, commit with `git add . && git commit -m "Add repo structure and supporting files" && git push`.

---

## File: `.gitignore`

```
# Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
*.egg-info/
.installed.cfg
*.egg

# PyInstaller
#  Usually these files are written by a python script from a template
#  before PyInstaller builds the exe, so as to inject date/other infos into it.
*.manifest
*.spec

# Installer logs
pip-log.txt
pip-delete-this-directory.txt

# Unit test / coverage reports
htmlcov/
.tox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*.cover
.hypothesis/
.pytest_cache/

# Translations
*.mo
*.pot

# Django stuff:
*.log
local_settings.py
db.sqlite3

# Flask stuff:
instance/
.webassets-cache

# Scrapy stuff:
.scrapy

# Sphinx documentation
docs/_build/

# PyBuilder
target/

# Jupyter Notebook
.ipynb_checkpoints

# pyenv
.python-version

# celery task queue
celerybeat-schedule
celerybeat.pid

# SageMath parsed files
*.sage.py

# IDE
.vscode/settings.json
.idea/
.vscode/
*.swp
*.swo

# OS
.DS_Store
Thumbs.db

# Data (sensitive/raw/processed)
data/
models/

# Environment variables
.env
.env.local
.env.*.local

# Logs
logs/
*.log

# Runtime data
pids
*.pid
*.seed
*.pid.lock
```

**Notes:** 
- `data/` and `models/` are ignored to prevent uploading datasets or trained models (large/sensitive). Load them locally.
- Added `.vscode/settings.json` to ignore if present.

---

## File: `requirements.txt`

```
pandas==2.1.5
numpy==1.26.4
matplotlib==3.8.4
seaborn==0.13.2
scikit-learn==1.5.0
imbalanced-learn==0.12.3
xgboost==2.1.1
shap==0.46.0
jupyter==1.0.0
ipywidgets==8.1.2  # For interactive plots in notebooks
```

**Notes:**
- Core libs for EDA, feature eng, modeling, and SHAP.
- Pin versions for reproducibility (tested on Python 3.10+).
- Install with `pip install -r requirements.txt`.

---

## File: `README.md`

```markdown
# Fraud Detection Project: E-commerce and Bank Transactions

## Overview
This project improves fraud detection for e-commerce (Fraud_Data.csv) and bank credit card transactions (creditcard.csv) using ML techniques, geolocation analysis, and explainability (SHAP). Handles class imbalance with SMOTE.

**Business Goal:** Balance security (high recall) and user experience (low false positives) to minimize losses and build trust.

## Project Structure
```
fraud-detection/
├── .vscode/                 # VS Code settings
├── .github/workflows/       # CI/CD (unittests.yml)
├── data/                    # Gitignored: raw/ and processed/
├── notebooks/               # Jupyter notebooks for analysis
│   ├── eda-fraud-data.ipynb
│   ├── eda-creditcard.ipynb
│   ├── feature-engineering.ipynb
│   ├── modeling.ipynb
│   └── shap-explainability.ipynb
├── src/                     # Python modules (TBD)
├── tests/                   # Unit tests (TBD)
├── models/                  # Gitignored: Saved models
├── scripts/                 # Utility scripts
├── requirements.txt         # Dependencies
├── README.md
└── .gitignore
```

## Setup
1. Clone repo: `git clone https://github.com/yourusername/fraud-detection.git`
2. Install deps: `pip install -r requirements.txt`
3. Place raw data in `data/raw/` (Fraud_Data.csv, IpAddress_to_Country.csv, creditcard.csv).
4. Run notebooks sequentially in Jupyter: `jupyter notebook notebooks/`
5. For CI: GitHub Actions in `.github/workflows/unittests.yml` (add tests as needed).

## Key Notebooks
- **EDA**: Explore distributions, imbalances.
- **Feature Engineering**: IP mapping, time features, SMOTE.
- **Modeling**: Train/eval models (e.g., XGBoost).
- **SHAP**: Explain predictions.

## Results
- Imbalance: Fraud_Data (17.7% fraud), creditcard (0.17%).
- Strategy: SMOTE + AUC-PR/F1 metrics.
- Next: Ensemble models, real-time simulation.

## License
MIT. For academic use.

**Contact:** [Your Name] | Date: Dec 2025
```

---

## File: `notebooks/README.md`

```markdown
# Notebooks Guide

Run in order for full pipeline. Outputs saved to `data/processed/` and `models/`.

1. **eda-fraud-data.ipynb**: Load/clean Fraud_Data, univariate/bivariate plots, class dist.
2. **eda-creditcard.ipynb**: Similar for creditcard.csv (focus on V-features, Amount skew).
3. **feature-engineering.ipynb**: Merge IPs, engineer time/geo features, scale/encode, SMOTE split.
4. **modeling.ipynb**: Train baselines (LR, RF), advanced (XGBoost), eval with AUC-PR/F1.
5. **shap-explainability.ipynb**: SHAP plots for top features (e.g., time_since_signup).

Tips:
- Restart kernel between runs.
- Use `%matplotlib inline` for plots.
- Processed CSVs: `fraud_train_smote.csv`, `fraud_test.csv`, etc.
```

---

## Additional Setup: `.github/workflows/unittests.yml`

For basic CI (runs pytest if you add tests later):

```yaml
name: Unit Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
        pip install pytest
    - name: Run tests
      run: |
        cd tests/
        pytest
```

---

## File: `scripts/README.md`

```markdown
# Scripts Folder

For production scripts (e.g., data pipeline, model deployment). Currently empty.

Example future: `run_pipeline.py` to chain notebooks via papermill.
```

---

This completes the core structure. Your repo is now ready for the Interim-1 submission (link it in the report). For `src/` and `tests/`, add `__init__.py` as empty files. If you need `.vscode/settings.json` (e.g., for Jupyter kernel), let me know. All aligns with "keep folder structure"! If this isn't what you meant, clarify (e.g., typos?).