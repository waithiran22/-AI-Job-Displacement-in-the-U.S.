# AI & Job Displacement in the U.S. Labor Market

This project explores how artificial intelligence and automation are transforming the U.S. labor market. It identifies which jobs and regions are most vulnerable, examines skill-based protections, and provides data-driven visualizations and insights.

---

## Table of Contents

- [Overview](#overview)
- [Scope of Study](#scope-of-study)
- [Data Sources](#data-sources)
- [Data Collection & Preparation](#data-collection--preparation)
- [Methodology](#methodology)
- [Visualizations and Results](#visualizations-and-results)
- [Key Insights](#key-insights)
  - [By Occupation](#by-occupation)
  - [By State](#by-state)
  - [Skill Intensity](#skill-intensity)
- [Limitations](#limitations)
- [Tools Used](#tools-used)
- [Contact and Contributions](#contact-and-contributions)

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

- Accountants & Auditors
- Customer Service Representatives
- Data Entry Keyers
- Construction Laborers
- Production Workers
- Truck Drivers

### States Covered:

- California
- Illinois
- Mississippi

### Timeline:

- Historical: 2017–2022
- Projected: 2022–2032

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

- Data for this project was sourced through the **U.S. Bureau of Labor Statistics (BLS) and O*NET databases.** 

- The OEWS national and state-level Excel files were manually downloaded and imported using the readxl package.
   
- For historical analysis, national-level employment data from 2017 to 2022 was compiled and cleaned using janitor and dplyr. Employment projections (2022–2032) were added manually via **structured interpolation to estimate 2027 midpoint values, which helped us identify short-term risk without overrelying on full-decade estimates.**
  
- **Context Scores** were extracted from O*NET's database and ** used to generate an automation risk metric.** These values were **joined with occupational codes** (SOC codes) after trimming inconsistencies in formatting using stringr.

- **Worker Profile data** was scraped and **compiled from O*NET's value importance ratings and activity ratings.**

- **Skill intensity scores** were averaged across multiple traits (e.g., critical thinking, active listening, complex problem-solving) to construct a composite skill index.

- State-level location quotient and employment data were processed for three specific states—California, Illinois, and Mississippi—to compare employment dynamics across urban, semi-industrial, and rural settings. Missing data was handled using conditional pipelines and fallback strategies to ensure smooth joins.

- This preprocessing pipeline resulted in three harmonized datasets: **national trends, state trends, and occupational profiles with risk scores.**

---

## Methodology

### Data Cleaning:

- Standardized column names using janitor::clean_names().
- Converted all relevant numeric fields, removed commas from number strings, and aligned occupation codes.

### Projections:

- Calculated 2027 estimates using linear interpolation:

```r
projected_2027 = emp_2022 + ((emp_2032 - emp_2022) * 0.5)
```
---
### Skill Intensity Score

Each job’s average skill score was derived by taking the mean of the top 3 rated skills from O*NET:

```r
skill_avg = mean(c(value_1, value_2, value_3), na.rm = TRUE)
```
---
### Logistic Regression Modeling

To predict whether a job is at high risk of automation, a logistic regression model was built with the following specifications:

- **Response Variable**:  
  - `risk_binary`: 1 = High Risk (automation_score ≥ 0.75), 0 = Otherwise  

- **Predictor Variables**:  
  - `automation_score` (normalized from O*NET context score)  
  - `a_mean` (average annual wage from OEWS data)  
  - `projected_change_pct` (job growth estimate from 2022–2032, interpolated for 2027)  
  - `skill_avg` (mean of top skill ratings per occupation)  
  - `loc_quotient` (state location quotient where available)  

The model was evaluated for accuracy and interpretability. Although it performed reasonably, feature correlation and dataset size limited deeper modeling.

---

### Why Clustering Was Not Finalized

Originally, Ward’s hierarchical clustering was implemented to group occupations by risk and skill intensity. However, clustering was ultimately not included in the final report due to:

- **Small dataset**: Only six occupations across three states, which leads to unstable clusters  
- **High within-group variance**: Occupations vary too widely in their skill and wage profiles  
- **Dimensional limitations**: With few features and entities, clustering results were misleading and not generalizable  

That said, clustering remains a valid future direction if more occupations and broader dimensions are included (e.g., tech exposure, job task decomposition).

---
## Visualizations and Results

### 1. National Employment Trends

![National Employment Trends](https://github.com/waithiran22/ai-job-displacement/blob/main/Visualizations/National%20employment%20trends%20by%20occupation.png?raw=true)

- Customer Service jobs show a slight national decline after 2020.  
- Accountants remain relatively stable across all years.  

---

### 2. State Employment Trends

![State Employment Trends](https://github.com/waithiran22/ai-job-displacement/blob/main/Visualizations/State%20employment%20trends%20by%20occupation.png?raw=true)

- California consistently reports higher employment numbers across occupations.  
- Mississippi shows the lowest employment volume, especially in high-risk jobs.  

---

### 3. Projected Job Growth by Occupation

![Projected Job Growth](https://github.com/waithiran22/ai-job-displacement/blob/main/Visualizations/Projected%20job%20growth%20by%20occupation.png?raw=true)

- Construction Laborers and Truck Drivers are projected to grow.  
- Data Entry jobs are projected to decline sharply due to automation.  

---

### 4. Automation Risk vs. Projected Growth

![Automation vs Growth](https://github.com/waithiran22/ai-job-displacement/blob/main/Visualizations/Automation%20Risk%20Vs%20Projected%20Job%20Growth.png?raw=true)

- High automation risk correlates with negative job growth (e.g., Data Entry).  
- Occupations like Accountants show low automation risk and positive growth.  

---

### 5. Top Skills by Occupation

![Top Skills](https://github.com/waithiran22/ai-job-displacement/blob/main/Visualizations/Top%20Skill%20Importance%20by%20Occupation.png?raw=true)

- Critical Thinking and Active Listening are top-rated across most occupations.  
- These skills are strongly associated with lower automation exposure.  

---

### 6. Top Work Activities by Occupation

![Top Activities](https://github.com/waithiran22/ai-job-displacement/blob/main/Visualizations/Top%20work%20activities%20by%20occupation.png?raw=true)

- Manual tasks like Documenting/Recording Information dominate at-risk jobs.  
- Cognitive and procedural tasks appear more in safer roles.  

---

### 7. Skill Intensity vs. Automation Risk

![Skill vs Risk](https://github.com/waithiran22/ai-job-displacement/blob/main/Visualizations/Skill%20Intensity%20vs%20Automation%20Risk.png?raw=true)

- Clear inverse relationship: higher skill intensity = lower automation risk.  
- Jobs that emphasize human-centric skills are significantly safer.  
---

## Key Insights

### By Occupation

- **Data Entry Keyers**
  - Highest automation risk score (~0.90+).
  - Sharp employment decline nationally.
  - Projected to shrink by over 25% by 2027.
  - Low skill intensity and heavy task repetition.

- **Truck Drivers**
  - High automation risk due to routine, physical tasks.
  - Yet projected to grow due to sustained demand in delivery/logistics.
  - Skill intensity moderate, but growth driven by labor shortages.

- **Customer Service Representatives**
  - Medium automation risk.
  - Modest employment decline post-2020.
  - Skills like active listening and service orientation reduce displacement risk.

- **Accountants & Auditors**
  - Low automation risk due to analytical and cognitive skill demands.
  - Employment remains stable or slightly growing.
  - High skill intensity—critical thinking, attention to detail, communication.

- **Production Workers**
  - Among the highest automation risk groups.
  - Moderate decline in employment from 2017–2022.
  - Tasks like equipment monitoring and object handling are highly automatable.

- **Construction Laborers**
  - Medium risk.
  - Strong projected growth due to sustained infrastructure needs.
  - Blend of physical/manual tasks with some variability protects against full automation.

---

### By State

- **California**
  - Highest employment levels across nearly all occupations.
  - More diverse industry mix contributes to greater job resilience.
  - Urban tech ecosystems (e.g., Bay Area) may accelerate or offset automation risk depending on sector.

- **Illinois**
  - Stable employment in most roles.
  - Balanced mix of high- and medium-risk jobs.
  - Urban centers like Chicago offer greater reskilling opportunities.

- **Mississippi**
  - Lowest employment levels.
  - Highest concentration of high-risk jobs (Production, Data Entry).
  - Fewer skill-building and transition pathways, increasing displacement vulnerability.

---

### Skill Intensity

- Occupations with higher skill intensity (e.g., speaking, critical thinking, problem-solving) show significantly lower automation risk.
- Jobs requiring routine, repetitive tasks—especially with low education or tech exposure—are the most automatable.
- Skill-focused interventions (upskilling, internal mobility) are crucial to mitigate displacement.

---
## Limitations

- **Public Data Granularity**: Government datasets (e.g., BLS, O*NET) aggregate occupations and update annually, limiting real-time analysis or task-level automation insights.

- **Sample Scope by Design**: A narrow focus on 6 key occupations and 3 representative states was chosen to prioritize interpretability and clarity over breadth.

- **Clustering Exclusion**: Clustering was initially explored but excluded due to low sample size and high dimensional variance. Including it would have risked misleading interpretations without more data.

- **Linear Projections**: Job growth estimates for 2027 were interpolated from 2022 and 2032 values due to limited projection intervals from the BLS. This assumes linear job trends which may not fully reflect industry disruptions.

- **Skill Ratings May Lag**: O*NET skill importance scores are based on periodic surveys and expert input, which may not fully capture fast-changing job requirements due to AI or tech adoption.

- **API Access Limits**: Real-time job market APIs (e.g., Indeed, LinkedIn) were considered but not used due to access restrictions and rate limits that would have required institutional credentials or paid tiers.

- **No Macroeconomic Controls**: The analysis does not include broader economic shocks (e.g., recessions, COVID-19 recovery), which may affect employment trends beyond automation.
---

## Tools Used

| Tool           | Purpose                      |
|----------------|------------------------------|
| **R**          | Core scripting environment   |
| **ggplot2**    | Data visualizations (static) |
| **plotly**     | Interactive plots            |
| **usmap**      | U.S. choropleth mapping      |
| **shiny**      | Web-based dashboard          |
| **janitor**    | Data cleaning                |
| **dplyr**      | Data wrangling               |
| **readxl**     | Excel file import            |
| **stringr**    | Text and code formatting     |
| **shinythemes**| Themed UI elements           |

---

### Contact and Contributions

- This project was created by **Waithira Ng’ang’a**  
- B.A. in Business Analytics and Marketing, Augustana College
- Feel free to fork the repository, open issues, or submit pull requests for improvements or extensions.
