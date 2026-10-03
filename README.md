# FUTURE_ML_01
# Sales & Demand Forecasting for Businesses
**Future Interns – Machine Learning Task 1 (2026)**

## Objective
Build a model that forecasts future sales from historical business data, and present the results in a way a business can use.

## Dataset
Superstore Sales dataset (Kaggle). The columns used are `Order Date` and `Sales`. Orders were grouped into **weekly total sales**.

## Method
1. **Data cleaning:** converted dates, removed missing values and duplicates.
2. **Feature engineering:** month, week of year, quarter, sales from the previous week (`lag_1`), sales 4 weeks ago (`lag_4`), and the average of the last 4 weeks (`roll_4`).
3. **Model:** Random Forest Regressor (300 trees).
4. **Validation:** time-ordered split. The first 80% of weeks were used for training and the last 20% for testing, so the model never sees the future.
5. **Forecast:** predicted the next 12 weeks, one week at a time.

## Results
| Metric | Value |
| MAE  | 6,178 |
| RMSE | 8,057 |
| MAPE | 40.4% |

On average, the weekly forecast is off by about 6,178 in sales (about 40%).

## Visualizations
**Weekly sales trend**
Trend (01_sales_trend.png)

**Actual vs predicted sales**
Actual vs Predicted (02_actual_vs_predicted.png)

**12-week forecast**
Forecast (03_future_forecast.png)

The forecast values are saved in `future_forecast.csv`.

## Business Insights
- **Seasonality:** Sales are highest in Nov,Dec,Sep and lowest in Jan,Feb (see `04_monthly_pattern.png`). The business should stock up and schedule extra staff before these months. The business should stock up and schedule extra staff before these periods.
- **Forecast outlook:** the model predicts weekly sales of roughly 5,800 to 10,000 over the next 12 weeks. This can guide short-term inventory ordering.
- **Use the forecast as a range, not an exact number.** Weekly sales are very volatile, so the forecast is best used to spot the general level and direction, not to predict one specific week.

## Limitations
- Weekly retail sales are noisy, which is why the error (MAPE) is high at 40.4%.
- The model does not know about promotions, holidays, or discounts.
- The dataset covers only a few years, so yearly patterns are learned from limited examples.
- The multi-week forecast uses its own earlier predictions, so errors can build up over time.

## Future Improvements
- Forecast **monthly** instead of weekly to reduce noise.
- Add holiday and promotion features.
- Compare with other models such as XGBoost or Prophet.

## Tools Used
Python, Pandas, NumPy, Matplotlib, Scikit-learn, Google Colab
