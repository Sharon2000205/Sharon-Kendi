---
title: "Simple Linear Regression"
subtitle: ""
excerpt: "Linear regression is a statistical method used to model the relationship between a dependent variable and one or more independent variables. Its main goal is to find the best-fitting linear equation that can predict the dependent variable based on the independent variables."
date: 2024-09-24
author: "Sharon Kendi"
draft: false
# layout options: single, single-sidebar
layout: single
categories:
- R Data Analysis
---
Simple Linear Regression: Involves one independent variable and one dependent variable, modeled as:

𝑦=𝛽0 +𝛽1𝑥+𝜖

where :

- y is the dependent variable, 

- x is the independent variable, 

- 𝛽0 is the intercept, 

- β 1 is the slope, and 

- ϵ is the error term.

## Assumptions

- Linearity: The relationship between the dependent and independent variables should be linear.
- Independence: Observations should be independent of each other.
- Homoscedasticity: The variance of error terms should be constant across all levels of the - independent variable.
- Normality: The residuals (errors) should be normally distributed.

## Basic Simple Linear Regression

``` r
# Load necessary data or generate sample data
x <- c(10, 20, 30, 40, 50)
y <- c(15, 30, 45, 50, 65)
```
## Fit the linear regression model

``` r
model <- lm(y ~ x)
```

## View the summary to understand model performance


``` r
summary(model)
```

```
## 
## Call:
## lm(formula = y ~ x)
## 
## Residuals:
##          1          2          3          4          5 
## -2.000e+00  1.000e+00  4.000e+00 -3.000e+00 -1.665e-15 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)   
## (Intercept)    5.000      3.317   1.508  0.22878   
## x              1.200      0.100  12.000  0.00125 **
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.162 on 3 degrees of freedom
## Multiple R-squared:  0.9796,	Adjusted R-squared:  0.9728 
## F-statistic:   144 on 1 and 3 DF,  p-value: 0.001245
```

## Plot and add regression line

``` r
plot(x, y, main = "Regression Example", xlab = "X values", ylab = "Y values", pch = 16)
abline(model, col = "red", lwd = 2)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

## Predict new values

``` r
new_data <- data.frame(x = c(25, 35))
predictions <- predict(model, newdata = new_data)
print(predictions)
```

```
##  1  2 
## 35 47
```




