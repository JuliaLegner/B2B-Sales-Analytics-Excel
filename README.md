# 📊 B2B Sales Analytics & Lead Prioritisation

## Overview

This project explores how data analytics and statistical methods can support more consistent, evidence-based decision-making in **B2B technology sales**.

Drawing on my previous experience in B2B tech sales, I focused on a common challenge faced by Sales Development Representatives (SDRs): **how to prioritise potential customers efficiently when working with limited information and large numbers of accounts.**

The project uses **Microsoft Excel** to transform and analyse transactional data, combining data cleaning, feature engineering, statistical analysis, PCA and data visualisation to investigate which factors may be useful for sales prioritisation.

The analysis demonstrates how even relatively accessible analytical tools can help move sales decision-making from intuition towards a more structured, data-driven approach.

---

## 🎯 Business Problem

Sales Development Representatives often need to decide which accounts to prioritise within a limited amount of time.

In practice, these decisions can rely heavily on individual judgement and incomplete information, potentially resulting in:

- inconsistent lead prioritisation
- inefficient use of SDR time
- missed sales opportunities
- difficulty identifying high-value accounts
- less predictable sales pipelines

The objective of this project was therefore to explore how **data science principles could support B2B sales teams in making more consistent lead-prioritisation decisions.**

---

## 🛠️ Tools & Techniques

**Tools**

- Microsoft Excel
- Excel Analysis ToolPak
- PivotTables and charts
- Excel statistical and matrix functions

**Data Analytics**

- Data cleaning and preprocessing
- Missing-value handling
- Duplicate detection
- Outlier detection using IQR
- Normalisation
- Standardisation
- Data binning
- Feature engineering
- Bootstrapping

**Statistical Analysis**

- Descriptive statistics
- Confidence intervals
- Hypothesis testing
- Correlation analysis
- Linear regression
- Principal Component Analysis (PCA)

**Data Visualisation**

- Histograms
- Bar charts
- Pie charts
- Scatter plots
- Trendlines
- Residual analysis

---

## 🔄 Analysis Workflow

The project followed an end-to-end analytical workflow:

```text
Raw Transaction Data
        │
        ▼
Data Quality Assessment
        │
        ▼
Data Cleaning
Missing Values • Duplicates • Outliers
        │
        ▼
Data Transformation
Normalisation • Standardisation • Binning
        │
        ▼
Feature Engineering
Leads Generated • Total Projects
        │
        ▼
Bootstrapping
        │
        ▼
Exploratory Data Analysis
        │
        ▼
Statistical Modelling
Correlation • Hypothesis Testing • Regression • PCA
        │
        ▼
Business Interpretation
        │
        ▼
B2B Lead Prioritisation Insights
```

---

## 🧹 Data Cleaning & Preparation

The raw transactional dataset was systematically prepared before analysis.

The preprocessing workflow included:

- identifying and handling missing values
- removing duplicate transactions
- identifying outliers using the **Interquartile Range (IQR)** method
- normalising numerical variables to a `[0,1]` range
- standardising variables using z-scores
- creating categorical HIGH/LOW variables through binning

The original raw dataset was retained separately to maintain a reference point throughout the analysis.

---

## 🔧 Feature Engineering

Transactional information alone may not fully represent customer engagement or lead quality in a B2B sales environment.

Two additional business-oriented variables were therefore introduced:

### `Leads_Generated`

Represents lead-generation activity associated with an account and provides an additional indicator of potential customer engagement.

### `Total_Projects`

Represents the extent to which a customer has already engaged with the organisation through projects.

Sample values for these variables were sourced from synthetic B2B datasets and extended to the required dataset size using **bootstrapping**.

This allowed the analysis to incorporate additional engagement-related information alongside transactional variables.

---

## 📐 Principal Component Analysis

Principal Component Analysis was explored to determine whether the engineered variables could be simplified while retaining most of their information.

The analysis found:

| Principal Component | Explained Variance |
|---|---:|
| PC1 | ~64.6% |
| PC2 | ~35.4% |

Although the first principal component explained the majority of variance, the second component still contained substantial information.

Therefore, reducing the variables to a single component would result in meaningful information loss.

This suggested that the variables represented different aspects of customer behaviour and should remain separate for subsequent analysis.

---

## 📊 Exploratory Data Analysis

Several visualisations were created to understand the structure of the dataset and communicate findings to non-technical stakeholders.

### Order Quantity Distribution

The distribution of `ProductQuantity` was right-skewed, with most orders containing approximately **1–14 units**, while relatively few transactions represented larger orders.

This suggests that smaller transactions dominate the dataset, while larger purchases are comparatively uncommon.

### Geographic Distribution

More than **90% of transactions originated in the UK**, with substantially fewer observations from Germany, Switzerland, Sweden and France.

This highlights a strong geographic concentration in the dataset.

### Price vs Order Quantity

A scatter plot indicated a weak negative relationship between `PricePerUnit` and `ProductQuantity`.

This suggested that price alone was unlikely to provide enough information for reliable sales prioritisation.

---

## 📈 Statistical Analysis

### Confidence Intervals

The mean Product Quantity was:

**11.28 units**

with a 95% confidence interval of:

**[9.38, 13.18]**

Price per unit showed substantially less variation, with a 95% confidence interval of:

**[0.94, 1.05]**

---

### Hypothesis Testing

A one-tailed hypothesis test was conducted to investigate whether average order quantity exceeded a business benchmark of **10 units**.

Results:

```text
Z-score = 1.31
p-value = 0.095
α = 0.05
```

Because the p-value exceeded the significance threshold, there was insufficient statistical evidence to conclude that average order quantity was significantly above 10 units.

From a business perspective, this suggests that SDRs should not automatically interpret accounts as high-value based solely on expected order volume.

---

## 🔗 Correlation Analysis

The analysis found a weak negative correlation between:

```text
PricePerUnit ↔ ProductQuantity
r ≈ -0.292
```

Transaction timestamp showed negligible correlation with the other analysed variables.

These findings indicate that simple transactional characteristics alone provide limited information about customer behaviour.

---

## 📉 Regression Analysis

A linear regression model was created using:

- **Independent variable:** `PricePerUnit`
- **Dependent variable:** `ProductQuantity`

The estimated model was:

```text
ProductQuantity = 20.96 - 9.76 × PricePerUnit
```

The price coefficient was statistically significant:

```text
p ≈ 0.0009
```

However, overall explanatory power was low:

```text
R² = 0.085
```

This means that price alone explained only approximately **8.5% of the variation in order quantity**.

### Business Interpretation

Although price showed a statistically significant relationship with order quantity, it was not sufficient as a standalone predictor of purchasing behaviour.

For practical lead prioritisation, richer information such as customer engagement, industry, project activity or lead source would likely be required.

---

## 💡 Key Findings

| Finding | Result | Business Interpretation |
|---|---:|---|
| Price vs Quantity Correlation | **-0.292** | Weak negative relationship |
| Regression R² | **0.085** | Price alone explains little variation in order quantity |
| Regression p-value | **~0.0009** | Relationship is statistically significant but has limited predictive value |
| Order Quantity Test | **p = 0.095** | Insufficient evidence that mean quantity exceeds 10 |
| PCA Component 1 | **64.6%** | Captures majority, but not enough to discard PC2 |
| UK Transaction Share | **>90%** | Dataset is strongly geographically concentrated |

---

## 💼 Business Takeaways

One of the main findings from this project is the distinction between **statistical significance and business usefulness**.

Although price had a statistically significant relationship with order quantity, its low explanatory power indicates that it should not be used as the primary factor for prioritising B2B sales accounts.

A more useful sales-prioritisation framework would combine multiple signals such as:

- account engagement
- number of active projects
- lead-generation activity
- industry or customer segment
- acquisition channel
- historical purchasing behaviour

This would allow SDR teams to build more robust and interpretable lead-scoring systems.

---

## ⚠️ Limitations

This project was designed as an exploratory academic analysis and has several important limitations.

The dataset is relatively small and includes synthetic/bootstrapped variables. The analysis should therefore be interpreted as a demonstration of analytical methodology rather than a production-ready lead-scoring system.

The regression model also uses a limited number of transactional variables and does not include many of the behavioural and CRM features that would typically be available in a real B2B sales environment.

---

## 🚀 Future Improvements

The project could be extended by:

- using a larger real-world CRM dataset
- incorporating opportunity and conversion outcomes
- adding lead source, industry and company-size features
- developing a multivariate lead-scoring model
- comparing regression and machine-learning approaches
- building an interactive **Power BI dashboard**
- integrating CRM-style account segmentation
- evaluating model performance against actual conversion outcomes

A future version could ultimately provide SDRs with an interpretable account-prioritisation dashboard combining customer engagement, sales activity and predicted conversion potential.

---

## 📁 Repository Contents

```text
B2B-Sales-Analytics-Excel/
│
├── README.md
├── B2B_Sales_Analytics.xlsm
│
├── report/
│   └── COMP1887_Coursework_Report.pdf
│
└── images/
    └── project_visualisations
```

---

## 🎓 Academic Context

This project was completed as part of the **COMP1887 Principles of Data Science** module within the **MSc Data Science and Its Applications** programme at the University of Greenwich.

The project allowed me to combine my previous experience in **B2B technology sales** with data analytics, applying statistical and data-science techniques to a business problem I had encountered professionally.

---

## 👤 Author

**Julia Legner**  
MSc Data Science and Its Applications  
University of Greenwich

**Focus:** Data Analytics • Business Intelligence • Data Science • B2B Technology
