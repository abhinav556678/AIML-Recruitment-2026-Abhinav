# AIML Recruitment 2026 

## 1. Candidate Details
Name: Abhinav

## 2. Tasks Completed
* Task 1: Air Quality Forecasting

## 3. Problem Statement
The objective of this task was to analyze historical air-quality measurements from the UCI Air Quality Dataset and build a robust machine learning model to predict future air-quality measurements (specifically forecasting Carbon Monoxide concentrations).

## 4. Approach
My methodology was divided into several key phases:
* Data Understanding & Preprocessing: Parsed European-formatted CSV data, combined date/time strings into a continuous Datetime index, and handled invalid sensor readings using time-based linear interpolation to preserve the timeline sequence.
* Exploratory Data Analysis (EDA): Visualized the distribution of pollutants, generated correlation heatmaps to identify relationships between variables, and plotted time-series trends to identify daily seasonality.
* Feature Engineering: Extracted cyclical time components (Hour, Day of Week, Month) and engineered historical memory features such as Lagged variables (1-hour, 2-hour, and 24-hour previous readings) and 6-hour rolling averages.
* Prediction & Analysis: Strictly split the dataset chronologically (80% Train, 20% Test) to prevent data leakage. Built and trained a RandomForestRegressor and evaluated its performance using MAE, MSE, RMSE, and R-squared metrics. Finally, analyzed Feature Importances to understand the model's decision-making process.

## 5. Technologies Used
* Python 3
* Pandas & NumPy (Data Manipulation & Preprocessing)
* Matplotlib & Seaborn (Data Visualization)
* Scikit-Learn (Machine Learning Modeling & Evaluation)
* Google Colab (Jupyter Notebook Environment)

## 6. Results
The Random Forest model successfully predicted future air quality, effectively capturing the daily rise and fall of pollution levels. The analysis of Feature Importances proved that the most immediate past pollution levels (CO_Lag_1) and short-term trends (CO_Rolling_6) were the strongest predictors of future air quality. The model was rigorously evaluated using standard regression metrics (MAE, MSE, RMSE, R2).

## 7. Key Learnings
1. Time-Series Integrity: I learned the critical importance of chronologically splitting time-series data rather than shuffling it, in order to completely avoid data leakage (look-ahead bias).
2. Feature Engineering for Time-Series: I learned how to engineer Lagged Features and Rolling Averages to mathematically give a machine learning model "memory" of past events.
3. Data Storytelling: I learned that real-world data reflects human behavior. The Exploratory Data Analysis clearly demonstrated how human commute routines directly drive daily cyclical spikes in Carbon Monoxide.

## 8. Challenges
* Challenge: The dataset contained numerous missing or invalid sensor readings recorded as -200. Because this is sequential time-series forecasting, simply dropping these rows would break the continuous timeline and ruin the model's ability to learn temporal patterns.
* Solution: I replaced all -200 values with standard NaNs, and then applied Pandas' time-based linear interpolation (interpolate(method='time')). This allowed me to accurately estimate the missing values based on the hours immediately preceding and following the gap, successfully keeping the timeline fully intact.
