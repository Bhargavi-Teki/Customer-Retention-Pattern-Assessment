# 📉 Customer Retention Pattern Assessment

## 📌 Overview
An executive-level diagnostic utilizing the IBM Telco dataset to uncover high-impact strategies for customer retention. This project transforms raw behavioral data into a **Power Pivot-driven analytical engine** to pinpoint high-priority segments and identify actionable shifts to decrease churn.

---

## 📊 Dashboard Preview

![CRPA Dashboard](https://github.com/Bhargavi-Teki/Customer-Retention-Pattern-Assessment/blob/main/Customer_Retention_Pattern_Assessment_Overview.png)

---

## 🎯 Business Objectives
* **Diagnose Attrition Drivers** – Pinpointing root causes of departure by correlating exit reasons with customer behavioral patterns.
* **Quantify Revenue Risk** – Assessing financial exposure by mapping total revenue against high-value demographics and segments.
* **Enable Proactive Retention** – Engineering a DAX-driven risk-scoring framework to identify high-risk customers for early intervention.

---

## 🛠 Tech Stack
Excel, Power Query, Power Pivot, DAX

---

## 📊 Calculated Intelligence (DAX Engine)
Custom logic was engineered to segment the dataset and isolate specific drivers of revenue and attrition.

#### 1. Demographic & Revenue Segmentation
*Quantifying financial contributions and churn rates across key customer profiles.*

```DAX
_Revenue Performance per Segment
Revenue_Senior := CALCULATE(Sum(Table1[Total revenue]), Table1[Senior Citizen]="Yes")
Revenue_Partners := CALCULATE(SUM(Table1[Total revenue]), Table1[Partner]="Yes")
Revenue_Dependents := CALCULATE(SUM(Table1[Total revenue]), Table1[Dependents]="Yes")

_Comparative Churn Impact
Churnrate_Senior := DIVIDE(CALCULATE(DISTINCTCOUNT(Table1[CustomerID]), Table1[Churn Label]="Yes", Table1[Senior Citizen]="Yes"), CALCULATE(DISTINCTCOUNT(Table1[CustomerID]), Table1[Churn Label]="Yes"))
Churnrate_Partners := DIVIDE(CALCULATE(DISTINCTCOUNT(Table1[CustomerID]), Table1[Churn Label]="Yes", Table1[Partner]="Yes"), CALCULATE(DISTINCTCOUNT(Table1[CustomerID]), Table1[Churn Label]="Yes"))
Churnrate_Dependents := DIVIDE(CALCULATE(DISTINCTCOUNT(Table1[CustomerID]), Table1[Churn Label]="Yes", Table1[Dependents]="Yes"), CALCULATE(DISTINCTCOUNT(Table1[CustomerID]), Table1[Churn Label]="Yes"))

```
---

#### 2. Risk Modeling & Volume Tracking
*Isolating at-risk customers for proactive retention and monitoring current attrition volume.*

```DAX
1. Proactive Risk Identification: Targetting the "Very High Risk" segment
At risk customers := CALCULATE(DISTINCTCOUNT(Table1[CustomerID]), Table1[Churn Label] = "No", Table1[Churn Band] = "Very High Risk", ALL(Table1[Churn Label], Table1[Churn Band]))

2. Retention Benchmarking
Total customers := CALCULATE(DISTINCTCOUNT(Table1[CustomerID]), ALL(Table1[Churn Label], Table1[Churn Band]))
Churned := CALCULATE(DISTINCTCOUNT(Table1[CustomerID]), Table1[Churn Label] = "Yes", ALL(Table1[Churn Label], Table1[Churn Band]))
Retained := [Total customers] - [At risk customers] - [Churned]

```
---

#### 3. Executive Health Metrics
*Standardized KPIs used to monitor the overall health of the customer lifecycle.*

```DAX
1. Churn Rate Calculation
Churn Rate := DIVIDE(CALCULATE(COUNTROWS(Table1), Table1[Churn Value] = 1), COUNTROWS(Table1))

2. Retention Rate Calculation
Retention Rate := 1 - [Churn Rate]

3. Average Customer Lifecycle (Years)
Average Tenure (Yrs) := AVERAGE(Table1[Tenure Months]) / 12

```
---

## 📂 Data Source

**Dataset:** IBM Telco Customer Churn (Sourced from Kaggle).

**Raw File:** [Download here](./Data/Customer_Retention_Pattern_Assessment.xlsx)

---

## 📈 Key Visualizations

**Gauge Charts:**  Tracking real-time Churn and Retention rates against organizational benchmarks.

**Donut Charts:** Visualizing the Churned vs. Retained rate percentage for a high-level population breakdown.

**Funnel Chart:** Mapping the customer journey from Total Customers to Retained and Churned volumes.

**Bar Charts:** Comparative analysis used to show churn distribution by Cities and specific Exit Reasons.

**Treemap:** Breakdown of the "Why" behind departures to identify the hierarchy of primary exit drivers.

**Combo Chart:** Analyzing revenue trends against transaction volume and tenure length.

**Heatmap / Risk Band Distribution:**  Visualizing the distribution of the customer base across specific Churn Scores and risk levels.

---

## 💡 Strategic Insights

**Support Quality:** Customer service attitude is the top reason for leaving; improving staff training is a key way to keep customers.

**Payment Methods:** Users paying by Electronic Check leave at a much higher rate (45%) than those on Auto-Pay (16%).

**Contract Length:** Month-to-month plans are very unstable; moving customers to 1-year contracts helps keep revenue steady.

---

## 🧠 What I Learned

*Implementing advanced DAX for conditional counting and risk scoring.

*Managing Power Query ETL to structure multi-dimensional behavioral datasets.

*Translating technical patterns into actionable executive recommendations.

---





