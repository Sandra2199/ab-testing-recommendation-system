# Recommendation System A/B Test Analysis

Evaluation of an e-commerce recommendation experiment using conversion funnels and statistical testing, with experiment-design limitations made explicit.

## Quick Access

- [Analysis notebook](AB_Testing_Recommendation_System.ipynb)
- [Experiment datasets](datasets/)
- [Conversion-rate visualization](images/conversion_rates.png)
- [Daily event-volume visualization](images/daily_event_volume.png)

## Executive Summary

This project evaluates an A/B experiment comparing an existing e-commerce experience (Group A) with a new recommendation system (Group B). The analysis follows EU users through product-page, cart, and purchase events during their first 14 days after registration.

The final filtered data contains **3,481 users** and **21,952 event records**. Group A had 2,604 users, while Group B had 877. Observed purchase conversion among login users was **31.99% for A** and **28.42% for B**, a difference of **−3.57 percentage points** for the treatment group.

A two-sided, two-proportion z-test returned **p = 0.0486**, but substantial design limitations prevent treating that result as clean causal evidence. In particular, 887 target-test participants also appeared in another experiment, group allocation was highly uneven, and many late registrants could not contribute a complete 14-day observation window. The evidence does not support rollout of the tested experience, but a clean follow-up experiment is needed before concluding that the recommendation system caused the lower conversion.

## Business Problem

An online retailer wanted to determine whether a new recommendation experience improved progression through the purchase journey.

The analysis addresses:

- Did treatment users reach product, cart, and purchase events at higher rates?
- Was the observed purchase-conversion difference statistically distinguishable from zero?
- Was the experiment implemented cleanly enough to support a product decision?

## Experiment and Analytical Scope

| Element | Definition used in the analysis |
|---|---|
| Control | Group A — existing experience |
| Treatment | Group B — new recommendation system |
| Target experiment | `recommender_system_test` |
| Target population | New EU users |
| Enrollment period | December 7–21, 2020 |
| Intended observation window | First 14 days after registration |
| Funnel events | `login`, `product_page`, `product_cart`, `purchase` |
| Conversion denominator | Unique login users within each group |
| Formal statistical test | Two-sided purchase-conversion z-test at α = 0.05 |

The event sequence is not strictly linear: more users recorded a purchase than a cart event. Funnel stages are therefore treated as distinct user actions relative to login, not as guaranteed sequential transitions.

## Data Sources

The repository includes four training datasets:

| Dataset | Analytical purpose |
|---|---|
| Marketing events | Identify campaigns overlapping the experiment period |
| New users | Registration date, region, and device |
| User events | Timestamped user actions and purchase details |
| Experiment participants | Experiment and group assignments |

The raw files are stored with `.csv.txt` extensions in [`datasets/`](datasets/).

## Analytical Approach

1. Profiled the four source tables and checked exact duplicate records.
2. Selected participants in `recommender_system_test` and joined registration attributes.
3. Restricted the sample to EU users and events occurring 0–13 days after registration.
4. Counted unique users reaching each event and calculated rates relative to login users.
5. Compared activity and funnel metrics between A and B.
6. Applied a two-sided, two-proportion z-test to the purchase-conversion difference.
7. Reviewed assignment integrity, overlapping experiments, calendar effects, and follow-up coverage before interpreting the test.

## Experiment Validation

| Validation check | Finding |
|---|---|
| Exact duplicate rows | None reported in the four source tables |
| Users assigned to both A and B within the target test | 0 |
| Target-test participants before EU filtering | 3,675 |
| Final EU sample | 3,481 users |
| Group allocation | A: 2,604; B: 877 |
| Target-test users also assigned to another experiment | **887** |
| EU marketing overlap | Christmas & New Year promotion began December 25 |
| Users without a complete 14-day window through the source-data end | **1,564** |

These conditions materially limit causal interpretation even though the within-test A/B assignments are mutually exclusive.

## Key Results

### Funnel and engagement metrics

| Metric | Group A | Group B | Observed difference |
|---|---:|---:|---:|
| Product-page conversion | 64.71% | 56.28% | −8.43 pp |
| Cart-event conversion | 30.03% | 27.85% | −2.18 pp |
| Purchase conversion | 31.99% | 28.42% | −3.57 pp |
| Average events per user | 6.62 | 5.38 | −1.24 |

The published conversion rates use 2,604 login users in Group A and 876 in Group B. One additional Group B user generated an event but no recorded login.

### Statistical testing

- **Null hypothesis:** Purchase conversion among login users is equal in Groups A and B.
- **Alternative hypothesis:** Purchase conversion among login users differs between Groups A and B.
- **Test:** Two-sided, two-proportion z-test.
- **Significance level:** α = 0.05.
- **Z-statistic:** −1.9717.
- **P-value:** 0.0486.

Under the test as implemented, the null hypothesis is rejected at the 5% level and the observed difference favours Group A. Only purchase conversion received a formal hypothesis test, so no multiple-testing adjustment was applied.

## Experiment Interpretation

- The treatment group did not show the intended improvement in any reported funnel metric.
- The purchase result is statistically marginal and represents an unadjusted comparison, not a reliable estimate of the recommendation system’s causal effect.
- The experiment does not provide sufficient evidence to support deploying the tested version.
- The most defensible next action is to investigate the experiment setup and rerun the test with exclusive participation, balanced assignment, a complete observation window, and predefined effect-size requirements.

No measured revenue impact, retention improvement, or production implementation outcome is established by this project.

## Visual Analysis

### Conversion rates by event

![Conversion rates by experimental group](images/conversion_rates.png)

### Daily event volume

![Daily event volume by experimental group](images/daily_event_volume.png)

The daily totals are influenced by the unequal group sizes and should not be interpreted as normalized performance measures.

## Limitations

- **887 users participated in both the target test and another experiment**, creating cross-experiment contamination that the original notebook did not remove.
- The 2,604-to-877 group split is substantially imbalanced and the final sample is below the stated expectation of 6,000 participants.
- Late registrants did not all have a complete 14-day observation window before the available event data ended.
- An EU Christmas and New Year promotion overlapped the final experiment dates.
- Conversion was calculated among login users rather than all assigned users; one treatment user had another event without a recorded login.
- The purchase p-value is close to 0.05, and the analysis does not establish statistical power, a minimum detectable effect, confidence intervals, or practical significance.
- Results describe this training dataset and should not be presented as a production experiment or measured commercial impact.

## Deliverables

- [Analysis notebook](AB_Testing_Recommendation_System.ipynb) — preparation, funnel analysis, visualizations, and statistical test
- [Experiment datasets](datasets/) — four source tables used by the notebook
- [Visual outputs](images/) — conversion and daily-volume charts

## Tools and Methods

**Tools**

- Python: pandas, NumPy, SciPy
- Matplotlib and Seaborn
- Jupyter/Google Colab

**Methods**

- Data-quality validation
- Event and funnel analysis
- Conversion-rate comparison
- Two-proportion z-test
- Experiment-design review
- Business-facing interpretation

## Repository Structure

```text
ab-testing-recommendation-system/
├── README.md
├── AB_Testing_Recommendation_System.ipynb
├── datasets/
│   ├── ab_project_marketing_events_us.csv.txt
│   ├── final_ab_events_upd_us.csv.txt
│   ├── final_ab_new_users_upd_us.csv.txt
│   └── final_ab_participants_upd_us.csv.txt
└── images/
    ├── conversion_rates.png
    └── daily_event_volume.png
```

## How to Explore

1. Review this README for the experiment decision and major validity constraints.
2. Open the [analysis notebook](AB_Testing_Recommendation_System.ipynb) for the implemented funnel calculations and z-test.
3. Review [`datasets/`](datasets/) to understand the source tables and [`images/`](images/) for the saved visualizations.

The notebook’s current file paths do not match the repository’s `datasets/*.csv.txt` paths, so a small path adjustment is required before rerunning it locally.

## Project Context

This project was completed as part of the TripleTen Data Analyst training program. It analyzes a simulated e-commerce recommendation-system experiment and demonstrates funnel analysis, statistical testing, and responsible evaluation of experiment validity. It does not build a recommendation algorithm or production experimentation platform.

---

**Sandra Quinones**  
Business & Operations | Reporting & Data Analysis
