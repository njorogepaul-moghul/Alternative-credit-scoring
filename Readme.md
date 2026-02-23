# Alternative Credit Scoring System

**A Predictive Model for Household Loan Default Risk using the 2021 FinAccess Survey**  
**Author:** Paulo – Level 300 Applied Math & CS, Kenyatta University

---

## 1. Project Overview
This project develops a practitioner-level credit scoring engine designed to assess the **creditworthiness of Kenyan individuals**. By leveraging the **2021 FinAccess Household Survey**, the model moves beyond traditional collateral-based lending to explore **alternative data**—including mobile money usage (M-Shwari, Fuliza), psychographic financial behavior, and household economic resilience.

---

## 2. The Problem Statement
Despite high mobile money penetration in Kenya, a significant portion of the population remains **"thin-file"** (lacking a traditional credit history). For institutions, the challenge is to accurately predict the probability of default (`PD`) using survey-based behavioral proxies.  

Inaccurate scoring can lead to:
- High **Non-Performing Loans (NPLs)**  
- Financial exclusion for deserving borrowers  

---

## 3. Objectives
- **Target Definition:** Quantify "Financial Distress" using markers like late repayments, asset liquidation, and meal-skipping due to debt  
- **Feature Engineering:** Extract high-signal predictors from mobile banking frequency, informal (Chama) involvement, and demographic stability  
- **Modeling:** Train a binary classification model (Logistic Regression, Random Forest, XGBoost) to differentiate between "Low Risk" and "High Risk" individuals  
- **Evaluation:** Measure performance via banking metrics such as **ROC-AUC**, **Gini Coefficient**, and **Precision-Recall curves**  

---

## 4. Data Source
The dataset is the **2021 FinAccess Household Survey (Weighted)**, a nationally representative survey of **22,000+ households** conducted by the **Kenya National Bureau of Statistics (KNBS)** and the **Central Bank of Kenya (CBK)**.

---

## 5. Technical Workflow

### Phase 1: Data Cleaning & Preparation
- **Initial Shape:** 22,024 rows × 2,353 columns  
- **Target Engineering:** Defined `is_high_risk` as 1 if the respondent defaulted, paid late, or experienced severe repayment distress; 0 otherwise  
- **Final Pre-processed Feature Matrix:** Deduplicated and cleaned into `encoded_data.csv` with 19,476 rows × 27 columns  

### Phase 2: Exploratory Data Analysis (EDA)
- **Income Normalization:** Monthly Income (B3I) had an **Extreme Positive Skew (7.55)**. A Natural Log Transformation normalized variance and prevented model bias toward high-income outliers  
- **Key Hypotheses Tested:**  
  - **Digital Signal:** Frequent mobile money/banking usage correlates with lower financial risk  
  - **Stability Factor:** Older respondents and those with formal education exhibit more stable repayment patterns  
- **Class Distribution:** 64.51% Low Risk (0) and 35.49% High Risk (1)  

### Phase 3: Modeling & Evaluation
- **Model Selection:** Logistic Regression, Random Forest, and XGBoost  
- **Preprocessing:** Addressed class imbalances and performed feature scaling  
- **Current Performance:** ROC-AUC plateau at **0.6681**  
- **Feature Importance:** Identified primary demographic and behavioral drivers of financial risk to assist data-driven lending decisions  

---

## 6. Conclusions & Future Maturity
The current performance suggests maximum signal has been extracted from raw features. To exceed **0.70 AUC**, future iterations will focus on:

- **Interaction Terms:** Combining demographic data (Age) with behavioral data (Mobile Banking) to capture hidden signals  
- **Wealth Indexing:** Synthesizing a 'Wealth Index' by combining income, asset ownership, and education for a more stable predictor  

This repository contains the **end-to-end pipeline** from raw KNBS survey data to a validated scoring engine.