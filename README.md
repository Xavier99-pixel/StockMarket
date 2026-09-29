# Stock Market Prediction — Internship Minor Project

Start with **minorproject.html** for a browser-readable executed report, or **minorproject.ipynb** for the editable notebook. **PROJECT_REPORT.md** is the submission report with student details to fill in.

## Run
Tested with Python 3.13.3. From this project directory:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m jupyter nbconvert --to notebook --execute --inplace minorproject.ipynb
python -m jupyter nbconvert --to html minorproject.ipynb
```

Alternatively run `python train.py` from this directory. This regenerates results but does not update the notebook, HTML export or written report. Run the notebook and export command for refreshed notebook output; update the report if data or settings change. In VS Code, select the environment's Python kernel and Run All.

## Contents
- minorproject.ipynb: full executed workflow, visualizations, evaluation and viva notes.
- minorproject.html: readable notebook export without requiring Jupyter.
- train.py: equivalent Python script.
- portfolio_data.csv: original supplied dataset.
- PROJECT_REPORT.md: methodology, actual results and limitations.
- requirements.txt: versions from the tested environment.
- results/: metrics, per-origin predictions, split dates, charts, dataset checksum and fitted models.

Model files are joblib artifacts; load only files you trust. Persistence has `model=None` in the saved dictionary and is explicitly marked as a baseline.

## Before submission
Fill student/institution/mentor details and add the original Kaggle dataset URL and license. Review the explanations so you can defend the implementation. Data ends on 14 May 2019: no result is a current market forecast. The HTML and notebook contain actual executed results, not claimed accuracy targets.
