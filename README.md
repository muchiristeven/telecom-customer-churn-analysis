# Telecom Customer Churn Analysis

## Project Overview

This project analyzes customer churn in a telecom dataset and develops a predictive model to identify customers who are at elevated risk of leaving.

The analysis combines:

- Exploratory Data Analysis (EDA)
- Statistical hypothesis testing
- Feature analysis
- Predictive modelling
- Model comparison and tuning
- Business interpretation

The final model was selected using stratified cross-validation and evaluated on a held-out test set.

## Business Problem

Customer churn can reduce revenue, increase customer acquisition costs, and weaken long-term customer relationships.

The objective of this project is to identify patterns associated with churn and develop a model that can help a telecom company prioritize customers for retention activity.

The analysis focuses on three questions:

1. Which customer characteristics and behaviours are associated with churn?
2. Which variables provide the strongest predictive information?
3. How accurately can churn be predicted using historical customer data?

## Dataset

The project uses the Iranian Telecom Customer Churn dataset from the UCI Machine Learning Repository.

The dataset contains 3,150 customer records and includes variables related to:

- customer usage behaviour;
- complaints;
- subscription characteristics;
- tariff plan;
- customer status;
- age;
- customer value;
- churn outcome.

### Target Variable

- `0` = Non-Churn
- `1` = Churn

The dataset is imbalanced, with approximately 15.7% of customers belonging to the churn class.

## Analytical Approach

The project followed a structured analytical workflow:

1. **Data Preparation**
   - Reviewed dataset structure and variable definitions
   - Standardized column names
   - Checked data quality and class distribution
   - Defined predictive features and target variable

2. **Exploratory Data Analysis**
   - Compared churn and non-churn customer behaviour
   - Examined usage, complaints, tariff plans, status, age, and customer value
   - Investigated correlations and distribution patterns

3. **Statistical Analysis**
   - Used Chi-square tests for categorical variables
   - Used Mann–Whitney U tests for numerical variables
   - Calculated effect sizes using Cramér's V and rank-biserial correlation

4. **Predictive Modelling**
   - Logistic Regression
   - Class-weighted Logistic Regression
   - Decision Tree
   - Random Forest

5. **Model Validation and Tuning**
   - Used stratified train-test splitting
   - Applied 5-fold stratified cross-validation
   - Tuned Decision Tree and Random Forest hyperparameters using GridSearchCV
   - Evaluated models primarily using churn-class F1-score

6. **Final Evaluation**
   - Evaluated the selected model on a held-out test set
   - Reviewed precision, recall, F1-score, confusion matrix, ROC-AUC, and Average Precision
   - Examined Random Forest feature importance

7. **Business Interpretation**
   - Identified customer characteristics associated with elevated churn risk
   - Translated model findings into potential customer-retention actions
   - Documented modelling limitations and deployment considerations

   ## Key Exploratory Findings

Several strong patterns emerged during exploratory analysis:

- Customers who submitted complaints had substantially higher churn rates than customers without complaints.
- Lower usage levels were strongly associated with churn.
- Non-churn customers generally had higher customer value and contacted a greater number of distinct numbers.
- Customer status showed one of the strongest relationships with churn.
- Tariff plan showed a statistically significant relationship with churn, although its predictive importance was relatively low once other variables were considered.

## Statistical Findings

Statistical testing was used to determine whether the patterns observed during EDA were supported by evidence and to quantify the strength of the relationships.

### Categorical Variables

- **Complaints and churn** showed a strong association, with Cramér's V ≈ 0.530.
- **Customer status and churn** also showed a strong association, with Cramér's V ≈ 0.498.
- **Age group and churn** were statistically associated, although the effect size was weak.
- **Tariff plan and churn** were statistically associated, but the effect size was relatively small.

### Numerical Variables

Mann–Whitney U tests showed statistically significant differences between churn and non-churn customers for several numerical variables.

The largest effects were observed for:

- `seconds_of_use`
- `frequency_of_use`
- `customer_value`

Moderate effects were observed for:

- `distinct_called_numbers`
- `frequency_of_sms`

Overall, churners tended to show lower engagement and lower customer value than non-churn customers.

## Predictive Modelling Results

Several classification models were compared using 5-fold stratified cross-validation with churn-class F1-score as the primary model-selection metric.

| Model | Mean CV F1 |
|---|---:|
| Original Logistic Regression | 0.558 |
| Class-Weighted Logistic Regression | 0.649 |
| Decision Tree | 0.810 |
| Random Forest | 0.876 |
| Tuned Random Forest | **0.882** |

The tuned Random Forest achieved the strongest validation performance.

### Final Tuned Random Forest

Best hyperparameters:

- `n_estimators = 300`
- `max_depth = None`
- `min_samples_leaf = 1`
- `max_features = "sqrt"`

### Held-Out Test Performance

| Metric | Result |
|---|---:|
| Accuracy | 0.97 |
| Churn Precision | 0.88 |
| Churn Recall | 0.95 |
| Churn F1-score | 0.91 |
| ROC-AUC | 0.985 |
| Average Precision | 0.886 |

The final confusion matrix showed:

- **518** correctly identified non-churn customers
- **94** correctly identified churn customers
- **13** false-positive churn alerts
- **5** missed churn customers

The strong churn recall indicates that the model identified most actual churners in the held-out test set while maintaining high precision.

## Feature Importance

Random Forest feature importance indicated that the model relied most heavily on the following variables:

| Rank | Feature | Importance |
|---:|---|---:|
| 1 | `status` | 0.167 |
| 2 | `frequency_of_use` | 0.138 |
| 3 | `seconds_of_use` | 0.131 |
| 4 | `complains` | 0.125 |
| 5 | `customer_value` | 0.106 |
| 6 | `subscription_length` | 0.102 |

Other variables such as `distinct_called_numbers`, `frequency_of_sms`, `call_failure`, and `age` also contributed to model predictions, but to a lesser extent.

Feature importance should be interpreted as predictive contribution within the Random Forest rather than evidence of causation. Several usage variables are also strongly correlated, so their individual importance values should not be interpreted independently.

## Business Recommendations

The findings suggest several practical retention strategies that a telecom company could evaluate:

- **Prioritize customers with complaint history** for proactive follow-up and service recovery.
- **Monitor declining customer activity**, particularly reductions in usage frequency and call duration.
- **Identify inactive or low-engagement customers early** and include them in retention campaigns before churn occurs.
- **Use churn-risk scores to prioritize retention resources** rather than treating all customers equally.
- **Segment retention interventions by cost and risk**, using low-cost actions such as automated communication for broader high-risk groups and more expensive incentives for customers with stronger churn signals.
- **Track intervention outcomes** to determine which retention actions actually reduce churn.

The predictive model should support business decision-making rather than automatically determine customer treatment.

## Limitations

This project has several limitations:

- The dataset contains only 3,150 customer records.
- The data comes from an historical Iranian telecom context and may not generalize directly to other countries, operators, or time periods.
- Several usage variables are strongly correlated, including `seconds_of_use` and `frequency_of_use`.
- `customer_value` is a calculated variable whose complete derivation is not documented in the available dataset description.
- Random Forest impurity-based feature importance does not establish causal relationships.
- Model performance may change as customer behaviour and market conditions change over time.
- Before deployment, the model should be validated using current operational data from the target telecom environment.

## Tools Used

The project used the following tools and technologies:

- **Python**
  - pandas
  - NumPy
  - matplotlib
  - scikit-learn
- **Jupyter Notebook**
- **SQL**
- **Statistical analysis**
- **Git and GitHub**
- **VS Code**

## Repository Structure

```text
telecom-customer-churn-analysis/
│
├── data/
│   └── raw/
│       └── Customer_Churn.csv
│
├── docs/
│   ├── business_problem.md
│   ├── Portfolio_Project_2_Checkpoint_1...
│   ├── Telecom_Churn_Checkpoint_2_EDA_Documentation.docx
│   ├── Telecom_Churn_Checkpoint_3_Statistical_Analysis_Documentation.docx
│   └── Telecom_Churn_Checkpoint_4_Predictive_Modelling_Documentation.docx
│
├── notebooks/
│   ├── 01_data_profiling_and_cleaning.ipynb
│   └── 02_churn_predictive_modeling.ipynb
│
├── .gitignore
├── README.md
└── requirements.txt

## Conclusion

This project demonstrates an end-to-end customer churn analysis workflow, from exploratory analysis and statistical testing through predictive modelling and business interpretation.

The analysis identified customer status, usage behaviour, complaints, customer value, and subscription characteristics as important churn signals.

Among the evaluated models, the tuned Random Forest achieved the strongest performance, with a churn F1-score of 0.91 and recall of 0.95 on the held-out test set.

The project demonstrates how statistical analysis and machine learning can be combined to support more targeted and evidence-based customer retention decisions.