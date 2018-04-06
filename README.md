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
![alt text](https://i.imgur.com/v3JdaP3.png)

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

# Visualization
  [**Click here to open map link**](https://kzhang49.github.io/data2020-midterm-project/map.html)


# Code
  [Visualization code](https://github.com/kzhang49/data2020-midterm-project/blob/master/geograph.Rmd)
  
  [Model code](https://github.com/kzhang49/data2020-midterm-project/blob/master/midterm_project.Rmd)
