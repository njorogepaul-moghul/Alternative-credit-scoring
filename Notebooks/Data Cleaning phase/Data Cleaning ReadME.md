# Alternative Credit Scoring System  
**Phase 1: Data Cleaning & Feature Engineering**

This README covers the initial phase of the **Alternative Credit Scoring System**, focusing on the rigorous data cleaning and feature engineering required to transform the **2021 FinAccess Household Survey** into a machine-learning-ready dataset.

---

## 📋 Table of Contents
- Project Overview  
- Target Variable Construction  
- Feature Selection Strategy  
- Data Cleaning Pipeline  
- Final Dataset Specifications  

---

## 🔍 Project Overview
Traditional lending often excludes *thin-file* individuals who lack formal bank credit history. This phase focuses on defining a robust **Ground Truth** for financial distress and preparing high-signal predictors—including mobile money usage (*M-Shwari, Fuliza*) and informal social finance (*Chamas*)—for classification modeling.

This repository contains the first phase of a predictive modeling project designed to assess **household loan default risk in Kenya**, using the **2021 FinAccess Household Survey** conducted by **KNBS** and **CBK**.

---

## 🎯 Target Variable Construction: The *High Risk* Label
A composite target variable, **`is_high_risk`**, was engineered to capture the nuances of credit failure in the Kenyan market.

An individual is classified as **High Risk (1)** if they meet **at least one** of the following criteria:

- **`defaulted`**: Hard default on loans or debt  
- **`paidlate`**: Recorded arrears or late payments  
- **`E2Ci23`**: Safety-net indicator capturing missed payments or general delinquency  

### Class Distribution

| Class | Label     | Count  | Percentage |
|------:|-----------|--------:|-----------:|
| 0     | Low Risk  | 14,613  | 66.35%     |
| 1     | High Risk | 7,411   | 33.65%     |

**Insight:**  
The ~34% risk rate reflects the breadth of Kenya’s informal and digital credit markets, yielding a balanced dataset suitable for supervised learning.

---

## 🛠 Feature Selection Strategy
To predict risk without traditional credit scores, features were selected across four strategic dimensions:

- **Demographics**  
  - Age (`A19`)  
  - Education level  
  *Proxies for earning capacity and long-term stability.*

- **Economic Indicators**  
  - Monthly income (`B3I`)  
  - Income sources (formal employment vs. casual work)  
  *Signals of cash-flow consistency.*

- **Digital Behavior**  
  - Mobile money and mobile banking usage  
  *Key alternative data signals for financial behavior.*

- **Social Resilience**  
  - Informal group participation (`infgp_usage`)  
  *Measures access to social safety nets.*

---

## ⚙️ Data Cleaning Pipeline
The raw survey data (**22,024 rows, 2,353 columns**) underwent the following steps:

### 1. Deduplication
- **Action:** Removed **2,548** duplicate rows  
- **Rationale:** Prevents overfitting by ensuring the model does not memorize identical observations  

### 2. Missing Value Imputation
- **Action:** Imputed **1,843** missing values in monthly income (`B3I`) using the **median**  
- **Rationale:** Retains informal-sector respondents and avoids bias introduced by listwise deletion  

### 3. Categorical Encoding
- **Action:** Applied **One-Hot Encoding** to categorical variables such as gender, education, and mobile money usage  
- **Rationale:** Avoids imposing false ordinal relationships on nominal categories  

---

## 📊 Final Dataset Specifications
The output of Phase 1 is a consolidated dataset: **`encoded_data.csv`**.

- **Final Observations:** 19,476 individuals  
- **Feature Space:** 26 predictor variables (post one-hot encoding)  
- **Target Variable:** 1 binary vector (`is_high_risk_target`)  

---

*End of Phase 1 Documentation*
