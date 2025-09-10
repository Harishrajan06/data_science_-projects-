# 📊 Telco Customer Churn Prediction

## 📌 Problem
Customer churn is one of the biggest challenges for telecom companies — acquiring a new customer is far more expensive than retaining an existing one.  
The goal of this project is to **predict which customers are at risk of leaving** so the business can take targeted retention actions (discounts, upgrades, proactive outreach).

---

## 📂 Dataset
- **Source:** IBM Telco Customer Churn dataset (Kaggle).  
- **Size:** ~7,043 customers × 21 features.  
- **Target:** `Churn` (Yes = customer left, No = stayed) → ~26% churn rate.  
- **Features:**  
  - Demographics: gender, senior citizen, dependents.  
  - Account: tenure, contract type, payment method.  
  - Services: phone, internet, streaming, tech support.  
  - Billing: monthly charges, total charges.  

---

## 🔎 Exploratory Data Analysis (EDA)
Key business findings:
- **Contract Type:** Month-to-month contracts churn 42.7%, vs. 2.8% for two-year contracts.  
- **Payment Method:** Electronic check customers churn 45% — highest among payment methods.  
- **Internet Service:** Fiber optic customers churn 41.9%, DSL only 19%.  
- **Monthly Charges:** High-bill customers churn almost twice as often (35% vs 18%).  
- **Tenure:** New customers (<12 months) churn 48%, while long-tenure customers (>5 years) churn only 6.7%.  

---

## ⚙️ Approach
- **Preprocessing:** missing values handled, numeric features scaled, categorical features one-hot encoded.  
- **Models tested:**  
  - Logistic Regression (Elastic Net) → interpretable baseline.  
  - Random Forest → nonlinear model with feature importance.  
  - Calibrated Linear SVC → margin-based model with probability calibration.  
- **Cost-sensitive threshold tuning:**  
  - Offer cost = $10  
  - Revenue saved (if churn prevented) = $80  
  - Revenue lost (if churn missed) = $200  

---

## 📈 Results
- **Test ROC-AUC:** 0.839  
- **Test PR-AUC:** 0.623 (baseline = 0.27)  
- **At optimal threshold (0.05):**  
  - Recall = 99% (catch nearly all churners)  
  - Precision = 35% (1 in 3 targeted customers are actual churners)  
  - Expected Value (ROI) = +$18.3k per campaign batch  

---

## 📊 Visualizations
**ROC Curve (Validation):** All models perform similarly, ROC-AUC ≈ 0.84.  
![ROC Curve](https://github.com/user-attachments/assets/809ae7c7-ef16-4cda-ad02-529c07af86b3)

**Precision-Recall Curve (Validation):** Precision stays well above baseline (0.27), PR-AUC ≈ 0.62.  
![PR Curve](https://github.com/user-attachments/assets/e0f274af-3fa2-4162-9920-60fcb687655d)

**Calibration Curve (Validation):** Predicted probabilities are well-calibrated, making thresholds reliable.  
![Calibration Curve](https://github.com/user-attachments/assets/ae2eb576-932b-4a5b-ba59-d55d35e0327a)

**Cumulative Gains Curve (Validation):** Top 20% of customers contain ~60%+ of churners — useful for campaign targeting.  
![Cumulative Gains](https://github.com/user-attachments/assets/58d5552e-0f5a-47cd-9a66-9cac63b39878)


---

## 💡 Insights
- **Who churns?**  
  - New customers (<12 months)  
  - Month-to-month contracts  
  - Electronic check payers  
  - High monthly charges  
  - Fiber optic users  

- **Who stays?**  
  - Long-tenure customers (>5 years)  
  - Annual/two-year contracts  
  - Auto-pay users (bank/credit card)  
  - Lower monthly charges  

---

## 🚀 Business Recommendation
- Target **high-risk customers** with proactive retention offers (discounts, loyalty perks, support calls).  
- Focus especially on **new month-to-month customers with high bills**.  
- Encourage **auto-pay enrollment** to reduce churn.  
- Prioritize **long-term contracts** in sales strategy.  

---



