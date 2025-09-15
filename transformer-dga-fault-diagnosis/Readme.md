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
| <img width="522" alt="XGBoost CM" src="https://github.com/user-attachments/assets/0b42887c-b259-4139-8cd7-d97c0a7a845e" /> | <img width="522" alt="CatBoost CM" src="https://github.com/user-attachments/assets/9a8b6fb2-14cf-4ca7-9ef9-6c57e27c87a2" /> |

✅ Very few misclassifications (<0.2%), **no missed Thermal <300°C faults**.  

---

## 📊 Feature Importance
XGBoost feature importance:  

<img width="790" alt="XGB Importance" src="https://github.com/user-attachments/assets/7d138ca7-4d18-43e1-aba2-bd0a1a920e5b" />

- **CH₄/H₂ ratio (R1)** is the strongest driver.  
- **Carbon Monoxide (CO)** and **Ethane (C₂H₆)** are also critical.  
- Matches domain knowledge:  
  - H₂/CH₄ → Partial Discharge.  
  - CO → Thermal faults.  

---

## 🤖 Model Explainability (SHAP)

### Global Importance (per class)
<img width="790" height="540" alt="Image" src="https://github.com/user-attachments/assets/edb714e7-da35-474c-8fde-5a29fbadf6b1" />

### Beeswarm (directional impact)
<img width="766" alt="shap_beeswarm" src="https://github.com/user-attachments/assets/b75745d6-e762-4dcf-89c6-9ae7a2d67324" />

### Local Explanations
- **Normal sample**  
<img width="925" height="600" alt="Image" src="https://github.com/user-attachments/assets/f84a2c01-72e5-4f9a-8309-ecf696e34a9c" />

- **Partial Discharge sample**  
<img width="895" alt="shap_pd" src="https://github.com/user-attachments/assets/fab3762e-5898-4da1-a1f9-5738c291bda7" />

- **Thermal <300°C sample**  
<img width="937" alt="shap_thermal" src="https://github.com/user-attachments/assets/daa13a35-05c6-4cf9-a71d-4b4baf6bacfc" />

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
