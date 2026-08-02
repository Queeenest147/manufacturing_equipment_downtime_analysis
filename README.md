# Daikibo Manufacturing Operations Analytics
### Machine Downtime & Gender Pay Equality Analysis

<p align="center">

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=Power%20BI&logoColor=black)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-005571?style=for-the-badge)
![Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![JSON](https://img.shields.io/badge/JSON-000000?style=for-the-badge&logo=json&logoColor=white)

</p>

---

## Table of Contents

- [Executive Summary](#-Executive-Summary)
- [Business Problem](#-Business-Problem)
- [Tools Used](#-Tools-Used)
- [Methodology](#-Methodology)
- [Data Cleaning & Preparation](#-Data-Cleaning--Preparation)
- [Dashboard Preview](#-Dashboard-Preview)
- [Key Insights](#-Key-Insights)
- [Recommendations](#-Recommendations)
- [Limitations](#-Limitations)
- [Implementation Plan](#-Implementation-Plan)
- [Business Impact](#-Business-Impact)

---

# Executive Summary

This project analyzes operational telemetry data collected from four **Daikibo manufacturing plants** to identify which factories and machine types experienced the highest downtime during **May 2021**.

The telemetry dataset was provided in **JSON format** and transformed using **Power Query** before being analyzed in **Power BI**. An additional **HR dataset** was analyzed in **Microsoft Excel** to classify job roles based on gender pay equality.

The analysis found that **Daikibo Factory Seiko** recorded the highest machine downtime, with **Laser Welders** and **Laser Cutters** contributing most of the production interruptions.

The pay equality assessment also categorized job roles into **Fair**, **Unfair**, and **Highly Discriminative** based on equality scores.

These insights help management prioritize equipment maintenance while also identifying departments requiring HR review.

---

# Business Problem

Daikibo Industrials wanted to answer two important business questions:

- Which factory experienced the highest machine downtime?
- Which machine types contributed most to that downtime?

In addition, the HR department wanted to investigate internal complaints about **gender pay inequality** by classifying job roles according to their **Equality Scores**.

Understanding both operational performance and workplace equality enables management to make better business decisions.

---

# Tools Used

| Tool | Purpose |
|-------|----------|
| **Power BI** | Data visualization & dashboard development |
| **Power Query** | Data cleaning and transformation |
| **DAX** | Feature engineering and calculated columns |
| **Microsoft Excel** | Gender pay equality classification |
| **JSON** | Telemetry data source |

---

# Methodology

The project followed a structured analytics workflow.

### 1️⃣ Data Collection

- Imported machine telemetry data from a JSON file.
- Imported HR Equality Score dataset from Excel.

### 2️ Data Preparation

- Cleaned and transformed both datasets.
- Converted raw telemetry data into an analysis-ready format.
- Created calculated fields for downtime analysis.
- Built interactive Power BI visuals.
- Classified Equality Scores using Excel formulas.

---

# Data Cleaning & Preparation

Since the telemetry dataset was stored as **nested JSON**, several preprocessing steps were required before analysis.

## Telemetry Dataset (Power Query)

✔ Imported JSON into Power BI

✔ Expanded nested **Location** records

✔ Expanded nested **Data** records

✔ Renamed columns into business-friendly names

✔ Converted Unix Timestamp into standard **DateTime**

✔ Corrected incorrect data types

✔ Checked for duplicate records

✔ Checked for missing values

✔ Standardized factory names

✔ Standardized country and city names

✔ Verified machine status values

✔ Removed unnecessary columns where applicable

---

## Feature Engineering

A calculated column named **Unhealthy** was created.

Each machine sends telemetry every **10 minutes**.

If the machine status is:

- **Unhealthy → 10**
- **Healthy → 0**

This allows downtime to be aggregated across factories and machine types.

```DAX
Unhealthy =
IF([Status] = "unhealthy", 10, 0)
```

---

## Equality Dataset (Excel)

The HR dataset contained:

- Factory
- Job Role
- Equality Score

A new field called **Equality Class** was created using an **IFS()** formula.

| Equality Score | Classification |
|---------------|----------------|
| -10 to 10 | Fair |
| -20 to -11 or 11 to 20 | Unfair |
| Less than -20 or greater than 20 | Highly Discriminative |

This transformed raw numerical scores into business-friendly categories for HR reporting.

---

# Dashboard Preview

## Machine Downtime Dashboard

<img width="866" height="478" alt="daikibo_machine_downtime_dashboard" src="https://github.com/user-attachments/assets/5c85ca0c-3a83-491a-be24-b643fb250234" />


Selecting a factory automatically displays the machine types responsible for downtime at that location.

---

# Key Insights

## Insight 1 — Daikibo Factory Seiko Recorded the Highest Downtime

### What happened?

Daikibo Factory Seiko experienced the highest amount of machine downtime among all four factories.

### Business Impact

High downtime reduces production efficiency, increases maintenance costs, and may delay manufacturing operations.

---

## Insight 2 — Daikibo Shenzhen Ranked Second

Shenzhen also experienced significant downtime, indicating that maintenance attention should not focus solely on one factory.

---

## Insight 3 — Laser Welders Were the Largest Source of Downtime

Laser Welders generated the greatest amount of downtime across all factories.

These machines appear to be the most failure-prone equipment within the production process.

---

## Insight 4 — Laser Cutters Ranked Second

Laser Cutters were the second-largest contributor to production interruptions.

Together, Laser Welders and Laser Cutters account for most operational downtime.

---

## Insight 5 — Berlin Factory Recorded the Lowest Downtime

Daikibo Berlin experienced minimal downtime compared to the other factories.

Possible reasons include:

- Better maintenance practices
- Newer equipment
- Improved operating conditions

These practices could potentially be replicated across other factories.

---

## Insight 6 — Gender Pay Equality Classification

The Equality Score analysis grouped job roles into:

- Fair
- Unfair
- Highly Discriminative

This enables HR teams to quickly identify departments requiring further investigation.

---

# Recommendations

### Improve Preventive Maintenance

Schedule routine maintenance for **Laser Welders** and **Laser Cutters**, as they account for the highest downtime.

---

### Investigate Factory Seiko

Conduct a root cause analysis to understand why Factory Seiko consistently experiences higher downtime.

---

### Benchmark Berlin

Study Berlin's maintenance processes and implement best practices across other factories.

---

### Implement Real-Time Monitoring

Deploy live telemetry dashboards with automated alerts to detect equipment failures before they escalate.

---

### HR Review

Review all job roles classified as **Highly Discriminative** to determine whether compensation adjustments are necessary.

---

# Limitations

- Data covers only **May 2021**.
- Machine downtime is inferred from telemetry status only.
- Root causes of equipment failures were not provided.
- HR data measures equality scores but does not explain the reasons behind pay differences.
- Historical maintenance records were unavailable.

---

# Implementation Plan

| Phase | Action |
|--------|--------|
| **Phase 1** | Monitor downtime daily using the dashboard |
| **Phase 2** | Prioritize maintenance for Laser Welders and Laser Cutters |
| **Phase 3** | Investigate operational processes at Factory Seiko |
| **Phase 4** | Review HR roles classified as Highly Discriminative |
| **Phase 5** | Automate reporting using scheduled Power BI refresh |

---

#  Business Impact

This analysis enables Daikibo Industrials to:

- Reduce production downtime
- Improve maintenance planning
- Allocate maintenance resources more effectively
- Monitor factory performance in real time
- Support data-driven HR decisions regarding pay equality
- Improve operational efficiency through continuous monitoring

---

## 👩🏽‍💻 Author

**Esther Matthew**

Data Analyst | Power BI | SQL | Excel | Python

🔗 **LinkedIn:** *linkedin.com/in/esther-matthew*

---

<p align="center">

⭐ If you found this project interesting, feel free to star the repository!

</p>
