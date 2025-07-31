# Heart Disease Prediction using Logistic Regression (from Scratch)

This project implements a logistic regression model from scratch to predict the likelihood of coronary heart disease (CHD) within 10 years using patient data. It includes steps such as data cleaning, feature engineering, normalization, model training, evaluation, and hyperparameter tuning.

---

## 📁 Files

- `heart_disease_train.csv`: Training dataset  
- `heart_disease_test.csv`: Testing dataset  
- `logistic_regression.ipynb`: Jupyter notebook with full code, training logic, and evaluation  

## 🩺 Dataset Overview

Sourced from the **Framingham Heart Study**, the dataset contains:
- **Features**: age, gender, BMI, glucose, heartRate, cigsPerDay, cholesterol, BPMeds, etc.
- **Target variable**: `TenYearCHD` (1 = CHD present within 10 years, 0 = absent)

---

## 🔄 Data Preprocessing

### Missing Value Imputation:
Used medically-informed group-based imputation strategies:
- **Glucose**: by `diabetes` and `gender`
- **BMI**: by `age group`, `gender`, `hypertension`, `diabetes`
- **Cholesterol**: by `gender` and `hypertension`
- **BPMeds**: by `systolic BP` category, `age`, `hypertension`
- **Heart Rate**: by `age group`, `gender`, `BMI group`
- **CigsPerDay**: 0 for non-smokers, grouped imputation for smokers

> ✅ All missing values were filled using fallback strategies  
> ❌ `education` was dropped as it's not directly clinically relevant

### Normalization:
- Applied **Z-score normalization** to continuous features:  
  \[
  z = \frac{x - \mu}{\sigma}
  \]
- Binary categorical variables were left untouched (0/1 format)

---

## ⚖️ Class Imbalance Handling

- The dataset was highly imbalanced (~15% positive class)
- Applied **undersampling** to the majority class with variable ratios (0.2, 0.3, 0.4)

---

## 🧠 Base Model: Logistic Regression

### Architecture:
- Activation: **Sigmoid**
- Loss: **Binary Cross-Entropy**
- Optimization: **Full-batch Gradient Descent**
- Bias term: added manually to input features
- Weight Initialization: He initialization

### Base Hyperparameters:
- Learning Rate: `0.2`  
- Epochs: `20`  
- Sampling Ratio: `0.3`

---

## 📊 Base Model Performance

### Training Set:
- Accuracy: **79.06%**
- Precision: **29.00%**
- Recall: **25.97%**
- F1 Score: **27.40%**
- AUC: **0.644**

### Test Set:
- Accuracy: **76.77%**
- Precision: **21.95%**
- Recall: **21.09%**
- F1 Score: **21.51%**
- AUC: **0.651**

> 🚨 The base model struggles with detecting CHD (low recall & F1)

---

## 🔧 Model Tuning: Grid Search + Mini-Batch Gradient Descent

### Optimization Technique:
- **Mini-batch Gradient Descent**
- Convergence tracked via cost difference
- Bias manually included

### Grid Search Parameters:
| Hyperparameter     | Values                         |
|--------------------|--------------------------------|
| Learning Rate       | `[0.01, 0.05, 0.1]`             |
| Batch Size          | `[32, 64, 128]`                |
| Epochs              | `[500, 1000, 2000]`            |
| Sampling Ratio      | `[0.2, 0.3, 0.4]`              |

> 🔎 **81 total combinations** evaluated

---

## 🏆 Best Model Performance (After Tuning)

**Test Set Results:**
- Accuracy: **84.43%**
- Precision: **47.37%**
- Recall: **28.12%**
- F1 Score: **35.29%**
- AUC: **0.765**

> ✅ Significant boost in F1 and AUC  
> ✅ Recall improved — critical for medical risk identification


## 🩺 Conclusion

- The base model was weak at identifying CHD cases.
- The best model, tuned via grid search and undersampling, offers **significant clinical value** by reducing false negatives.

---

## 📈 Visualizations

- 📉 Cost vs Epoch curve
- 📊 ROC Curve for Train and Test sets
- 📐 AUC computed using trapezoidal integration

---

## ⚙️ Techniques Implemented

- Manual implementation of:
  - Sigmoid
  - Binary cross-entropy loss
  - Gradient computation
  - ROC curve and AUC
- Mini-batch gradient descent with early stopping
- Undersampling-based resampling strategy
- Grid search for 4 hyperparameters

---

## 🚀 Recommendations for Future Work

- Apply **SMOTE** for synthetic oversampling
- Add **L1/L2 regularization** to reduce overfitting
- Try ensemble methods like **Random Forest**, **XGBoost**
- Implement **cost-sensitive learning**
- Introduce model explainability using **SHAP/LIME**

---

## 📚 References

- Dataset: [Framingham Heart Study](https://www.nhlbi.nih.gov/science/cardiovascular-health-study-chs)
- Research-guided imputation strategies:  
  - https://academic.oup.com/aje/article-abstract/157/1/74/66183  
  - https://www.sciencedirect.com/science/article/pii/S1443950616315311

---

## 🧠 Author Notes

This project is intended for educational purposes and demonstrates how interpretable and accurate models can be built using fundamental ML concepts, even without relying on high-level libraries like `scikit-learn`.

