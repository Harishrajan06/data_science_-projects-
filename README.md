# Data Science Projects Portfolio

This repository contains my end-to-end data science and machine learning projects.  
Each project is organized in its own folder with notebooks, results, and a detailed report.  
More projects will be added over time.

---

## 📂 Projects

### [Fraud Detection (IEEE-CIS)](./ieee-cis-fraud-detection)

#### 🔎 Problem
Online payment fraud is a multi-billion dollar challenge. Fraudulent transactions are rare (only ~3.5% of cases) but extremely costly if missed.  
The goal is to predict whether a transaction is fraudulent, balancing **recall** (catch more fraud) and **precision** (minimize false alarms).

#### 📦 Dataset
- Kaggle **IEEE-CIS Fraud Detection** dataset  
- After merging: ~590k transactions × 434 features  
- Highly imbalanced target: `isFraud` (positives ≈ 3.5%)  
- Rich but messy features: transaction details, card info, billing addresses, device/browser info, anonymized engineered features (`V*`, `C*`, `D*`, `id_*`)

#### 🧭 Approach
1. **EDA**: explored fraud patterns across amounts, product codes, cards, emails, devices, and time (`TransactionDT`).  
2. **Feature Engineering**:  
   - Time features: day, hour, weekday/weekend  
   - Amount transformations: log scaling, quantile bins  
   - Email domain grouping (`free`, `edu`, `other`, `missing`) + sender/receiver match flag  
   - Device/OS/browser simplification  
   - Missingness indicators for `id_*` and `V*` blocks  
   - Frequency encoding for high-cardinality features (e.g. `card1`, `addr1`)  
3. **Validation**: time-based split (last 30 days as hold-out) to avoid leakage.  
4. **Model**: LightGBM (with `scale_pos_weight` for imbalance, early stopping).  
5. **Evaluation**: ROC-AUC, PR-AUC, threshold tuning (recall vs precision).  
6. **Explainability**: Feature importance + SHAP values to understand fraud drivers.

#### 📈 Results
- **ROC-AUC:** 0.926  
- **PR-AUC:** 0.569 (vs baseline prevalence ~0.035 → ~16× better than random)

**Threshold trade-offs:**  
- **Recall-heavy (F2-optimal, thr ≈ 0.592)**  
  - Recall ≈ 66%, Precision ≈ 36%  
  - Good for catching more fraud with manual review queue  
- **Precision-heavy (Precision ≥ 0.90, thr ≈ 0.987)**  
  - Precision ≈ 90%, Recall ≈ 18%  
  - Good for auto-blocking high-confidence frauds  

#### 💡 Insights
- **Email domains** (free/disposable vs edu/corporate) strongly signal fraud.  
- **Card issuer/type** matters: some issuers show higher fraud risk.  
- **Transaction timing & delays (`D*`)** reveal unusual activity patterns.  
- **Transaction amounts** show fraud clustering in specific ranges.  
- Anonymized `V*` features capture hidden but powerful fraud patterns.  

📊 See full details in the project folder → [ieee-cis-fraud-detection](./ieee-cis-fraud-detection)
