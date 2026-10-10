# Report Summary: Superstore Dataset Profit Analysis

## Objective
Maximise profit by identifying the factors behind profitable and loss-making sales, using the full statistical learning process: data understanding, preparation, exploratory analysis, feature engineering and predictive modelling. **Target variable: Profit.**

## Data
- 9,994 order lines and 21 columns from a US superstore (2014–2017), covering:
  - order and ship dates and shipping mode
  - customer segment
  - city, state and region
  - product category and sub-category
  - sales, quantity, discount and profit

## Data preparation
- Removed one duplicate row and four uninformative columns (row ID, customer name, postal code, and country, which is the same for every row).
- Confirmed there are no missing values.
- Engineered new features:
  - profit margin
  - profit per unit
  - delivery days
  - order year
  - day of week

## Exploratory and statistical analysis
- **Normality:** D'Agostino's K² test shows that profit, sales, quantity and discount are all non-normal, so non-parametric tests were used.
- **Kruskal–Wallis tests:** profit differs significantly across categories, sub-categories, regions, cities and shipping modes, but not across customer segments (p = 0.107).
- **Spearman correlations with profit:** discount −0.54, sales +0.52, quantity +0.23.
- **Discounts:** orders discounted above 20% are loss-making on average.
- **Customers:** the top 20% of profitable customers contribute 59% of positive profit, and the bottom 20% of loss-making customers account for 71% of losses.
- **Products and geography:** profitability varies strongly by sub-category (copiers, phones and accessories earn the most, while tables, bookcases and supplies lose money overall) and by state and city.
- **Outliers:** profit was winsorised at 2% on each tail and sales at the top 2%, to limit the influence of extreme orders without deleting data.

## Modelling
- **Features:** sales, quantity, discount, year, plus one-hot encoded shipping mode, segment, category, sub-category, region, state and city.
- **Validation:** 80/20 train/test split.

| Model | R² | Notes |
|---|---:|---|
| Linear Regression (standardised) | 0.497 | Captures only linear effects |
| **Random Forest (100 trees)** | **0.889** | MAE 10.28, RMSE 26.41 |

The most important features are sales (0.47) and discount (0.32).

## Recommendations
- Limit discounts above 20%, which consistently turn orders unprofitable.
- Focus pricing reviews on loss-making sub-categories and locations, rather than on customer segments.
- Retain and target the most profitable customers, and review terms for the small group of customers driving most losses.
