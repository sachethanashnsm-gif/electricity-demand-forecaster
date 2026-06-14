# ⚡ Electricity Demand Forecaster

A machine learning solution for forecasting electricity consumption, complete with an interactive Streamlit application for real-time operational planning.

## 📌 Project Overview

This project develops an end-to-end forecasting pipeline to predict electricity demand based on historical consumption patterns and meteorological variables (Temperature, Humidity). Accurate electricity demand forecasting is crucial for grid operators, preventing power outages, and optimizing resource allocation.

The project utilizes data from 2020 to 2024 to train a high-performance XGBoost model and deploys it via an interactive Streamlit interface.

## 🌟 Key Features

* **Machine Learning Pipeline:** Data preprocessing, complex feature engineering, and model training.
* **XGBoost Model:** A robust forecasting model capturing non-linear relationships and seasonality.
* **Advanced Feature Engineering:** Includes temporal features, daily and weekly lagged demand, and rolling statistics.
* **Interactive Streamlit App:** Allows users to interactively generate dynamic hourly and aggregated daily forecasts.

## 📊 Dataset Overview

The forecasting model learns from a time-series dataset covering 2020–2024.

* **Timestamp:** The chronological index (converted to Datetime format).
* **Demand (MW):** The hourly electricity consumption (Target variable).
* **Temperature (°C) & Humidity (%):** Meteorological inputs.

## ⚙️ Machine Learning Pipeline

### Data Preprocessing
To handle temporal complexity and missing data, the following steps are executed:
1.  **Datetime Conversion:** `Timestamp` is converted to datetime objects.
2.  **Indexing:** The `Timestamp` is set as the DataFrame's index.
3.  **Missing Value Imputation:** Partial missing data is handled using `ffill`, `bfill`, and linear `time interpolation` on the `Demand` variable.

### Feature Engineering
The raw data is transformed into powerful predictive inputs:
* **Temporal Features:** Extraction of `hour`, `dayofweek`, `month`, `year`, `quarter`, and `weekofyear`.
* **Weekend Indicator:** A boolean feature to distinguish behavior on weekends versus weekdays.
* **Lagged Features:** Demand at the same hour yesterday (Lag 24h) and last week (Lag 168h) are engineered.
* **Rolling Statistics:** 24-hour rolling mean and standard deviation to capture demand trends and volatility.

### Model and Evaluation
An `XGBRegressor` model is trained using the following configuration:
* **Rounds:** Up to 1000 boosting rounds.
* **Learning Rate:** 0.01 (Conservative learning to prevent overfitting).
* **Early Stopping:** Training stops if validation error doesn’t improve for 50 rounds.
* **Metrics:** Performance is evaluated using RMSE and MAE.

## 🚀 Interactive Streamlit Application

The model is deployed via a Streamlit web application, providing an accessible tool for operational planning.

### Why it is useful:
Grid operators or stakeholders can open the application, select a future start date, choose the number of days to forecast (up to 14), and instantly generate:
1.  A granular **Hourly Demand Line Chart**.
2.  An aggregated **Daily Demand Bar Chart**.

This abstracts the complex machine learning model into a user-friendly decision support tool.

