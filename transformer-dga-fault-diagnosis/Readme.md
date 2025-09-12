# ⚡ Transformer Fault Diagnosis (Dissolved Gas Analysis - DGA)

## 📌 Problem
Transformers are critical assets in power systems, and their failures can lead to **costly outages** and reliability issues.  
The goal of this project is to **predict transformer fault types from dissolved gas analysis (DGA)**, combining **rule-based methods (Rogers Ratio)** with **machine learning (XGBoost, CatBoost)** for accurate and explainable fault detection.  

We classify samples into:
- **Normal**
- **Partial Discharge**
- **Thermal <300°C**

---

## 📂 Dataset
- **Source:** Lewis et al. (2022) UK Transformer DGA dataset (Zenodo).  
- **Size:** ~17,540 samples × 28 features.  
- **Features:** Concentrations of 9 key gases (H₂, CH₄, C₂H₂, C₂H₄, C₂H₆, CO, CO₂, O₂, H₂O).  
- **Target labels:** Derived using **Rogers Ratio diagnostic rules**.  

📊 **Class distribution:**
- Thermal <300°C → 16,566  
- Normal → 5,774  
- Partial Discharge → 1,842  

---

## 🔎 Exploratory Data Analysis (EDA)
- Different transformers had different subsets of gas measurements.  
- Strong **class imbalance** observed (Thermal <300°C dominant).  
- Ratios **R1 (CH₄/H₂)**, **R2 (C₂H₂/C₂H₄)**, and **R3 (C₂H₄/C₂H₆)** were engineered for fault diagnosis.  

---

## ⚙️ Approach
- **Baseline:** Rogers Ratio classification (traditional rule-based).  
- **Feature Engineering:** Derived ratios + raw gas values.  
- **Models:**  
  - XGBoost (tree-based boosting).  
  - CatBoost (handles categorical + robust to imbalance).  
- **Explainability:** SHAP for global, per-class, and local feature impact.  

---

## 📈 Results

### Classification Reports
Both **XGBoost** and **CatBoost** achieved near-perfect performance:  

- Accuracy ≈ 100%  
- Precision & Recall ≈ 1.0 across all classes  

### Confusion Matrices
| XGBoost | CatBoost |
|---------|----------|
| ![xgb_cm](images/xgb_cm.png) | ![cat_cm](images/cat_cm.png) |

✅ Very few misclassifications (<0.2%), **no missed Thermal <300°C faults**.  

---

## 📊 Feature Importance
XGBoost feature importance:  

![xgb_importance](images/xgb_importance.png)  

- **CH₄/H₂ ratio (R1)** is the strongest driver.  
- **Carbon Monoxide (CO)** and **Ethane (C₂H₆)** are also critical.  
- Matches domain knowledge:  
  - H₂/CH₄ → Partial Discharge.  
  - CO → Thermal faults.  

---

## 🤖 Model Explainability (SHAP)

### Global Importance (per class)
![shap_class_bar](images/shap_class_bar.png)

### Beeswarm (directional impact)
![shap_beeswarm](images/shap_beeswarm.png)

### Local Explanations
- **Normal sample**  
![shap_normal](images/shap_normal.png)

- **Partial Discharge sample**  
![shap_pd](images/shap_pd.png)

- **Thermal <300°C sample**  
![shap_thermal](images/shap_thermal.png)

---

## 💡 Insights
- **R1 (CH₄/H₂ ratio)** is the most reliable diagnostic feature, confirming Rogers rules.  
- **CO concentration** is a key thermal fault indicator.  
- ML models not only replicate traditional rules but achieve **higher reliability and explainability**.  
- SHAP provides transparency, making results interpretable for power engineers.  

---

## 🚀 Impact
This project demonstrates how **domain expertise (Rogers Ratios)** can be combined with **modern machine learning** to:  
- Improve transformer fault diagnosis accuracy.  
- Provide interpretable results to engineers.  
- Reduce the risk of costly transformer failures.  

---

