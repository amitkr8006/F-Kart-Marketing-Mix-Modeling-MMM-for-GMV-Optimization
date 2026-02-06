# F-Kart Marketing Mix Modeling (MMM) for GMV Optimization

This project applies Marketing Mix Modeling (MMM) to quantify the key drivers of weekly Gross Merchandise Value (GMV) for an e-commerce retailer (F-Kart) and generate actionable, ROI-focused recommendations for marketing budget allocation, pricing/discount strategy, and operational planning.

The analysis focuses on three product categories:
- Home Audio
- Camera Accessories
- Gaming Accessories

A full year of weekly data (Jul 2023 – Jun 2024) was used to compare multiple regression-based MMM approaches, including lag/adstock transformations to capture delayed marketing effects.

---

## Key Objectives
- Identify which factors (media spend, pricing, product mix, operations) drive GMV.
- Capture delayed effects (1–3 weeks) using lag variables and adstock transformations.
- Compare multiple modeling approaches and select best-fit models per category.
- Translate model outputs into practical marketing and business recommendations.

---

## Key Features
- End-to-end MMM workflow: cleaning → feature engineering → modeling → evaluation → recommendations
- Multiple model families benchmarked:
  - Linear Regression (baseline)
  - OLS Regression (interpretable coefficients + p-values)
  - Recursive Feature Elimination (RFE)
  - Adstock-transformed OLS (media memory effects)
  - Gradient Boosting + Koyck-style lag framing
  - Distributed Lag Models (DLM)
  - Exponential/Multiplicative (log-log) regression for elasticity interpretation
- Consistent evaluation strategy (80/20 train-test split) using R² / Adjusted R² and RMSE

---

## Results Summary (Highlights)
- Best overall performance: Gaming Accessories using Exponential/Multiplicative (log-log) model  
  - R² ≈ 0.8592, RMSE ≈ 0.3334
- Distributed Lag Models (DLM) performed strongly across categories, indicating meaningful lag effects.

Common patterns observed:
- Discounting often shows negative association with GMV (price/value sensitivity).
- Marketing impact frequently appears with 1–3 week delays (lag effects).
- On-time delivery and operational reliability support higher GMV.

---

## Tech Stack
- Python
- pandas, NumPy
- scikit-learn (LinearRegression, RFE, StandardScaler, OneHotEncoder, ColumnTransformer, GradientBoostingRegressor)
- statsmodels (OLS)
- ydata-profiling
- seaborn (EDA/correlation)

---

## Data
Data comes from internal weekly aggregated records (Jul 2023 – Jun 2024), split into three category-specific datasets. Fields include:
- Sales & pricing: units sold, MRP, discounts
- Marketing: TV/digital/online/radio/content spends (+ adstock variants)
- Operations: delivery time, SLA compliance, procurement lag indicators
- Time effects: GMV lags, landing page and purchase order lag variables

> Note: Raw datasets are not included in this repository if they are confidential.

---

## Methodology (High-Level)
1. Load + validate datasets (category-wise)
2. Data profiling + cleanup (missing values, constants, outliers, inf handling)
3. Multicollinearity reduction using correlation filtering
4. Feature engineering:
   - GMV lags (1–3 weeks)
   - Moving averages
   - Campaign/ops lag features
   - Adstock transformation for media memory effects
5. Preprocessing pipeline:
   - StandardScaler (numeric)
   - OneHotEncoder (categorical)
   - ColumnTransformer for reproducibility
6. Train/test evaluation and model comparison (R², RMSE; p-values for OLS)
7. Business interpretation + recommendations

---

## Repository Structure (Suggested)
- `notebooks/` — Jupyter notebooks (main analysis)
- `src/` — reusable helper functions (adstock, feature engineering, evaluation)
- `reports/` — final report / write-up
- `figures/` — charts and visual outputs
- `data/` — (optional) sample or anonymized data + data dictionary

---

## How to Run (Typical)
1. Create environment and install dependencies
   - `pip install -r requirements.txt`
2. Open and run the notebook(s) inside `notebooks/`
3. Outputs (figures/results) will be generated during execution

---

## Business Recommendations (Examples)
- Prioritize Gaming Accessories for investment due to strongest modeled response.
- Use lag-aware campaign planning (launch campaigns 2–3 weeks before peak demand).
- Avoid deep discounting; focus on product-led targeting and value messaging.
- Align inventory/procurement and delivery operations with campaign calendars.
- Build weekly monitoring dashboards (GMV, lags, adstock, delivery KPIs).

---

## Limitations
- Mostly additive models; interaction/synergy not explicitly modeled.
- Adstock decay parameters based on heuristics, not optimized.
- One-year window may limit seasonality and external factor capture.

---

## Future Work
- Bayesian MMM / hierarchical MMM
- Nonlinear ML (e.g., XGBoost) for interactions and complex response curves
- External signals: competitor pricing, macro factors, Google Trends
- Optional integration with MTA when user-level data is available

---

## Reference Link (from report appendix)
```text
