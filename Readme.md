# 🛡️ Alternative Credit Scoring System
### Predicting Household Loan Default Risk Using Kenya's 2021 FinAccess Survey

**Author:** Paul Njoroge | Applied Mathematics & CS (Applied Maths Option) | Kenyatta University, Kenya

[![Live App](https://img.shields.io/badge/🚀_Live_App-Streamlit-FF4B4B)](https://alternativecreditscoring-app-gojkhneajqbfpnshgxsyv3.streamlit.app/)
![Python](https://img.shields.io/badge/Python-3.10-blue)
![XGBoost](https://img.shields.io/badge/Model-XGBoost-orange)
![Data](https://img.shields.io/badge/Data-KNBS_FinAccess_2021-green)

---

## 📌 Project Overview

Kenya has high mobile money penetration yet a significant portion of the population remains **"thin-file"** — lacking formal credit history. Traditional scoring systems exclude these individuals entirely, creating a massive financial inclusion gap.

This project builds an end-to-end **alternative credit scoring engine** using the 2021 FinAccess Household Survey (22,000+ households) conducted by KNBS and CBK. Instead of bank statements, it uses **behavioral signals** — mobile money usage, Chama participation, savings behavior — to predict the probability of loan default.

| Metric | Value |
|---|---|
| Raw Survey Rows | 22,024 |
| Cleaned Records | 19,476 |
| Feature Variables | 26 |
| Models Compared | 3 |

---

## 🎯 The Problem

- Despite 80%+ mobile money penetration, millions of Kenyans have **no formal credit score**
- Traditional lenders rely on bank statements and payslips — inaccessible to informal-sector workers
- Poor scoring leads to high Non-Performing Loans (NPLs) or blanket exclusion of creditworthy borrowers
- **Core question:** Can behavioral and demographic data replace traditional credit history?

---

## ⚙️ Technical Workflow

### Phase 1 — Data Cleaning & Feature Engineering

| Step | Detail |
|---|---|
| Raw Data | 22,024 rows × 2,353 columns (FinAccess 2021) |
| Deduplication | Removed 2,548 duplicate rows |
| Missing Value Imputation | 1,843 income values imputed using median |
| Target Engineering | `is_high_risk`: defaulted OR paid late OR delinquent |
| Encoding | One-hot encoding on gender, education, usage patterns |
| **Final Dataset** | **19,476 rows × 27 columns → encoded_data.csv** |

### Phase 2 — Exploratory Data Analysis

- **Income Skew:** Monthly income had extreme positive skew (7.55) — corrected with `log(1+x)` transformation
- **Digital Signal:** Daily/weekly mobile money users showed significantly lower default rates
- **Social Capital:** Chama participants demonstrated higher financial discipline and lower risk
- **Age Pattern:** Credit risk peaks at 20–35, stabilises with maturity
- **Education:** Strongest demographic predictor of credit stability across all models

### Phase 3 — Modelling & Evaluation

| Model | ROC-AUC | Role |
|---|---|---|
| Logistic Regression | Baseline | Interpretable baseline; suited for regulated lending |
| Random Forest | Benchmark | Captures complex feature interactions via Gini splits |
| **XGBoost (Tuned) ✅** | **0.6681** | **Champion model — deployed to Streamlit app** |

---

## 📊 XGBoost Final Performance

| Class | Precision | Recall | F1-Score | Support |
|---|---|---|---|---|
| Low Risk (0) | 0.77 | 0.58 | 0.66 | 2,513 |
| High Risk (1) | 0.47 | 0.68 | 0.55 | 1,383 |
| **Weighted Avg** | **0.66** | **0.61** | **0.62** | **3,896** |

> **Key insight:** The model captures **68% of actual high-risk borrowers** (recall = 0.68) — the priority metric in credit risk, where missing a defaulter is more costly than a false positive.

---

## 🔑 Top Predictive Features (Cross-Model Consensus)

| Feature | Logistic Reg. | Random Forest | XGBoost |
|---|---|---|---|
| Mobile Banking Frequency | ⭐ Top | ⭐ Top | ⭐ Top |
| Savings Behaviour | ⭐ Top | High | ⭐ Top |
| Chama Participation | High | High | High |
| Log Income (B3I_log) | High | ⭐ Top | High |
| Education Level | High | High | High |
| Age (A19) | Medium | ⭐ Top | Medium |

---

## 🛠️ Tech Stack

| Layer | Tools |
|---|---|
| Modelling | Python · XGBoost · Scikit-Learn · Pandas · NumPy |
| Visualisation | Matplotlib · Seaborn |
| Deployment | Streamlit · Joblib |
| Data Source | KNBS FinAccess 2021 Household Survey |

---

## 🚀 Live Demo

👉 [**Try the Alternative Credit Scoring App**](https://alternativecreditscoring-app-gojkhneajqbfpnshgxsyv3.streamlit.app/)

Input demographic and behavioral data, get an instant High/Low risk prediction with feature contribution breakdown.

---

## 📁 Repository Structure

```
├── Data_cleaning_phase.ipynb       # Phase 1: Cleaning & feature engineering
├── Exploratory_Data_Analysis_phase.ipynb  # Phase 2: EDA & hypothesis testing
├── Modelling.ipynb                 # Phase 3: Model training & evaluation
├── Alternative_app.py              # Streamlit deployment app
├── xgb_credit_model.joblib         # Trained XGBoost model
├── scaler.joblib                   # StandardScaler for preprocessing
├── requirements.txt                # Dependencies
```

---

## 🔭 Future Roadmap

- **Interaction Terms:** Age × Mobile Banking — captures hidden household economic signals
- **Wealth Index:** Synthesise income, assets, and education into a single stability score
- **SHAP Integration:** Full explainability layer for regulated credit decisions
- **Target:** Push ROC-AUC beyond 0.70 through engineered features

---

## 📬 Contact

**Paul Njoroge** | larneymogul@gmail.com | Kenyatta University, Kenya
