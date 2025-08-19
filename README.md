# Palmora-Group-HR-Analysis

> **A storytelling HR analytics case study built in Power BI**

“Palmoria Group, a major player in the Nigerian manufacturing industry, recently came under fire for alleged gender inequality practices. Headlines like *`the Manufacturing Patriarchy.`* threatened not just its image, but also its expansion plans into new regions and global markets. To prevent further damage, the CEO tasked the CHRO to identify the root causes. That’s where I came in: to uncover the truth hidden in Palmoria’s HR data and guide management on the path forward.”

This repository documents the analysis, visuals, and decisions derived from the data. It is written as a narrative that takes management from 
**problem → evidence → insight → action**.

---

## 📑 Table of Contents

* [Business Context](#business-context)
* [Case Scenario & Questions](#case-scenario--questions)
* [Data & Assumptions](#data--assumptions)
* [Tools Used](#tools-used)
* [Data Preparation](#data-preparation)
* [Key Measures (DAX)](#key-measures-dax)
* [Visual Design](#visual-design)
* [Insights & Story](#insights--story)

  * [1) Workforce & Gender Distribution](#1-workforce--gender-distribution)
  * [2) Performance Ratings by Gender](#2-performance-ratings-by-gender)
  * [3) Compensation & Gender Pay Gap](#3-compensation--gender-pay-gap)
  * [4) Salary Banding & Regulatory Compliance](#4-salary-banding--regulatory-compliance)
  * [5) Bonus Allocation & Total Payouts](#5-bonus-allocation--total-payouts)
* [Recommendations](#recommendations)
* [Skills Demonstrated](#skills-demonstrated)
* [Limitations](#limitations)
* [Conclusion](#conclusion)

---

### 🏢 Business Context

A recent headline labeled Palmora *“the Manufacturing Patriarchy.”* Leadership wants clarity on:

1. the **true state of gender representation**, 
2) whether a **gender pay gap** exists and where, and 
3) what **corrective actions** will deliver the most impact fastest.

**Mandate:**

* Focus on gender-related issues at the **organization, region, and department** levels.
* Use accessible visuals to drive discussion and decisions with executives.

---

### 🎯 Case Scenario & Questions

**Pointers from Mr. Gamma (insider):**

1. What is the gender distribution in the organization? Distill to regions and departments.
2. Show insights on ratings based on gender.
3. Analyze the salary structure. Identify if there is a gender pay gap; if yes, where should management focus (departments/regions)?
4. A new regulation mandates a **minimum salary of \$90,000** for manufacturing staff.

   * Does Palmora comply?
   * Show the **pay distribution in \$10,000 bands**; also break down by region.
5. Allocate **annual bonus** by performance rules and report:

   * Bonus per employee
   * **Total amount per employee** (salary + bonus)
   * **Totals by region** and **company-wide**

---

### 📊 Data & Assumptions

* Palmora Group emp-dataset (demographics, department, region, base salary, performance rating)
* Bonus rules dataset (mapping performance rating to % bonus)
* **Assumptions / Requirements applied:**

  * Employees with **no salary** are considered **inactive** and removed from analysis.
  * Rows with **Department = NULL** are excluded.
  * Employees with undisclosed gender are assigned a generic **“Undisclosed”** category (kept separate from Male/Female).

---

### 🛠 Tools Used

- **Power Query**: Data cleaning, removal of duplicates, calculated columns, column transformations, currency formatting, etc. 
- **DAX Measures**: Created measures for Total Salary, Average Salary, Total Bonus Pay, Gender Pay Gap %, etc. 
- **Visualizations**: Charts, matrix tables, KPI cards, and slicers.

--- 

### 🧹 Data Preparation

**Cleaning & transformations (Power Query + DAX):**

* Filter out inactive employees (Salary is blank or 0).
* Remove rows with missing or `NULL` Department values.
* Create a **Salary Band** column in \$10k steps for distribution analysis.
* Create a **Bonus Payments and Total Amount** column for the purpose of Bonus allocation.
* Ensure **Undisclosed** gender is consistently tagged.

---

### 🔑 Key Measures (DAX)

> Representative measures used in this report:

 - `Total Employees` = COUNTROWS('Palmoria Group emp-data')
 - `Employees Male` := CALCULATE([Total Employees], 'Palmoria Group emp-data'[Gender] = "Male")
 - `Employees Female` := CALCULATE([Total Employees], 'Palmoria Group emp-data'[Gender] = "Female")
 - `Employees Undisclosed` := CALCULATE([Total Employees], 'Palmoria Group emp-data'[Gender] = "Undisclosed")

 - `Total Salary` := SUM('Palmoria Group emp-data'[Salary])
 - `Average Salary` := AVERAGE('Palmoria Group emp-data'[Salary])
 - `Avg Male Salary` := CALCULATE(AVERAGE('Palmoria Group emp-data'[Salary]),'Palmoria Group emp-data'[Gender] = "Male")
 - `Avg Female Salary` := CALCULATE(AVERAGE('Palmoria Group emp-data'[Salary]),'Palmoria Group emp-data'[Gender] = "Female")

 - `Pay Gap %` := DIVIDE([AvgMaleSal] - [AvgFemaleSal], [AvgMaleSal])

 - `Total Bonus Paid` = SUM('Palmoria Group emp-data'[Bonus Payment])
 - `Total Amount Paid` := SUM('Palmoria Group emp-data'[Salary]) + SUM('Palmoria Group emp-data'[Bonus Payment])
 - `Total Average Amount` = AVERAGE('Palmoria Group emp-data'[Salary]) + AVERAGE('Palmoria Group emp-data'[Bonus Payment])
   
 - `Employees ≥ $90k` = CALCULATE([Total Employees], 'Palmoria Group emp-data'[Salary] >= 90000) + 0
 - `Compliance % ≥ $90k` = DIVIDE([Employees ≥ $90k], [Total Employees], 0)

---

### 🎨 Visual Design

The report is a **two-page Power BI dashboard** with synced slicers and a clean, executive layout.

**Page 1 – HR Overview**

* KPIs: Total Employees (943), Male (464, 49.2%), Female (440, 46.7%), Undisclosed (39, 4.1%)
* Salary Distribution (Min: **\$28.13k**, Avg: **\$73.75k**, Max: **\$119.93k**)
* Gender distribution by **Region** and by **Department**
* Employee performance rating

**Page 2 – Compensation Analysis**

* KPIs: **Total Salary \$69.54M**, **Bonus Payments \$2.19M**, **Total Amount Paid \$71.74M**, **Avg Amount Paid \$76.07k**, **Min Wage Compliance \292 (31.0%)**
* Departmental salary structure: Avg Male vs Avg Female vs **%PayGap** with dominance flag
* Regional salary structure: (e.g., Abuja \~ \$73k vs \$70k, Kaduna \~ \$75k vs \$72k, Lagos \~ \$77k vs \$74k; PayGap ≈ 3–4%)
* Salary band charts (overall and by region)

**Screenshots**

<img width="886" height="499" alt="BI Dashboard1" src="https://github.com/user-attachments/assets/b0b6dbd1-3cfc-413c-8672-fd1326fb1aae" />
<img width="886" height="499" alt="BI Dashboard2" src="https://github.com/user-attachments/assets/cb1b7040-9f35-4202-9573-60b7e5aae042" />


---

### 🔍 Key Insights and Story

#### 1) Workforce & Gender Distribution

* Palmora employs **943** people: **49.2% male**, **46.7% female**, and **4.1% undisclosed**.
* Representation by **region** is broadly balanced, with small skews by department (e.g., Account and Legal more male dominance; Research and Service more female dominance).
* The **undisclosed** segment, while small, is non-trivial—important for compliance reporting and inclusivity messaging.

**What this means:** the company is not overwhelmingly male, but **pockets of imbalance** exist at the department level that could fuel the narrative.


#### 2) Performance Ratings by Gender

**The performance ratings** show that while the majority of employees both gender were rated **Average** 
female employees are more likely to achieve higher performance ratings **Good and Very Good**, 
whereas male employees are more concentrated in the lower performance categories **Poor” and “Very Poor**. 

**This suggests** a gender performance gap that may influence bonus distribution.

#### 3) Compensation & Gender Pay Gap

The company shows a **3.6% overall gender Pay Gap** in favor of males, with the most significant disparities in **Human Resources (9.8%), 
Business Development (9.0%), and Service (8.0%)**. While some departments **Engineering, Marketing, Training** favor females, 
the general trend across most departments and all regions is higher male earnings.

**What this means:** A measurable **pay gap exists**, varying by region/department. It is moderate but material and reputationally risky.

#### 4) Salary Banding & Regulatory Compliance

* Palmoria **does not comply** with the new **$90,000 minimum wage** regulation.
* The largest concentration of employees is in the **$70k–$80k** band (117 employees)
  and **$80k–$90k** band (108 employees) — just below the required threshold.
* Only **292 (31%)** of employees are paid **$90,000 and above**

**What this means:** **Non-compliance risk** exists—HR must uplift sub-\$90k roles or justify exemptions.

#### 5) Bonus Allocation & Total Payouts

* **Bonus pool** calculated from performance rules ≈ **\$2.19M**.
* **Total amount paid** (base + bonus) ≈ **\$71.74M**.
* Regional totals allow budget planning and equity checks.

**What this means:** The bonus framework is functioning, but to safeguard fairness, HR should stress-test the bonus framework 
ensuring ratings calibration does not reintroduce bias.

---

### ✅ Recommendations

1. **Immediate Pay Equity Audit**
   * Prioritize departments with the highest **%PayGap**.
   * Management should investigate whether these gaps are due to role distribution, seniority,
     or systemic inequities, and take corrective action to promote pay equity
   * Implement **structured salary bands** with clear progression and publish them internally.
     
2. **Minimum Salary Compliance Plan**
   * Identify all sub-\$90k roles and design a staged uplift plan with finance.
   * Track compliance monthly; add a KPI tile to the dashboard.

3. **Ratings Calibration**
   * Run cross-department calibration sessions pre-bonus to mitigate bias drift.
   * Add a **Rating by Tenure/Role** view to separate performance from role seniority.

4. **Data Hygiene & Disclosure**
   * Encourage voluntary gender disclosure (confidential) to reduce the “Undisclosed” group.

5. **Quarterly Executive Review**
   * Use the dashboard as a standing item in EXCO meetings; track the pay gap trend and compliance to \$90k.

---

### 🧑‍💻 Skills Demonstrated

* Data cleaning (Power Query), data modeling (star schema)
* DAX measures (KPIs, pay gap, compliance, bonus allocation)
* Visual storytelling & executive dashboards
* HR analytics: representation, pay equity, compensation design

---

### ⚠️ Limitations

 * **Data Quality & Completeness:** Some employees’ gender was tagged as Undisclosed, limiting the depth of gender-specific insights.
 * **Patterns, Not Proof** The analysis highlights patterns (e.g., females tend to perform better on ratings, while males earn more on average). However, these findings do not prove causal discrimination. Without additional qualitative data (e.g., role seniority, promotion, job responsibilities), it’s not possible to confirm whether pay gaps are due to bias, structural factors, or legitimate business reasons.

---

### 🧾 Conclusion

 * Palmora Group is not overwhelmingly male-dominated (49% male vs 47% female), but **gender imbalances persist at department levels,** fueling the negative `“patriarchy”` narrative.

 * Female employees show **stronger performance ratings,** yet a **pay gap of 3–4% in favor of males exists,**.

 * **Non-compliance with the $90k minimum wage** is a critical business risk, with **69% of employees** falling below the threshold.

 * Bonus distribution works in principle, but fairness depends on consistent and bias-free performance ratings.

To protect Palmora’s reputation and expansion goals, the company must act swiftly: conduct a pay equity audit, uplift salaries to meet compliance, calibrate performance ratings, and improve gender data disclosure.

---

#### Credits

* Analysis & report: **Ngbede Frank Ajo**
* Stakeholders: **Mr. Ayodeji Chukwuma (CEO)**, **Mr. Yunus Shofoluwe (CHRO)**

---


 




