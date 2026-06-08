# A/B Testing Recommendation System Analysis

## Project Overview

This project evaluates the effectiveness of a new recommendation system through an A/B test conducted on users from the European Union (EU) region.

The objective was to determine whether the new recommendation system improved user engagement and purchase conversion rates compared to the existing recommendation experience.

The analysis includes data preparation, exploratory data analysis (EDA), funnel performance evaluation, statistical hypothesis testing, and business recommendations.

---

## Business Problem

An e-commerce company introduced a new recommendation system intended to increase user engagement and improve conversion performance across the purchase funnel.

To measure its impact, an A/B test was conducted where:

* **Group A** represented the existing recommendation system (control group)
* **Group B** represented the new recommendation system (treatment group)

The goal was to determine whether the new recommendation system generated a meaningful improvement in conversion behavior.

---

## Dataset Overview

The analysis was performed using four datasets:

| Dataset                 | Description                                             |
| ----------------------- | ------------------------------------------------------- |
| Marketing Events        | Marketing campaigns active during the experiment period |
| New Users               | User registration information                           |
| User Events             | User interactions and purchase activity                 |
| Experiment Participants | Experimental group assignments                          |

### Final Analytical Sample

* **3,481 users analyzed**
* **21,952 filtered event records**
* **EU region users only**
* **First 14 days after registration**

---

## Analysis Process

* Cleaned and validated experiment datasets
* Filtered users according to experiment requirements
* Verified experiment integrity and group assignments
* Evaluated user activity and engagement patterns
* Analyzed conversion funnel performance
* Calculated conversion rates by experimental group
* Visualized funnel performance and event activity trends
* Conducted a two-proportion Z-test to evaluate statistical significance
* Generated business recommendations based on experiment results

---

## Key Findings

### Conversion Rates

| Funnel Stage | Group A | Group B |
| ------------ | ------- | ------- |
| Product Page | 64.71%  | 56.28%  |
| Product Cart | 30.03%  | 27.85%  |
| Purchase     | 31.99%  | 28.42%  |

### User Engagement

| Metric                  | Group A | Group B |
| ----------------------- | ------- | ------- |
| Average Events per User | 6.62    | 5.38    |

### Experiment Validation

* No duplicate records identified
* No users assigned to multiple groups
* Consistent activity observed throughout the experiment period

---

## Visualizations

### Conversion Rates by Funnel Stage

![Conversion Rates](images/conversion_rates.png)

### Daily Event Volume by Experimental Group

![Daily Event Volume](images/daily_event_volume.png)

---

## Statistical Results

A two-proportion Z-test was performed to compare purchase conversion rates between the experimental groups.

### Results

* **Group A Purchase Conversion:** 31.99%
* **Group B Purchase Conversion:** 28.42%
* **Z-statistic:** -1.9717
* **P-value:** 0.0486
* **Significance Level (α):** 0.05

Since the p-value is below the significance threshold, the null hypothesis was rejected.

The analysis indicates a statistically significant difference between the two groups. However, the difference favors the control group rather than the treatment group.

---

## Business Recommendations

1. Maintain the existing recommendation system rather than deploying the tested version.
2. Investigate potential causes of reduced engagement within the treatment group.
3. Analyze user behavior throughout the purchase funnel to identify friction points.
4. Conduct follow-up experiments using alternative recommendation strategies.
5. Continue monitoring conversion performance after future recommendation updates.

---

## Project Files

* **Notebook:** `AB_Testing_Recommendation_System.ipynb`
* **Datasets:** `/datasets`
* **Visualizations:** `/images`
