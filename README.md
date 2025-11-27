# Customer Churn Prediction with MLOps

This project demonstrates an **end-to-end MLOps pipeline** for predicting customer churn using the [Telco Customer Churn dataset](https://www.kaggle.com/blastchar/telco-customer-churn).

## Features

- **MLflow**: Experiment tracking, model logging, and model serving.
- **DVC**: Dataset & pipeline versioning.
- **Streamlit**: Interactive web app for predictions.
- **Scikit-learn**: Random Forest classifier.

## Project Structure

churn-mlops/
│── data/
│   └── raw/                # Original dataset (DVC tracked)
│   └── processed/          # Preprocessed dataset (DVC pipeline output)
│── src/
│   ├── train.py            # Training script (with MLflow logging)
│   ├── utils.py            # Data cleaning & preprocessing
│── app.py                  # Streamlit app for demo
│── requirements.txt        # Python dependencies
│── MLproject               # MLflow project definition
│── dvc.yaml                # DVC pipeline definition
│── README.md               # Project documentation
│── .gitignore
│── .dvcignore

## Setup

```bash
    git clone https://github.com/<your-username>/churn-mlops.git
    cd churn-mlops
    pip install -r requirements.txt
```
## Training and Monitoring
```bash
  python src/train.py --n_estimators 100 --max_depth 5

```
