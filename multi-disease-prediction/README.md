# 📊 Multi-Disease Prediction (Diabetes, Heart Disease, Stroke)

## 📌 Problem
Chronic diseases such as **Diabetes, Heart Disease, and Stroke** are major public health concerns. Early detection can significantly improve patient outcomes and reduce healthcare costs.  
The goal of this project is to **predict which patients are at risk for these three diseases simultaneously** using clinical and demographic data.

---

## 📂 Dataset
- **Sources:** Three publicly available healthcare datasets:  
  1. Diabetes dataset  
  2. Heart Disease dataset  
  3. Stroke dataset  
- **Size:** Combined dataset → 6,484 patients × 34 features  
- **Targets:**  
  - `Diabetes` (0 = no, 1 = yes)  
  - `HeartDisease` (0 = no, 1 = yes)  
  - `Stroke` (0 = no, 1 = yes)  
- **Features:** Age, BMI, hypertension, heart disease history, glucose levels, smoking status, gender, and additional clinical measures from each dataset.  

---

## 🔎 Exploratory Data Analysis (EDA)
Key observations:
- **Age & BMI** are strong indicators across multiple diseases.  
- **Hypertension & Heart Disease history** are highly predictive of heart conditions.  
- **Glucose levels & BMI** correlate with diabetes risk.  
- **Stroke** is highly imbalanced (~60 positive cases vs 1,237 negative).  

---

## ⚙️ Approach
- **Preprocessing:**  
  - Aligned common features across all datasets.  
  - Handled missing values (median for numeric, mode for categorical).  
  - Encoded categorical variables using `LabelEncoder`.  
  - Scaled numeric features using `StandardScaler`.  

- **Modeling:**  
  - Base classifier: **Random Forest** (`n_estimators=200`, `max_depth=10`, `class_weight='balanced'`)  
  - Multi-disease prediction using **MultiOutputClassifier**.  
  - Probability calibration using **CalibratedClassifierCV** for more reliable confidence scores.  

- **Evaluation Metrics:**  
  - Accuracy  
  - F1-Score  
  - ROC-AUC  
  - Confusion matrices  

- **Explainability:**  
  - **SHAP** values used to understand feature importance for each disease prediction.

---

## 📈 Results
| Disease        | Accuracy | ROC-AUC |
|----------------|----------|---------|
| Diabetes       | 95.8%    | 0.979   |
| Heart Disease  | 99.5%    | 0.9997  |
| Stroke         | 95.4%    | 0.853   |

**Sample Predictions:**  

**Binary Predictions (first 5 rows)**  

---

## 📊 Visualizations

**1️⃣ Predicted Class Distribution**  
- **Diabetes**:  
  ![Predicted Class Distribution - Diabetes](path_to_image_diabetes.png)  
- **Heart Disease**:  
  ![Predicted Class Distribution - Heart Disease](path_to_image_heart.png)  
- **Stroke**:  
  ![Predicted Class Distribution - Stroke](path_to_image_stroke.png)  

**2️⃣ Confusion Matrices**  
- **Diabetes Confusion Matrix**  
  ![Confusion Matrix - Diabetes](path_to_cm_diabetes.png)  
- **Heart Disease Confusion Matrix**  
  ![Confusion Matrix - Heart Disease](path_to_cm_heart.png)  
- **Stroke Confusion Matrix**  
  ![Confusion Matrix - Stroke](path_to_cm_stroke.png)  

**3️⃣ SHAP Summary Plots**  
- Highlights most important features driving predictions for each disease.

---

## 💡 Insights
- **Diabetes:** BMI, glucose levels, age, and pregnancies are top predictors.  
- **Heart Disease:** Age, cholesterol, resting blood pressure, and prior heart conditions are key drivers.  
- **Stroke:** Hypertension, age, and glucose levels are most important, but predictions are limited due to class imbalance.  

---

## 🚀 Business/Healthcare Recommendations
- Use model probabilities to **flag high-risk patients** for preventive screenings.  
- Focus lifestyle interventions on patients with high BMI, hypertension, or prior heart conditions.  
- Consider **data augmentation or additional stroke data** to improve predictive power.  
- SHAP insights can inform **personalized treatment plans** for at-risk individuals.  

---

