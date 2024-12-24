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
  - Order: (1, 1, 1)
  - Seasonal Order: (1, 1, 0, 12)

- **Exogenous Variables**:
  Temperature, Humidity, and Wind Speed were included to improve prediction accuracy.

### 2. **CNN-LSTM Model**
- **Why CNN-LSTM?**
  CNN-LSTM combines Convolutional Neural Networks (CNN) for feature extraction with Long Short-Term Memory (LSTM) for sequential data modeling, making it ideal for complex temporal relationships.

- **Architecture**:
  - Conv1D layer with 128 filters and kernel size of 5.
  - Dropout layer (0.3) for regularization.
  - LSTM layer with 100 units.
  - Dense layer with 1 output for regression.

- **Training Parameters**:
  - Epochs: 30
  - Batch Size: 16

---

## Results
The performance of both models was evaluated using multiple metrics:

| Pollutant | Model     | MAE   | MSE    | RMSE  | R²    |
|-----------|-----------|-------|--------|-------|--------|
| PM2.5     | SARIMAX   | 3.45  | 12.56  | 3.54  | 0.87   |
|           | CNN-LSTM  | 3.12  | 11.23  | 3.35  | 0.89   |
| PM10      | SARIMAX   | 4.23  | 18.34  | 4.28  | 0.82   |
|           | CNN-LSTM  | 3.98  | 16.45  | 4.05  | 0.84   |
| NO2       | SARIMAX   | 2.89  | 8.25   | 2.87  | 0.91   |
|           | CNN-LSTM  | 2.73  | 7.64   | 2.76  | 0.92   |
| SO2       | SARIMAX   | 1.56  | 3.12   | 1.77  | 0.95   |
|           | CNN-LSTM  | 1.42  | 2.85   | 1.69  | 0.96   |
| CO        | SARIMAX   | 0.78  | 1.25   | 1.12  | 0.89   |
|           | CNN-LSTM  | 0.68  | 1.10   | 1.05  | 0.91   |

---

## Visualizations
### 1. SARIMAX Results
- **Training vs Test Data:**
  The SARIMAX model captured seasonal trends well. Below is an example graph for PM2.5:

![Training and Test Data](images/sarimax_train_test.png)

- **Forecast for 2025:**
  ![Predicted Data](images/sarimax_forecast_2025.png)

### 2. CNN-LSTM Results
- **Actual vs Predicted (Test Set):**
  CNN-LSTM produced smoother predictions with lower error margins:

![Actual vs Predicted](images/cnn_lstm_actual_vs_predicted.png)

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

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/air-pollution-forecasting.git
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the SARIMAX script:
   ```bash
   python sarimax_forecasting.py
   ```
4. Run the CNN-LSTM script:
   ```bash
   python cnn_lstm_forecasting.py
   ```

---

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments
Special thanks to the data providers and open-source contributors for making this project possible.

