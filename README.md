# Diabetes-Related Hospital Readmissions: A Predictive Modeling Approach
**Author:** Alex Nite  
**Dataset:** UCI Diabetes 130-US Hospitals (1999–2008) + HRRP Hospital-Level Dataset

---

##  Project Overview
This project builds a predictive modeling framework to identify which diabetes patients are most likely to be readmitted within 30 days. Using the UCI Diabetes 130-US Hospitals dataset and the Hospital Readmissions Reduction Program (HRRP) dataset, the analysis integrates **patient-level clinical features** with **hospital-level performance metrics** to understand both individual and system-wide drivers of readmission risk.

The project applies **data cleaning, feature engineering, PCA, supervised machine learning, and exploratory analysis** to uncover patterns behind readmissions and evaluate model performance.

---

## Key Objectives
- Predict 30‑day readmissions for diabetes patients  
- Identify the strongest patient-level predictors of readmission  
- Examine hospital-level performance using HRRP metrics  
- Compare multiple machine learning models  
- Use PCA to explore latent structure and reduce noise  
- Provide actionable insights for reducing preventable readmissions  

---

## Datasets Used

### **1. UCI Diabetes 130-US Hospitals Dataset**
- 100,000+ patient encounters  
- Demographics, diagnoses, labs, medications, admission/discharge details  
- Readmission categories: *NO*, *>30*, *<30*  
- Collected from 130 U.S. hospitals (1999–2008)

### **2. HRRP Hospital-Level Dataset**
- Expected vs. actual readmission rates  
- Excess readmission ratios  
- Hospital penalties under HRRP  
- System-level performance indicators  

---

##  Data Cleaning & Preprocessing

### **Diabetes Dataset**
- Dropped high-missingness columns (A1Cresult, medical_specialty, payer_code, weight, etc.)  
- Removed low-variance medication features  
- Created **total_prior_visits** (sum of outpatient, emergency, inpatient visits)  
- Converted readmission into binary target:  
  - `0 = NO`  
  - `1 = <30 or >30`  
- Imputed missing race values  
- Normalized all numeric features  
- Applied class weights to address imbalance  

### **Hospital Dataset**
- Removed administrative and low-information columns  
- Median imputation for missing numeric values  
- Created binary target:  
  - `1 = Excess readmissions (ratio > 1.0)`  
  - `0 = Within expected range`  
- One-hot encoded categorical features  
- Standardized all numeric variables  

---

##  PCA (Dimensionality Reduction)

### **Diabetes Dataset**
PCA revealed interpretable components:

- **PC1:** Visit complexity (length of stay, meds, labs)  
- **PC3:** Prior visits + readmission tendency  
- **PC4:** Admission type (emergency vs elective)  
- **PC6:** Discharge disposition  
- **PC7:** Chronic frequent users vs. stable patients  

### **Hospital Dataset**
- **PC1:** Readmission rate dimension (predicted + expected)  
- **PC2:** Hospital size/volume  
- **PC5:** Provider ID + excess readmission linkage  

PCA helped reduce noise and highlight structural patterns.

---

## Machine Learning Models

### **Models Applied**
- Logistic Regression  
- Decision Tree  
- Random Forest  
- K-Nearest Neighbors (KNN)  
- PCA + ML pipelines  

### **Why These Models?**
- Logistic Regression → interpretability  
- Decision Tree → rule-based structure  
- Random Forest → strong performance + robustness  
- KNN → baseline non-parametric comparison  

### **Model Insights**
- **Random Forest** consistently performed best across accuracy, F1, and AUC  
- Logistic Regression provided the clearest interpretability  
- KNN struggled due to dataset size and high dimensionality  
- PCA improved stability but reduced interpretability  

---

## Key Predictors of Readmission
Across models and PCA loadings, the strongest predictors were:

### **Patient-Level**
- Age  
- Number of prior inpatient/emergency visits  
- Medication changes during visit  
- Discharge disposition  
- Number of diagnoses  
- Length of stay  
- Admission type  

### **Hospital-Level**
- Excess readmission ratio  
- Predicted vs. expected readmission rate  
- Hospital size (number of discharges)  

These factors align with clinical literature on diabetes readmissions.

---

## 📈 Exploratory Data Analysis (Highlights)
- Most patients were **not** readmitted; <30-day readmissions were the smallest group  
- Women represented a slightly larger portion of the dataset  
- Readmission risk increased with age, especially 60–80  
- Patients with medication changes had significantly higher readmission rates  
- Higher lab procedure counts correlated with more complex cases  

---

##  Key Findings
- Tree-based models (Random Forest) outperform simpler models  
- Readmissions are driven by both **clinical complexity** and **care transitions**  
- PCA reveals meaningful latent structure tied to visit complexity and patient history  
- HRRP metrics show variation in excess readmission performance across hospitals  
- Predictive modeling can help identify high-risk patients early  

---

## Limitations
- UCI dataset is older (1999–2008) and may not reflect current practices  
- Missingness in labs and medications required feature removal  
- KNN limited by computational constraints  
- HRRP dataset lacks patient-level detail  
- PCA reduces interpretability of transformed features  

---

##  Future Work
- Apply XGBoost and LightGBM for improved performance  
- Use SHAP for model interpretability  
- Integrate social determinants of health (SDOH)  
- Build a real-time readmission risk dashboard  
- Explore deep learning (LSTM) for sequential visit modeling  

---

