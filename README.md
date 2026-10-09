# ShowTime — Predicting First-Day Content Viewership

![Course](https://img.shields.io/badge/Course-Predictive%20Modeling-6f42c1)
![Grade](https://img.shields.io/badge/Grade-A%2B%20(4.33)-success)
![Type](https://img.shields.io/badge/Type-Linear%20Regression-blue)
![Tools](https://img.shields.io/badge/Tools-statsmodels%20%C2%B7%20pandas%20%C2%B7%20Seaborn-orange)

A linear regression project that predicts **how many people will watch a title on its first day** on an OTT streaming platform, and identifies which levers actually move that number.

---

## Business Problem

OTT platforms live or die on momentum. **First-day viewership drives word-of-mouth and long-term engagement.** ShowTime wanted to know what drives first-day views so it could make better decisions about content scheduling, marketing spend and platform engagement.

## Objective

Build a linear regression model that predicts first-day viewership (`views_content`) and identify the most impactful variables, then validate the model against the assumptions of linear regression.

## Data

**1,000 content releases** with 8 variables: weekly platform visitors, ad impressions, whether a major sports event coincided, genre, day of week, season, trailer views, and first-day content views (the target).

## Approach

1. **EDA** — univariate distributions and boxplots for all numeric variables; bar charts and frequency tables for categoricals; correlation heatmap and pairplot.
2. **Outlier treatment** — applied a **log transformation** to `ad_impressions` and `views_trailer` to tame heavy right skew while keeping all records. Left the target and visitors untouched.
3. **Feature engineering** — one-hot encoded categorical variables with `drop_first` to avoid the dummy-variable trap; added an intercept term.
4. **Modelling** — 80/20 train-test split, then an **OLS regression** using statsmodels.
5. **Assumption testing** — residual normality (Q-Q plot, Shapiro-Wilk) and homoscedasticity (Goldfeld-Quandt), plus VIF for multicollinearity.

## Key Findings

**Model performance**
- **R² = 0.784** and adjusted R² = 0.780 — the model explains about **78%** of the variation in first-day views.
- F-statistic **141.3** (p < 0.001) confirms overall significance; Durbin-Watson **1.983** shows no autocorrelation.

**What drives first-day views**

| Driver | Effect |
|---|---|
| **Trailer views** | **Strongest driver** — coefficient **0.2222**, correlation 0.75 with the target |
| **Platform visitors** | Coefficient **0.1249** — more pre-release traffic means more first-day views, but weaker than trailers |
| **Major sports events** | Coefficient **−0.0623**, significant — releasing on a sports-event day lowers first-day views by roughly **12.5%** (median ~0.42M vs ~0.48M) |
| **Release day** | Saturday (**+0.0541**), Wednesday (**+0.0456**), Sunday (**+0.0406**) outperform the baseline. Friday is the most common release day but the most inconsistent |
| **Season** | Mild effect — Summer (**+0.0458**) and Spring (**+0.0278**) positive |
| **Ad impressions** | **Do not predict success** — correlation only 0.05, not significant |
| **Genre** | Mostly neutral, except **Sci-Fi (+0.0178)** which is positive and significant |

## Recommendations

1. **Invest in trailer visibility and engagement** — the single most effective lever for first-day performance.
2. **Schedule major releases mid-week (especially Wednesday) or on weekends**, and avoid clashing with major sports events.
3. **Re-think ad spend** — raw impressions do not move first-day views, so targeting and creative quality matter more than volume.
4. **Study the high-performing outliers** (blockbuster titles and heavy promotional pushes) for repeatable strategies.
5. **Break down the large "Others" genre category** (25.5% of titles) to uncover hidden high-performing niches.

## Skills Demonstrated

Linear regression with statsmodels · log transformation for skew · one-hot encoding · train-test splitting · regression diagnostics (residual normality, homoscedasticity, autocorrelation, VIF) · translating coefficients into business actions.

## Repository Structure

```
├── notebooks/
│   └── showtime_linear_regression.ipynb
├── reports/
│   └── ShowTime_Business_Report.pdf
├── screenshots/
│   ├── notebook_chart_01.png … notebook_chart_10.png
│   └── report_page_01.png … report_page_04.png
└── README.md
```

---

*PGP in Data Science & Business Analytics · Great Lakes Executive Learning / The University of Texas at Austin, McCombs School of Business. Content drawn from the project notebook, business report and course transcript.*
