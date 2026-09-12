# Electricity Consumption Prediction

## Project Overview

This project focuses on predicting household electricity consumption using machine learning regression algorithms.

The target variable is **`Global_active_power`**, which represents the household's global active electricity power consumption.

The project includes data cleaning, date-time feature engineering, chronological train-test splitting, model training, and regression evaluation.

## Dataset

**Dataset Name:** Individual Household Electric Power Consumption

**Source:** UCI Machine Learning Repository

**Dataset Link:** https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption

The dataset contains household electricity measurements recorded over time.

### Main Columns

* `Date`
* `Time`
* `Global_active_power`
* `Global_reactive_power`
* `Voltage`
* `Global_intensity`
* `Sub_metering_1`
* `Sub_metering_2`
* `Sub_metering_3`

## Objective

The main objective is to build a regression model that predicts `Global_active_power` using electrical measurements and time-related features.

## Data Preprocessing

The following preprocessing steps were performed:

1. Loaded the dataset using the semicolon separator.
2. Replaced `?` values with `NaN`.
3. Converted measurement columns from object type to numeric type.
4. Handled missing numerical values using linear interpolation.
5. Used forward-fill and backward-fill for any remaining missing values.
6. Combined `Date` and `Time` into a datetime column.
7. Extracted the following time-based features:

   * `Year`
   * `Month`
   * `Day`
   * `DayOfWeek`
   * `Hour`
   * `Minute`
8. Removed the original date-time columns after feature extraction.
9. Removed `Global_intensity` from the features because it had an extremely high correlation with the target.

## Target Variable

```text
Global_active_power
```

## Features Used

* `Global_reactive_power`
* `Voltage`
* `Sub_metering_1`
* `Sub_metering_2`
* `Sub_metering_3`
* `Year`
* `Month`
* `Day`
* `DayOfWeek`
* `Hour`
* `Minute`

## Train-Test Split

Because the dataset is time-dependent, a chronological split was used:

* **80%:** Training data
* **20%:** Testing data

The earlier observations were used for training, while later observations were used for testing. This better represents the real-world situation of using past data to predict future electricity consumption.

## Machine Learning Models

The following regression models were evaluated:

1. Linear Regression
2. Decision Tree Regressor
3. Random Forest Regressor
4. Gradient Boosting Regressor

## Model Evaluation

The models were evaluated using:

* **Mean Absolute Error (MAE):** Measures the average absolute prediction error.
* **Mean Squared Error (MSE):** Measures the average squared prediction error.
* **Root Mean Squared Error (RMSE):** Measures prediction error in the target's units.
* **R² Score:** Measures how much variation in the target is explained by the model.

For MAE, MSE, and RMSE, lower values are better. For R², a higher value is better.

## Results

| Model                       |    MAE |    MSE |   RMSE | R² Score |
| --------------------------- | -----: | -----: | -----: | -------: |
| Linear Regression           | 0.2870 | 0.1474 | 0.3840 |   0.8082 |
| Decision Tree Regressor     | 0.2389 | 0.1446 | 0.3803 |   0.8118 |
| Random Forest Regressor     | 0.2996 | 0.2806 | 0.5297 |   0.6349 |
| Gradient Boosting Regressor | 0.2108 | 0.1069 | 0.3269 |   0.8610 |

## Best Model

The best-performing model was **Gradient Boosting Regressor**.

Its results were:

* **MAE:** 0.2108
* **MSE:** 0.1069
* **RMSE:** 0.3269
* **R² Score:** 0.8610

The model explains approximately **86.10% of the variation** in global active power consumption on the test data.

## Important Observation

`Global_intensity` had a correlation of approximately **0.9989** with `Global_active_power`. Because this relationship was extremely strong, the feature was removed to reduce redundancy and avoid an overly optimistic evaluation result.

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Jupyter Notebook

## Future Improvements

* Perform hyperparameter tuning for Gradient Boosting.
* Add prediction-versus-actual visualizations.
* Analyze daily, weekly, and monthly electricity consumption patterns.
* Test additional regression algorithms.
* Create a user interface for making electricity consumption predictions.
* Experiment with advanced time-series forecasting methods.

## Conclusion

This project demonstrates how machine learning regression algorithms can be used to predict household electricity consumption. After comparing multiple models, Gradient Boosting Regressor achieved the best performance among the tested models.

The project also demonstrates the importance of time-based feature engineering, chronological data splitting, missing-value handling, and checking for highly correlated or redundant features.
