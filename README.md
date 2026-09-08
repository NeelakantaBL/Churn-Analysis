# Churn-Analysis
This project analyzes customer churn using Python, Pandas, Matplotlib, Seaborn, and SQLite.

# Churn Analysis

## Overview

This project analyzes customer churn using **Python, Pandas, Matplotlib, Seaborn, and SQLite**.

The analysis combines customer, subscription, and customer support data to understand **customer retention, churn behavior, subscription plan performance, customer risk levels, revenue at risk, and support-related factors associated with churn**.

The goal is to identify patterns that can help businesses understand why customers leave and support better customer retention strategies.

---

## Business Problem

Customer churn can directly affect recurring revenue and long-term customer value.

This project focuses on answering questions such as:

* What is the overall customer churn rate?
* What percentage of customers are retained?
* Which subscription plans have higher churn?
* What is the average revenue per user (ARPU)?
* What is the average customer tenure?
* How much monthly revenue is at risk from churned customers?
* How frequently do customer support escalations occur?
* Is there a relationship between support escalations and customer churn?
* Which customers fall into low, medium, and high churn-risk categories?
* How does churn vary across states and over time?

---

## Dataset

The project uses three SQLite tables:

### 1. Customer Table — `db_customer`

Contains customer information such as:

* Customer ID
* Customer Name
* Country
* State
* Gender
* Date of Birth
* Interests
* Pincode

### 2. Subscription Table — `db_subscription`

Contains subscription and churn-related information:

* Customer ID
* Subscription Start Date
* Subscription Type
* Renewal Date
* Plan Type
* Contract Type
* Cancellation Date
* Cancellation Reason
* Monthly Charges
* CLTV
* Churn Score

### 3. Support Table — `db_support`

Contains customer support information:

* Customer ID
* Complaint Date
* Escalations
* CSAT Score
* Comments

The three datasets were joined using `customerid` to create a combined analytical dataset.

---

## Tools & Technologies

* **Python**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **SQLite**
* **Jupyter Notebook**

---

## Project Workflow

The project follows these main steps:

1. Connect to SQLite database
2. Explore database tables
3. Load tables into Pandas DataFrames
4. Perform data cleaning
5. Standardize and transform columns
6. Create churn-related features
7. Merge customer, subscription, and support data
8. Calculate business KPIs
9. Perform churn analysis
10. Create visualizations
11. Generate the final analytical dataset

---

## Data Cleaning & Preparation

The following cleaning and transformation steps were performed:

* Renamed `name` to `customer_name`
* Removed unused `interests` and `pincode` columns
* Converted date columns to datetime format
* Standardized gender values such as `Men` and `Women` to `Male` and `Female`
* Filled missing country values using state-country mapping
* Removed unused support columns
* Converted complaint dates to datetime
* Created a `churn_flag` based on cancellation status
* Created a `complaint_count` feature
* Merged customer, subscription, and support tables

The final merged dataset contained **21 customers and 21 analytical columns** before later feature additions.

---

## Feature Engineering

Several analytical features were created during the project.

### Churn Flag

A binary `churn_flag` was created from customer cancellation information.

* `0` → Customer retained
* `1` → Customer churned

### Tenure

Customer tenure was calculated using:

* Cancellation date for churned customers
* Current date for active customers

### Churn Risk

Customers were categorized based on their `churn_score`:

| Churn Score  | Risk Level |
| ------------ | ---------- |
| Below 50     | Low        |
| 50–69        | Medium     |
| 70 and above | High       |

This classification was implemented directly in the notebook.

### Complaint Count

The number of support complaints was calculated for each customer to support customer-experience analysis.

---

## Key Analysis

### 1. Churn Rate

The overall churn rate was calculated as:

**Churn Rate = 28.57%**

### 2. Retention Rate

The calculated retention rate was:

**Retention Rate = 71.43%**

These KPIs were calculated from the `churn_flag` created in the merged dataset.

---

### 3. Churn by Plan Type

The analysis compared churn rates across subscription plans:

| Plan Type | Churn Rate |
| --------- | ---------: |
| Basic     |     60.00% |
| Standard  |     22.22% |
| Premium   |     14.29% |

The **Basic plan recorded the highest churn rate**, while the Premium plan recorded the lowest.

---

### 4. Average Revenue Per User

The calculated ARPU was:

**₹18.85**

This represents the average monthly charge per customer in the analyzed dataset.

---

### 5. Average Customer Tenure

The average customer tenure was calculated as:

**1,524 days**

Tenure was calculated using the subscription start date and either the cancellation date or current date.

---

### 6. Revenue at Risk

Monthly revenue associated with churned customers was calculated as:

**₹73.94**

This metric represents the monthly charges from customers who had churned.

---

### 7. Escalation Rate

The customer support escalation rate was:

**19.05%**

This was calculated based on support records marked with an escalation value of `Y`.

---

### 8. Customer Complaints

The average number of complaints per customer was:

**0.43 complaints per customer**.

---

### 9. Escalation vs Churn

The project calculated the correlation between support escalations and churn.

**Correlation = 0.77**

This indicates a strong positive relationship within this small project dataset. It should be interpreted as an observed association rather than proof that escalations directly cause churn.

---

## Visualizations

The project includes visual analysis using **Matplotlib and Seaborn**.

### Matplotlib Visualizations

* Monthly churn trend
* Churn by plan type
* Churn by state

The monthly churn analysis shows churn occurrences across February, May, September, October, and November 2024, with September having the highest count in the available data.

### Seaborn Visualizations

* Correlation heatmap
* Pairplot
* Customer plan and monthly-charge comparisons
* Churn-risk comparisons using categorical visualizations

A pivot table was also used to compare churn rates across subscription plans.

---

## Key Insights

Based on the analysis:

* The overall churn rate is **28.57%**.
* The retention rate is **71.43%**.
* The **Basic plan has the highest churn rate at 60%**.
* The **Premium plan has the lowest churn rate at 14.29%**.
* Average monthly revenue per user is **₹18.85**.
* Average customer tenure is approximately **1,524 days**.
* Churned customers represent **₹73.94 in monthly revenue at risk**.
* The escalation rate is **19.05%**.
* The analysis found a **0.77 correlation between support escalations and churn**.
* Churn-risk categories help identify customers with low, medium, and high predicted risk based on their churn scores.

---

## Business Recommendations

Based on the project findings:

1. **Focus on Basic Plan Customers**
   Investigate the reasons behind the high churn rate of Basic plan customers and consider improving the value offered by this plan.

2. **Monitor High-Risk Customers**
   Use churn scores to identify high-risk customers and prioritize retention activities.

3. **Improve Customer Support**
   Monitor escalations and complaints because the analysis shows a strong association between escalation status and churn.

4. **Develop Retention Strategies**
   Create targeted retention offers or engagement campaigns for customers showing high churn risk.

5. **Monitor Churn Trends**
   Track churn over time to identify periods where customer cancellations increase.

---

## Project Structure

```text
Churn-Analysis/
│
├── exported_churn_data.csv
├── test_database.sqlite
├── churn_analysis.ipynb
└── README.md
```

---

## How to Run

### 1. Clone the Repository

```bash
git clone <your-github-repository-url>
```

### 2. Install Required Libraries

```bash
pip install pandas numpy matplotlib seaborn
```

### 3. Open the Notebook

Open:

```text
churn_analysis.ipynb
```

using Jupyter Notebook or JupyterLab.

### 4. Run the Analysis

Make sure the SQLite database file is available in the expected project location before running the notebook.

The notebook connects to SQLite, loads the database tables, performs data preparation and analysis, and exports the combined dataset as:

```text
exported_churn_data.csv
```

---

## Project Deliverables

* Python/Jupyter Notebook
* SQLite Database
* Exported Analytical Dataset
* Churn Analysis PDF
* Data Cleaning & Feature Engineering
* Exploratory Data Analysis
* Business KPI Analysis
* Data Visualizations

---

## Skills Demonstrated

* Python for Data Analysis
* Pandas Data Manipulation
* NumPy
* SQLite Database Handling
* Data Cleaning
* Data Transformation
* Feature Engineering
* Exploratory Data Analysis
* Customer Churn Analysis
* KPI Calculation
* Data Visualization
* Matplotlib
* Seaborn
* Business Insight Generation

---

## Project Highlights

* Calculated **28.57% customer churn rate**
* Identified **Basic plan as the highest-churn segment**
* Calculated **₹18.85 ARPU**
* Calculated **1,524-day average customer tenure**
* Identified **₹73.94 monthly revenue at risk**
* Analyzed customer support escalations and churn relationship
* Created **low, medium, and high churn-risk categories**
* Built churn visualizations using **Matplotlib and Seaborn**
* Exported a consolidated analytical dataset for further analysis
