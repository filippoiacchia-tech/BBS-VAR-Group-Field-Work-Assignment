# 🏭 Steel Coil Defect Prediction
### Surface defect prediction using PLC sensor data and Machine Learning analytics

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1gvn414sWfIazjJFL1FOf6NmcIg7O9Hip#scrollTo=cell-coil-agg)

## 📌 Project Overview
[cite_start]The objective of this project is to identify the root causes of defects in steel coil production[cite: 42, 43]. [cite_start]By integrating **PLC (Programmable Logic Controller)** sensor data with inspection records, we developed a predictive model to detect anomalies early and support real-time decision-making[cite: 37, 39].

**Business Goals:**
* [cite_start]Reduce waste and production costs[cite: 48].
* [cite_start]Improve process control and final product quality[cite: 49].

## 🛠 Methodology & Pipeline
[cite_start]The project follows a structured Machine Learning pipeline divided into 4 main phases[cite: 54]:

1.  [cite_start]**EDA & Data Merge:** Integration of 299,384 rows of sensor data (106 channels) with defect records[cite: 65, 67, 107].
2.  [cite_start]**Preprocessing & Feature Engineering:** Handling "tail-out" effects and performing dimensionality reduction (PCA) within semantic groups[cite: 138, 328, 341].
3.  [cite_start]**Model Training:** Implementation of an **XGBoost** classifier with **GroupKFold** validation to prevent data leakage between coils[cite: 361, 364, 370].
4.  [cite_start]**Defect Prediction & Interpretation:** Results analysis using SHAP values for Root Cause Analysis[cite: 368, 448].

## 📊 Key Findings: The "Process Drivers"
[cite_start]Through K-Means clustering and SHAP analysis, we isolated two critical factors that double the risk of defects[cite: 240, 241, 245]:

* **LASER_RAFF_1:** Strip position post-furnace. [cite_start]If the strip exits the furnace at the wrong height, surface defects are significantly more likely[cite: 247].
* **AIR_Z5 / GAS_Z5:** Zone 5 furnace combustion. [cite_start]When this zone runs too hot, the strip surface is damaged before the cooling process even begins[cite: 248].

## 📈 Main Target Performance (Tipo 3 & 4)
[cite_start]The model focuses on the most prevalent defects (Tipo 3: 34.6%)[cite: 236, 256].
* [cite_start]**Mean Accuracy:** ~83%[cite: 428, 435].
* [cite_start]**Lift @ Top 20%:** The model predicts defects nearly **3 times better** than random guessing[cite: 421].
* [cite_start]**Gain @ Top 40%:** We capture 80% of the defective population by analyzing only the first 40% of the coils[cite: 420].

## 🚀 The Solution: Live Dashboard
[cite_start]The project proposes a shift from reactive inspection to proactive monitoring through a **Live Dashboard** that integrates[cite: 518, 519, 530]:
* [cite_start]**Stream 1:** Real-time processed PLC data (every 7 meters)[cite: 520, 534, 550].
* [cite_start]**Stream 2 (Proposed):** Computer Vision for immediate auto-labeling of defects at the line exit[cite: 521, 524, 549].

---
[cite_start]**DSBA Team - ML Fieldwork** [cite: 5, 7]
[cite_start]*Team members: Edoardo Cerri, Israa Ismail, Giovanni Duca, Filippo Iacchia, Anastasija Smiljkovska*[cite: 12, 15, 20, 23, 29].
