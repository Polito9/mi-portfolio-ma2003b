# Multivariate Analysis Portfolio

This repository contains a comprehensive collection of three business analytics case studies. These projects demonstrate the application of multivariate statistical methods and machine learning algorithms to solve real-world business problems ranging from customer satisfaction to credit risk and market segmentation.

---

## 1. Team Information

**Authors:**
* **Diego Colin Reyes** - A01666354
* **Daniel Alejandro López Martínez** - A01770442
* **Eduardo Ramírez Almanza** - A01660118

---

## 2. Case Studies Summary

| Case | Business Context | Primary Problem | Methodology Applied | Key Outcome |
| :--- | :--- | :--- | :--- | :--- |
| **01. TechnoServe Solutions** | IT & Project Management | Inability to quantify specific drivers of customer satisfaction and prioritize strategic investments. | **Factor Analysis (EFA)** & **PCA** | Identified "Project Delivery" and "Support Modernization" as critical drivers. Created a model to predict NPS and Churn. |
| **02. LendSmart** | FinTech / Credit Risk | High default rate (28%) in the loan portfolio; need for a rigorous approval filter. | **Discriminant Analysis (LDA & QDA)** | Achieved **100% Accuracy/AUC** on test data. LDA selected for superior interpretability of risk factors (e.g., Payment History). |
| **03. MegaMart** | Retail / E-commerce | "One-size-fits-all" marketing was inefficient; lack of distinct customer profiles. | **Clustering (K-Means)** | Segmented 3,000 customers into 4 distinct profiles (e.g., "The Elite", "At-Risk"), enabling targeted VIP and win-back campaigns. |

---

## 3. Methodological Comparison

This portfolio explores three distinct approaches to multivariate analysis. Below is a comparison of how each method was applied to solve specific types of problems.

### A. Factor Analysis (Case 01)
* **Type:** Dimensionality Reduction (Unsupervised -> Supervised Hybrid).
* **Goal:** To uncover **latent variables** (hidden concepts) that explain the correlation between many observed variables.
* **Application:** We reduced 23 survey questions into a few actionable business "drivers" (e.g., Technical Excellence, Project Delivery).
* **Distinction:** Unlike clustering (which groups rows/people), Factor Analysis groups columns/variables to understand *structure*.

### B. Discriminant Analysis (Case 02)
* **Type:** Classification (Supervised).
* **Goal:** To maximize the separation between known categories (Defaulters vs. Non-Defaulters).
* **Application:** We utilized LDA and QDA to draw a decision boundary that predicts if a new applicant will default.
* **Distinction:** This is predictive. Unlike the other two cases, we had a "ground truth" target variable (`loan_status`) that the model had to learn to replicate.

### C. Cluster Analysis (Case 03)
* **Type:** Segmentation (Unsupervised).
* **Goal:** To find natural groupings in data based on similarity, without pre-existing labels.
* **Application:** We used K-Means to identify 4 customer personas based on spending and behavior.
* **Distinction:** Exploratory by nature. There was no "correct" number of clusters initially; we had to use the Elbow Method and Silhouette Scores to find the most logical business structure.

---

## 4. Lessons Learned & Final Reflection

Through the execution of these three cases, we derived insights regarding the data science lifecycle:

1.  **Data Preparation is Paramount:**
    Across all cases, the quality of the model depended heavily on preprocessing. Whether it was **imputing missing values** with KNN (Case 01), **encoding categorical variables** (Case 02), or **standardizing data** to prevent magnitude bias (Case 03), the "garbage in, garbage out" principle held true.

2.  **Interpretability vs. Complexity:**
    In Case 02, while QDA is a more flexible model, we chose **LDA** because its linear coefficients were easier to explain to stakeholders. In a business context, knowing *why* a customer is rejected (e.g., "low payment history") is often as important as the prediction accuracy itself.

3.  **From Model to Strategy:**
    The math is only half the work. The true value was unlocked when we translated statistical outputs into business actions:
    * *Case 01:* Transforming "Factor Loadings" into a **PMO implementation plan**.
    * *Case 03:* Transforming "Cluster Centroids" into a **VIP Loyalty Program**.

4.  **The Power of Hybrid Approaches:**
    Case 01 demonstrated that methods do not need to exist in isolation. Combining **Unsupervised learning** (to find factors) with **Supervised learning** (to predict NPS based on those factors) provided a much richer insight than either method could have achieved alone.