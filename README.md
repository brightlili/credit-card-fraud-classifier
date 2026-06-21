# credit-card-fraud-classifier — Credit Card Fraud Detection
ML-powered credit card fraud detection proof of concept, built with Python, Scikit-Learn, and Pandas. Demonstrates model training, evaluation, and financial data analysis for a SaaS banking platform.

> A machine learning proof of concept for detecting fraudulent credit card transactions, built as the foundation for a SaaS fraud detection platform serving banking institutions.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Lab Tasks](#lab-tasks)
- [Model Results](#model-results)
- [Key Findings](#key-findings)
- [Future Work](#future-work)

---

## Overview

This project was developed as a proof of concept for a financial services startup building a SaaS fraud detection platform for banking institutions. A banking partner provided a labeled dataset of credit card transactions, and the goal was to train a machine learning model that can reliably identify fraudulent transactions.

**Business Goal:** Demonstrate that ML-based fraud detection is viable enough to build a production SaaS platform on top of.

---

## Dataset

| Attribute | Detail |
|-----------|--------|
| File | `credit_card.csv` |
| Total Records | 59,073 transactions |
| Features | 22 columns (20 after cleaning) |
| Target Column | `is_fraud` (0 = Legitimate, 1 = Fraudulent) |
| Fraud Rate | ~12.7% of all transactions |
| Date Range | January 2019 – December 2020 |
| Missing Values | None |

> ⚠️ The dataset is not included in this repository. Place `credit_card.csv` in the project root before running the notebook.

---

## Project Structure

```
credit-card-fraud-classifier/
├── .venv/                  # Virtual environment (not committed)
├── .ipynb_checkpoints/     # Jupyter auto-saves
├── notebook.ipynb          # Main Jupyter notebook (all 10 tasks)
├── credit_card.csv         # Dataset (not committed)
├── requirements.txt        # Pinned dependencies
├── .gitignore
├── LICENSE
└── README.md
```

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3.12 | Core language |
| Pandas | Data loading & manipulation |
| NumPy | Numerical operations |
| Matplotlib | Plot rendering |
| Seaborn | Statistical visualization |
| Scikit-Learn | ML model & evaluation |
| Jupyter Notebook | Interactive development |
| VS Code | IDE |

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/brightlili/credit-card-fraud-classifier.git
cd credit-card-fraud-classifier
```

### 2. Create and activate virtual environment

```bash
# Create venv
python3 -m venv .venv

# Activate — Mac/Linux
source .venv/bin/activate

# Activate — Windows
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Register the Jupyter kernel

```bash
.venv/bin/python -m ipykernel install --user --name=fraudguard --display-name "FraudGuard POC"
```

### 5. Add the dataset

Place `credit_card.csv` in the project root directory.

### 6. Launch Jupyter

```bash
jupyter notebook
```

Open `notebook.ipynb` and select the **FraudGuard POC** kernel from the top-right kernel picker.

> 💡 **Tip:** If you see `ModuleNotFoundError`, make sure Jupyter is using the `.venv` kernel — not the system Python kernel.

---

## Lab Tasks

| # | Task | Description |
|---|------|-------------|
| 1 | Load Data | Read `credit_card.csv` into a Pandas DataFrame |
| 2 | Statistical Analysis | Compute mean, median, variance, std & check for NaN values |
| 3 | Fraud Spend Analysis | Compare average spend on fraudulent vs. legitimate transactions |
| 4 | Card-Level Analysis | Calculate total fraud/legit spend for card `344709867813900` |
| 5 | Data Cleaning | Drop irrelevant columns, bin timestamps into time-of-day categories |
| 6 | Correlation Heatmap | Seaborn heatmap of feature correlations with `is_fraud` |
| 7 | Label Encoding | Encode all categorical string features using Scikit-Learn |
| 8 | Train-Test Split | Split data 90% train / 10% test |
| 9 | Model Training | Train a Random Forest Classifier with balanced class weights |
| 10 | Evaluation | Accuracy score + confusion matrix on test set |

---

## Model Results

```
Overall Accuracy:  98.17%

Confusion Matrix:
                  Predicted: Legit    Predicted: Fraud
Actual: Legit         5,083                48
Actual: Fraud            60               717
```

| Metric | Value |
|--------|-------|
| True Negatives | 5,083 |
| False Positives | 48 |
| False Negatives | 60 |
| True Positives | 717 |
| Fraud Recall | 92.3% (717/777) |

---

## Key Findings

- **Fraudulent transactions tend to have higher average and median spend amounts** compared to legitimate ones — transaction amount is a strong fraud signal.
- **Time of day matters** — late night transactions (00:00–05:59) showed elevated fraud rates. Binning the timestamp into four time-of-day categories improved the model's temporal awareness.
- **Geographic signals are predictive** — merchant location (`merch_lat`, `merch_long`) showed meaningful correlation with the fraud label in the heatmap analysis.
- **The model achieves 98.17% accuracy** with `class_weight='balanced'` to handle the natural class imbalance (87% legit vs. 13% fraud).

---

## Future Work

- [ ] Tune decision threshold to reduce false negatives (missed fraud)
- [ ] Add transaction velocity features (e.g. transactions per card per hour)
- [ ] Wrap model in a REST API for real-time scoring
- [ ] Build a client dashboard for fraud alert management
- [ ] Retrain quarterly on fresh data to prevent model drift
- [ ] Achieve SOC 2 Type II compliance before banking client onboarding

---

## License

This project is licensed under the terms in the `LICENSE` file.

---

*Built as a proof of concept for the FraudGuard SaaS fraud detection platform.*