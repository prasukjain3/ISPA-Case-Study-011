# Customer Retention Case Study: Predicting Churn in a Telecom Service Provider

This case study presents an end-to-end analytical workflow for understanding and predicting customer churn for a telecommunications provider. It highlights data preparation, exploratory analysis, model development, rule extraction, and operational deployment considerations typically required in an ISPA analytics submission.

---

## Objective

The study aims to build a reliable churn-prediction system that not only scores individual customers but also uncovers the underlying behavioral patterns associated with attrition. The outcome supports proactive retention strategies by the business.

---

## Analytical Process

### 1. Data Preparation & Exploratory Insights

- **Data Quality Treatment:**  
  The original dataset contained inconsistencies in the `TotalCharges` field. After reviewing the distribution, 11 entries with missing values were excluded to ensure clean numerical input.

- **Response Variable:**  
  The churn variable is moderately imbalanced — roughly **one in four** customers in the sample had ended their service. This imbalance was considered during modeling and evaluation.

- **Preprocessing Steps:**  
  - Categorical attributes were transformed using **One-Hot Encoding**.  
  - Continuous variables (`tenure`, `MonthlyCharges`, `TotalCharges`) were standardized.  
  These steps ensured that both linear and tree-based models received well-structured input.

---

### 2. Drivers of Customer Attrition

The analyses consistently pointed to three influential factors:

- **Type of Contract:**  
  Customers opting for **monthly renewal** agreements showed the highest likelihood of discontinuing services.

- **Internet Connectivity Type:**  
  Subscriptions involving **Fiber Optic connections** exhibited markedly higher attrition tendencies.

- **Length of Relationship:**  
  **Low-tenure** customers appeared more volatile, particularly when combined with flexible contract options.

These findings outline clear priority segments for retention campaigns.

---

### 3. Segment Discovery Through Rule Induction

A decision-tree model, used in place of a CHAID procedure, was employed to reveal human-interpretable segments. The model’s root node split on **Contract Type**, reinforcing its importance as a churn determinant.

**Illustrative High-Risk Segment:**  
Customers who are both **new to the company**, on a **month-to-month plan**, and using **Fiber Optic service** form one of the most churn-sensitive groups. Such rules provide tangible guidance for designing targeted interventions.

---

### 4. Predictive Model Evaluation

Two contrasting algorithms were examined:

| Performance Metric | Decision Tree | Logistic Regression |
|-------------------|---------------|--------------------|
| **ROC–AUC Score** | 0.8220        | **0.8378**         |

Although the decision tree was valuable for explainability, **Logistic Regression** delivered the superior overall discriminative ability and was therefore selected as the primary scoring engine.

---

## Operationalization & Lifecycle Management

### Model Packaging
The final predictive solution is stored as a **single serialized pipeline** (via Joblib), bundling preprocessing transformers together with the trained model. This ensures that incoming production data undergo identical transformations before scoring.

### Monitoring & Refresh Strategy
Since customer behavior evolves over time, the model must be routinely evaluated for performance decay caused by **concept drift**. An MLOps workflow should automate:

- Performance tracking  
- Scheduled retraining (e.g., quarterly)  
- Deployment of updated models into production environments

This framework keeps the churn-prediction system aligned with current customer dynamics.

---
