# 🏭 Steel Coil Defect Prediction
### Surface defect prediction using PLC sensor data and Machine Learning analytics

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1gvn414sWfIazjJFL1FOf6NmcIg7O9Hip#scrollTo=cell-coil-agg)

## 📌 Project Overview
The objective of this project is to identify the root causes of defects in steel coil production by integrating **PLC (Programmable Logic Controller)** sensor data with inspection records.

## 🛠 Model Focus: XGBoost Classifier
The core of this project is a high-performance Gradient Boosting model. Given the imbalance and complexity of the tabular sensor data, **XGBoost** was selected for its robustness and efficiency.

### ⚙️ Hyperparameter Tuning
To ensure optimal performance and prevent overfitting, the model was tuned using a **ParameterGrid** search combined with **GroupKFold** cross-validation. The key hyperparameters used in the final model are:

* **n_estimators:** 200 (Number of boosting rounds)
* **max_depth:** 4 (Controlled tree depth to limit complexity)
* **learning_rate:** 0.05 (Small step size for stable convergence)
* **subsample:** 0.8 (Fraction of samples used for each tree)
* **colsample_bytree:** 0.8 (Fraction of features used for each tree)
* **scale_pos_weight:** Adjusted based on defect prevalence to handle class imbalance.

### 🧪 Cross-Validation Strategy
We implemented a **GroupKFold (n_splits=5)** strategy, grouping by `COIL` ID. This ensures that data from the same coil is never present in both the training and validation sets simultaneously, guaranteeing a realistic estimate of model performance on new, unseen coils.

## 📊 Classification Results
The model was evaluated on individual defect types and a global "Any Defect" target. Below are the performance metrics (Mean CV):

| Target | Accuracy | Precision | Recall | F1-Score |
| :--- | :--- | :--- | :--- | :--- |
| **DIF_TIPO_3** (Most Prevalent) | 83.1% | 0.81 | 0.85 | 0.83 |
| **DIF_TIPO_4** | 88.4% | 0.84 | 0.79 | 0.81 |
| **ANY_DEFECT** (Global) | 85.6% | 0.84 | 0.87 | 0.85 |

*Key Insight:* The model shows particularly strong performance on **DIF_TIPO_6**, while maintaining high stability on the most frequent defect (**TIPO_3**).

## 🔍 Root Cause Analysis (SHAP)
Model interpretability through **SHAP values** confirmed that thermal factors are the primary "drivers" in the defect formation process.

### 🌡️ Temperature as the Primary Driver
[cite_start]From the analysis of SHAP plots (both Beeswarm and Feature Importance), it is clear that **Temperature Zones** (represented in the model via PCA) have the most significant impact on the probability of a defect:

* [cite_start]**Positive Correlation:** The plots show that high values in thermal sensors (indicated by red dots in the Beeswarm plots) are strongly associated with an increased risk of defects (positive SHAP value).
* [cite_start]**Critical Process Points:** **Furnace Zone 5 (AIR_Z5 / GAS_Z5)** was isolated as a critical point[cite: 248]. [cite_start]Excessive temperatures in this stage act as a trigger, damaging the coil surface before the cooling phase even begins[cite: 248, 249].
* [cite_start]**Physical Positioning:** Beyond temperature, the **LASER_RAFF_1** sensor indicates that the vertical position of the strip exiting the furnace affects thermal stability, doubling the risk of surface anomalies if not maintained within optimal parameters[cite: 247, 249].

[cite_start]In summary, the model proves that the thermal stability of the furnace is the key to reducing production waste[cite: 516].

---
**DSBA Team - ML Fieldwork**
*Team members: Filippo Iacchia, Israa Ismail, Giovanni Duca, Edoardo Cerri, Anastasija Smiljkovska*.
