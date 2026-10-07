# HR Analytics Dashboard \| Tableau

## 📊 Project Overview

The **HR Analytics Dashboard** is an interactive Tableau project
designed to provide a comprehensive view of an organization's workforce
and support data-driven Human Resources (HR) decision-making.

The main objective of this project was to bring key HR metrics into a
**single interactive dashboard** and analyze employee demographics,
hiring and termination trends, departmental structure, education,
performance, location, age, and salary.

The dashboard helps HR teams and management quickly understand the
current workforce structure, identify trends, compare employee groups,
and detect potential HR issues that may require further investigation.

------------------------------------------------------------------------

## 🎯 Project Objectives

The project was developed to answer the following HR-related questions:

-   How many employees have been hired, terminated, and remain active?
-   How have hiring and termination levels changed over time?
-   Which departments have the largest number of employees?
-   How are employees distributed between headquarters and branches?
-   Where are employees geographically located?
-   What is the gender composition of the workforce?
-   How are employees distributed across different age groups?
-   What education levels are most common among employees?
-   Is there a relationship between education level and performance?
-   How do salaries differ by education level and gender?
-   How does employee age relate to salary across different job
    positions?

------------------------------------------------------------------------

## 🛠️ Tools & Technologies

-   **Tableau Calculated Fields** -- KPI calculations, employee
    classification, age groups, location categories, and percentage
    calculations
-   **Line Chart** -- hiring and termination trends over time
-   **Area Chart** -- visual emphasis of workforce movement over time
-   **Bar Chart** -- department, location, and education comparisons
-   **Pie / Donut Chart** -- gender distribution
-   **Heat Map** -- age/education distribution and education/performance
    analysis
-   **Barbell Chart** -- salary comparison by education and gender
-   **Scatter Plot** -- age and salary relationship by job position
-   **Dashboard Containers** -- structured and organized dashboard
    layout

------------------------------------------------------------------------

# 🔎 Key Insights

Based on the dashboard, several important HR observations can be made.

### 1. The organization has a large active workforce

The dashboard reports approximately:

-   **7,984 Active Employees**
-   **8,950 Hired Employees**
-   **966 Terminated Employees**

The active employee KPI provides management with an immediate overview
of the current workforce size.

### 2. Hiring activity is considerably higher than termination activity

The number of employees classified as hired is substantially higher than
the number classified as terminated. This indicates that the
organization has experienced significant workforce recruitment activity
relative to the recorded terminations.

However, these metrics should be interpreted according to the dataset's
definitions and time period rather than being treated as a direct
employee turnover rate.

### 3. The workforce is concentrated in several major departments

The department visualization shows that some departments have
considerably larger employee populations than others.

This can help HR teams evaluate:

-   Workforce allocation
-   Recruitment demand
-   Departmental capacity
-   Potential staffing shortages or concentration

### 4. The workforce is geographically distributed

The map demonstrates that employees are distributed across multiple
cities and states, while the HQ/Branch analysis separates New York as
the headquarters from the remaining branch locations.

This can support location-based workforce planning and resource
allocation.

### 5. The workforce is slightly male-dominated

The gender visualization shows an approximately **54% male and 46%
female** workforce distribution.

Although the difference is not extremely large, the gender composition
can be useful for monitoring workforce diversity and supporting future
HR initiatives.

### 6. Bachelor's degree holders form the largest education group

The education analysis shows that employees with a **Bachelor's degree**
make up the largest education category.

This indicates that bachelor's-level education is the most common
educational background within the organization.

### 7. Age 25--44 represents an important part of the workforce

The age analysis shows a strong concentration of employees in the
**25--34 and 35--44** age ranges.

This suggests that the organization has a relatively strong working-age
and mid-career workforce, which may be important for succession
planning, career development, and retention strategies.

### 8. Education and performance show a noticeable pattern

The education vs. performance heat map suggests that employees with
higher education levels have a larger share of **Good and Excellent**
performance ratings.

At the same time, the visualization should be interpreted as a
correlation/pattern in the dataset, not as evidence that education alone
determines employee performance.

### 9. Salary differences exist across education levels and gender

The salary analysis indicates that compensation varies across education
groups and between genders.

Higher education levels generally correspond to higher salary ranges,
while the Barbell Chart makes gender-based differences within education
categories easier to identify.

This can be useful for HR teams when investigating compensation equity
and salary structures.

### 10. Senior roles are associated with higher salaries

The Age vs. Salary scatter plot shows that senior managerial roles
generally appear at higher salary levels than assistant, coordinator,
and specialist positions.

Therefore, employee age alone does not explain salary differences. **Job
title, responsibility, and seniority are important factors.**

------------------------------------------------------------------------

## 🧹 Data Preparation

The dataset was first loaded into Tableau and the available fields and
data types were checked before starting the analysis.

I then created several **Calculated Fields** to generate the main HR
KPIs and analytical dimensions used throughout the dashboard.

### Total Hired

``` text
COUNT([Employee_ID])
```

This measure represents the total number of employee records/hired
employees in the dataset.

### Total Terminated

``` text
COUNT(
    IF NOT ISNULL([Termdate])
    THEN [Employee_ID]
    END
)
```

This calculation counts employees who have a termination date.

### Total Active

``` text
COUNT(
    IF ISNULL([Termdate])
    THEN [Employee_ID]
    END
)
```

This calculation identifies employees whose termination date is missing
and therefore treats them as currently active.

### Employee Status Logic

The basic classification used in the dashboard is:

``` text
If Termination Date is NULL → Active
If Termination Date exists → Terminated
```

These calculated measures were then used as the main KPI indicators.

------------------------------------------------------------------------

## 📈 Analysis & Visualizations

### 1. Hiring and Termination Trends

I analyzed the number of hired and terminated employees over time.

For hiring, I used:

-   **Columns:** Hire Date
-   **Rows:** Total Hired
-   **Visualization:** Line + Area Chart

I duplicated the visualization and applied the same approach to
termination data using **Term Date** and **Total Terminated**.

Combining the line and area charts makes changes in workforce movement
easier to recognize visually.

### 2. Department and Job Distribution

I analyzed the number of employees across departments and job positions
using bar charts.

This allows HR management to identify:

-   The largest departments
-   Departments with relatively small workforces
-   The organizational distribution of employees
-   Areas where workforce planning may be required

### 3. Headquarters vs. Branches

To compare employees working at headquarters and branches, I created a
calculated field:

``` text
CASE [State]
    WHEN 'New York' THEN 'HQ'
    ELSE 'Branch'
END
```

New York was classified as the **Headquarters (HQ)**, while the
remaining locations were classified as **Branches**.

This comparison provides a high-level view of workforce distribution
between the main office and other locations.

### 4. Geographic Distribution

I visualized employees by **city and state** using a map.

This helps identify the geographical concentration of the workforce and
provides a clear view of where the organization's employees are located.

### 5. Gender Distribution

A donut/pie chart was created to analyze the gender composition of
employees.

I also created the following calculated field:

``` text
[Total Hired] / TOTAL([Total Hired])
```

This was used to calculate the percentage contribution of each gender to
the total workforce.

### 6. Age Group Analysis

Employee age was calculated using:

``` text
DATEDIFF('Year', [Birthdate], TODAY())
```

I then created age groups:

``` text
IF [Age] < 25 THEN '<25'

ELSEIF [Age] >= 25 AND [Age] < 35 THEN '25-34'

ELSEIF [Age] >= 35 AND [Age] < 45 THEN '35-44'

ELSEIF [Age] >= 45 AND [Age] < 55 THEN '45-54'

ELSEIF [Age] >= 55 THEN '55+'
END
```

The resulting age groups were compared with employee counts and
education levels using heat-map and bar-chart visualizations.

### 7. Education Level

I analyzed the number of employees within each education category.

The dashboard shows that **Bachelor's degree holders represent a
particularly large part of the workforce**, while Master's, High School,
and PhD groups form smaller portions.

This provides useful context for understanding the educational structure
of the organization.

### 8. Education vs. Performance

A heat map was used to investigate the relationship between **education
level and employee performance rating**.

The dashboard indicates that performance is not distributed equally
across education groups. For example, the higher education categories
show a stronger representation of **Excellent** and **Good** performance
ratings, while the High School group has a comparatively larger share of
**Satisfactory** and **Needs Improvement** ratings.

This should be treated as an observed pattern rather than proof that
education directly causes better performance.

### 9. Salary by Education and Gender

A **Barbell Chart** was used to compare salaries across education levels
for both genders.

This visualization makes it easier to identify:

-   Salary differences between genders
-   Salary progression across education levels
-   Education groups with larger salary gaps
-   General salary patterns within the workforce

The dashboard suggests that salary levels generally increase with higher
education, while differences between male and female salary levels can
also be observed.

### 10. Age vs. Salary

A scatter plot was created to investigate the relationship between
employee age and salary across job positions.

The analysis shows that salary is influenced not only by age but also by
**job role and seniority**. Higher-level managerial positions tend to
appear at higher salary levels, while assistant and coordinator
positions are concentrated at lower salary ranges.

This indicates that job position is an important factor when
interpreting the relationship between age and salary.

------------------------------------------------------------------------

# 🧩 Dashboard Design

After completing the individual visualizations, I created the final
Tableau dashboard using **Dashboard Containers**.

The dashboard was structured into several logical sections:

-   **Overview** -- workforce KPIs and hiring/termination trends
-   **Demographics** -- gender, age, education, and performance
-   **Income** -- salary comparisons and age/salary analysis
-   **Departments & Location** -- organizational and geographical
    distribution

The dashboard was designed so that HR managers can move from a
high-level overview to more detailed demographic, organizational, and
compensation analysis.
