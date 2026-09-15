# 📊 Project Findings — B2B Sales Analytics & Lead Prioritisation

## 🎯 Overview

This project investigated how **data analytics and statistical methods can support B2B sales teams in prioritising accounts more consistently**.

Drawing on my previous experience in B2B technology sales, the analysis explored whether transactional and engagement-related variables could provide useful signals for identifying potentially valuable accounts.

The project covered the complete analytical workflow from:

```text
Raw Transaction Data
        ↓
Data Cleaning
        ↓
Feature Engineering
        ↓
Exploratory Analysis
        ↓
Statistical Testing
        ↓
Regression & PCA
        ↓
Business Interpretation
```

The findings below summarise the most important analytical and business insights.

---

# 📦 Finding 1 — Most Transactions Were Relatively Small

The distribution of `ProductQuantity` was right-skewed.

Most transactions contained approximately:

### **1–14 units**

while larger orders occurred considerably less frequently.

### 💡 Business Interpretation

The dataset was dominated by relatively small transactions.

This means that a small number of large orders should not automatically be treated as representative of typical customer purchasing behaviour.

For sales teams, this highlights the importance of understanding the **distribution of account behaviour rather than relying only on averages**.

---

# 🌍 Finding 2 — Transactions Were Highly Concentrated in the UK

Geographic analysis showed that:

### **More than 90% of transactions originated in the United Kingdom**

with substantially fewer transactions coming from:

- 🇩🇪 Germany
- 🇨🇭 Switzerland
- 🇸🇪 Sweden
- 🇫🇷 France

### 💡 Business Interpretation

The dataset represents a highly geographically concentrated customer base.

This has two implications:

1. overall results are strongly influenced by UK transactions
2. conclusions should not automatically be generalised to other geographic markets

A larger commercial analysis would benefit from more balanced regional data before developing country-specific sales strategies.

---

# 💰 Finding 3 — Price and Order Quantity Have a Weak Negative Relationship

Correlation analysis found:

### **r ≈ -0.292**

between:

```text
PricePerUnit ↔ ProductQuantity
```

This represents a **weak negative relationship**.

As price per unit increased, order quantity showed some tendency to decrease.

However, the relationship was not strong.

### 💡 Business Interpretation

Price may influence purchasing behaviour, but it does not provide enough information on its own to explain why customers place larger orders.

For B2B sales prioritisation:

> **Price should be treated as one signal rather than a standalone indicator of account value.**

---

# 📉 Finding 4 — Statistical Significance Does Not Equal Business Usefulness

A linear regression model was estimated using:

```text
Independent Variable:
PricePerUnit

Dependent Variable:
ProductQuantity
```

The resulting model was:

```text
ProductQuantity
=
20.96 − 9.76 × PricePerUnit
```

The price coefficient was statistically significant:

### **p ≈ 0.0009**

However, the model's explanatory power was:

### **R² = 0.085**

This means that price explained only approximately:

### **8.5% of the variation in order quantity**

---

## 💡 Key Interpretation

This is one of the most important findings from the project.

A variable can be **statistically significant without being sufficiently useful for prediction or business decision-making**.

```text
Statistical Significance
        ≠
Strong Predictive Value
```

Although there was evidence of a relationship between price and quantity, approximately **91.5% of the variation in order quantity remained unexplained by price alone**.

For practical B2B lead prioritisation, additional customer and engagement variables would therefore be required.

---

# 🧪 Finding 5 — Average Order Quantity Was Not Significantly Above the Business Benchmark

The mean order quantity was:

### **11.28 units**

A one-tailed hypothesis test investigated whether average order quantity was significantly greater than:

### **10 units**

The test produced:

```text
Z-score = 1.31
p-value = 0.095
α = 0.05
```

Because:

```text
0.095 > 0.05
```

there was insufficient statistical evidence to conclude that the true average order quantity exceeded 10 units.

### 💡 Business Interpretation

Although the observed sample mean was **11.28**, the difference from the 10-unit benchmark was not statistically strong enough at the selected significance level.

This demonstrates why business decisions should not rely only on comparing raw averages.

Statistical uncertainty should also be considered.

---

# 📐 Finding 6 — Confidence Intervals Provide Context Around Average Behaviour

The analysis estimated a 95% confidence interval for average product quantity:

### **9.38 – 13.18 units**

with a sample mean of:

### **11.28 units**

Price per unit showed considerably less variation, with a 95% confidence interval of:

### **0.94 – 1.05**

### 💡 Interpretation

Confidence intervals provide more information than a single average because they communicate the uncertainty surrounding the estimate.

Instead of reporting only:

```text
Average Quantity = 11.28
```

the analysis can communicate:

```text
Estimated Average
        ↓
11.28 units

95% Confidence Interval
        ↓
9.38 – 13.18 units
```

This provides decision-makers with a more complete understanding of the data.

---

# 🧩 Finding 7 — PCA Suggested the Engineered Variables Capture Different Information

Principal Component Analysis was applied to the engineered variables.

The resulting explained variance was approximately:

| Component | Explained Variance |
|---|---:|
| PC1 | **64.6%** |
| PC2 | **35.4%** |

PC1 captured the majority of variation.

However, PC2 still contained:

### **35.4% of the information**

### 💡 Interpretation

Reducing the variables to only one principal component would discard a substantial amount of information.

The analysis therefore suggested retaining both dimensions rather than simplifying them into a single score.

This indicates that the variables may represent **different aspects of customer behaviour**.

For a future sales-prioritisation model, maintaining separate engagement signals may therefore provide more useful information than prematurely combining them.

---

# 🔧 Finding 8 — Engagement Variables Could Add Context Beyond Transactions

Two additional variables were introduced:

### `Leads_Generated`

Representing lead-generation activity associated with an account.

### `Total_Projects`

Representing previous customer engagement through project activity.

These variables were incorporated to explore information beyond basic transactional characteristics.

### 💡 Business Interpretation

This reflects an important principle in B2B sales analytics.

Account potential is unlikely to be explained by transaction price or quantity alone.

More useful signals may include:

```text
Account Engagement
        +
Historical Purchasing
        +
Project Activity
        +
Lead Generation
        +
Customer Characteristics
        ↓
More Complete Account Profile
```

This provides the basis for a more sophisticated future lead-scoring system.

---

# 🎯 Finding 9 — Transactional Variables Alone Are Insufficient for Lead Prioritisation

Across the statistical analyses, simple transactional characteristics provided relatively limited information about customer behaviour.

The key results were:

| Analysis | Result |
|---|---:|
| Price vs Quantity Correlation | **-0.292** |
| Regression R² | **0.085** |
| Regression p-value | **~0.0009** |
| Order Quantity Test | **p = 0.095** |
| PCA PC1 | **64.6%** |
| UK Transaction Share | **>90%** |

### 💡 Overall Interpretation

The findings do not support using a single transactional variable as the primary basis for B2B account prioritisation.

Instead, a stronger framework would combine multiple signals.

---

# 💼 Finding 10 — A Better B2B Lead Score Would Combine Multiple Signals

Based on the analysis, a future lead-prioritisation framework could incorporate:

```text
              Account
                 │
      ┌──────────┼──────────┐
      ▼          ▼          ▼
 Engagement   Customer    Historical
 Activity     Profile     Behaviour
      │          │          │
      └──────────┼──────────┘
                 ▼
          Lead / Account
           Priority Score
```

Potential variables include:

- 🎯 lead-generation activity
- 🤝 number of previous projects
- 💰 historical purchasing behaviour
- 🏢 company size
- 🏭 industry
- 🌍 geographic market
- 📣 lead source
- 🔄 previous engagement
- 📈 opportunity history
- ✅ conversion history

### 💡 Business Interpretation

For an SDR, the purpose of such a system would not necessarily be to replace judgement.

Instead, analytics could provide a **consistent starting point for deciding where limited sales time should be allocated**.

---

# 🧹 Data Preparation Findings

The project also demonstrated the importance of preparing data before statistical analysis.

The preprocessing workflow included:

```text
Raw Data
   ↓
Missing-Value Assessment
   ↓
Duplicate Detection
   ↓
Outlier Detection
   ↓
Normalisation
   ↓
Standardisation
   ↓
Binning
   ↓
Feature Engineering
   ↓
Analysis-Ready Dataset
```

Outliers were identified using the **Interquartile Range (IQR)** method.

Numerical variables were also normalised and standardised where required for subsequent analysis.

### 💡 Key Takeaway

Statistical modelling is only one stage of an analytics project.

Reliable analysis depends heavily on understanding and preparing the underlying data before models or statistical tests are applied.

---

# 📊 Overall Business Findings

The project produced several broader insights relevant to B2B sales analytics.

### 1️⃣ Account value cannot be explained by price alone

The relationship between price and order quantity was statistically significant but weak in explanatory power.

### 2️⃣ Statistical significance should be separated from practical significance

A low p-value does not automatically mean that a variable is useful enough to support a business decision.

### 3️⃣ Sales prioritisation requires richer customer information

Engagement, project history, customer characteristics and conversion outcomes could provide substantially more useful information.

### 4️⃣ Geographic concentration affects interpretation

With more than 90% of transactions originating in the UK, the results primarily represent one geographic market.

### 5️⃣ Data-driven prioritisation can support sales judgement

Analytics can provide a consistent framework for prioritisation while allowing sales professionals to incorporate qualitative account knowledge.

---

# ⚠️ Limitations

Several limitations should be considered when interpreting the findings.

### Dataset Size

The dataset is relatively small and should not be interpreted as representative of the wider B2B technology market.

### Synthetic / Bootstrapped Variables

Some engagement-related variables were created using synthetic data and extended using bootstrapping.

They should therefore be interpreted as analytical demonstrations rather than observed customer behaviour.

### Limited Customer Features

The dataset does not contain many variables normally available in a CRM environment, such as:

- company size
- industry
- opportunity stage
- lead source
- historical conversions
- sales activity
- email engagement
- decision-maker information

### Geographic Concentration

More than 90% of transactions originated in the UK.

This limits the ability to generalise the results internationally.

### Predictive Limitations

The regression analysis was exploratory and was not developed or validated as a production predictive model.

---

# 🚀 Future Development

The strongest next step would be to extend the project using a realistic CRM dataset.

A future model could combine:

```text
CRM Data
   +
Sales Activity
   +
Historical Purchases
   +
Account Characteristics
   +
Engagement Signals
        │
        ▼
 Feature Engineering
        │
        ▼
 Lead Scoring Model
        │
        ▼
 Account Priority
        │
        ▼
 Power BI Dashboard
```

Potential improvements include:

- larger real-world CRM datasets
- opportunity and conversion outcomes
- multivariate regression
- logistic regression
- machine-learning classification
- account segmentation
- model validation
- lead-scoring thresholds
- Power BI dashboards
- CRM integration

---

# 🎯 Overall Conclusion

The central finding of this project was that **simple transactional variables are not sufficient for robust B2B lead prioritisation**.

Although price had a statistically significant relationship with order quantity:

### **p ≈ 0.0009**

the model explained only:

### **8.5% of order-quantity variation**

This demonstrates an important analytical distinction:

> **A statistically significant relationship is not necessarily strong enough to support a business decision.**

The analysis suggests that practical B2B lead prioritisation would benefit from combining transactional information with richer signals such as **customer engagement, project activity, account characteristics and historical conversion behaviour**.

From a technical perspective, the project demonstrates an end-to-end Excel analytics workflow covering:

**Data Cleaning → Feature Engineering → EDA → Statistical Testing → Regression → PCA → Business Interpretation**

From a business perspective, it demonstrates how my previous experience in **B2B technology sales** can be combined with data analytics to investigate practical commercial problems.

---

# 🎓 Academic Context

Originally developed for **COMP1887 – Principles of Data Science** as part of the MSc Data Science and Its Applications programme at the University of Greenwich.

For this portfolio repository, the project is presented as a **B2B sales analytics case study** focused on applying statistical analysis to a practical commercial decision-making problem.

---

# 👩🏼‍💻 Author

**Julia Legner**  
MSc Data Science and Its Applications  
University of Greenwich

**Portfolio Focus:** Data Analytics • Business Intelligence • B2B Technology • Sales Analytics
