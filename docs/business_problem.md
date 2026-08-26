
# Telecom Customer Churn & Retention Analysis

## Business Context

A telecommunications company wants to reduce customer churn by identifying behavioural patterns associated with customers who leave the service.

The available dataset contains customer-level behavioural and service information collected during an observation period, together with a churn outcome recorded later.

The goal of this project is to use SQL, Python, statistical analysis, and business reasoning to identify which customer behaviours are most strongly associated with churn and determine how the business could prioritize retention interventions.

## Primary Stakeholder

The primary stakeholder is the **Head of Customer Retention / Commercial Director**.

The analysis is intended to support decisions about which customer groups should receive the highest priority in a targeted retention programme.

## Business Problem

Customer churn represents lost future revenue and may increase customer acquisition costs if the company must continually replace departing customers.

The core business question is:

> **Which customer behaviours are most strongly associated with churn, and how can the company use those findings to identify and prioritize customers for retention intervention?**

This analysis will focus on identifying associations rather than claiming causal relationships.

## Decision to Support

The project will support the following management decision:

> **Which customer segments and behavioural warning signals should be prioritized when designing a targeted customer retention strategy?**

## Analytical Questions

The project will investigate the following questions:

1. What is the overall level and distribution of customer churn?
2. Which customer characteristics differ between churned and retained customers?
3. Which behavioural variables are statistically associated with churn?
4. How large are the observed differences and relationships?
5. Which customer segments appear to represent the highest retention opportunity?
6. What practical actions could management take based on the findings?

## Initial Hypotheses

The following hypotheses will be tested during the analysis.

### H1 — Complaints

Customers who lodge complaints have a higher churn rate than customers who do not lodge complaints.

### H2 — Service Usage

Customers with lower service usage are more likely to churn than customers with higher service usage.

### H3 — Subscription Length

Customer churn differs according to subscription length.

### H4 — Customer Value

The distribution of customer value differs between churned and retained customers.

### H5 — Call Failures

Customers experiencing a higher number of call failures are more likely to churn.

## Analytical Approach

The analysis will follow this general workflow:

1. Validate and profile the raw dataset.
2. Use SQL for data-quality checks, aggregation, segmentation, and exploratory business analysis.
3. Use Python for exploratory data analysis and visualization.
4. Apply appropriate statistical tests, confidence intervals, and effect-size measures.
5. Evaluate both statistical significance and practical business significance.
6. Develop customer segments and retention priorities.
7. Translate findings into business recommendations.

## Scope

This project focuses on exploratory, statistical, and business analysis of customer churn.

Predictive machine-learning modelling may be included later as an optional extension, but the primary objective is to understand the business problem and the factors associated with churn before building any predictive model.

## Limitations

The dataset is observational. Therefore, statistical associations identified in this project should not automatically be interpreted as causal relationships.

The analysis is also limited to the variables available in the dataset. Other factors that may influence churn, such as competitor activity, pricing changes, network coverage, customer-support interactions, or broader economic conditions, may not be represented.
