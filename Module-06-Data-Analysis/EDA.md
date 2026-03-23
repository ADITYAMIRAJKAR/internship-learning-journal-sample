# Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) is the critical first step in any data analysis process. It involves investigating datasets to summarize their main characteristics, often employing statistical graphics and other data visualization methods. 

The goal of EDA is not to make formal conclusions, but to understand the "shape" of the data, discover patterns, spot anomalies, and formulate hypotheses.

## 1. The Core Objectives of EDA
* **Understand the underlying structure:** What kinds of variables exist? (Categorical, numerical, datetime, etc.)
* **Identify missing data and outliers:** Are there gaps that will skew the analysis? Are there extreme values that need investigation?
* **Test underlying assumptions:** Is the data normally distributed? 
* **Uncover relationships:** How do different variables interact with each other?

---

## 2. The Standard EDA Workflow

A thorough EDA typically follows these stages:

### A. Data Profiling & Inspection
Getting a high-level overview of the dataset's size and variable types.
* **Shape:** How many rows and columns?
* **Data Types:** Are dates loaded as strings? Are numbers loaded as objects?
* **Missing Values:** What percentage of each column is null?

### B. Univariate Analysis
Analyzing one variable at a time to understand its distribution and central tendency.
* **Continuous Variables:** Look at Mean, Median, Mode, Standard Deviation, Min, and Max. Use histograms or box plots.
* **Categorical Variables:** Look at frequency counts and percentages. Use bar charts.

### C. Bivariate / Multivariate Analysis
Analyzing two or more variables to understand their relationships and correlations.
* **Numerical vs. Numerical:** Scatter plots, Correlation matrices (Pearson correlation).
* **Categorical vs. Numerical:** Box plots (e.g., comparing 'Salary' distribution across 'Job Titles').
* **Categorical vs. Categorical:** Stacked bar charts, cross-tabulations.

---

## 3. Programmatic EDA Example (Python)

Using `pandas` is the industry standard for conducting EDA programmatically. Here is a typical starter workflow:

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# 1. Load the data
df = pd.read_csv('dataset.csv')

# 2. Basic Inspection
print(df.head())          # View first 5 rows
print(df.info())          # Check data types and non-null counts
print(df.describe())      # Statistical summary of numerical columns

# 3. Check for Missing Values
print(df.isnull().sum())

# 4. Univariate: Distribution of a specific variable
sns.histplot(df['revenue'], kde=True)
plt.title('Distribution of Revenue')
plt.show()

# 5. Bivariate: Correlation Matrix
# Select only numeric columns for correlation
numeric_df = df.select_dtypes(include=['float64', 'int64'])
correlation_matrix = numeric_df.corr()

sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.show()
