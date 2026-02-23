# Phase 2: Exploratory Data Analysis (EDA)

## 1. Overview
This phase transitions the **"Alternative Credit Scoring System"** from raw data to actionable insights. By analyzing the **FinAccess 2021 dataset**, we examine the socioeconomic and digital behaviors that distinguish **"High Risk"** from **"Low Risk"** individuals in Kenya's informal economy.

## 2. Objectives
- **Feature Engineering & Transformation:** Address extreme skewness in financial variables to ensure model stability.  
- **Risk Profiling:** Identify the primary drivers of credit risk across demographic, financial, and digital dimensions.  
- **Data Integrity:** Perform a final audit of outliers (e.g., age and income) to prevent biased model weights.  

## 3. Key Findings & Insights

### 3.1 Financial Behavior & Distribution
- **The Income Skew:** Monthly income exhibited an extreme positive skew (7.55). We applied a Natural Log Transformation (`log(1+x)`) to normalize the variance, ensuring the model treats percentage changes in income consistently.  
- **Capacity vs. Risk:** While higher income correlates with lower risk, significant overlap exists in the middle-income brackets, justifying the need for non-traditional "Alternative" data.  

### 3.2 The Digital Signal (Alternative Data)
- **Mobile Money & Banking:** Frequent usage (Daily/Weekly) is a high-quality proxy for financial inclusion. High transactional velocity correlates strongly with Low Risk status.  
- **Social Capital:** Participation in informal groups (Chamas) serves as "Social Collateral." Frequent contributors demonstrate higher financial discipline and lower default rates.  

### 3.3 Demographic Stability
- **Age Factor:** Credit risk peaks in the 20–35 age bracket and stabilizes with maturity. We capped age outliers to maintain focus on the statistically significant active labor force.  
- **Education Anchor:** Higher educational attainment is the strongest demographic predictor of credit stability, acting as a "stability anchor" for individuals without formal bank statements.  

## 4. Visual Analysis Summary
The following charts were analyzed to validate our economic hypotheses:  
- **Income Distributions:** Original vs. Log-Transformed  
- **Risk Distributions:** Segmented by Age, Gender, and Education  
- **Digital Footprint:** Risk rates by Mobile Money and Mobile Banking frequency  
- **Social Connectivity:** Risk rates by Informal Group (Chama) involvement  
- **Correlation Heatmap:** Identifying the strongest linear drivers of credit distress  

## 5. Technical Implementation
- **Libraries:** Pandas, Matplotlib, Seaborn, Numpy  
- **Transformations:** Natural Log scaling for Income; Outlier capping for Age  
- **Target Balance:** The dataset contains a ~35% "High Risk" class, providing a robust signal for supervised learning  

## 6. Conclusion
The EDA confirms that creditworthiness in the informal sector is multi-dimensional. Income alone is insufficient; however, by combining **Income** with **Digital Footprint** and **Social Capital**, we have a viable path to score the "unbanked" population.