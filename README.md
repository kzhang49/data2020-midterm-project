# Overview
  Our data is a census tracts in New York City. It shows the income level, total population, race, poverty level and different types of jobs in New York City and surrounding area. We are trying to figure out which of these features affect the median household income and income per capita. We sought to predict the income level based on useful information like population, job positions and other useful features. In addition, we are trying to investigate these questions:
  - Which area has higher income per capita?
  - Which area has higher unemployment rate?
  - Can we integrate these useful features into some predictive models that would predict income level and income per capita in the future?
  - What is the relationship between race and median household income?

  We wanted to answer these questions after studying and visualizing this data.

# Exploratory Analysis
First, we explored the relationships between the features and the target: Income. We picked some features that we think are important, and draw graphs to better demonstrate the relationships. 

1) Income: The income is distributed as below.
  
![alt](https://i.imgur.com/0RmZxp9.png)
The five counties, Bronx, Kings, New York, Queens and Richmond are represented by label “1, 2, 3, 4, 5”. We can see that New York has highest income and the distribution of its income is more spread out than others. While Bronx and Richmond have relatively lower income. We can tell that County is a good candidate for the features we can use in the model.

2) Poverty and ChildPoverty: The Poverty and ChildPoverty are distributed as below.
![alt text](https://i.imgur.com/FoQQdtr.png)
![alt text](https://i.imgur.com/Km5oqIz.png)
We can see from the graphs that the shape of Poverty and ChildPoverty to Income are very similar. We could consider there would be a correlation between Poverty and ChildPoverty. And the confirmed our inference as following:

![alt text](https://i.imgur.com/C95WzQv.png)
There is a linear relationship between Poverty and ChildPoverty. We would consider remove one of the features in our model.

3) Service & Professional: The Service is distributed as below.
![alt text](https://i.imgur.com/0FRB7rY.png)
We can see that there seems a linear relationship between Service and Income. The lower % employed in service jobs, the higher the income is. People who work in service jobs tend to have lower salary. We infer that with higher % employed in professional jobs, the income should be higher, and we confirmed our thoughts as followed. We can see from the figure below that Professional and Income do have a positive relationship.
![alt text](https://i.imgur.com/o4t62r7.png)

4) Drive: The Drive is distributed as following.
![alt text](https://i.imgur.com/xA68cJi.png)
We can see that there is a positive relationship between % commuting along a car, van or truck and the income. It is easy to understand that people can afford of buying cars are more likely to be richer. The outliers are very likely to be the New York. Most people who live in New York do not have cars because driving is too difficult in Manhattan, but they still have high income so that they can afford of living in Manhattan.


# Methodology
  - **Data cleaning**: In the original data, there are some N/A values. If a row contains N/A value, we should delete that row.In addition, since some of variables in the original data contain factor values, we should change factor to numeric. Our data is clean after removing N/A values and changing factor values to numeric values.

  - **Data analysis**: We compute the correlation among all the features and targets to do the feature selection. Correlation can help us come up with an initial list of importance. The idea is that those features which have a high correlation with the dependent variable are strong predictors when used in a model. We eliminated the features that have low correlation with both **_Income_** and **_IncomePerCap_**. Those features are _Men_, _Women_, _TotalPop_, _Native_, _PrivateWork_, _Asian_, and _FamilyWork_. We also deleted some features that have very high correlation with one or more other features, such as _CensusTract_, _Borough_, _White_, _ChildPoverty_, _Transit_, _Employed_, _IncomePerCapErr_, and _IncomeErr_.

  - **Model**: We use these four models to train our data and to predict the median household income and income per capita. After that, we choose the best model based on the Mean Squared Error.
    - Simple Linear Regression
    - Ridge Regression
    - Lasso Regression
    - Stepwise Regression<br />
    
  - **Visualization**: We use census_tract_loc.csv which contains latitude, longitude, county and state to generate an interactive geo graph.

# Analysis
  - **Simple Linear Regression**
  We use simple linear regression to fit median of household income, the result and plot we get is:
![alt text](https://i.imgur.com/jHPqtOL.png)
![alt text](https://i.imgur.com/E2ta2uE.png)
The adjusted R-squared for linear regression is 0.8534, which indicates our linear model for the median of household income is relatively good.
  - **Ridge Regression**:
    - **Median of household income**
    After selecting 19 relevant features as our predictors, we would like to further improve our prediction by utilizing regularized term, lambda. We separated the dataset into training data and testing data, fitted ridge regression model onto the training data, and predicted the Income for testing data. Still utilizing the 19 relevant predictors,  we calculated the MSE as the criteria to determine the optimal prediction model. As a result, the MSE is 117,376,314 using a 5-fold cross validation process. 
    ![alt text](https://i.imgur.com/8wURzU0.png)
    - **Income per capita**
    At the same time, we fitted ridge regression on income per capita with the 19 predictors. We received an MSE of 34,693,520, which is smaller than the MSE on income. 
    ![alt text](https://i.imgur.com/TVLpCe9.png)
    
  - **Lasso Regression**:
    - **Median of household income**
    We used L2 regularization of ridge regression model previously, and we would like to compare the model with L1 regularization of lasso regression model, since different regularized terms affect predictions. In order to make the comparison, we again kept 19 predictors as our features. After a 5-fold cross validation, we determined the MSE is 106,552,141. Comparing the MSE with ridge regression, lasso regression is more accurate for Income prediction. The reason maybe that L2 regression penalizes large values disproportionately; however L1 regression is “indifferent” about the large values. Since the income for each geolocation is at least thousands or ten thousands, we are more likely to penalize income under ridge regression.
    ![alt text](https://i.imgur.com/KPP4uRE.png)
    - **Income per capita**
    We applied the same 19 predictors to lasso regression in order to predict for income per capita. The MSE is 32,693,923, which is again smaller than the MSE of ridge regression (34,693,520). Since income per capita is quite large as well, lasso performs slightly better than the ridge regression. 
    ![alt text](https://i.imgur.com/SqwLS6F.png)
    
  - **Stepwise Regression**:
    - **Median of household income**
    Stepwise method is an efficient way to find the significant predictors by using known trained data points. Upon fitting the key predictors onto the test data, we are able to predict the unknown Income level using these predictors. In detail, with the forward stepwise method, we selected the best subset of 11 predictors out of the total 19 predictors that have a greater impact on Income level. They are “County”,  “Hispanic”,  “Black”, “Citizen”,  “Poverty”, “ Professional”, “Drive”, “Walk”, “OtherTransp”, “WorkAtHome”,  and “PublicWork”. We applied cross validation and received a MSE of 210,167,539. However, without interaction terms, log transformation, and regularization terms, the MSE is more than 10 times larger comparing to MSE of lasso and ridge regression models. 
    - **Income per capita**
    For Income Per capita, we also duplicated the stepwise forward method utilizing the 19 predictors. The model displayed 15 most influential predictors: “ County”, “Hispanic”, “Black”, “Citizen”, “Poverty”, “Professional”, “Production”, “Carpool”,  “Walk”, “OtherTransp”, “WorkAtHome”, “MeanCommute”, “PublicWork”, “SelfEmployed”, and “Unemployment”. As a result, the optimal MSE is 168,289,557. Comparing to Income prediction, Income per capita has a lower MSE in stepwise forward model. The 5 additional predictors that are significant to Income per capita are “Production”, “Carpool”, “MeanCommute”, “SelfEmployed”, and “Unemployment”, and 1 insignificant predictor that is influential to Income above is “Drive”. 
    
    Comparing the MSE of these models, we choose Lasso regression to do the prediction.
    
# Visualization
  [**Click here to open map link**](https://kzhang49.github.io/data2020-midterm-project/map.html)


# Code
  [Visualization code](https://github.com/kzhang49/data2020-midterm-project/blob/master/geograph.Rmd)
  
  [Model code](https://github.com/kzhang49/data2020-midterm-project/blob/master/midterm_project.Rmd)
