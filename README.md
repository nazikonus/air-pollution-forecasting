# air-pollution-forecasting
Analysis and forecasting of air pollution in Almaty
# Air Pollution Forecasting Project

## Overview
This project focuses on forecasting air pollution levels, specifically PM2.5, PM10, NO2, SO2, and CO concentrations. We utilized statistical and machine learning methods, including SARIMAX and CNN-LSTM models, to predict pollutant levels based on historical data and exogenous factors like temperature, humidity, and wind speed. The goal is to provide actionable insights for ecological monitoring and decision-making.

---

## Dataset
### Source
The dataset was obtained from a publicly available air quality monitoring source. It includes pollutant concentrations and meteorological data collected daily.

### Features
- **Pollutants**:
  - PM2.5
  - PM10
  - NO2
  - SO2
  - CO
- **Exogenous Variables**:
  - Temperature
  - Humidity
  - Wind Speed

### Preprocessing
1. Missing values were filled using linear interpolation for pollutants and meteorological variables.
2. The data was resampled to a daily frequency to ensure uniformity.
3. Normalization was applied to scale data for the CNN-LSTM model.

---

## Methods

### 1. **SARIMAX Model**
- **Why SARIMAX?**
  SARIMAX (Seasonal AutoRegressive Integrated Moving Average with eXogenous regressors) was chosen for its ability to model seasonal trends and incorporate external variables like temperature, humidity, and wind speed.

- **Configuration**:
  - `order=(1, 1, 1)`: A basic ARIMA structure with 1 lag, first-order differencing, and 1 moving average term.
  - `seasonal_order=(1, 1, 0, 12)`: Captures yearly seasonality.
  - Exogenous variables: Temperature, Humidity, and Wind Speed.

- **Custom Functionality**:
  - The `extend_exog` function ensures that exogenous variables are extended properly to match the forecast length.
  - Forecasts were made for 365 days, leveraging seasonal patterns and the exogenous variables. 

### 2. **CNN-LSTM Model**
Why CNN-LSTM? CNN-LSTM combines Convolutional Neural Networks (CNN) for feature extraction with Long Short-Term Memory (LSTM) for sequential data modeling, making it ideal for complex temporal relationships.

Architecture:

Conv1D layer with 256 filters and kernel size of 3.

Dropout layer (0.3) for regularization.

Bidirectional LSTM layer with 100 units and an additional LSTM layer with 100 units.

Dense layer with 1 output for regression.

Training Parameters:

Epochs: 50

Batch Size: 32

Implementation Details:

The model inputs sequences of 15 time steps for both pollutant levels and exogenous variables.

Data is preprocessed using MinMaxScaler to normalize values between 0 and 1.

The model was trained using the Adam optimizer and mean squared error loss function.

Exogenous variables (e.g., temperature, humidity, wind) were concatenated with pollutant data for enhanced prediction accuracy.

---

## Results
The performance of both models was evaluated using multiple metrics:

| Pollutant | Model     | MAE   | MSE    | RMSE  | R²    |
|-----------|-----------|-------|--------|-------|--------|
| PM2.5     | SARIMAX   | 3.45  | 12.56  | 3.54  | 0.87   |
|           | CNN-LSTM  | 3.12  | 11.23  | 3.35  | 0.89   |
| PM10      | SARIMAX   | 4.23  | 18.34  | 4.28  | 0.82   |
|           | CNN-LSTM  | 3.98  | 16.45  | 4.05  | 0.84   |

---


## Conclusion
1. Both SARIMAX and CNN-LSTM models successfully predicted pollutant concentrations, with CNN-LSTM performing slightly better across all metrics.
2. Seasonal patterns and exogenous variables significantly improved prediction accuracy.

### Recommendations
1. Explore additional exogenous factors like traffic data and industrial activity.
2. Use more advanced neural network architectures (e.g., Transformer models) for better performance on complex datasets.

---

## How to Run
### Prerequisites
- Python 3.8+ 
- Required libraries: TensorFlow, NumPy, Pandas, Matplotlib, scikit-learn, statsmodels
---
 

## Acknowledgments
Special thanks to the data providers and open-source contributors for making this project possible.

