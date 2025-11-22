# Air Quality Prediction Project

## Overview

This project predicts air pollution levels using machine learning
models. It follows a structured 5‑week workflow involving data loading,
cleaning, feature engineering, model training, and evaluation.

## Week 1 --- Data Loading

-   Loaded Global Air Pollution Dataset.
-   Checked dataset structure, missing values, and data types.

## Week 2 -5 Data Cleaning & EDA
Data Understanding and Cleaning (Weeks 1-3 Prep)This phase focused on getting the data ready for analysis and modeling.A. 

Initial Data InspectionDataset: A dataset containing air quality information for numerous cities and countries worldwide.Columns:

 The dataset has 12 columns, including:Geographic: Country, CityOverall AQI: AQI Value (a numerical score) and AQI Category (e.g., Good, Moderate)Pollutant-Specific AQI: CO AQI Value, Ozone AQI Value, NO2 AQI Value, PM2.5 AQI Value, and their respective Category columns.

 The dataset has 23,463 rows and 12 columns.Missing Values: We found a small number of missing values, notably: 178 missing Country values and 1 missing City value.B.
 
  Data Cleaning (Handling Missing Values)Method: The missing values in the Country and City columns were filled using the Mode (the most frequent value) of each column.Code: df["Country"]=df["Country"].fillna(df["Country"].mode()[0])Result: All missing values were successfully resolved, ensuring a complete dataset for the next steps.
  
  # Exploring data
   Data Exploration (Visuals)Boxplot: The boxplot visualization showed that the numerical AQI columns contain many outliers (extreme values far from the bulk of the data). This is expected in real-world air pollution data, where a few locations might experience extremely high or "Hazardous" AQI scores.
   
   Histograms: Histograms showed the distribution of the pollutant AQI values. They confirmed that most cities fall into the lower, healthier range, but there are long "tails" of high values, consistent with the outliers seen in the boxplot.
   
   AQI Category Frequency: A bar chart showed the distribution of the overall AQI Category. This is crucial:The 'Good' category is the most frequent.The data is imbalanced, with significantly fewer instances of categories like 'Hazardous' or 'Very Unhealthy'.
   
# Feature Engineering
 Feature Engineering (Creating New Variables)To enrich the model, we created several new features based on the existing pollutant AQI values:avg_pollutant_aqi: The average of all specific pollutant AQI values.

 max_pollutant_aqi: The maximum of all specific pollutant AQI values. This is especially important because the overall AQI Value is typically the maximum of the individual pollutant AQI values.min_pollutant_aqi: The minimum of all specific pollutant AQI values.pollutant_range: The difference between the max and min pollutant AQI.
 Target Encoding: The categorical column AQI Category (e.g., 'Good', 'Moderate') was converted into a numerical target column (e.g., 0, 1, 2, 3...) for use in classification models.
 
  # Correlation and Model Preparation (Week 3/4 Prep)
  A. Correlation AnalysisHeatmap: A correlation heatmap was generated for all numerical features.Key Insight: The overall AQI Value showed a very strong, positive correlation (close to 1.0) with the individual pollutant values, particularly PM2.5 AQI Value and the newly engineered max_pollutant_aqi. This confirms that the maximum individual pollutant score is the dominant factor in determining the overall AQI. 
  # week 4
  B. Data SplittingBefore building models, the data was split into Training and Testing sets (80% training, 20% testing) to evaluate the models on unseen data.4. Regression Modeling: Predicting AQI Value (Week 4)We built models to predict the numerical AQI Value based on the individual pollutant AQI values (CO AQI Value, Ozone AQI Value, NO2 AQI Value, PM2.5 AQI Value).
  
  A. Random Forest RegressorMetricTraining DataTest DataRMSE (Root Mean Squared Error)0.9991.002R-Squared ($R^2$)0.99990.9999RMSE: The error is extremely low (around 1), indicating the model's predictions are virtually identical to the actual AQI values.$R^2$: A value of 0.9999 means the model explains 99.99% of the variance in the AQI Value.Inference: The model is exceptionally accurate, which is expected since the overall AQI is calculated directly from the max of the individual pollutant AQI values. The extremely small gap between training and test results suggests minimal overfitting and excellent generalization.
  
  B. Linear RegressionMetricTraining DataTest DataRMSE2.5052.551R-Squared ($R^2$)0.99960.9996Inference: Linear Regression also performed incredibly well, with an $R^2$ of 0.9996. While still highly accurate, the Random Forest model's slightly better performance (RMSE $\approx$ 1.0) suggests it captures the complex, non-linear relationship between the pollutants and the final AQI slightly better than a simple linear model.5. Classification Modeling: Predicting AQI Category (Week 4/9)We built models to predict the categorical AQI Category (e.g., 'Good', 'Moderate') based on the AQI values and the engineered features.A. 
  # week 5
  #model comparison
  Model ComparisonWe trained and compared three different classification models:
  Random Forest ClassifierNaive Bayes (GaussianNB)Logistic RegressionModelAccuracy Score (Test Set)Random Forest0.9999Naive Bayes0.9329Logistic Regression0.9859Bar Graph: The bar graph clearly visualizes this comparison, showing the Random Forest Classifier as the best performer by a significant margin.B. Hyperparameter Tuning (Optimizing Random Forest)The best model, Random Forest, was further optimized using Grid Search to find the best settings (hyperparameters) for improved performance.Best Parameters Found: max_depth: 10, min_samples_leaf: 1, n_estimators: 100Best Cross-Validation Accuracy: 0.9999C. Final Evaluation of Tuned ModelThe optimized Random Forest model was tested on the unseen data (Test Set).
  # Final Test accuracy
  Final Test Accuracy: 0.9999 (Near-perfect prediction)Confusion Matrix: The confusion matrix showed that the model correctly predicted almost every single AQI category. The matrix is essentially a diagonal line, with extremely high numbers in the correct prediction cells and almost zero errors. This confirms the model's exceptional ability to classify the AQI category.Feature Importance: A bar plot was generated to see which features were most important to the optimized model:max_pollutant_aqi (Highest Importance)AQI ValuePM2.5 AQI Valueavg_pollutant_aqi...and so on.Inference: This confirms our earlier hypothesis: the overall AQI Category is determined almost entirely by the highest individual pollutant value (max_pollutant_aqi) and the overall AQI Value.
  

-  
## Files Included

-   Air_Quality_Prediction_Report.pdf (full formal report)
-   Notebooks and model outputs (from Google ColLab)
