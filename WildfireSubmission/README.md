## DOCUMENTATION / SUBMISSION NOTES

###Executive Summary:###

the general approach used to address the problem and the summary of insights and recommendations.
The approach taken to predict the area growth rate of a wildfire was to take input into account weather data, fire fuel sources. Different regression models were developed, but ultimately an XGBoost Regression model performed best overall with a root mean squared error of 9%. 


###Problem Statemen:t###

For our analysis of the 2019 wildfires, we aim to predict the area growth rate of a wildfire utilizing various features, including various weather conditions associated with the wildfire location. 

###Datasets Used:###

Three datasets were used for the analysis. A dataset with information related to the wildfire was taken as a main dataset (Wildland_Fire_Incident_Locations.csv). Then, a shape file of wildfire final perimeters. Both of the first two datasets are from the National Interagency Fire Center website. NASA (fire.csv) was used to define the points of fire, brightness, and much more. Finally, Open-Meteo API was used to obtain the 2019 weather data in the location and time period of the fires from the Wildland_Fire_Incident_Locations.csv. This API provided features including temperature (°F), soil temperature (°F) and soil moisture (m³/m³) at various depths, wind direction, wind speed (km/h), precipitation (mm), and cloud cover (%).

###Preprocessing Steps:###

Each individual dataset was preprocessed. The X and Y values in the Fire dataset were converted into coordinates which were used to merge the three datasets. Missing values and duplicate values were removed from the data. The data were sorted in terms of their coverage perimeter which was later used to determine the growth rate of the largest fire. If there were any gaps or holes in the polygon data, they were filled in. In addition, many wildfires had multiple rows of data, so we decided to compute the largest polygon representing the fire.
Regarding the weather data, the average weather metrics were determined for each wildfire over the recorded duration of the fire. 

###Data Exploration:###

The features, relative humidity, temperature, and wind speed, all violate normality, with relative humidity and wind speed having a right skewed distribution and temperature having a left skewed distribution. Furthermore, we analyzed the features from the weather to determine if any of the predictors have a strong correlation with each other. The following correlation heatmap reveals that the most correlated features among the weather data are temperature and soil temperatures. Additionally, dewpoint and temperature also have relatively high correlation with each other with a value around 0.85.


###Methodology:###

We chose to use XGBoost since our dataset contains 60 features and also included hourly weather data, and the computational cost would be higher for our methodology. XGBoost runs efficiently since it utilizes the gradient boosting method. The estimated time of training for sample dataset is demonstrated in our code. Additionally,  we utilized CatBoost to generate the importance of each feature as it is specifically designed to handle categorical data well.
Some of the methods we attempted using to predict wildfire area growth rate include linear models and LASSO. These methods did not produce a valid model as there were problems with multicollinearity and violations of the assumptions of normality and nonconstant variance in the residuals. We decided against utilizing neural networks because it made our model computationally heavy.


###Modeling and Analysis:###

Description of models or predictions derived from analysis, discussion of limitations and uncertainties, possible areas for further analysis. XGBoost: The machine learning technique XGBoost makes use of gradient boosting and decision trees. While decision tree-based algorithms are currently thought to perform best for structured/tabular data of small to medium size, artificial neural networks are typically the best option for prediction tasks involving unstructured input, such as photos or text. 
Consider XGBoost to be gradient boosting on "steroids" (Extreme Gradient Boosting is its name for a reason!). In order to produce better results with fewer computer resources and in the shortest amount of time, it is the ideal mix of software and hardware optimization techniques.

###Algorithm:### 

Load the dataset
Split the dataset into training and testing sets
Initialize the model parameters (e.g. number of trees, learning rate, max depth)
For each tree:
a. Calculate the gradients and hessians for each instance in the training set.
b. Train a decision tree on the gradients and hessians using the current model parameters.
c. Make predictions on the training set using the decision tree.
d. Update the model parameters based on the errors (e.g. using gradient descent).
    Make predictions on the testing set by combining the predictions of all the trees.
e. Evaluate the performance of the model using a suitable metric (e.g. accuracy, MSE).
Repeat steps 4-6 until the desired number of trees is reached or the performance on the testing set stops improving.

###CatBoost:### 

CatBoost is a gradient boosting method specifically designed for categorical data (but can be used to process for both numerical data) and makes use of symmetric trees. This resulted in a  testing performance of an R-squared value of 0.76, meaning that  a relatively high proportion of the variability in Y was explained by the predictors given a lower complexity in feature engineering. 


###Conclusions and Recommendations:### 

Real world data requires high computation which may be obtained through XGBoost or the CatBoost as they train the data efficiently. We recommend XGBoost for very large datasets since it’s more efficient computationally. For our purpose we predict the training time of the model  should be in minutes. In addition, CatBoost could take longer computational time than XGBoost; it can be useful with categorical data. The datasets used had high dimensionality which made it difficult to compute using the linear regression model. 

