# Customer Attrition Prediction 

This project demonstrates an **end-to-end MLOps pipeline** for predicting customer churn using the [Telco Customer Churn dataset](https://www.kaggle.com/blastchar/telco-customer-churn).

## Features

- **MLflow**: Experiment tracking, model logging, and model serving.
- **DVC**: Dataset & pipeline versioning.
- **Scikit-learn**: Random Forest classifier.

## 2. Project Structure

```
app/
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
```

---



## Setup

```bash
    git clone https://github.com/<your-username>/Customer_Attrition.git
    cd churn-mlops
    pip install -r requirements.txt
```
## Training and Monitoring
```bash
  python src/train.py --n_estimators 100 --max_depth 5

```





