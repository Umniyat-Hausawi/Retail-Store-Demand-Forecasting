# Retail Store Demand Forecasting Using Time Series Machine Learning

## Project Overview

This project focuses on forecasting future retail demand using historical sales data and machine learning techniques.

The objective was to build an end-to-end forecasting pipeline capable of learning historical sales behavior, identifying seasonal demand patterns, and generating future sales predictions.

Accurate demand forecasting helps businesses improve inventory planning, reduce stock shortages, avoid overstocking, and support better operational decision-making.

---

## Business Problem

Retail businesses often struggle to estimate future demand accurately.

Poor demand forecasting may lead to:

- Stock shortages and lost sales
- Overstock and increased inventory costs
- Poor replenishment planning
- Inefficient operational decisions

This project addresses the following question:

> Can historical sales behavior be used to predict future retail demand accurately?

---

## Dataset

Dataset Source: Kaggle Demand Forecasting Challenge

Dataset Link:  
https://www.kaggle.com/competitions/demand-forecasting-kernels-only/data

The dataset contains historical daily retail sales data across multiple stores and products.

### Dataset Features

- `date` → sales date
- `store` → store identifier
- `item` → product identifier
- `sales` → daily sales quantity (target variable)

The test dataset does not include the target variable (`sales`), making this a real forecasting problem where future demand must be predicted using historical patterns.

### Dataset Size

#### Training Dataset
- ~913,000 rows
- Historical sales records
- Includes target variable (`sales`)

#### Test Dataset
- ~45,000 rows
- Future unseen observations
- No target variable included

---

## Project Workflow

The project followed a complete machine learning forecasting pipeline:

1. Business understanding
2. Data loading and inspection
3. Exploratory Data Analysis (EDA)
4. Time series pattern analysis
5. Feature engineering
6. Time-based validation split
7. Model training
8. Model comparison
9. Model evaluation
10. Feature importance analysis
11. Future demand forecasting
12. Submission file generation

---

## Exploratory Data Analysis (EDA)

Several important demand patterns were discovered during analysis:

### Key Insights

- Sales distribution was right-skewed.
- Total daily sales showed a clear upward trend over time.
- Strong **weekly seasonality** was observed.
- Weekend sales were generally higher than weekdays.
- Monthly demand patterns suggested seasonal behavior across the year.

These findings guided the feature engineering process.

---

## Feature Engineering

To convert the time series forecasting problem into a supervised machine learning problem, multiple engineered features were created.

### Time-Based Features

Extracted from the `date` column:

- `year`
- `month`
- `day`
- `day_of_week`
- `week_of_year`
- `quarter`
- `is_weekend`

These features helped the model understand calendar-related patterns.

### Lag Features

Historical demand features were created to help the model learn from previous sales behavior:

- `lag_1`
- `lag_7`
- `lag_30`

Example:

- `lag_1` → sales from yesterday
- `lag_7` → sales from the same day last week
- `lag_30` → sales from roughly one month ago

### Rolling Features

Moving averages were added to smooth short-term fluctuations and capture demand trends:

- `rolling_mean_7`
- `rolling_mean_30`

Feature engineering played a major role in improving forecasting performance.

---

## Train / Validation Strategy

Since this is a **time series forecasting problem**, a random train-test split was avoided to prevent **data leakage**.

Instead, a **time-based validation split** was used:

- Earlier dates → training data
- Later dates → validation data

This better simulates real-world forecasting scenarios.

---

## Models Used

Three tree-based regression models were trained and compared.

| Model | MAE | RMSE |
|--------|------|------|
| Random Forest | 6.21 | 8.10 |
| Gradient Boosting | 6.04 | 7.84 |
| XGBoost | 6.02 | 7.81 |

---

## Final Model Selection

XGBoost was selected as the final model because it achieved the best forecasting performance.

Although the improvement over Gradient Boosting was relatively small, XGBoost produced:

- Lowest MAE
- Lowest RMSE
- Stable and realistic predictions

---

## Feature Importance Analysis

Feature importance analysis revealed that historical sales behavior was the strongest predictor of future demand.

### Most Important Features

1. `rolling_mean_7`
2. `lag_7`
3. `rolling_mean_30`
4. `day_of_week`
5. `lag_1`

This confirms that **weekly demand patterns** played a major role in forecasting accuracy.

---

## Evaluation Metrics

Two evaluation metrics were used.

### MAE — Mean Absolute Error

Measures the average prediction error.

It represents how many sales units the model misses on average.

### RMSE — Root Mean Squared Error

Penalizes large prediction errors more heavily.

Useful for understanding whether the model produces large forecasting mistakes.

---

## Final Output

The final XGBoost model was used to generate future sales predictions for the unseen test dataset.

The final submission file contains:

- `id`
- `sales`

Generated file:

```text
submission.csv
```

---

## Business Impact

This forecasting approach can help retail businesses:

- Improve inventory planning
- Reduce stock shortages
- Prevent overstocking
- Understand demand seasonality
- Support better operational decisions

---

## Limitations

Some limitations remain in the current version:

- No holiday data included
- No promotions or discount information
- No pricing information
- Extreme sales spikes may be underestimated

The model relies mainly on historical sales patterns.

---

## Future Improvements

Potential next steps include:

- Adding holiday and event data
- Including promotions and pricing
- Hyperparameter tuning
- Testing longer historical lags (`lag_365`)
- Comparing with LightGBM and CatBoost
- Building an interactive demand forecasting dashboard

---

## Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- XGBoost
- Google Colab

---

## Conclusion

In this project, an end-to-end time series forecasting workflow was developed to predict future retail sales demand using machine learning.

EDA revealed important demand patterns such as weekly seasonality, weekend effects, and long-term trends.

Feature engineering using lag and rolling features significantly improved model performance by allowing the models to learn historical demand behavior.

Among the tested models, **XGBoost achieved the best performance**, producing stable and realistic demand predictions.

Overall, this project demonstrates how historical retail data can be transformed into actionable demand forecasts to support better inventory planning and data-driven business decisions.


## 👤 Author

**Umniyat Hausawi**  
Aspiring Data Scientist | AI & NLP Projects
