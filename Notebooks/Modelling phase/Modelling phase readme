# 🤖 Phase 3: Modelling & Evaluation
### Alternative Credit Scoring System — From Features to a Validated Scoring Engine

> This phase trains, compares, and evaluates three classification models on the cleaned FinAccess dataset. The objective is a validated scoring engine that identifies high-risk borrowers using behavioral and demographic signals — without relying on traditional credit history.

---

## 📌 Overview

Performance is measured using **ROC-AUC** — the standard metric in credit risk modelling. ROC-AUC captures the model's ability to rank borrowers by risk regardless of classification threshold, making it more meaningful than raw accuracy in imbalanced credit datasets.

| Dataset Split | Value |
|---|---|
| Training Set | 80% (stratified) |
| Test Set | 20% (stratified) |
| Class Balance | 64.51% Low Risk / 35.49% High Risk |

---

## ⚙️ Preprocessing

| Step | Detail |
|---|---|
| Train/Test Split | 80/20 with stratification to maintain class balance |
| Feature Scaling | `StandardScaler` applied — critical for Logistic Regression coefficient reliability |
| Class Imbalance | `class_weight='balanced'` applied to Logistic Regression for the 35% minority class |

---

## 🏆 Model Comparison

| Model | Purpose | Design Decision |
|---|---|---|
| Logistic Regression | Baseline | `class_weight='balanced'`; interpretable coefficients for regulated lending |
| Random Forest | Nonlinear Benchmark | Gini importance; captures complex feature interactions without feature scaling |
| **XGBoost (Tuned) ✅** | **Champion** | RandomizedSearchCV over `learning_rate`, `max_depth`, `subsample`; 5-fold CV |

---

## 📊 Champion Model: Tuned XGBoost

### Performance Metrics

| Class | Precision | Recall | F1-Score | Support |
|---|---|---|---|---|
| Low Risk (0) | 0.77 | 0.58 | 0.66 | 2,513 |
| High Risk (1) | 0.47 | 0.68 | 0.55 | 1,383 |
| **Weighted Avg** | **0.66** | **0.61** | **0.62** | **3,896** |

**ROC-AUC: 0.6681**
**Overall Accuracy: 0.61**

### Confusion Matrix

| | Predicted Low Risk | Predicted High Risk |
|---|---|---|
| **Actual Low Risk** | 1,459 | 1,054 |
| **Actual High Risk** | 448 | 935 |

---

## 💡 Business Interpretation of Results

| Metric | Value | Business Meaning |
|---|---|---|
| High Risk Recall | 0.68 | Model catches **68% of actual defaulters** — the priority metric in credit risk |
| Low Risk Precision | 0.77 | When model predicts low risk, it is correct **77% of the time** |
| Threshold | 0.40 (default) | Adjustable to balance risk appetite vs portfolio growth |

> In credit risk, missing a true defaulter (false negative) is more costly than a false positive. The model is deliberately tuned to prioritise recall on the high-risk class.

---

## 🔑 Feature Importance — Cross-Model Analysis

Across all three models, the same features consistently ranked at the top. When Logistic Regression, Random Forest, and XGBoost all agree — the signal is structural, not model-specific.

| Feature | Logistic Reg. | Random Forest | XGBoost |
|---|---|---|---|
| Mobile Banking Frequency | ⭐ Top | ⭐ Top | ⭐ Top |
| Savings Behaviour | ⭐ Top | High | ⭐ Top |
| Chama Participation | High | High | High |
| Log Income (`B3I_log`) | High | ⭐ Top | High |
| Education Level | High | High | High |
| Age (`A19`) | Medium | ⭐ Top | Medium |

### Model-Specific Insights

**Logistic Regression:**
Digital financial engagement (mobile banking, savings usage) strongly influences predicted default probability. Education and income segmentation also play a significant role. Provides directional interpretability — suitable for regulated credit environments.

**Random Forest:**
Tree-based splits emphasise behavioral and transformed financial variables. The prominence of `A19` (age) and `B3I_log` (log income) suggests nonlinear interactions not fully captured by linear models.

**XGBoost:**
Boosting confirms that transactional and savings behavior are the strongest predictive drivers. Income and education remain consistently relevant, reinforcing their structural importance in credit risk segmentation.

---

## 🚀 Hyperparameter Tuning

The XGBoost model was optimised via **RandomizedSearchCV**, exploring:

```python
param_grid = {
    'learning_rate': [0.01, 0.05, 0.1, 0.2],
    'max_depth': [3, 4, 5, 6],
    'subsample': [0.7, 0.8, 0.9, 1.0],
    'n_estimators': [100, 200, 300]
}
# 5-fold cross-validation, scoring='roc_auc'
```

---

## 💾 Deployment Artifacts

| File | Description |
|---|---|
| `xgb_credit_model.joblib` | Tuned XGBoost classifier — champion model |
| `logistic_regression_model.joblib` | Interpretable baseline for regulated environments |
| `random_forest_model.joblib` | Nonlinear benchmark |
| `scaler.joblib` | StandardScaler — **required** for preprocessing new inputs before prediction |

---

## 🔭 Current Limitations & Future Roadmap

The ROC-AUC plateau at **0.6681** indicates the model has extracted maximum signal from the current raw features. Further gains will come from feature engineering, not additional tuning.

| Next Step | Expected Impact |
|---|---|
| Interaction Terms | Age × Mobile Banking — captures hidden household economics |
| Wealth Index | Income + Assets + Education → single stability score |
| SHAP Integration | Full explainability for regulated credit decisions |
| **Target** | **Push ROC-AUC beyond 0.70** |

---

## 🛠️ Tech Stack

```
Python · XGBoost · Scikit-Learn · Pandas · NumPy · Joblib · Matplotlib · Seaborn
```

---

## 📁 Notebook

```
Modelling.ipynb
```

---

## 🚀 Live App

👉 [**Alternative Credit Scoring App**](https://alternativecreditscoring-app-gojkhneajqbfpnshgxsyv3.streamlit.app/)

---

> **← [Phase 2: Exploratory Data Analysis](../Exploratory_Data_Analysis_phase.ipynb)**
