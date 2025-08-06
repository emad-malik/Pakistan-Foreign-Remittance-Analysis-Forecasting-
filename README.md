# Foreign Remittance Analysis

## Overview
This project builds a machine learning pipeline to forecast monthly remittances for individual countries using historical time-series data collected from the SBP website.
The model is trained using **XGBoost Regressor** and incorporates lag features, rolling averages, and temporal patterns to improve prediction accuracy.

---

## Key Features

### Data Cleaning & Preprocessing
- Handles inconsistent country names and removes summary/aggregated rows.
- Converts dates to proper datetime format.
- Creates lag features and rolling averages per country.

### Feature Engineering
- Lag values: `lag_1`, `lag_2`, `lag_3`, `lag_6`
- Rolling means: `rolling_3`, `rolling_6`
- Time-based features: `month`, `year`
- Encoded categorical feature: `country_code`

### Modeling
- Uses **XGBoost Regressor** with tuned hyperparameters.
- Evaluates performance on the last 6 months of data.

### Forecasting
- Generates predictions for the next month (e.g., **July 2025**) for each country.

---

## Data Requirements
### Required Columns
- `Country` (string)  
- `Observation Date` (datetime)  
- `Observation Value` (float) → renamed internally to `Remittance`

---

## Exploratory Data Analysis (EDA)
- **Missing Values Check**: Identify null/missing values in remittance data.  
- **Trend Analysis**: Visualized monthly remittance trends by country.  
- **Top Contributing Countries**: Identified countries contributing the most to remittances.  
- **Seasonality Check**: Observed repeating seasonal patterns in specific countries (e.g., UAE, Saudi Arabia).  
- **Correlation Analysis**: Checked lag correlations to support feature engineering.  

---

## Workflow
1. **Data Preprocessing**
   - Remove summary rows (e.g., `Total`, `Other GCC Countries`, `EU Countries`).
   - Normalize country names.
   - Sort by country and date.
2. **Feature Engineering**
   - Create lag and rolling features.
   - Encode countries as numeric codes.
3. **Model Training**
   - Train XGBoost model on historical data.
   - Evaluate model on the last 6 months (test set).
4. **Forecast Generation**
   - Use the latest country-specific features to generate next-month forecasts.

---

## Next Steps
Experiment with hyperparameter tuning.
Experiment with LSTM or Temporal Fusion Transformers for improved sequence modeling.
Deploy as a REST API for real-time predictions.

## Results
```text
         Country  Forecast_July2025
0      Abu Dhabi         188.30
1        Bahrain         143.87
2        Belgium         116.97
...
Test RMSE: ~42.61 (last 6 months)
