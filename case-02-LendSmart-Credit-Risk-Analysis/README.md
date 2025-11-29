# Credit Risk Analysis - LendSmart

**Authors:**
- Diego Colin Reyes
- Daniel Alejandro López Martínez
- Eduardo Ramírez Almanza

---

## 1. Business Context

**Client Description & Problem:**
**LendSmart** is a FinTech company specializing in personal and small business loans. Currently, its loan portfolio has a **default rate of 28%**, a level management considers excessively high. The company requires a predictive model to accurately identify high-risk applicants before loans are approved.

**Strategic Importance:**
This analysis transforms credit data into a **predictive classification model** that allows LendSmart to:
- **Reduce financial losses** by minimizing the approval of loans that will eventually default.
- **Optimize profitability** by maintaining an acceptable level of rejected "good" loans (false positives).
- **Improve decision-making** by identifying key factors driving default risk.
- **Increase investor confidence** through more scientific, data-driven risk management.

---

## 2. Methodology

**Applied Classification Methods:**
Two discriminant analysis techniques were compared:
1.  **Linear Discriminant Analysis (LDA):** Assumes that classes share the same covariance matrix.
2.  **Quadratic Discriminant Analysis (QDA):** Allows each class to have its own covariance matrix.

**Justification:**
-   **Data Preparation:** Applied **one-hot encoding** to categorical variables (`education_level`, `marital_status`) and **standardization** to numerical features using `StandardScaler`.
-   **Data Splitting:** An 80-20 (train-test) split was used with `stratify=y` to maintain class proportions.
-   **Statistical Assumptions:** Multivariate normality and homogeneity of covariance matrices were discussed, hypothesizing that QDA might outperform LDA due to observed differences in distributions.

**Tools & Libraries:**
-   **Python:** Primary programming language.
-   **Pandas & NumPy:** Data manipulation and analysis.
-   **Scikit-learn:** Implementation of LDA, QDA, StandardScaler, train_test_split, and evaluation metrics.
-   **Plotly:** Interactive result visualizations and exploratory analysis.

---

## 3. Data

**Dataset Description:**
The analysis was based on the `credit_risk_data.csv` file, containing **2,500 loan applications** with **18 variables** each.

**Key Variables:**
The variable set includes:

-   **Predictor Variables (17 features):**
    -   **Financial:** `annual_income`, `loan_amount`, `debt_to_income_ratio`, `savings_ratio`, `asset_value`.
    -   **Credit:** `credit_score`, `credit_utilization`, `payment_history_score`, `open_credit_lines`.
    -   **Employment & Demographic:** `employment_years`, `job_stability_score`, `age`, `education_level`, `marital_status`, `residential_stability`.

-   **Target Variable (1 variable):**
    -   `loan_status`: Binary indicator (0 = Non-Defaulter, 1 = Defaulter).

**Data Quality:**
-   No null values were found in the dataset.
-   Distributions showed clear separability between defaulters and non-defaulters.

---

## 4. Key Findings

The analysis concluded that both models (LDA and QDA) achieved **perfect performance** on the test set, with **100% accuracy and an AUC of 1.0000**.

**Critical Factors (Identified via LDA Coefficients):**
The main drivers of default risk, in order of importance, are:
1.  **`payment_history_score`** (Coef: -15.47): A strong payment history drastically reduces risk.
2.  **`job_stability_score`** (Coef: -13.05): Job stability is a key reliability factor.
3.  **`credit_utilization`** (Coef: +11.77): High use of available credit significantly increases risk.
4.  **`debt_to_income_ratio`** (Coef: +4.47): Higher debt relative to income increases the probability of default.
5.  **`credit_score`** (Coef: -3.98): A high credit score reduces risk, as expected.

**High-Risk Profile:**
-   Low payment history.
-   Low job stability.
-   High utilization of available credit.
-   High debt-to-income ratio.

**Model Selection:**
Although both models are perfect, **LDA** is recommended for its **interpretability**, as it provides linear coefficients that clearly explain the impact of each variable on the credit decision.

---

## 5. Business Recommendations

**Primary Recommendation:**
Implement the **LDA model** in LendSmart's loan application evaluation process.

**Expected Impact:**
-   **Identification of 100% of defaulters** in the test data.
-   **Drastic reduction in losses** from bad debt.
-   **Greater efficiency in capital allocation** by approving only low-risk loans.
-   **Decision transparency** thanks to the model's interpretability.

**Business Trade-Off:**
The perfect model implies that no good clients will be rejected, nor will bad loans be approved in the test data, representing an ideal scenario with no trade-offs in this specific dataset.

**Next Steps:**
-   **Validation on real-time data** to confirm model performance outside the test set.
-   **Development of a scoring system** based on LDA coefficients for operational use.
-   **Continuous monitoring** of the model to detect changes in credit risk patterns.