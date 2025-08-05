# Emergency Room Patient Volume Prediction

A complete machine learning project to predict emergency room patient volume 4 hours in advance using synthetic data and multiple ML algorithms.

## Project Structure

```
er-patient-prediction/
├── er_patient_prediction.ipynb    # Main Jupyter notebook with complete analysis
├── er_prediction_script.py        # Python script version (standalone)
├── setup_and_run.sh              # Automated setup script
├── requirements.txt               # Project dependencies
└── README.md                     # This file
```

## Target Metrics

- **MAE (Mean Absolute Error)**: < 3 patients
- **MAPE (Mean Absolute Percentage Error)**: < 20%
- **R² (Coefficient of Determination)**: > 0.70

## Features

The model uses various features to predict patient volume:

### Time-based Features
- Hour of day (cyclical encoding)
- Day of week (cyclical encoding)
- Month (cyclical encoding)
- Holiday indicators
- Weekend indicators
- Business hours, night time, rush hours

### Historical Features
- Lag features (1h, 2h, 4h, 6h, 12h, 24h, 48h, 168h)
- Rolling statistics (mean, std, max, min) over different windows

### Weather Features
- Temperature
- Rainfall indicators
- Rainfall amount
- Weather interaction features

## Models Implemented

1. **Linear Regression**: Baseline model with feature scaling
2. **Random Forest**: Tree-based ensemble method
3. **XGBoost**: Gradient boosting algorithm

## Quick Start

### Option 1: Automated Setup (Recommended)
Run the setup script which will install all dependencies and verify the installation:
```bash
./setup_and_run.sh
```

### Option 2: Manual Installation
1. Install required packages:
```bash
pip3 install --user pandas numpy matplotlib seaborn scikit-learn xgboost jupyter ipykernel
```

2. Run the Jupyter notebook:
```bash
jupyter notebook er_patient_prediction.ipynb
```

OR run the standalone script:
```bash
python3 er_prediction_script.py
```

## Data Generation

The project generates synthetic emergency room data with realistic patterns:

- **Hourly patterns**: Higher volume during day, lower at night
- **Weekly patterns**: Increased volume on weekends
- **Seasonal patterns**: Flu season effects in winter
- **Weather impact**: Temperature extremes and rain increase patient volume
- **Holiday effects**: Higher volume during holidays

## Visualizations

The project generates several visualizations:

1. **Hourly Trends**: Patient count patterns by hour, day of week, month, and day type
2. **Weather Impact**: Analysis of temperature and rainfall effects
3. **Model Predictions**: Scatter plots showing predicted vs actual values
4. **Time Series**: 7-day prediction visualization with error analysis

## Results

The models are evaluated using multiple metrics and visualizations show:
- Feature importance analysis
- Prediction accuracy over time
- Error distribution analysis
- Model performance comparison

## Usage Notes

- The synthetic data mimics realistic emergency room patterns
- Time-based train/test split maintains temporal integrity
- Feature engineering includes lag variables and rolling statistics
- Models are compared on multiple evaluation metrics
- Visualizations provide insights into data patterns and model performance