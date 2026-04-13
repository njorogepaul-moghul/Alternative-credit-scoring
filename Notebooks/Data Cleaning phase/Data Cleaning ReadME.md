# 🧹 Phase 1: Data Cleaning & Feature Engineering
### Alternative Credit Scoring System — FinAccess 2021 Survey (KNBS)

> This notebook transforms a 22,024-row national survey into a machine-learning-ready feature matrix. It is the foundation of the entire project — poor cleaning here cascades into model bias and unreliable predictions downstream.

---

## 📌 Why This Phase Matters

The raw FinAccess 2021 dataset contains **22,024 rows and 2,353 columns** — a survey designed for policy research, not machine learning. Before any model can be trained, the data must be surgically reduced, cleaned, and restructured into a feature matrix that a classifier can actually use.

This phase also defines what "credit risk" means in the Kenyan informal economy — a non-trivial problem when most respondents have no formal credit history at all.

---

## 🎯 The Business Context: Why Alternative Data?

Traditional credit scoring excludes **"thin-file"** individuals — those without formal bank statements or payslip history. In Kenya, this describes a large portion of the working population: informal traders, casual workers, Chama members, and mobile-money-only users.

This phase identifies and engineers **behavioral and demographic features** that serve as credible proxies for creditworthiness in the absence of traditional credit history.

---

## 🎯 Target Variable Construction: `is_high_risk`

A composite binary target was engineered to reflect the reality of credit failure in Kenya's informal economy.

An individual is labelled **High Risk (1)** if they meet **at least one** of the following:

| Condition | Description |
|---|---|
| `defaulted` | Hard default on any loan or debt obligation |
| `paidlate` | Recorded arrears or late payments |
| `E2Ci23` | Safety-net indicator — missed payments or general delinquency |

### Class Distribution

| Class | Label | Count | Share |
|---|---|---|---|
| 0 | Low Risk | 14,613 | 66.35% |
| 1 | High Risk | 7,411 | 33.65% |

> The ~34% high-risk rate reflects the breadth of Kenya's informal and digital credit markets — yielding sufficient minority class signal for supervised learning without extreme imbalance.

---

## ⚙️ Data Cleaning Pipeline

### Step 1 — Deduplication
- **Action:** Removed **2,548 duplicate rows** from the raw 22,024-row dataset
- **Rationale:** Duplicates in survey data introduce artificial class patterns that inflate model confidence on training data while hurting generalisation on unseen data

### Step 2 — Missing Value Imputation
- **Action:** Imputed **1,843 missing values** in the monthly income field (`B3I`) using the column **median**
- **Rationale:** Listwise deletion was rejected — it would disproportionately remove informal-sector respondents, the very population this model is designed to score

### Step 3 — Categorical Encoding
- **Action:** Applied **One-Hot Encoding** to nominal variables: gender, education level, mobile money usage frequency, mobile banking frequency, Chama participation, and savings behaviour
- **Rationale:** Ordinal encoding was deliberately avoided to prevent imposing false ranking assumptions on categorical survey responses

---

## 🔍 Feature Selection Strategy

26 predictor variables retained across four strategic dimensions:

| Dimension | Features | Rationale |
|---|---|---|
| Demographics | Age (`A19`), Education Level | Proxy for earning capacity and long-term stability |
| Economic | Monthly Income (`B3I`), Income Group, Employment vs Casual Work | Cash-flow consistency signals |
| Digital Behavior | Mobile Money & Banking frequency | High-quality alternative credit signal |
| Social Resilience | Chama / Informal Group participation | Measures access to social safety nets |

---

## 📊 Final Dataset Specifications

| Property | Value |
|---|---|
| Output File | `encoded_data.csv` |
| Rows (Clean) | 19,476 individuals |
| Feature Columns | 26 predictor variables |
| Target Column | `is_high_risk_target` (binary) |
| Class Balance | 66.35% Low Risk / 33.65% High Risk |

---

## 🛠️ Tech Stack

```
Python · Pandas · NumPy · Scikit-Learn
```

---

## 📁 Notebook

```
Data_cleaning_phase.ipynb
```

---

> **Next → [Phase 2: Exploratory Data Analysis](../Exploratory_Data_Analysis_phase.ipynb)**
