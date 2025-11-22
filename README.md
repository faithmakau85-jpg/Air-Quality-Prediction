# Global air predicitions
Introduction & Project Goal
The primary objective of this project was to analyze a global air pollution dataset to understand the relationship between key pollutants (CO, Ozone, NO2, and PM2.5) and the overall Air Quality Index (AQI). We developed and compared machine learning models for two tasks:

Regression: Accurately predicting the numerical AQI Value.

Classification: Classifying the AQI Category (e.g., Good, Hazardous).

#Data Understanding and Cleaning (Weeks 1-3 Prep)
This phase focused on getting the data ready for analysis and modeling.

A. Initial Data Inspection
Dataset: A dataset containing air quality information for numerous cities and countries worldwide.

Columns: The dataset has 12 columns, including:

Geographic: Country, City

Overall AQI: AQI Value (a numerical score) and AQI Category (e.g., Good, Moderate)

Pollutant-Specific AQI: CO AQI Value, Ozone AQI Value, NO2 AQI Value, PM2.5 AQI Value, and their respective Category columns.

Size: The dataset has 23,463 rows and 12 columns.

Missing Values: We found a small number of missing values, notably: 178 missing Country values and 1 missing City value.

B. Data Cleaning (Handling Missing Values)
Method: The missing values in the Country and City columns were filled using the Mode (the most frequent value) of each column.

Code: df["Country"]=df["Country"].fillna(df["Country"].mode()[0])

Result: All missing values were successfully resolved, ensuring a complete dataset for the next steps.

C. Data Exploration (Visuals)
Boxplot: The boxplot visualization showed that the numerical AQI columns contain many outliers (extreme values far from the bulk of the data). This is expected in real-world air pollution data, where a few locations might experience extremely high or "Hazardous" AQI scores.

Histograms: Histograms showed the distribution of the pollutant AQI values. They confirmed that most cities fall into the lower, healthier range, but there are long "tails" of high values, consistent with the outliers seen in the boxplot.

AQI Category Frequency: A bar chart showed the distribution of the overall AQI Category. This is crucial:

The 'Good' category is the most frequent.

The data is imbalanced, with significantly fewer instances of categories like 'Hazardous' or 'Very Unhealthy'.

D. Feature Engineering (Creating New Variables)
To enrich the model, we created several new features based on the existing pollutant AQI values:

avg_pollutant_aqi: The average of all specific pollutant AQI values.

max_pollutant_aqi: The maximum of all specific pollutant AQI values. This is especially important because the overall AQI Value is typically the maximum of the individual pollutant AQI values.

min_pollutant_aqi: The minimum of all specific pollutant AQI values.

pollutant_range: The difference between the max and min pollutant AQI.

Target Encoding: The categorical column AQI Category (e.g., 'Good', 'Moderate') was converted into a numerical target column (e.g., 0, 1, 2, 3...) for use in classification models.
