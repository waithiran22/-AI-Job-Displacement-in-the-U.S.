# AI & Job Displacement in the U.S. Labor Market

<p align="center">
  <img src="banner.png" width="800">
</p>

---

![Made with R](https://img.shields.io/badge/Made%20with-R-blue?logo=r)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)


## Overview

Artificial Intelligence (AI) and automation are reshaping the future of work. This project explores how automation risk varies across U.S. occupations and states, and how **skills** can protect workers from displacement.  

---

## Table of Contents
- [Overview](#overview)
- [Scope](#scope-of-study)
- [Data Sources](#data-sources)
- [Methodology](#methodology)
- [Visualizations](#visualizations-and-results)
- [Key Insights](#key-insights)

---

## Overview

Artificial Intelligence (AI) and automation are reshaping the future of work. This project:

- Identifies which occupations are most vulnerable to automation.
- Analyzes job trends across selected U.S. states.
- Shows how skills can protect workers from displacement.
- Provides an interactive Shiny dashboard.

---


##  Scope of Study

### Occupations Analyzed:

### High-Risk (Repetitive / Blue-Collar)

*-Data Entry Keyers*: Routine, clerical → very vulnerable to AI/automation.

*-Production Workers:* Repetitive, machine-facing → high automation exposure.

*-Truck Drivers:* Routine, physical → automation risk from self-driving tech, but demand persists.

### Medium-Risk (Service-Oriented / Mixed Skill)

*-Customer Service Representatives*: — chatbots & AI assistants replace some tasks, but human interaction still valuable.

*-Construction Laborers:* Some automation risk, but variability in job sites and physical adaptability provide protection.

### Low-Risk (Analytical / White-Collar)

*Accountants & Auditors*: High cognitive/analytical demands, low risk. Jobs rely heavily on judgment, regulation, and interpretation.

---

### States Covered:

- California : As a tech hub with Silicon Valley and a diversified economy, California illustrates how automation reshapes urban, high-skill labor markets.
  
- Illinois : With Chicago’s finance and logistics sector alongside midwestern manufacturing, Illinois represents a balanced “middle ground” between high-skill and at-risk jobs.
  
- Mississippi: As a rural, less diversified economy with heavy reliance on manual labor, Mississippi highlights the heightened displacement risk from automation and limited upskilling pathways
  
---

### Timeline:

- Historical: 2017–2022
- Projected: 2022–2032

---

### Core Research Questions:

- Which jobs are most at risk of automation?
- Are risks clustered in specific regions or industries?
- How does skill intensity influence vulnerability?
- What are the projected job trends for key occupations?

---

## Data Sources

| Dataset | Source | Use |
|---------|--------|-----|
| Occupational Employment & Wage Statistics (OEWS) | BLS | Employment & wages (2017-2022) |
| Employment Projections | BLS | Forecasted demand (2022-2032) |
| Context Scores | O*NET | Automation risk estimation |
| Worker Profiles | O*NET | Skill & task importance per job |

---

### Automation Score Formula:

```r
automation_score = 1 - (context_score / 100)
```

### Risk Level Classification:

| Risk Level | Score Range | Description |
|------------|-------------|-------------|
| High Risk | ≥ 0.75 | Likely to be automated |
| Medium Risk | 0.50–0.74 | Some automation exposure |
| Low Risk | < 0.50 | Human-reliant/safe |

---

## Data Collection & Preparation
- Downloaded BLS + O*NET data (employment, wages, skills, tasks).  
- Cleaned data using `janitor` + `dplyr` (R).  
- Handled missing values with conditional pipelines.  
- Linear interpolation for midpoint projections (2027).  
- Built harmonized datasets:
  - National trends  
  - State trends  
  - Occupation profiles with risk scores  

---

### Methodology
- **Data Cleaning**: Standardized SOC codes, removed inconsistencies.  
- **Projections**: Linear midpoint for 2027 from 2022–2032 forecasts.  
- **Skill Intensity**: Average of top 3 skills per occupation.  
- **Modeling**: Logistic regression to predict high-risk jobs using:
  - Automation score  
  - Wage  
  - Projected job growth  
  - Skill intensity  
  - Location quotient  

---

### Why Clustering Was Not Finalized
>  Clustering was explored but excluded due to small sample size (6 occupations × 3 states).
 
---
## Visualizations and Results

### 1. National Employment Trends

<img src="National%20employment%20trends%20by%20occupation.PNG" width="700">
---

### 2. State Employment Trends

<img src="State%20employment%20trends%20by%20occupation.PNG" width="700">
---

### 3. Projected Job Growth by Occupation

<img src="Projected%20job%20growth%20by%20occupation.PNG" width="700">
---

### 4. Automation Risk vs. Projected Growth

<img src="Automation%20Risk%20Vs%20Projected%20Job%20Growth.PNG" width="700">
---

### 5. Top Skills by Occupation

<img src="Top%20Skill%20Importance%20by%20Occupation.PNG" width="700">
---

### 6. Top Work Activities by Occupation

<img src="Top%20work%20activities%20by%20occupation.PNG" width="700">
---

### 7. Skill Intensity vs. Automation Risk

<img src="Skill%20Intensity%20vs%20Automation%20Risk.PNG" width="700">
---

## Key Insights

### By Occupation

- **Data Entry Keyers** → Highest automation risk (~0.90), projected decline >25% by 2027.  
- **Truck Drivers** → High automation risk, but demand growth offsets displacement.  
- **Accountants** → Low risk, stable growth due to analytical skill demand.  
- **Production Workers** → High risk, moderate decline in employment.  
---

### By State

- **California** → Highest employment levels, more resilient due to industry diversity.  
- **Illinois** → Balanced risk distribution, reskilling opportunities in urban hubs.  
- **Mississippi** → Lowest employment levels, most concentrated in high-risk jobs.  

---

### Skill Intensity

- Higher skill intensity = significantly lower automation risk.  
- Cognitive & human-centric skills (critical thinking, communication) = best protection.

---
## Limitations

- Aggregated government datasets (BLS, O*NET) update annually.  
- Narrow focus (6 occupations, 3 states).  
- Linear projections may not capture disruptive shocks.  
- O*NET skill ratings may lag behind emerging trends.  


## Tools Used

- **R** → Core analysis  
- **ggplot2** → Visualizations  
- **plotly** → Interactive plots  
- **usmap** → Choropleth mapping  
- **shiny** → Dashboard  
- **janitor, dplyr, stringr** → Cleaning & wrangling

---
