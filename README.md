# Construction_Risk_Prediction_Project
# Project Title: Predictive Analysis of Schedule Delays and Cost Overruns in Building Construction Using Machine Learning

## 1. Abstract

Construction projects often face two major challenges: **schedule delays and cost overruns**. This project uses machine learning to predict these risks in building construction projects.

Three classification models—**Logistic Regression, Random Forest, and XGBoost**—are compared separately for schedule delay and cost-overrun prediction. The selected models are then used to estimate the **probability of risk for a new project**. Finally, **SHAP (SHapley Additive exPlanations)** is used to understand which project factors influence the predictions.

The aim is to develop a practical and interpretable approach for early construction-project risk assessment.

---

## 2. Keywords

`Building Construction` `Construction Management` `Schedule Delay` `Cost Overrun` `Machine Learning` `Logistic Regression` `Random Forest` `XGBoost` `Probability Prediction` `SHAP` `Explainable AI` `Risk Prediction`

---

## 3. Introduction

Construction projects involve many interconnected activities, resources, materials, equipment, workers, and external conditions. Even with careful planning, unexpected changes can affect both project duration and cost.

This project focuses on two important construction-management problems: **whether a building project is likely to be delayed and whether it is likely to experience a cost overrun**.

The project goes one step further than a simple Yes/No prediction by also estimating the probability of each risk and using SHAP to explain the factors influencing an individual prediction.

---

## 4. Dataset

The project uses the **BIM-AI Integrated Dataset** available on **Kaggle**. The dataset contains information related to construction cost, schedule, structural health, environmental conditions, resources, and safety.

**Dataset:** BIM-AI Integrated Dataset — Kaggle  
https://www.kaggle.com/datasets/ziya07/bim-ai-integrated-dataset/data

For this project, only the variables relevant to **building construction schedule delay and cost-overrun prediction** were retained.

The final working dataset contains **190 projects**.

---

## 5. Data Preprocessing

The raw dataset was cleaned and prepared before EDA and machine learning.

The main preprocessing steps were:

1. Removing irrelevant variables.
2. Checking and handling missing values.
3. Correcting data types where required.
4. Separating numerical and categorical variables.
5. Encoding categorical variables.
6. Checking unusual or extreme values.
7. Removing variables that could cause data leakage.
8. Creating one final clean processed dataset.

The objective was to retain only information that could reasonably be available for assessing construction-project risk.

---

## 6. Exploratory Data Analysis

EDA was performed specifically around the two objectives of the project rather than analyzing every variable in the dataset.

The analysis examined project duration, cost, labor, material usage, equipment utilization, weather, safety, environmental conditions, and other relevant construction factors.

### Main EDA Results

The final dataset contains **190 projects**.

- **134 projects (70.53%)** experienced schedule delays.
- **56 projects (29.47%)** did not experience schedule delays.
- **124 projects (65.26%)** experienced cost overruns.
- **66 projects (34.74%)** did not experience cost overruns.
- Average schedule delay was **21.35%**.
- Average cost overrun was **18.32%**.
- Average planned duration was **554.7**, compared with an average actual duration of **673.0**.
- Average planned cost was approximately **27.75M**, compared with an actual cost of approximately **33.08M**.

### Weather Analysis

Rainy projects showed the highest observed schedule-delay percentage at **74.42%**. For cost overrun, rainy projects also showed the highest percentage at **72.09%**.

### Correlation Analysis

The strongest observed correlation with schedule delay was:

- `Actual_Duration` — **r = 0.342**

For cost overrun, the strongest observed correlations were:

- `Actual_Cost` — **r = 0.332**
- `Material_Usage` — **r = 0.167**
- `Planned_Cost` — **r = 0.101**

These are observed correlations in the dataset and should not be interpreted as proof of causation.

---

## 7. Machine Learning Methodology

Schedule delay and cost overrun were treated as **two separate binary classification problems**.

### 7.1 Schedule Delay

```text
No  → 0
Yes → 1
```

### 7.2 Cost Overrun

```text
No  → 0
Yes → 1
```

For each target, three models were trained:

- **Logistic Regression** — used as a baseline and relatively interpretable model.
- **Random Forest** — used to capture nonlinear relationships and interactions.
- **XGBoost** — used as a gradient-boosting model for more complex patterns.

The models were compared using **Accuracy, Precision, Recall, F1-score, and ROC-AUC**, and the best model was selected separately for each prediction task.

---

## 8. Model Results

### 8.1 Schedule Delay

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 50.00% | 70.00% | 51.85% | 59.62% | 0.495 |
| **XGBoost** | **65.79%** | **71.88%** | **85.19%** | **78.00%** | 0.465 |
| Random Forest | 60.53% | 71.43% | 74.07% | 72.73% | 0.451 |

**XGBoost performed best overall for schedule-delay prediction**, particularly in Accuracy, Recall, and F1-score.

### 8.2 Cost Overrun

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| **Logistic Regression** | **63.16%** | **73.91%** | 68.00% | **70.83%** | **0.563** |
| XGBoost | 57.89% | 66.67% | **72.00%** | 69.23% | 0.529 |
| Random Forest | 60.53% | 70.83% | 68.00% | 69.39% | 0.517 |

**Logistic Regression performed best overall for cost-overrun prediction**, while XGBoost achieved the highest recall.

---

## 9. Probability Prediction

After model comparison, the selected models were used to assess a new building project.

Instead of returning only a Yes/No result, the prediction code provides both the classification and estimated probability.

One tested project produced:

| Risk | Prediction | Probability |
|---|---|---:|
| Schedule Delay | **NO** | **11.07%** |
| Cost Overrun | **YES** | **99.86%** |

This means that, for this particular test project, the model estimated a relatively low probability of schedule delay but a very high probability of cost overrun.

These probabilities are **model-based estimates and are not guarantees of the actual project outcome**.

---

## 10. SHAP Explainability

SHAP (**SHapley Additive exPlanations**) was used to understand why the selected models make their predictions.

For the tested cost-overrun project, some of the observed SHAP contributions were:

```text
Material_Usage       +5.34
Vibration_Level      -0.98
Labor_Hours          -0.95
```

A positive SHAP value pushes the prediction toward the positive class, while a negative value pushes it away from the positive class. A larger absolute SHAP value indicates a stronger contribution for that particular prediction.


---

## 11. Results and Discussion

The EDA showed that schedule delays and cost overruns are frequent in the dataset, with **70.53% of projects delayed** and **65.26% experiencing cost overruns**.

For schedule-delay prediction, **XGBoost achieved the strongest overall results**, with **65.79% accuracy, 85.19% recall, and 78.00% F1-score**.

For cost-overrun prediction, **Logistic Regression performed best overall**, achieving **63.16% accuracy, 73.91% precision, 70.83% F1-score, and 0.563 ROC-AUC**.

The probability-prediction stage demonstrated that the framework can provide more information than a simple classification. The SHAP stage then adds interpretability by showing which features contributed to an individual prediction.

Overall, the results show the potential of machine learning as a **construction-project risk assessment tool**, while also highlighting that model performance depends on the available data and should be improved with larger and more representative datasets.

---

## 12. Libraries Used

The main Python libraries used in the project are:

```text
Pandas
NumPy
Scikit-learn
XGBoost
SHAP
Matplotlib
Seaborn
Joblib
```

They are used for data handling, preprocessing, visualization, machine learning, model evaluation, model saving/loading, and explainable AI.

---

## 13. Conclusion

This project developed a machine-learning framework for predicting **schedule delays and cost overruns in building construction projects**.

The analysis showed that both risks are common in the studied dataset. XGBoost was selected for schedule-delay prediction, while Logistic Regression was selected for cost-overrun prediction based on the reported model-comparison results.

The project combines three useful outputs:

**Prediction + Probability + Explainability**

This makes the framework more useful for construction risk assessment than a simple Yes/No classification system. Future improvements could include larger real-world building datasets, project-progress information, BIM data, procurement information, and schedule data from tools such as Primavera P6 or MS Project.

---

## 14. References

1. **BIM-AI Integrated Dataset.** Kaggle.  
   https://www.kaggle.com/datasets/ziya07/bim-ai-integrated-dataset/data

2. Lagos, C. I., Herrera, R. F., Mac Cawley, A. F., & Alarcón, L. F. (2024). **Predicting construction schedule performance with Last Planner System and machine learning.** *Automation in Construction, 167*, 105716.

3. Hamdan, M. M., Thneibat, M., & Hyari, K. H. (2025). **Predicting cost overrun in construction projects using machine learning algorithms: The case of Jordan.** *Engineering, Construction and Architectural Management, 33*(6), 4732–4763.

4. Shehadeh, A., & Abuaddous, M. (2025). **XAI-enabled probabilistic pipeline for predicting delay and cost overrun risk in construction.** *Engineering, Construction and Architectural Management.*

5. Tian, Y., Chen, Y., & Ning, Y. (2026). **Identifying and predicting delay risks in prefabricated construction: An explainable ensemble learning approach.** *Advanced Engineering Informatics, 71*, 104219.

