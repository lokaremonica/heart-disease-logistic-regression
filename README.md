# Heart Disease Prediction using Logistic Regression (from Scratch)

This project implements a logistic regression model from scratch to predict the likelihood of coronary heart disease (CHD) within 10 years using patient data. It includes steps such as data cleaning, feature engineering, normalization, model training, evaluation, and hyperparameter tuning.

---

## 📁 Files

- `heart_disease_train.csv`: Training dataset  
- `heart_disease_test.csv`: Testing dataset  
- `logistic_regression.ipynb`: Jupyter notebook with full code, training logic, and evaluation  

---

## 🩺 Dataset Overview

Based on the Framingham Heart Study, the dataset includes features such as:
- `age`, `gender`, `BMI`, `glucose`, `heartRate`, `BPMeds`, `cigsPerDay`, etc.  
- **Target variable:** `TenYearCHD` (0 = no CHD, 1 = CHD)

---

## 🔍 Workflow Summary

### 1. Data Preprocessing
- Loaded and examined missing values in features like `glucose`, `BMI`, `cholesterol`, etc.
- Imputed missing values using **group-based strategies**.
- Removed the `education` column due to irrelevance.
- Categorical values such as `BPMeds` were cast from float to int.

### 2. Normalization
- All continuous variables normalized using **Z-score standardization**:  
z = (x - mean) / std
- Binary categorical variables retained in 0/1 format.

### 3. Class Imbalance Handling
- Significant class imbalance observed (~15% CHD).
- Used **undersampling** of the majority class for balanced learning.

---

## 🧠 Model Architecture

### Base Model (Logistic Regression from Scratch)
- Used sigmoid activation:  
sigmoid(z) = 1 / (1 + e^-z)

- Loss: **Binary Cross-Entropy**
- Optimization: **Batch Gradient Descent**

### Parameters
- Learning Rate: 0.2  
- Epochs: 50

---

## 📊 Comprehensive Model Comparison

### 🔹 Base Model Metrics

**Training Set:**
- **Confusion Matrix:**  
  `[[2546  328], [ 382  134]]`
- **Accuracy:** 79.06%
- **Precision:** 29.00% – Of predicted positive cases, 29.00% were correct.
- **Recall:** 25.97% – The model identified only 25.97% of actual positive cases (CHD).
- **F1 Score:** 27.40% – Indicates poor balance between precision and recall, highlighting the challenge of identifying the positive class.
- **AUC:** 0.6437 – Moderate ability to distinguish between classes, but still underperforming.

**Test Set:**
- **Confusion Matrix:**  
  `[[624  96], [101  27]]`
- **Accuracy:** 76.77%
- **Precision:** 21.95% – Of predicted positive cases, only 21.95% were correct.
- **Recall:** 21.09% – Identified just 21.09% of actual positive cases.
- **F1 Score:** 21.51% – Consistent with training, showing the model’s struggle with classifying the minority class.
- **AUC:** 0.6512 – Slightly above random guessing, indicating limited class separation.

---

### 🔹 Best Model Metrics (After Hyperparameter Tuning)

**Training Set:**
- **Confusion Matrix:**  
  `[[2593  281], [ 358  158]]`
- **Accuracy:** 81.15%
- **Precision:** 35.99% – Improved from the base model, though still affected by false positives.
- **Recall:** 30.62% – Significant gain in detecting CHD-positive cases.
- **F1 Score:** 33.09% – Improved balance between precision and recall.
- **AUC:** 0.7238 – Better ability to distinguish between positive and negative classes.

**Test Set:**
- **Confusion Matrix:**  
  `[[656  64], [85  43]]`
- **Accuracy:** 82.43%
- **Precision:** 40.19% – More correct CHD predictions than the base model.
- **Recall:** 33.59% – Further recall improvement, critical in medical diagnostics.
- **F1 Score:** 36.60% – Clear improvement in model’s positive class prediction performance.
- **AUC:** 0.7648 – Stronger generalization and separation between CHD and non-CHD.

---

## 🧠 Interpretation

- ✅ **Best model outperforms** the base model on all metrics: recall, F1 score, and AUC.
- 📈 The recall and F1 score improvements reflect the model’s better ability to identify CHD-positive cases.
- 🎯 While precision slightly decreased, **higher recall is prioritized** in medical risk predictions.
- 🔄 **Consistent metrics across train and test** sets show good generalization and minimal overfitting.
- 📊 **AUC increased** from 0.6437 → 0.7648, confirming better class separation.

---

## 🩺 Conclusion

- The base model was weak at identifying CHD cases.
- The best model, tuned via grid search and undersampling, offers **significant clinical value** by reducing false negatives.

---

## 📌 Recommendations for Further Improvement

- Use **SMOTE** to synthetically oversample minority class.
- Add **L1/L2 regularization** to reduce variance.
- Experiment with **tree-based models** (e.g., Random Forest, XGBoost).
- Explore **cost-sensitive learning** to further optimize recall-precision trade-offs.

---

## 🔗 Acknowledgments

- **Dataset**: Framingham Heart Study
- **Modeling Decisions**: Guided by cardiovascular risk prediction literature and domain best practices.
