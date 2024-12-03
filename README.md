# Rico_Martin_Sitorus_Data_Science_Purwadhika_Capstone3_Project
This repository contains the machine learning model to predict the apartment price

BUSINESS CONTEXT : 

- Apartments serve as a primary solution to housing needs in urban environments, especially due to limited land availability and high levels of business activity.
- Apartment prices are significantly influenced by various internal factors (e.g., size, facilities within the apartment) and external factors (e.g., proximity to public facilities and transportation).
- The goal of this analysis is to understand and predict apartment prices to help property owners and buyers set prices that align with market conditions

Evaluation metrics :

- MSE to check the error in quadratic terms, this metric is usefull when evaluating the effect of large residual data to overall model. The larger MSE, means the larger difference (gap) between test and residual. This metrics used when we tune the parameters to see which parameters are suitable to minimize the large error.
- MAE is used to check the absolut difference between actual test set and predicted values, it’s quite the same with MSE, but the MSE will give us more intuitive approach, as this fact show the average distance/gap between actual test and predicted data.
- MAPE is used to see the difference of predicted data vs actual test data in percent. This is usefull fact especially for the stakeholders as they can know that the accuracy of the model may predict the price around X% difference than the actual.
- R-squared, this facts can tell us how good the model to represent the variance of the data.

Data Preprocessing :

- In processing the data we delete the duplicates as these data have no impact to the normality (distribution), hence maintaining these duplicates will not give any usefull additional informations and tend to consume our storage more.
- We split the test and train data before doing any encoding and scaling, this method chose to minimize the information leakage to the test data.
- The encoding used is get.dummies from pandas, considering the categorical data is not more than 5 categories, hence the dummies already sufficient.
- The scaling happened for Year and Size parameters, as these parameters scale are comparably much higher compared to other variables.
- The scaling method used is Min-Max scaller, this method chose considering the distribution of the parameters that is not normally distributed and tend to right-skewed.


Model:

- Based on the data distribution and considering the outlier, we can set the confident level for our model to work the best when the data is within the range of Price under 521,900 WON. Year Built of apartment from 1980 to 2015, and size of apartment between 107 - 1803 sqft
- We tried to utilize several methods, the linear model and the tree-based regressor.
- The model started from Linear Model utilizing simple linear regeression, Ridge and Lasso.
- Our data show multicollinearity between the variables, hence we try to conside tree-based regressor that are able to handle multicollinearity better.
- From our oubservation, the Ridge with hyperparameter tuning is the best for Linear Model, while XGBoost is the best model for tree-based regressor, as the tree
- Among these models, we found that the XGboost regressor is the best model to predict the price
- XGboost regressor able to represent around 79.1% of the data variances with the price accuracy about 19.6% (the price can varies around 19.6% from the actual price)

Recommendations : 

Despite of the XGBoost model able to show more accuracy, we still obseve the heteroskedasticity observed in our regression results is likely caused by a non-normal distribution of the target variable, non-linear relationships not fully captured by the model, or the presence of significant outliers.

Several things that we can consider to increase further our model : 
- Try to make more sampling data, the more the sampling data, hopefully the data become more normally distributed.
- Try to drop the significant outliers that may dragging up our predicted value hence affecting the MSE
- We understand that the size, price scale varies so much, for example in our range itself the price varies from <500 up to > 600,000 Won, and the size varies from <50 sqft up to >2,000 sqft. Tranforming these variables into log scale can help to minimize the variance of the data. We can transform them when modeling, fitting and predicting the data, after the prediction obtained, we can transformed back the log into numerical scale.
- We can try to consider to have more robust variables, for example, the variable number of other facilities, it's not clear what type of facilities captured. If we have more detailed iformation, like the number of shopping mall or minimarket, we can use our domain knowldge better to choose the more important features.
