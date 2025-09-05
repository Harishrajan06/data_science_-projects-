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

---
