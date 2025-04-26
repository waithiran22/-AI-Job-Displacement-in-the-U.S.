# 🤖 AI & Job Displacement in the U.S. Labor Market

This project explores how artificial intelligence and automation are transforming the U.S. labor market. It identifies which jobs and regions are most vulnerable, examines skill-based protections, and provides data-driven visualizations and insights.

---

## 📁 Table of Contents

- 📘 [Introduction](#-introduction)  
- 🔎 [Scope of Study](#-scope-of-study)  
- 🧪 [Methods Overview](#-methods-overview)  
- 🧼 [Data Cleaning](#-data-cleaning)  
- 🔍 [Exploratory Data Analysis (EDA)](#-exploratory-data-analysis-eda)  
- 📊 [Visualizations](#-visualizations)  
- 📦 [Clustering & Modeling](#-clustering--modeling)  
- 📈 [Summary & Insights](#-summary--insights)

---

## 📘 Introduction

AI and automation are reshaping the future of work. This project:

- Identifies occupations most vulnerable to automation  
- Analyzes national and state-level employment trends  
- Highlights skill intensity as a protective factor  
- Builds an interactive dashboard for exploration

---

## 🔎 Scope of Study

### Occupations Analyzed

- 13-2011: Accountants & Auditors  
- 43-4051: Customer Service Representatives  
- 43-9021: Data Entry Keyers  
- 47-2061: Construction Laborers  
- 51-9198: Production Workers  
- 53-3032: Truck Drivers

### States Covered

- California  
- Illinois  
- Mississippi

### Timeline

- Historical: 2017–2022  
- Projected: 2022–2032

### Research Questions

- Which jobs are most at risk of being automated?  
- What regions are most exposed?  
- What skills help protect jobs from automation?  
- Are AI-related job losses clustered by industry?

---

## 🧪 Methods Overview

### Datasets Used

- **BLS OEWS (2017–2022):** Employment & wage data  
- **BLS Projections (2022–2032):** Forecasted employment  
- **O*NET Context Scores:** Automation risk probabilities  
- **Worker Profiles:** Top skills & tasks per job

### Automation Score Formula

A normalized score between 0 and 1 derived from O*NET context scores:

`automation_score = 1 - (context_score / 100)`

### Risk Level Classification

| Risk Level    | Score Range | Description                |
|---------------|-------------|----------------------------|
| High Risk     | ≥ 0.75      | Likely to be automated     |
| Medium Risk   | 0.50–0.74   | Some automation exposure   |
| Low Risk      | < 0.50      | Human-reliant/safe         |

---

## 🧼 Data Cleaning

### Cleaning Process

- Standardized occupation codes and column names  
- Filtered for selected occupations and states  
- Merged automation, employment, wage, and projection data  
- Calculated 2027 job projections by interpolating 2022–2032 values  

---

## 🔍 Exploratory Data Analysis (EDA)

### National Trends

- **Data Entry:** sharp decline in employment  
- **Truck Drivers & Customer Service:** stable overall  
- **Accountants:** modest growth, low automation risk  

### State-Level Trends

- **California:** highest employment levels across sectors  
- **Illinois:** steady employment with some volatility  
- **Mississippi:** lower job counts, higher automation risk concentration  

### Skill Intensity Patterns

- Higher average skill = lower automation risk  
- Low-risk jobs emphasize:  
  - Speaking  
  - Reading Comprehension  
  - Critical Thinking  
- High-risk jobs rely on repetitive/manual tasks  

---

## 📊 Visualizations

### 1. Automation Risk Score by Occupation

![Automation Risk Score by Occupation](./Automation%20Risk%20Score%20by%20Occupation.png)    
This chart shows how likely each job is to be automated (0 = low, 1 = high).  
- Construction Laborers, Data Entry Keyers, and Truck Drivers face the highest risk.  
- Accountants have the lowest automation risk.  
- Jobs are color-coded by risk category: High (red), Medium (blue), Low (green).

---

### 2. Automation Risk vs. Projected Job Growth

![Automation Risk vs. Projected Job Growth](./Automation%20Risk%20vs.%20Projected%20Job%20Growth.png) 
This scatter plot compares automation risk with projected job growth by state.  
- Truck Drivers and Construction Laborers are high risk but still growing.  
- Data Entry Keyers show both high risk and declining growth.  
- Accountants and CSRs are low-to-medium risk and show stable projections.

---

### 3. Average Employment by State (2019–2022)

![Average Employment by State](./Average%20Employment%20by%20State%20(2019-2022).png)  
This U.S. map shows average employment in California, Illinois, and Mississippi.  
- California has the highest average employment.  
- Mississippi has the lowest, reflecting a smaller labor force.  
- Darker shades = higher average employment.

---

### 4. Employment Trends by State & Occupation (2019–2022)

![Employment Trends by State & Occupation](./Employment%20Trends%20by%20State%20&%20Occupation%20(2019-2022).png)  
Each panel tracks job trends for one occupation across the three states.  
- Truck Drivers and Construction Laborers are rising.  
- Data Entry and Production Workers are declining — possible automation effects.  
- Accountants and CSRs remain steady.

---

### 5. National Employment Trends by Occupation

![National Employment Trends by Occupation](./National%20Employment%20Trends%20by%20Occupation.png)
This chart shows national job trends over time (2017–2022).  
- Customer Service Reps have the largest employment overall.  
- Data Entry and Production jobs show consistent decline.  
- Accountants and Truck Drivers are growing steadily.

---

### 6. Top Skill Importance by Occupation

![Top Skill Importance by Occupation](./Top%20Skill%20Importance%20by%20Occupation.png)   
Displays the most important skill for each occupation.  
- Reading Comprehension dominates across most jobs.  
- Speaking is critical for manual labor roles.  
- Operations Monitoring is key for Truck Drivers.  
- Highlights how soft/cognitive skills help protect against automation.

---

### 7. Top Work Activity by Occupation

![Top Work Activity by Occupation](./Top%20Work%20Activity%20by%20Occupation.png)   
Shows the top daily task for each job type.  
- Manual labor = “Handling and Moving Objects”  
- Office jobs = “Entering/Recording Information”  
- Truck Drivers = “Operating Vehicles”  
- Repetitive/manual tasks correlate with higher automation risk.


---

## 📦 Clustering & Modeling

### Goal

Group occupations based on automation risk and skill intensity to identify similar jobs and highlight career mobility/reskilling opportunities.

### Method

- Used Ward's method for hierarchical clustering  
- Inputs: automation score + average skill intensity  
- Output: clusters of similar job types based on vulnerability and required skill levels

---

## 📈 Summary & Insights

### By Occupation

- **Data Entry Keyers:** High risk, sharp employment decline  
- **Truck Drivers:** High risk, but projected to grow  
- **Customer Service Reps:** Medium risk, stable trends  
- **Accountants:** Low risk, slow but steady growth  
- **Production Workers:** High risk, slight decline  
- **Construction Laborers:** Medium risk, strong growth across states
  
---
### By State

#### California

- Strong employment across occupations  
- More resilient due to industry diversity  

#### Illinois

- Moderate risk mix  
- Some decline in production-related roles  

#### Mississippi

- Most exposed to automation  
- Lower employment, more high-risk, low-skill jobs
   
---
### Key Takeaways

- High-risk jobs are not always declining (e.g., Truck Drivers)  
- Communication and cognitive skills significantly reduce automation risk  
- Rural, low-income states are more vulnerable to displacement  
- Skill intensity is a strong protective factor

---

## ⚠️ Limitations  
- Assumes current pace of AI adoption continues linearly  
- Real-time job posting APIs (e.g., LinkedIn, Indeed) not integrated  
- Skill scores based on O*NET ratings, which may lag behind rapid tech changes  

---

## 🛠️ Tools Used

| Tool        | Purpose                        |
|-------------|--------------------------------|
| **R**       | Core programming environment   |
| **ggplot2** | Static visualizations          |
| **usmap**   | State-level choropleth maps    |
| **dplyr**   | Data wrangling & filtering     |
| **readxl**  | Import Excel datasets          |
| **janitor** | Clean column names             |
| **plotly**  | Interactive plots (future use) |
| **shiny**   | Web dashboard (in progress)    |

---

## 📊 Shiny Dashboard

An interactive dashboard is in development that will allow users to:

- Explore automation risk by occupation, state, or skill level  
- Filter job trends and skill gaps by region  
- View automation vulnerability and projected job growth  
- Interact with charts and maps in real-time

**Coming soon to this repository!**

