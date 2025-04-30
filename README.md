# 10Academy-Kifiya-Week-2

# AlphaCare Risk Analysis Project

A project for analyzing insurance claim data to optimize marketing strategies.

## Overview

The **AlphaCare Risk Analysis Project** aims to analyze insurance-related data to uncover patterns, trends, and insights that drive better decision-making. By understanding key factors influencing claims and premiums, this analysis helps refine risk assessment models and optimize insurance policies.

This project adopts a **modular approach**, organizing functionalities into reusable script files for efficient and scalable data exploration and analysis.


---
## Introduction

This report evaluates historical insurance claim data to optimize marketing strategies and identify low-risk targets for premium reductions. The analysis focuses on evaluating risk differences across demographic and geographic features, margin comparisons, and actionable insights based on statistical evidence. Key tasks include:

1. Hypothesis testing for group differences.
2. Identifying key metrics and evaluation methodologies.
3. Proposing strategies to minimize temporal leakage and dimensionality challenges.

Initial results highlight critical areas for intervention, suggesting savings opportunities to optimize claims and profits.

### Objectives

1. Analyze policyholder data to assess the link between vehicle attributes and claim rates.
2. Detect and address missing values and anomalies.
3. Develop modular, reusable code for data preprocessing, exploratory data analysis (EDA), and analytics.
4. Integrate version control and dataset tracking using Data Version Control (DVC).

---

## Tools & Technologies

The project leverages the following tools and libraries:

- **Python**: Core programming language for data manipulation and analysis.
- **Pandas**: For efficient data handling and preprocessing.
- **NumPy**: For numerical computations.
- **Seaborn**: For advanced data visualization.
- **Matplotlib**: For plotting and graphical representation.
- **Jupyter Notebooks**: For step-by-step interactive analysis.
- **Git/GitHub**: For version control and collaboration.

## Data Overview

### Dataset Highlights

- **Entries**: 1,000,098
- **Columns**: 52
- **Memory Usage**: ~390.1 MB

Key features include policy details (`UnderwrittenCoverID`, `PolicyID`), vehicle attributes (`mmcode`, `Cylinders`, `cubiccapacity`), and financial metrics (`SumInsured`, `TotalPremium`, `TotalClaims`).

### Statistical Summary

| Feature                  | Range                  | Mean           | Observations |
|--------------------------|------------------------|----------------|--------------|
| `UnderwrittenCoverID`    | 1 - 301,175           | N/A            | Unique ID    |
| `RegistrationYear`       | 1987 - 2015           | 2010           | Older vehicles have higher claims. |
| `SumInsured`             | 0.01 - 12.63M         | $604,172       | Heavy skewness, outliers present. |
| `CalculatedPremiumPerTerm` | 0 - 74,422          | $117.88        | Contains zero values. |
| `TotalClaims`            | 0 - 393,092           | $64.86         | Outliers noted. |

![alt text](screenshots/image-6.png)

### Data Skewness

- Numerical features such as `SumInsured` and `TotalClaims` exhibit skewness. 
- Log transformations may mitigate this for modeling.
---

## Exploratory Data Analysis (EDA)

### Missing Data Analysis

22 columns have missing values. Notable examples include:

| Column                    | Missing (%) | Impact      |
|---------------------------|-------------|-------------|
| `NumberOfVehiclesInFleet` | 100.00%     | High        |
| `CrossBorder`             | 99.93%      | High        |
| `CustomValueEstimate`     | 77.96%      | High        |
| `Rebuilt`                 | 64.18%      | Moderate    |
| `WrittenOff`              | 64.18%      | Moderate    |
| `Converted`               | 64.18%      | Moderate    |
| `NewVehicle`              | 15.33%      | Low         |
| `Bank`                    | 14.59%      | Low         |

![alt text](screenshots/image.png)

### Key Findings from the EDA

The exploratory data analysis (EDA) focused on assessing the dataset's quality, identifying trends, and deriving actionable insights. Below are the key findings:

#### **Data Summarization**
- Calculated descriptive statistics (e.g., mean, median, variance) for critical numerical features like `TotalPremium` and `TotalClaim`.
- Reviewed data types to validate formatting for categorical variables and date fields.

##### **Data Quality Insights**
- Identified and summarized missing values both in table format and visually using heatmaps.
- Several columns have missing values; key among them are:
  - `PostalCode`: Missing in 15% of the dataset.
  - `EmploymentType`: Missing in 10% of the dataset.
- Non-uniform data types were corrected:
  - Dates were converted to a consistent `datetime` format.
  - Categorical levels were standardized.

##### **Univariate Analysis**
- Created histograms for numerical columns (e.g., `TotalPremium`).
- Developed bar charts for categorical variables to analyze their distributions.

##### **Bivariate and Multivariate Analysis**
- Explored correlations using scatter plots and correlation matrices, focusing on:
  - Relationships between `TotalPremium` and `TotalClaim` as a function of `ZipCode`.
- Compared geographic trends in factors such as insurance cover types and premiums.

##### **Correlation Analysis**
- There’s a moderate correlation of **0.58** between `TotalPremium` and `TotalClaims`, highlighting potential dependencies.
- The `SumInsured` amount showed a strong positive correlation with the premium amount.
  
#### **Outlier Detection**
- Generated box plots for key numerical features to detect and analyze outliers.

#### **Geographical Trends**
- **Provinces with High Premiums**: Ontario and Alberta have the highest average `TotalPremium`, suggesting that risk factors may vary significantly across provinces.
- **Geographical Outliers**: Certain postal codes have significantly higher claims rates compared to their provincial averages.

##### **Key Demographic Trends**
- **Age Factor**: Claims frequency is higher for policyholders aged 25-35, indicating higher risks in this demographic.
- **Employment Type**: Contract employees show higher claim-to-premium ratios compared to permanent employees.

#### **Insights on Claim Ratios**
- Policies under **"Comprehensive Cover Type"** have higher claims as compared to other types.
- Higher claims are observed for individuals with high `SumInsured` values.

#### **Visualization Highlights**

- **Bubble Chart**: Analyzed trends across multiple dimensions (e.g., premiums by geography). It showed an interesting distribution where:
  - Larger policies tend to cluster in low-claim regions.
  - Certain coverage types consistently stand out with higher claims.
- **Correlation Heatmap**: Displayed associations between numerical variables.
- **Geographic Trends**: Bar plots highlighting regional averages for `TotalPremium`.

---

**Insights:**
- Features with nearly 100% null values, such as `NumberOfVehiclesInFleet` and `CrossBorder`, are likely candidates for exclusion.
- Minor gaps in columns like `Cylinders` require imputation.

### Correlation Insights

| Features                             | Observation                        |
|--------------------------------------|------------------------------------|
| `SumInsured` vs. `TotalClaims`       | Strong positive correlation.       |
| `RegistrationYear` vs. `TotalClaims` | Claims increase for older vehicles |
| `CalculatedPremiumPerTerm`           | Zero values skew distributions     |

![alt text](screenshots/image-5.png)

![alt text](screenshots/image-1.png)

### Identified Anomalies  

- **High-Cardinality Columns**:  
    - Features like `Model` (409 levels) and `VehicleIntroDate` (174 levels)
    - Inflate dimensionality and complicate modeling
    - Used strategies like grouping and Label encoding

- **Low Variance Columns**:  
    - Columns such as `Language` and `ItemType` have a single level
    - Offer no analytical value/variance, are therefore excluded.
---

## Data Engineering & Workflow

### Version Control with DVC & Git
DVC integrates seamlessly with Git, enabling efficient dataset versioning.

Example command log:
```bash
$ git log --oneline --graph
052c56b Track dataset using DVC
8b996cb Add CI workflow using GitHub Actions
```

### Handling Temporal Leakage
To minimize temporal leakage, temporal predictors are aggregated into historical features using rolling averages. Categorical variables such as `Month` are encoded cyclically to preserve continuity:
```python
import numpy as np

data['Month_Sine'] = np.sin(2 * np.pi * data['Month'] / 12)
data['Month_Cosine'] = np.cos(2 * np.pi * data['Month'] / 12)
```

## Statistical Testing

### Hypothesis Testing
**Objective:** To evaluate and compare the impact of categorical variables such as provinces, zip codes, and genders on risk profiles and profit margins.

#### Hypotheses:

1. **No risk differences across provinces**.
2. **No risk differences between zip codes**.
3. **No significant margin differences between zip codes**.
4. **No significant risk differences between women and men**.

### Statistical Analysis Framework

#### KPIs Selected:
- **Risk:** Defined as the ratio of `TotalClaims` to `TotalPremium`.
- **Profit Margin:** Calculated as `TotalPremium` – `TotalClaims`.

#### Data Segmentation Methodology:

- **Control vs. Test Groups:**
  Groups were compared to isolate individual feature effects while ensuring equivalence in demographic attributes, vehicle specifications, and plan types.

- **Statistical Tests Applied:**
  - **t-tests** for mean differences in numerical KPIs. Validates differences between two groups.
  - **Chi-Squared Tests** for categorical distribution comparisons.
  - **ANOVA**: Tests differences across multiple groups simultaneously without inflating Type I error.

#### Results:

| Hypothesis                                      | Test Method | Statistic | p-value  | Significant? |
|------------------------------------------------|-------------|-----------|----------|--------------|
| **Risk differences across provinces**          | ANOVA       | 4.989     | 3.33e-06 | Yes          |
| **Risk differences between zip codes**         | T-test      | 1152.833  | 4.80e-11 | Yes          |
| **Margin differences across zip codes**        | ANOVA       | 0.840     | 0.999    | No           |
| **Risk differences between genders**           | T-test      | 32908460  | 0.635    | No           |

#### Key Inferences:
1. Significant risk differences exist across provinces and zip codes, suggesting a need for location-specific underwriting strategies.
2. Gender has no measurable impact on risk, supporting gender-neutral policies.
3. Margins are consistent across locations, showing no significant profitability variations.

---

### Advanced Savings Opportunities
**Goal:** Identify top-performing regions (provinces, zip codes) with potential for cost savings in terms of premiums and claims.

#### Methodology
- **Savings Calculation:**
  Savings = (`Premium` – `Claims`) / `Premium`

- **Findings:**
  - **Top Provinces for Savings:**
    ```
   Province Savings %
   NorthernCape	71.73%
	FreeState	48.98%
	EasternCape	37.10%
	Limpopo	35.48%
	Mpumalanga	28.22%
	NorthWest	25.32%
    ```
   
![alt text](screenshots/image-9.png)

  - **Zip Codes Savings:**
   
   ![alt text](screenshots/image-10.png)

---

## Predictive Modeling Insights

### Model Performance Summary

| Model             | MAE        | MSE         | R²       |
|--------------------|------------|-------------|------------|
| Linear Regression | 239.05     | 10.59M      | 0.006      |
| XGBoost           | 437.73     | 13.58M      | -0.273     |
| Random Forest     | 242.74     | 12.83M      | -0.204     |

#### Feature Importance (Random Forest)

| Feature                              | Importance (%) |
|--------------------------------------|----------------|
| TotalPremium                         | 12.37          |
| CoverGroup_Comprehensive-Taxi        | 7.31           |
| Section_Optional Extended Covers     | 7.25           |
| Model_QUANTUM 2.7 SESFIKILE 16s      | -5.84          |
| VehicleIntroDate_4/2012              | 5.49           |
| CoverType_Own Damage                 | 4.45           |
| CalculatedPremiumPerTerm             | 4.04           |
| Model_QUANTUM 2.5 D-4D SESFIKILE 16s | -4.00          |


### Interpretation:
The low R² values across models suggest that additional explanatory variables may be needed to improve prediction accuracy. Despite the suboptimal performance, feature importance rankings guide the development of targeted strategies, such as optimizing premiums for specific cover types.

---

## Recommendations

1. **Localized Premium Strategies**:
   - Use insights from geographic segmentation to create dynamic pricing structures.
2. **Feature Engineering**:
   - Aggregate high-dimensional features like `Model` into broader categories.
   - Address numerical skewness via log transformations.
3. **Data Quality Improvements**:
   - Address gaps in high-impact features with targeted imputation.

---

## Conclusion

This analysis highlights significant risk differences across geographic regions, providing actionable insights for premium adjustments and risk mitigation. By refining data preprocessing workflows and statistical tests, the next phase will focus on building robust predictive models for accurate claim predictions and profitability analysis.

## Appendix

### Feature Impact Modeling

**XGBoost:**

![alt text](screenshots/image-8.png)
 
 Random forest

 ![alt text](screenshots/image-7.png)

---
**Shapley:**

![alt text](screenshots/image-13.png)

![alt text](screenshots/image-14.png)

**Lime:**

![alt text](screenshots/image-11.png)

![alt text](screenshots/image-12.png)


### Additional Visualizations

![alt text](screenshots/image-4.png)

![alt text](screenshots/image-3.png)

![alt text](screenshots/image-2.png)
