# 📊 Phase 2: Exploratory Data Analysis
### Alternative Credit Scoring System — From Raw Survey to Actionable Insights

> This phase transitions the project from a cleaned dataset to a validated analytical foundation. The goal is not just to understand the data — it is to confirm or reject the core hypothesis: that behavioral and digital signals can predict credit risk without formal credit history.

---

## 📌 Objectives

- **Hypothesis Testing:** Validate that mobile money usage, Chama participation, and education level are credible credit risk signals
- **Feature Transformation:** Address extreme skewness in financial variables to ensure model stability
- **Risk Profiling:** Identify the primary drivers of credit risk across demographic, financial, and digital dimensions
- **Data Integrity:** Final audit of outliers (age and income) to prevent biased model weights

---

## 🔑 Key Findings

### 1. The Income Skew Problem
Monthly income (`B3I`) exhibited an **extreme positive skew of 7.55** — typical of informal-economy income distributions where a small number of high earners distort the mean significantly.

**Fix applied:** Natural Log Transformation `log(1+x)` to normalise variance.

> Without this transformation, the model would systematically over-weight high-income outliers and fail to learn meaningful patterns from the majority of respondents.

---

### 2. The Digital Signal — Mobile Money as Credit Proxy
Daily and weekly mobile money users showed **materially lower default rates** compared to infrequent or non-users. This validates the core alternative data hypothesis: transactional velocity on **M-Shwari and Fuliza** is a genuine proxy for financial discipline.

> Mobile banking frequency emerged as the **single strongest predictor** across all three models tested in Phase 3 — confirming EDA intuition before modelling began.

---

### 3. Social Capital — Chamas as Financial Discipline Signals
Frequent **Chama** (informal savings group) participants demonstrated consistently lower financial risk. Chama membership signals:
- Regular savings discipline
- Peer accountability structures
- Access to informal credit safety nets

> This is a uniquely Kenyan alternative data signal with broad applicability across East African markets.

---

### 4. The Age-Risk Profile
Credit risk **peaks in the 20–35 age bracket** and stabilises with maturity. Age outliers were capped to maintain focus on the statistically significant active labour force.

> This nonlinear age-risk relationship is better captured by tree-based models (Random Forest, XGBoost) than by Logistic Regression.

---

### 5. Education as a Stability Anchor
Higher educational attainment was the **strongest demographic predictor of credit stability**. Individuals with secondary or tertiary education showed significantly lower default rates even when controlling for income level.

---

## ✅ Hypotheses Tested

| Hypothesis | Result | Confidence |
|---|---|---|
| Digital mobile usage predicts lower credit risk | ✅ Confirmed | High |
| Chama participation signals financial discipline | ✅ Confirmed | High |
| Higher income = lower risk (linear relationship) | ⚠️ Partial | Medium — significant overlap in middle-income brackets |
| Education stabilises repayment behaviour | ✅ Confirmed | High |
| Age has a nonlinear risk profile | ✅ Confirmed | High |

---

## 📈 Visualisations Produced

| Chart | Purpose |
|---|---|
| Income Distribution (original vs log-transformed) | Skew correction validation |
| Risk Distribution by Age | Confirming the 20–35 peak |
| Risk Rates by Gender and Education | Demographic segmentation |
| Default Rate by Mobile Money Frequency | Digital signal validation |
| Default Rate by Mobile Banking Frequency | Alternative data hypothesis |
| Chama Participation vs Financial Risk Rate | Social capital signal |
| Correlation Heatmap | Linear drivers of credit distress |

---

## 🛠️ Technical Implementation

| Component | Detail |
|---|---|
| Libraries | Pandas, Matplotlib, Seaborn, NumPy |
| Income Transformation | `log(1+x)` — Natural Log applied to `B3I` |
| Age Handling | Outlier capping at statistically significant bounds |
| Class Balance | 64.51% Low Risk / 35.49% High Risk |
| Notebook | `Exploratory_Data_Analysis_phase.ipynb` |

---

## 💡 Conclusion

The EDA confirms that creditworthiness in Kenya's informal economy is **multi-dimensional**. Income alone is an unreliable predictor — the signal is too noisy without transformation and the relationship is nonlinear.

The combination of:
- **Digital footprint** (mobile money & banking frequency)
- **Social capital** (Chama participation)
- **Demographic stability** (education, age)

...provides a viable and ethically grounded path to scoring the unbanked population.

> These findings directly informed the feature selection and model architecture decisions in Phase 3.

---

## 📁 Notebook

```
Exploratory_Data_Analysis_phase.ipynb
```

---

> **← [Phase 1: Data Cleaning](../Data_cleaning_phase.ipynb)** &nbsp;|&nbsp; **[Phase 3: Modelling →](../Modelling.ipynb)**
