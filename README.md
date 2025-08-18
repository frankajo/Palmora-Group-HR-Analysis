# Palmora-Group-HR-Analysis
Welcome to my first Power BI project — **Palmora Group HR Analysis.** In this project, I apply data analysis techniques to HR datasets to highlight potential issues of gender inequality and provide insights for decision-making.

---

## 📌 Introduction
“Palmoria Group, a major player in the Nigerian manufacturing industry, recently came under fire for alleged gender inequality practices. Headlines like *`the Manufacturing Patriarchy.`* threatened not just its image, but also its expansion plans into new regions and global markets. To prevent further damage, the CEO tasked the CHRO to identify the root causes. That’s where I came in: to uncover the truth hidden in Palmoria’s HR data and guide management on the path forward.”

This repository documents the analysis, visuals, and decisions derived from the data. It is written as a narrative that takes management from 
**problem → evidence → insight → action**.

---

## Table of Contents

* [Business Context](#business-context)
* [Case Scenario & Questions](#case-scenario--questions)
* [Data & Assumptions](#data--assumptions)
* [Data Preparation](#data-preparation)
* [Data Model](#data-model)
* [Key Measures (DAX)](#key-measures-dax)
* [Visual Design](#visual-design)
* [Insights & Story](#insights--story)

  * [1) Workforce & Gender Distribution](#1-workforce--gender-distribution)
  * [2) Performance Ratings by Gender](#2-performance-ratings-by-gender)
  * [3) Compensation & Gender Pay Gap](#3-compensation--gender-pay-gap)
  * [4) Salary Banding & Regulatory Compliance](#4-salary-banding--regulatory-compliance)
  * [5) Bonus Allocation & Total Payouts](#5-bonus-allocation--total-payouts)
* [Recommendations](#recommendations)
* [How to Use the Report](#how-to-use-the-report)
* [Repository Structure](#repository-structure)
* [Skills Demonstrated](#skills-demonstrated)
* [Future Enhancements](#future-enhancements)

---

## Business Context

A recent headline labeled Palmora *“the Manufacturing Patriarchy.”* Leadership wants clarity on:

1. the **true state of gender representation**, 
2) whether a **gender pay gap** exists and where, and 
3) what **corrective actions** will deliver the most impact fastest.

**Mandate:**

* Focus on gender-related issues at the **organization, region, and department** levels.
* Use accessible visuals to drive discussion and decisions with executives.

---

## 🎯 Case Scenario & Questions

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

## 📊 Data & Assumptions

* Palmora Group emp-dataset (demographics, department, region, base salary, performance rating)
* Bonus rules dataset (mapping performance rating to % bonus)
* **Assumptions / Requirements applied:**

  * Employees with **no salary** are considered **inactive** and removed from analysis.
  * Rows with **Department = NULL** are excluded.
  * Employees with undisclosed gender are assigned a generic **“Undisclosed”** category (kept separate from Male/Female).

---

