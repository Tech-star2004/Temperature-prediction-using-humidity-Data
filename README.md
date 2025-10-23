# Temperature Prediction
# Author: Nandipati Lakshmi Narasimha Reddy
## Project Goal
The primary objective of this project was to develop and evaluate a machine learning model capable of accurately predicting **Temperature** ($^\circ$C) based on various atmospheric sensor readings, including pressure, humidity, and location (latitude/longitude).

## Key Results

| Metric | Model: XGBoost Regressor | Interpretation |
| **R-squared ($R^2$) Score** | **0.9727** | **Excellent fit:** The model explains over 97% of the variance in temperature. |
| **Mean Absolute Error (MAE)** | **1.72$^\circ$C** | On average, predictions are off by only **1.72 degrees Celsius**. |
| **Root Mean Squared Error (RMSE)** | **2.30$^\circ$C** | Used as the 'Final Realistic Error'. |

## Methodology & Model Diagnosis

### 1. Model Selection
- **Initial Attempt:** A **Linear Regression** model was first used but struggled to capture complex, non-linear interactions between humidity and temperature.
- **Final Model:** A **Gradient Boosting Regressor (XGBoost)** was selected for its ability to model intricate, non-linear feature relationships, leading to a significant increase in $R^2$.

### 2. Residual Analysis (The Outlier Problem)
A key part of this project was diagnosing the difference between the MAE ($1.72^\circ\text{C}$) and the RMSE ($2.30^\circ\text{C}$). This gap suggests the presence of large, infrequent prediction errors (outliers).
- **Visualization:** The Residuals vs. Predicted values plot () showed extreme prediction errors, particularly when humidity was near its physical boundaries (0% or 100%).
- **Hypothesis:** These large errors are likely due to **sensor malfunctions or data anomalies** at extreme humidity levels, and not a fundamental flaw in the model's structure.

### 3. Feature Importance (Implicit in XGBoost)
The model relies heavily on the **inverse relationship between Humidity and Temperature**. Low humidity strongly predicts higher temperature, and high humidity predicts lower temperature.

## Data and Technologies

### Dataset
- **Source:** `humidity.csv`
- **Size:** Over 700,000 records.
- **Features Used:** `sensor_id`, `lat`, `lon`, `pressure`, `humidity` (Target: `temperature`).

### Libraries
- Python 3.x
- Pandas, NumPy
- **XGBoost** (for regression)
- Scikit-learn (for splitting and metrics)
- Matplotlib, Seaborn (for visualization)

## How to Get Started

### Prerequisites

Ensure you have **Python 3.9+** installed on your system.

### Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Tech-star2004/Temperature-prediction-using-humidity-Data.git](https://github.com/Tech-star2004/Temperature-prediction-using-humidity-Data.git)
    cd Temperature-prediction-using-humidity-Data
    ```
2.  **Install Dependencies:**
    It is recommended to use a virtual environment. Install all required libraries using `pip`:
    ```bash
    pip install pandas numpy xgboost scikit-learn matplotlib seaborn jupyter
    ```

## Running the Project

The entire workflow, including data loading, preprocessing, training, and evaluation, is contained within the Jupyter Notebook.

1.  **Start Jupyter:**
    ```bash
    jupyter notebook
    ```
2.  **Run the Notebook:**
    Open the file `Temperature Prediction_Test.ipynb` in your browser and run all cells.

## Future Work
Based on the diagnostic phase, the immediate next steps to achieve sub-2.0 $\text{RMSE}$ performance are:
1.  **Outlier Removal:** Implement an aggressive data cleaning step to filter out records where humidity is $\approx 0\%$ or $\approx 100\%$ and the temperature value is highly suspicious (e.g., manually verifying sensor errors).
2.  **Hyperparameter Tuning:** Use `GridSearchCV` or `RandomizedSearchCV` to optimize the `max_depth` and `n_estimators` for the XGBoost model.

