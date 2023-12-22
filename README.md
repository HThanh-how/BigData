# Big Data and Intelligence in  Business 

## Project Big Data for Weather Forecasting 

## 1. Introduction

### Problem Statement:

Weather forecasting, a complex task due to the dynamic nature of the Earth's atmosphere, is essential for various applications such as agriculture, aviation, defense, tourism, and disaster management. Traditional methods, including physical models and numerical weather prediction, face limitations in accuracy and computational efficiency.

### Applications:

Accurate weather predictions have widespread applications, impacting agriculture, aviation, defense, tourism, and disaster management. Optimizing activities based on precise weather forecasts can maximize benefits and minimize risks.

### Existing Solutions and Their Limitations:

Traditional methods like persistence, trend, statistical techniques, and numerical weather prediction have pros and cons. While numerical weather prediction provides accurate forecasts, it demands substantial computational resources. This project explores the use of Machine Learning (ML) to overcome limitations and enhance weather forecasting.

### Our Approach:

We leverage Machine Learning, specifically using PySpark, a Python library for big data processing. PySpark's ability to handle large datasets and perform distributed computing makes it suitable for big data applications. The project focuses on implementing and evaluating ML models, including logistic regression, SVM, and random forest, to develop a scalable and accurate weather forecasting model.

## 2. Methods/Approaches

### Overview:

The project employs PySpark to implement a machine learning pipeline for weather forecasting. The pipeline includes data preprocessing, model training, and weather prediction. Key steps involve handling missing data, normalizing data, and converting weather data into a numerical format suitable for ML models.

### Architecture/Method Pipeline:

1. **Data Preprocessing:** Prepare the dataset by handling missing data, removing noise, and normalizing data. Convert weather data into a numerical form.
2. **Model Training:** Split the dataset, train ML models (logistic regression, SVM, random forest) on the training set.
3. **Weather Prediction:** Use trained models to predict weather conditions based on current data.
4. **Model Evaluation:** Assess prediction accuracy by comparing predictions with actual data.

### Main Steps:

1. **Data Preprocessing:** Clean data by removing noise and normalizing it for ML processing.
2. **Model Training:** Train logistic regression, SVM, and random forest models on preprocessed data.
3. **Weather Prediction:** Use trained models to predict current weather conditions.
4. **Model Evaluation:** Assess accuracy by comparing predictions with actual data.

## 3. Experiments

### Overview:

The project utilizes PySpark to implement and evaluate ML models for weather forecasting. The dataset used is sourced from Kaggle, containing hourly weather data for various cities.

### 3.1 Description

**Implementation Description:** The project uses PySpark and MLlib to implement a distributed ML pipeline for weather forecasting. Benchmark datasets from Kaggle are used for testing, including temperature, humidity, pressure, wind direction, wind speed, and weather description.

### 3.2 Data Preprocessing

1. **Download the Dataset:** Obtain data from Kaggle, including temperature, humidity, pressure, wind direction, wind speed, and weather description.
2. **Load Dataset:** Load data into Koalas DataFrame objects for further processing.
3. **Data Cleaning:** Remove noise, normalize data, and handle missing values.
4. **Aggregation:** Aggregate similar weather conditions to refine target classes.
5. **Undersampling:** Address class imbalance using undersampling.

### 3.3 Training and Evaluating the Model

#### A. Random Forest

Train a Random Forest classification model and evaluate its performance on the test set.

#### B. KNN (K-Nearest Neighbors)

Train a KNN model and evaluate its performance on the test set.

## 4. Improvements and Application Proposals

### Improvements:

1. **Data Quality and Quantity:** Enhance data quality by removing outliers and incorporating additional data sources.
2. **Feature Engineering:** Experiment with different feature combinations and create new features based on domain knowledge.
3. **Model Selection and Tuning:** Explore various ML models and fine-tune hyperparameters for optimal performance.
4. **Ensemble Methods:** Implement ensemble methods like bagging and boosting to improve overall model performance.

### Application Proposals:

1. **Agriculture:** Aid farmers in planning activities like sowing, irrigation, and harvesting.
2. **Renewable Energy:** Predict production of wind and solar power for efficient grid management.
3. **Disaster Management:** Provide early warnings for severe weather conditions to facilitate timely evacuation.
4. **Climate Research:** Contribute to climate research by studying long-term weather patterns and climate change impacts.
5. **Recreation and Leisure:** Assist event organizers in planning outdoor events and help travelers plan vacations based on accurate weather predictions.




## 5. **Acknowledgments**

We would like to express our sincere gratitude to **Nguyễn Trọng Nghĩa**(https://github.com/ngaymai) for his valuable contributions to this project. His dedication and expertise significantly enhanced the development and implementation of the weather forecasting model. The collaborative effort and commitment to excellence demonstrated by Nguyễn Trọng Nghĩa have been instrumental in the success of this project.



[Nguyễn Trọng Nghĩa ](https://github.com/ngaymai)

Thank you for your hard work and commitment to advancing the field of weather forecasting through innovative solutions.

## 6. **GitHub Repository**

The complete project, including the codebase, documentation, and resources, can be found on our GitHub repository:

[Big Data for Weather Forecasting - GitHub](https://github.com/ngaymai/Big-data-for-weather-forecasting)

Feel free to explore the repository, provide feedback, and contribute to the ongoing development of this project.

Thank you for your interest and support!

---

*Note: Please make sure to replace placeholders such as "Nguyễn Trọng Nghĩa" with the correct names and details based on the actual contributors.*

## 7. References

1. [Kaggle: Historical Hourly Weather Data 2012-2017](https://www.kaggle.com/datasets/selfishgene/historical-hourly-weather-data)
2. [K-Nearest Neighbor (KNN) Algorithm](https://www.geeksforgeeks.org/k-nearest-neighbours/)
3. [Machine Learning in Weather Prediction and Climate Analyses](https://www.mdpi.com/2073-4433/13/2/180)
4. [Weather Forecasting on Pyspark using Big Data Techniques](https://github.com/Chinmaya083/Weather-Forecasting-using-Pyspark)
5. [Building a Weather Data Pipeline with PySpark, Prefect, and Google Cloud](https://arxiv.org/abs/2309.10808)