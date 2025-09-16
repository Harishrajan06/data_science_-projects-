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

Transformer Fault Diagnosis (DGA)  
Fault classification for power transformers using Dissolved Gas Analysis (DGA) data.

Problem: Detect transformer faults (Normal, Partial Discharge, Thermal <300°C) using gas concentration ratios, since failures can cause costly outages.

Approach:
- Applied Rogers Ratio method for rule-based labeling.
- Built ML models (XGBoost, CatBoost) on gas concentrations + ratios.
- Used SHAP for explainability (global + per-class + local).

Results:
- XGBoost & CatBoost achieved ≈100% accuracy.
- CH₄/H₂ ratio (R1) and CO identified as top drivers, consistent with engineering knowledge.
- SHAP visualizations confirmed interpretability of model predictions.

📊 Full details → [transformer-dga-fault-diagnosis](transformer-dga-fault-diagnosis)


---

### Multi-Disease Prediction (Diabetes, Heart Disease, Stroke)  
Predict multiple common diseases simultaneously using patient health records.  

**Problem:** Identify patients at risk of **Diabetes, Heart Disease, and Stroke** based on clinical and demographic features. Early prediction can help in preventive care and targeted interventions.  

**Approach:**  
- Merged three healthcare datasets (Diabetes, Heart Disease, Stroke) and aligned features.  
- Handled missing values, scaled numeric features, and encoded categorical features.  
- Built a **Random Forest-based Multi-Output Classifier** to predict multiple diseases simultaneously.  
- Calibrated probabilities for more reliable predictions and used **SHAP** for feature explainability.  
- Evaluated using **Accuracy, ROC-AUC, F1-Score**, and visualized predicted distributions and confusion matrices.  

**Results:**  
- High accuracy for Diabetes and Heart Disease (≈96–99%).  
- Moderate performance for Stroke due to class imbalance (~85% ROC-AUC).  
- Probabilities can be thresholded to adjust sensitivity for each disease.  
- SHAP analysis highlights the most important medical features for each prediction.  

📊 Full details → `multi-disease-prediction`

