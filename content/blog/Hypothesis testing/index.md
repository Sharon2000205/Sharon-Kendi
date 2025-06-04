---
title: "Hypothesis Testing"
subtitle: ""
excerpt: "Hypothesis testing is a statistical method used to determine if there is enough evidence to reject a null hypothesis (H0) in favor of an alternative hypothesis (𝐻𝑎 ). By analyzing sample data, the process involves setting a significance level, calculating a test statistic, and comparing it to a critical value or P-value to make data-driven decisions. Common tests include t-tests, z-tests, and chi-square tests, applied in diverse fields to validate assumptions and drive conclusions."
date: 2024-11-29
author: "Kelvin Kiprono"
draft: false
# layout options: single, single-sidebar
layout: single
categories:
- R Data Analysis
---
## T-TEST 

The t tests are based on an assumption that data come from the normal distribution. In the one-sample case we thus have data x1, . . . , xn assumed to be independent realizations of random variables with distribution N(µ, σ2), which denotes the normal distribution with mean µ and variance σ2, and we wish to test the null hypothesis that µ = µ0. We canestimate the parameters µ and σ by the empirical mean x¯ and standard deviations, although we must realize that we could never pinpoint their values exactly.

Here is an example concerning daily energy intake in kJ for 11 women


``` r
daily.intake <- c(5260,5470,5640,6180,6390,6515,
+ 6805,7515,7515,8230,8770)
```
Let us first look at some simple summary statistics, even though these are hardly necessary for such a small data set


``` r
mean(daily.intake)
```

```
## [1] 6753.636
```

``` r
sd(daily.intake)
```

```
## [1] 1142.123
```

``` r
quantile(daily.intake)
```

```
##   0%  25%  50%  75% 100% 
## 5260 5910 6515 7515 8770
```
You might wish to investigate whether the women’s energy intake deviates systematically from a recommended value of 7725 kJ. Assuming that data come from a normal distribution, the object is to test whether this
distribution might have mean µ = 7725. This is done with t.test as follows

``` r
t.test(daily.intake,mu=7725)
```

```
## 
## 	One Sample t-test
## 
## data:  daily.intake
## t = -2.8208, df = 10, p-value = 0.01814
## alternative hypothesis: true mean is not equal to 7725
## 95 percent confidence interval:
##  5986.348 7520.925
## sample estimates:
## mean of x 
##  6753.636
```
You can immediately see that p < 0.05 and thus that (using the customary 5% level of significance) data deviate significantly from the hypothesis that the mean is 7725.

**alternative hypothesis: true mean is not equal to 7725**

This contains two important pieces of information:
 - (a) the value wewanted to test whether the mean could be equal to (7725 kJ) 
 - (b) that the test is two-sided (“not equal to”)
 
 **95 percent confidence interval:**
**5986.348 7520.925**

This is a 95% confidence interval for the true mean; that is, the set of (hypothetical) mean values from which the data do not deviate significantly.
It is based on inverting the t test by solving for the values of µ0 that cause t to lie within its acceptance region.

The function t.test has a number of optional arguments, three of which are relevant in one-sample problems. We have already seen the use of mu to specify the mean value µ under the null hypothesis (default is mu=0). In
addition, you can specify that a one-sided test is desired against alternatives greater than µ by using alternative="greater" or alternatives less than µ using alternative="less". The third item that can be specified is the confidence level used for the confidence intervals; you would write conf.level=0.99 to get a 99% interval.

## WILCOXON SIGNED-RANK TEST
For the one-sample Wilcoxon test, the procedure is to subtract the theoretical mu=0 and rank the differences according to their numerical value,ignoring the sign, and then calculate the sum of the positive or negative ranks. The point is that, assuming only that the distribution is symmetric around µ0, the test statistic corresponds to selecting each number from 1 to n with probability 1/2 and calculating the sum. The distribution of the test statistic can be calculated exactly, at least in principle. It becomes computationally excessive in large samples, but the distribution is then very
well approximated by a normal distribution.

**Practical application of the Wilcoxon signed-rank test is done almost exactly like the t test:**

``` r
wilcox.test(daily.intake, mu=7725)
```

```
## Warning in wilcox.test.default(daily.intake, mu = 7725): cannot compute exact
## p-value with ties
```

```
## 
## 	Wilcoxon signed rank test with continuity correction
## 
## data:  daily.intake
## V = 8, p-value = 0.0293
## alternative hypothesis: true location is not equal to 7725
```
The Wilcoxon tests are susceptible to the problem of ties, where several observations share the same value. In such cases, you simply use the average of the tied ranks; for example, if there are four identical values corresponding to places 6 to 9, they will all be assigned the value 7.5. This is not a problem for the large-sample normal approximations, but the exact small-sample distributions become much more difficult to calculate and wilcox.test cannot do so.
- The test statistic V is the sum of the positive ranks.
- The function wilcox.test takes arguments mu and alternative,just like t.test.

#TWO SAMPLE T TEST
The two-sample t test is used to test the hypothesis that two samples may be assumed to come from distributions with the same mean.
The theory for the two-sample t test is not very different in principle from that of the one-sample test. Data are now from two groups, x11, . . . , x1n1 and x21, . . . , x2n2
, which we assume are sampled from the normal distributions N(µ1, σ1^2) and N(µ2, σ2^2), and it is desired to test the null hypothesis µ1 = µ2.

# Example

``` r
library(ISwR)
```

```
## Warning: package 'ISwR' was built under R version 4.4.2
```

``` r
attach(energy)
energy
```

```
##    expend stature
## 1    9.21   obese
## 2    7.53    lean
## 3    7.48    lean
## 4    8.08    lean
## 5    8.09    lean
## 6   10.15    lean
## 7    8.40    lean
## 8   10.88    lean
## 9    6.13    lean
## 10   7.90    lean
## 11  11.51   obese
## 12  12.79   obese
## 13   7.05    lean
## 14  11.85   obese
## 15   9.97   obese
## 16   7.48    lean
## 17   8.79   obese
## 18   9.69   obese
## 19   9.68   obese
## 20   7.58    lean
## 21   9.19   obese
## 22   8.11    lean
```
The factor stature contains the group and the numeric variable expend the energy expenditure in mega-Joules.The object is to see whether there is a shift in level between the two groups,so we apply a t test as follows:

``` r
t.test(expend~stature)
```

```
## 
## 	Welch Two Sample t-test
## 
## data:  expend by stature
## t = -3.8555, df = 15.919, p-value = 0.001411
## alternative hypothesis: true difference in means between group lean and group obese is not equal to 0
## 95 percent confidence interval:
##  -3.459167 -1.004081
## sample estimates:
##  mean in group lean mean in group obese 
##            8.066154           10.297778
```
- The use of the tilde (~) operator to specify that expend is described by stature.
The confidence interval is for the difference in means and does not contain 0, which is in accordance with the p-value indicating a significant difference at the 5% level.

# Comparison of variances
R provides the var.test function for thatpurpose, implementing an F test on the ratio of the group variances.

``` r
var.test(expend~stature)
```

```
## 
## 	F test to compare two variances
## 
## data:  expend by stature
## F = 0.78445, num df = 12, denom df = 8, p-value = 0.6797
## alternative hypothesis: true ratio of variances is not equal to 1
## 95 percent confidence interval:
##  0.1867876 2.7547991
## sample estimates:
## ratio of variances 
##           0.784446
```
The test is not significant, so there is no evidence against the assumption that the variances are identical. However, the confidence interval is very wide. For small data sets such as this one, the assumption of constant variance is largely a matter of belief.

# TWO-SAMPLE WILCOXON TEST
The two-sample Wilcoxon test is based on replacing the data by their rank (without regard to grouping) and calculating the sum of the ranks in one group, thus reducing the problem to one of sampling n1 values without replacement from the numbers 1 to n1 + n2.

``` r
wilcox.test(expend~stature)
```

```
## Warning in wilcox.test.default(x = DATA[[1L]], y = DATA[[2L]], ...): cannot
## compute exact p-value with ties
```

```
## 
## 	Wilcoxon rank sum test with continuity correction
## 
## data:  expend by stature
## W = 12, p-value = 0.002122
## alternative hypothesis: true location shift is not equal to 0
```
# PAIRED T TEST
Paired tests are used when there are two measurements on the same experimental unit.The theory is essentially based on taking differences and thus reducing the problem to that of a one-sample test.i.e post - pre
- We are going to use intake(pre- and postmenstrual energy intake in a group of women) data from ISwR package.
The point is that the same 11 women are measured twice, so it makes sense to look at individual differences


``` r
attach(intake)
intake
```

```
##     pre post
## 1  5260 3910
## 2  5470 4220
## 3  5640 3885
## 4  6180 5160
## 5  6390 5645
## 6  6515 4680
## 7  6805 5265
## 8  7515 5975
## 9  7515 6790
## 10 8230 6900
## 11 8770 7335
```
The point is that the same 11 women are measured twice, so it makes sense to look at individual differences

``` r
post-pre
```

```
##  [1] -1350 -1250 -1755 -1020  -745 -1835 -1540 -1540  -725 -1330 -1435
```
All the women have a lower energy intake postmenstrually than premenstrually.The paired t test is obtained as follows

``` r
t.test(pre,post,paired = TRUE)
```

```
## 
## 	Paired t-test
## 
## data:  pre and post
## t = 11.941, df = 10, p-value = 3.059e-07
## alternative hypothesis: true mean difference is not equal to 0
## 95 percent confidence interval:
##  1074.072 1566.838
## sample estimates:
## mean difference 
##        1320.455
```
- You have to specify *paired-T*
