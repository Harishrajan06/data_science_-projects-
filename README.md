# 📊 Data Science Projects Portfolio

Welcome! This repository is my collection of **data science and machine learning projects**.  
Each project is organized in its own folder with:  
- 📓 Jupyter notebooks (EDA, feature engineering, modeling)  
- 📊 Visualizations and results  
- 📝 A project-specific README with problem, approach, and insights  

The goal of this portfolio is to demonstrate my ability to:
- Explore and clean real-world datasets  
- Engineer meaningful features  
- Build and evaluate predictive models  
- Interpret results and communicate insights clearly  

---

## 📂 Projects

### [Fraud Detection (IEEE-CIS)](./ieee-cis-fraud-detection)
End-to-end fraud detection pipeline using Kaggle’s IEEE-CIS dataset.  

- **Problem**: Detect rare fraudulent online transactions (~3.5% fraud rate).  
- **Approach**: Time-aware train/validation split, feature engineering (time, amount, email, device, missingness), and LightGBM modeling.  
- **Results**:  
  - ROC-AUC = **0.926**  
  - PR-AUC = **0.569** (≈16× better than random)  
- **Threshold Trade-offs**:  
  - Recall-heavy: Recall ~66%, Precision ~36% (good for manual review)  
  - Precision-heavy: Precision ~90%, Recall ~18% (good for auto-blocking high-confidence frauds)  
- **Insights**: Fraud strongly linked to free email domains, certain card issuers/types, transaction timing, and specific amount ranges.  

📊 Full details → [ieee-cis-fraud-detection](./ieee-cis-fraud-detection)

### Customer Churn Prediction (Telco)
End-to-end churn prediction pipeline using IBM’s Telco Customer Churn dataset.  

**Problem:** Predict which telecom customers are likely to churn (~26% churn rate), so the business can take targeted retention actions.  

**Approach:**  
- Data preprocessing (missing values, scaling, one-hot encoding).  
- Exploratory analysis: churn is highest for **month-to-month contracts, electronic check payments, short tenure, high charges, and fiber-optic customers**.  
- Models: Logistic Regression (Elastic Net), Random Forest, Calibrated SVC.  
- Cost-sensitive threshold tuning based on business assumptions (offer cost = $10, revenue saved = $80, loss from churn = $200).  

**Results:**  
- Test ROC-AUC = **0.839**, PR-AUC = **0.623** (vs baseline 0.27).  
- At optimal threshold (0.05): **Recall = 99%**, **Precision = 35%**, maximizing campaign ROI (**+ $18.3k expected value per batch**).  

**Insights:**  
- **Who churns?** New customers (<12 months), month-to-month contracts, electronic check payers, high monthly charges.  
- **Who stays?** Long-tenure customers, 1–2 year contracts, auto-pay users, lower charges.  
- Business can prioritize **retention offers** for high-risk groups to reduce churn profitably.  

📊 Full details → `telco-churn-prediction`

---
