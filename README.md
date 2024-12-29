# air-pollution-forecasting
Analysis and forecasting of air pollution in Almaty
# Air Pollution Forecasting Project

## Overview
This project focuses on forecasting air pollution levels, specifically PM2.5, PM10 concentrations. We utilized statistical and machine learning methods, including SARIMAX , CNN and LSTM models, to predict pollutant levels based on historical data and exogenous factors like temperature, humidity, and wind speed. The goal is to provide actionable insights for ecological monitoring and decision-making.

---

## Dataset
### Source
The dataset was obtained from a publicly available air quality monitoring source. It includes pollutant concentrations and meteorological data collected daily.

### Features
- **Pollutants**:
## Pollutants Overview

### PM2.5 (Particulate Matter < 2.5 microns)

- **What it is**: Fine particles smaller than 2.5 microns that can penetrate deep into the lungs and bloodstream.
- **Units**: µg/m³ (micrograms per cubic meter).
- **Sources**: Industrial emissions, vehicle exhaust, wildfires, and construction dust.
- **Impact**: Major component of smog, causing respiratory issues and reducing visibility.

### PM10 (Particulate Matter < 10 microns)

- **What it is**: Particles smaller than 10 microns that can irritate the respiratory system.
- **Units**: µg/m³.
- **Sources**: Transport, dust from construction sites, agriculture, and wildfires.
- **Impact**: Contributes to smog and health problems, particularly in urban areas.

### NO2 (Nitrogen Dioxide)

- **What it is**: A gas produced by combustion processes, especially from vehicles and power plants.
- **Units**: ppm (parts per million) or µg/m³.
- **Sources**: Vehicles, industrial emissions, power plants.
- **Impact**: Contributes to photochemical smog, aggravates asthma, and reduces air quality.

### SO2 (Sulfur Dioxide)

- **What it is**: A gas released from burning fossil fuels and volcanic activity.
- **Units**: µg/m³ or ppm.
- **Sources**: Power plants, industrial processes, volcanoes.
- **Impact**: Forms acid rain, harms respiratory health, and contributes to smog.

### CO (Carbon Monoxide)

- **What it is**: A colorless, odorless gas produced by incomplete combustion of carbon-containing fuels.
- **Units**: ppm.
- **Sources**: Vehicle emissions, industrial processes, and household heating.
- **Impact**: Reduces oxygen delivery in the body, contributing to smog and health risks.

### Smog Impact:
These pollutants, when combined, form smog that reduces air quality, visibility, and harms human health, especially in urban areas with high traffic and industrial activity.
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

### SARIMAX Model
| Pollutant | MAE   | MSE    | RMSE  | R²    |
|-----------|-------|--------|-------|-------|
| PM2.5     | 19.99 | 675.67 | 25.99 | 0.91  |
| PM10      | 12.98 | 363.98 | 19.08 | 0.91  |

### CNN Model
| Pollutant | MAE   | MSE    | RMSE  | R²    |
|-----------|-------|--------|-------|-------|
| PM2.5     | 17.52 | 517.66 | 22.75 | 0.75  |
| PM10      | 10.25 | 259.99 | 16.12 | 0.82  |

### LSTM Model
| Pollutant | MAE   | MSE    | RMSE  | R²    |
|-----------|-------|--------|-------|-------|
| PM2.5     | 15.78 | 442.50 | 21.04 | 0.86  |
| PM10      | 12.11 | 291.25 | 17.07 | 0.73  |

---


## Conclusion
Among the models evaluated, SARIMAX outperformed both CNN and LSTM models in predicting pollutant concentrations. While CNN-LSTM showed slightly better results in some areas, SARIMAX proved to be more effective overall due to its ability to account for seasonal patterns and incorporate exogenous variables. These factors significantly improved the prediction accuracy, making SARIMAX the preferred choice for time-series forecasting in this context.

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

