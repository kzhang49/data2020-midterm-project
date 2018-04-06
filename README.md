# Overview
Our data is a census tracts in New York City. It shows the income level, total population, race, poverty level and different types of jobs in New York City and surrounding area. We are trying to figure out which of these features affect the median household income and income per capita. We sought to predict the income level based on useful information like population, job positions and other useful features. In addition, we are trying to investigate these questions:
- Which area has higher income per capita?
- Which area has higher unemployment rate?
- Can we integrate these useful features into some predictive models that would predict income level and income per capita in the future?
- What is the relationship between race and median household income?

We wanted to answer these questions after studying and visualizing this data.

# Exploratory Analysis


# Methodology
- **Data cleaning**: In the original data, there are some N/A values. If a row contains N/A value, we should delete that row.In addition, since some of variables in the original data contain factor values, we should change factor to numeric. Our data is clean after removing N/A values and changing factor values to numeric values.

- **Data analysis**: We compute the correlation among all the features and targets to do the feature selection. Correlation can help us come up with an initial list of importance. The idea is that those features which have a high correlation with the dependent variable are strong predictors when used in a model. We eliminated the features that have low correlation with both **_Income_** and **_IncomePerCap_**. Those features are _Men_, _Women_, _TotalPop_, _Native_, _PrivateWork_, _Asian_, and _FamilyWork_. We also deleted some features that have very high correlation with one or more other features, such as _CensusTract_, _Borough_, _White_, _ChildPoverty_, _Transit_, _Employed_, _IncomePerCapErr_, and _IncomeErr_.

- **Model**: We use these four models to train our data and to predict the median household income and income per capita. After that, we choose the best model based on the Mean Squared Error.
  - Simple Linear Regression
  - Ridge Regression
  - Lasso Regression
  - Stepwise Regression
  
- **Visualization**: We use census_tract_loc.csv which contains latitude, longitude, county and state to generate an interactive geo graph.

# Analysis

# Visualization
[**Click here to open map link**](https://kzhang49.github.io/data2020-midterm-project/map.html)

# Code
