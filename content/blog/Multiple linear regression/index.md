---
title: "Multiple Linear Regression"
subtitle: ""
excerpt: ""
date: 2024-11-13
author: "Kelvin Kiprono"
draft: false
# layout options: single, single-sidebar
layout: single
categories:
- Linear Regression
---

Multiple Linear Regression (MLR) is a statistical technique used to model the relationship between a dependent variable and two or more independent variables. It extends simple linear regression by allowing multiple predictors, making it useful for more complex data where a single variable does not explain the outcome adequately.

## Formula for Multiple Linear Regression

The general formula for a multiple linear regression model is:

**𝑌 = 𝛽0 + 𝛽1𝑋1 + 𝛽2𝑋2 + ⋯ +𝛽𝑛𝑋𝑛 + 𝜖**
Where:

 - Y = Dependent variable (the outcome you're trying to predict)
 - β0 = Intercept (the value of 𝑌 when all 𝑋𝑖are 0)
 - β 1,β 2 ,…,β n = Coefficients (show the impact of each independent variable on the dependent variable)
 - X 1,X 2 ,…,X n = Independent variables (predictors or features)
 - ϵ = Error term (captures the variation in 𝑌 not explained by the independent variables)
 
## Assumptions of Multiple Linear Regression  

- Linearity: The relationship between the dependent variable and the independent variables is linear.
- Independence: The observations are independent of each other.
- Homoscedasticity: The variance of errors is constant across all levels of the independent variables.
- Normality of Errors: The residuals (errors) of the model are normally distributed.
- No multicollinearity: The independent variables are not highly correlated with each other.

## Steps for Fitting a Multiple Linear Regression Model in R:

- Prepare the Data: Ensure that the data is clean and appropriately formatted.

   - For example, check for missing values and outliers.
   
## Fit the Model 

Use the lm() function in R to fit a multiple linear regression model.

- model <- lm(dependent_variable ~ independent_variable1 + independent_variable2 + ..., data = your_data)
- summary(model)

## Interpret the Results: 

The summary(model) will give you a summary of the model's coefficients, significance levels, R-squared, and residuals.

- Coefficients: These tell you the magnitude and direction of the relationship between each predictor and the dependent variable.
- R-squared: Represents the proportion of the variance in the dependent variable that is explained by the independent variables.
- p-values: Help determine the statistical significance of each predictor.

## Check Assumptions:

Residuals vs Fitted Plot: Check for homoscedasticity.
- Q-Q Plot: Check if residuals follow a normal distribution.
- VIF (Variance Inflation Factor): To check for multicollinearity (high VIF suggests collinearity).

### Example in R:
**Note**
The regression analysis presented below is based on a sample example and is intended solely for educational and illustrative purposes. The interpretations and recommendations made here should not be generalized to real-world datasets without careful consideration of the specific context, data characteristics, and additional model diagnostics. For actual data, it's essential to verify the assumptions, check for multicollinearity, and possibly refine the model through techniques like increasing the sample size.

Let’s say we have a dataset where we want to predict the price of a house based on square footage (sqft), the number of bedrooms (bedrooms), and the age of the house (age).


``` r
data <- data.frame(
  price = c(200000, 250000, 300000, 350000, 400000),
  sqft = c(1500, 1800, 2200, 2500, 3000),
  bedrooms = c(3, 3, 4, 4, 5),
  age = c(10, 15, 20, 5, 8)
)
```

``` r
# Fit the multiple linear regression model
model <- lm(price ~ sqft + bedrooms + age, data = data)
```


``` r
# Get the model summary
summary(model)
```

```
## 
## Call:
## lm(formula = price ~ sqft + bedrooms + age, data = data)
## 
## Residuals:
##       1       2       3       4       5 
##  -655.8 -3716.1  3570.4  5173.4 -4371.9 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)
## (Intercept)  21786.65   24865.99   0.876    0.542
## sqft           172.98      31.18   5.548    0.114
## bedrooms    -27645.00   21171.41  -1.306    0.416
## age            233.17     821.15   0.284    0.824
## 
## Residual standard error: 8536 on 1 degrees of freedom
## Multiple R-squared:  0.9971,	Adjusted R-squared:  0.9883 
## F-statistic:   114 on 3 and 1 DF,  p-value: 0.06871
```
## Model Overview:

- Formula: The model tries to predict price based on three independent variables: sqft, bedrooms, and age.

## Coefficients:

Each coefficient tells you how much the dependent variable (price) is expected to change for a one-unit change in the predictor variable, while holding other variables constant.

- Intercept: The intercept is 21,786.65. This means that when sqft, bedrooms, and age are all zero, the predicted price would be 21,786.65 (though this interpretation might not make sense in a real-world context, as having zero square footage, bedrooms, or age is unrealistic).

- sqft (172.98): The price increases by approximately 172.98 for each additional square foot, assuming bedrooms and age stay constant. However, the p-value for sqft is 0.114, which is greater than 0.05, indicating that this variable may not be statistically significant at the 5% level.

- bedrooms (-27,645.00): The price decreases by 27,645 for each additional bedroom, assuming sqft and age are held constant. The p-value of 0.416 is much greater than 0.05, suggesting that this predictor is not statistically significant either.

- age (233.17): The price increases by 233.17 for each additional year of age, assuming sqft and bedrooms are constant. The p-value of 0.824 is very high, indicating that this predictor is also not statistically significant.

## Model Statistics:

- Residual Standard Error (8536): This measures the typical size of the residuals. It tells you the standard deviation of the residuals. A higher value suggests that the model is not fitting the data well.

- R-squared (0.9971): This indicates that 99.71% of the variance in the dependent variable (price) is explained by the independent variables (sqft, bedrooms, and age). While this seems very high, it's important to note that a high R-squared can sometimes be misleading, especially with a small sample size.

- Adjusted R-squared (0.9883): This is a more reliable measure of model fit when you have multiple predictors, as it accounts for the number of predictors. The adjusted R-squared of 0.9883 still indicates a very good fit, but the large gap between R-squared and adjusted R-squared suggests that adding more predictors (such as bedrooms and age) might not be improving the model significantly.

- F-statistic (114): This tests whether the model as a whole is statistically significant. The associated p-value of 0.06871 is just above the 0.05 threshold, meaning the overall model isn't statistically significant at the 5% level. This could suggest that at least one predictor (or possibly all of them) is not contributing meaningfully to the model.

## Interpretation and Recommendations:

- The high R-squared value could be a result of overfitting, especially if your dataset is small. The adjusted R-squared is more conservative but still very high.

- None of the predictors (sqft, bedrooms, age) have p-values less than 0.05, suggesting that none of them are statistically significant at the 5% level. This could indicate multicollinearity, or an insufficient number of observations to draw conclusions.

## Conclusion

Multiple linear regression is a powerful tool for modeling the relationship between a dependent variable and multiple independent variables. By carefully interpreting the coefficients and assessing the model assumptions, you can use MLR for prediction and inference in various domains, such as economics, social sciences, and business.
