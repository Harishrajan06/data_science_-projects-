# Fraud Detection (IEEE-CIS)

End-to-end fraud detection project using the Kaggle **IEEE-CIS Fraud Detection** dataset.  
The focus is on handling class imbalance, building robust models, and evaluating business trade-offs between precision and recall.

---

## 🔎 Problem
Online payment fraud is a **rare but costly** event (~3.5% of transactions in this dataset).  
The goal is to predict whether a transaction is fraudulent while balancing:  
- **Recall (catching more frauds)** vs.  
- **Precision (avoiding false alarms for genuine customers)**  

---

## 📦 Dataset
- Source: [Kaggle IEEE-CIS Fraud Detection](https://www.kaggle.com/c/ieee-fraud-detection)  
- After merging: ~590k rows × 434 columns  
- Target: `isFraud` (1 = fraud, 0 = genuine)  
- Fraud rate: ~3.5%  
- Features include:  
  - Transaction details (`TransactionAmt`, `ProductCD`, etc.)  
  - Card information (`card1`–`card6`)  
  - Address and email domains  
  - Device and browser info (`DeviceInfo`, `id_30`, `id_31`)  
  - Anonymized engineered features (`C*`, `D*`, `V*`, `id_*`)

---

## 🧭 Approach

### 1. Exploratory Data Analysis (EDA)
- Checked fraud distribution (3.5% → strong class imbalance).  
- Fraud amounts clustered in specific ranges.  
- Certain product codes, card issuers, and email domains showed higher fraud rates.  
- Device/browser types revealed unusual patterns.  
- Converted `TransactionDT` into days, hours, weekdays to capture time trends.

### 2. Feature Engineering
- **Time-based features**: day, hour, weekday, weekend flag.  
- **Amount features**: log-transformed `TransactionAmt`, quantile bins.  
- **Email grouping**: free domains, edu, corporate, missing; flag for sender/receiver match.  
- **Device simplification**: extract OS/browser families.  
- **Missingness indicators**: counts of missing `id_*` and `V*` features (missingness itself is predictive).  
- **Encoding**: frequency encoding for high-cardinality features like `card1`, `addr1`, `emaildomain`.

### 3. Modeling
- **Validation strategy**: Time-based split (last 30 days as validation) to avoid leakage.  
- **Model**: LightGBM with `scale_pos_weight` to handle class imbalance.  
- Early stopping and tuned hyperparameters (`num_leaves`, `subsample`, `colsample_bytree`).  

### 4. Evaluation Metrics
- ROC-AUC (overall ranking ability).  
- PR-AUC (important for imbalanced datasets).  
- Threshold analysis (precision vs recall trade-offs).  
- Confusion matrices at key thresholds.  
- SHAP values for explainability.

---

## 📈 Results

- **ROC-AUC:** 0.926  
- **PR-AUC:** 0.569 (baseline prevalence = 0.035 → ~16× better than random).  

### Threshold Trade-offs
- **Recall-heavy (F2-optimal, thr ≈ 0.592):**  
  - Recall ~66%, Precision ~36%  
  - TP = 2065, FP = 3682, FN = 1049, TN = 82,530  
  - ✅ Good for manual review (catch more fraud).  

- **Precision-heavy (Prec ≥ 0.90, thr ≈ 0.987):**  
  - Precision ~90%, Recall ~18%  
  - ✅ Good for automatic blocking of high-confidence fraud.  

---

## 🖼️ Key Visuals

<p float="left">
  <img src="../ieee-cis-fraud-detection/images/roc_curve.png" width="45%" />
  <img src="../ieee-cis-fraud-detection/images/pr_curve.png"  width="45%" />
</p>

<p float="left">
  <img src="../ieee-cis-fraud-detection/images/confusion_f2_opt.png" width="45%" />
  <img src="../ieee-cis-fraud-detection/images/confusion_prec90.png"  width="45%" />
</p>

<p float="left">
  <img src="../ieee-cis-fraud-detection/images/feature_importance.png" width="45%" />
  <img src="../ieee-cis-fraud-detection/images/shap_summary_bar.png"  width="45%" />
</p>

---

## 💡 Insights
- **Email domains**: Free/disposable emails more fraud-prone.  
- **Card types/issuers**: Some issuers show higher risk.  
- **Transaction timing**: Odd hours/weekends have higher fraud likelihood.  
- **Transaction amounts**: Fraud often clusters in specific low-to-mid ranges.  
- **Anonymized features (`V*`, `D*`, `C*`)**: carry strong hidden fraud signals.  

---

## 🛠️ Tech Stack
- Python, Pandas, NumPy  
- LightGBM (gradient boosting for tabular data)  
- Scikit-learn (metrics, preprocessing)  
- Matplotlib, Seaborn (EDA & plots)  
- SHAP (explainability)

---

## 🚀 How to Run
```bash
pip install -r requirements.txt
# Open the notebook:
# ieee_fraud_detection.ipynb

