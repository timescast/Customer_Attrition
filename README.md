Here’s a clean and concise README for a **Customer Attrition Rate Prediction** project using **Random Forest**, **MLflow**, and **DVC**—written in an expert, Python/ML–friendly style.

---

# Customer Attrition Rate Prediction

**Random Forest + MLflow Tracking + DVC Data Versioning**

## 1. Overview

This project builds a **customer attrition (churn) prediction model** using a **RandomForestClassifier**.
It uses:

* **DVC** for data versioning & reproducible pipelines
* **MLflow** for experiment tracking & model registry
* **Python** as the main development language

Goal: create a fully reproducible ML workflow from data → model → deployment.

---

## 2. Project Structure

```
.
├── data/                     # Raw & processed data (tracked by DVC)
│   ├── raw/                 
│   └── processed/
├── src/
│   ├── preprocess.py         # Data cleaning & feature engineering
│   ├── train.py              # Model training with MLflow
│   ├── utils.py
│   └── config.yaml           # Hyperparameters & paths
├── models/                   # MLflow manages final models
├── dvc.yaml                  # DVC pipeline definition
├── params.yaml               # Model & preprocess parameters
├── requirements.txt
├── README.md
└── mlruns/                   # MLflow local tracking directory
```

---

## 3. Installation

```bash
git clone <repo-url>
cd customer-attrition
python -m venv venv
source venv/bin/activate  # windows: venv\Scripts\activate
pip install -r requirements.txt
```

---

## 4. Data Versioning with DVC

### Initialize DVC

```bash
dvc init
dvc add data/raw/customers.csv
git add data/.gitignore customers.csv.dvc
git commit -m "Add raw dataset to DVC"
```

### Define Pipeline

`dvc.yaml` typically contains:

* stage: preprocess
* stage: train

Run pipeline:

```bash
dvc repro
```

Push data to remote storage:

```bash
dvc remote add -d s3 s3://<bucket>/dvc-storage
dvc push
```

---

## 5. MLflow Experiment Tracking

### Start MLflow UI

```bash
mlflow ui
```

Open browser at:

```
http://127.0.0.1:5000
```

### Train Model with Tracking

`train.py` logs:

* metrics (accuracy, recall, f1_score)
* confusion matrix
* feature importance
* model artifact (pickle)
* parameters (n_estimators, max_depth, etc.)

Run:

```bash
python src/train.py
```

MLflow logs are saved in `mlruns/`.

---

## 6. Training Workflow

### 1. Preprocessing

* Handle missing values
* Encode categorical variables
* Scale numerical features
* Train/valid split

### 2. Model

RandomForestClassifier with hyperparameters from `params.yaml`:

```yaml
model:
  n_estimators: 200
  max_depth: 12
  min_samples_split: 4
  class_weight: balanced
```

### 3. Outputs

* metrics.json
* model.pkl
* feature_importance.json

All captured by MLflow.

---

## 7. Reproducibility

To reproduce the exact model:

```bash
git pull
dvc pull             # get correct dataset version
dvc repro            # rerun preprocessing + training
```

To load a past MLflow model version:

```python
model = mlflow.pyfunc.load_model("runs:/<run-id>/model")
```

---

## 8. Deployment

Export model:

```bash
mlflow models serve -m "runs:/<run-id>/model" -p 8000
```

Use API:

```bash
curl -X POST -H "Content-Type: application/json" \
     --data '{"data": [[45, 120000, 3, 0, 1]]}' \
     http://127.0.0.1:8000/invocations
```

---

## 9. Future Enhancements

* Hyperparameter tuning with Optuna
* Continuous training pipeline using GitHub Actions
* SHAP-based model explanations
* Dockerized MLflow + DVC pipeline

---
 
