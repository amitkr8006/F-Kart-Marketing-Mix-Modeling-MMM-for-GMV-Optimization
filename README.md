# F-Kart Marketing Mix Modeling (MMM) for GMV Optimization

This project applies Marketing Mix Modeling (MMM) to quantify the drivers of weekly Gross Merchandise Value (GMV) for an e-commerce retailer (F-Kart) and convert the insights into practical, ROI-focused recommendations for marketing allocation, pricing/discount strategy, and operational planning. The analysis covers three categories—Home Audio, Camera Accessories, and Gaming Accessories—using weekly data from Jul 2023 to Jun 2024.

## Objectives
- Measure how marketing, pricing, product mix, and operations influence GMV.
- Capture delayed marketing impact using 1–3 week lag variables and adstock transformation.
- Compare multiple regression-based MMM approaches and select best-performing, interpretable models per category.
- Translate model outputs into actionable business recommendations.

## Tech Stack
- **Python**
- **pandas, NumPy**
- **scikit-learn** (LinearRegression, RFE, StandardScaler, OneHotEncoder, ColumnTransformer, GradientBoostingRegressor)
- **statsmodels** (OLS regression for inference and significance testing)
- **ydata-profiling** (data profiling and quality checks)
- **seaborn** (EDA and correlation analysis)

## Data (High-Level)
Weekly aggregated category-level datasets (Jul 2023–Jun 2024) including:
- **Sales & Pricing:** units sold, MRP, discount percentage, product sub-types
- **Marketing:** TV/digital/online/radio/content spends (plus adstock variants)
- **Operations:** delivery time, SLA compliance, procurement-related lag indicators
- **Time Effects:** GMV lags and related lagged signals (e.g., landing page / purchase-order lags)

## Methodology
1. **Profiling & Cleaning:** identified missing values, constants, outliers, and invalid entries; handled infinities; improved overall dataset reliability.
2. **Multicollinearity Control:** removed highly correlated variables (correlation threshold filtering) to stabilize coefficient interpretation.
3. **Feature Engineering for MMM Realism:** created 1–3 week lag features and moving-average signals to represent persistence and delayed effects.
4. **Preprocessing Pipeline:** scaled numeric variables and one-hot encoded categorical variables using a repeatable ColumnTransformer workflow.
5. **Model Benchmarking:** compared multiple MMM frameworks including:
   - Linear Regression (baseline)
   - OLS Regression (interpretability + statistical significance)
   - RFE + OLS (parsimonious feature selection)
   - Adstock + OLS (media memory effects)
   - Gradient Boosting + lag framing (nonlinear signal capture)
   - Distributed Lag Models (DLM) (explicit lag response modeling)
   - Exponential/Multiplicative (log-log) regression (elasticity interpretation)
6. **Evaluation:** 80/20 train-test split with R² / Adjusted R² and RMSE, alongside coefficient and significance interpretation for OLS families.

## Results (Highlights)
- **Gaming Accessories (Best overall):** Exponential/Multiplicative model achieved **R² ≈ 0.859** and **RMSE ≈ 0.333**, indicating strong predictive fit and clear elasticity-style interpretation.
- **Home Audio:** Distributed Lag Model performed strongly with **Adjusted R² ≈ 0.818** and **Test R² ≈ 0.794**, confirming meaningful lagged demand and media effects.
- **Camera Accessories:** DLM and Exponential models were competitive (e.g., **Test R² ≈ 0.738** for DLM), showing stable performance across alternative specifications.

## Key Insights
- **Lag effects are real:** marketing and demand signals frequently impacted GMV with a **1–3 week delay**, supporting lag-aware planning.
- **Discounting often showed negative association with GMV:** suggesting that heavy discounting can reduce value perception or margins without proportional GMV lift, especially in premium segments.
- **Product mix matters:** certain product sub-types consistently contributed more to GMV, enabling more targeted merchandising and campaign design.
- **Operations influence revenue:** delivery delays and weaker SLA performance correlated with lower GMV, highlighting cross-functional impact beyond marketing.

## Business Recommendations
- Prioritize **Gaming Accessories** for investment given the strongest modeled response and highest explanatory power.
- Plan campaigns with **lead time (2–3 weeks)** to align with lagged response patterns and maximize GMV impact.
- Reduce reliance on deep discounting; shift toward **product-led targeting** and value-based messaging, especially for premium products.
- Align inventory/procurement and delivery operations with campaign calendars to avoid stockouts and minimize delivery-related GMV loss.

## Limitations & Next Steps
- Models were primarily additive; channel synergies and saturation effects can be better captured with nonlinear or Bayesian MMM approaches.
- Adstock decay parameters were heuristic rather than optimized; future work can tune decay and test multiple carryover shapes.
- Adding external signals (competitor pricing, macro factors, search trends) could strengthen robustness and explainability.
