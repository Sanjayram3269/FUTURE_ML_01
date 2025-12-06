# Task 1 – Weekly Sales Forecasting (Walmart Dataset)

This task is part of the **Future Interns Machine Learning Internship**.  
Goal: build a time–series model to forecast **weekly store sales** and present the insights in a **Power BI dashboard**.

---

## 1. Problem Statement

Retail companies like Walmart need to plan inventory, staffing and marketing based on future demand.  
In this task, I forecast **weekly total sales** using historical data and evaluate how well the model can predict the last few weeks.

Key questions:
- What is the overall weekly sales trend?
- How accurate is the forecasting model?
- Do holidays increase sales?
- Which stores perform the best on average?

---

## 2. Dataset

- Source: Walmart weekly sales dataset (Kaggle)
- Main fields used:
  - `Store` – store ID  
  - `Dept` – department ID  
  - `Date` – week ending date  
  - `Weekly_Sales` – sales for that store–dept–week  
  - `IsHoliday` – whether the week includes a major holiday  

For modelling, I aggregated to **total weekly sales** across all stores and departments.

---

## 3. Approach

1. **Data Loading & Cleaning**
   - Loaded `train.csv` from GitHub.
   - Converted `Date` to datetime.
   - Aggregated to weekly level:  
     `total weekly sales = sum(Weekly_Sales)` per `Date`.

2. **Exploratory Data Analysis**
   - Plotted **weekly total sales over time**.
   - Observed clear spikes around major holidays.

3. **Feature Preparation for Prophet**
   - Prophet expects columns:  
     - `ds` → date  
     - `y` → target value  
   - Renamed `Date → ds`, `Sales → y`.
   - Split into:
     - **Train** – all weeks except last 12
     - **Test** – last 12 weeks (to evaluate forecast)

4. **Modeling with Facebook Prophet**
   - Trained a **Prophet** model on the training data.
   - Generated **12-week ahead** forecasts with weekly frequency (`freq='W-FRI'`).
   - Merged predictions with the test set.

5. **Evaluation**
   - Metrics on last 12 weeks:
     - **MAE (Mean Absolute Error): ~838,219**
     - **RMSE (Root Mean Squared Error): ~1,084,491**
   - Visualised **Actual vs Forecasted sales** for the test period.

6. **Business Insights**
   - Compared **Holiday vs Non-Holiday weeks** using average weekly sales.
   - Identified **Top 5 stores** by average weekly sales.

---

## 4. Power BI Dashboard

All dashboard files are in:  
`Task1_Sales_Forecasting/Task1_Sales_Forecasting/dashboards/`

The report includes:

1. **KPI Cards**
   - Mean Absolute Error (MAE) – 838K  
   - Root Mean Squared Error (RMSE) – 1M  

2. **Actual vs Forecasted Weekly Sales**
   - Line chart showing model performance on the last weeks.
   - Two series:
     - *Actual Sales*
     - *Forecasted Sales*

3. **Holiday Impact on Weekly Sales**
   - Bar chart of **Average Weekly Sales** for:
     - Holiday weeks
     - Non-holiday weeks

4. **Top 5 Stores by Average Weekly Sales**
   - Horizontal bar chart ranking the best performing stores.

---

## 5. Project Structure

```text
Task1_Sales_Forecasting/
├── Task1_Sales_Forecasting/
│   ├── data/
│   │   ├── train.csv
│   │   ├── actual_vs_forecast.csv
│   │   └── holiday_sales_summary.csv
│   ├── notebooks/
│   │   └── sales_forecasting.ipynb
│   ├── dashboards/
│   │   ├── forecast_output.csv
│   │   └── Task1_Sales_Forecasting_Dashboard.pbix
│   └── src/
│       └── .keep
└── README.md
