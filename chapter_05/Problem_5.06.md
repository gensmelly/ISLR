---
title: "Problem 5.6"
author: "Yuwen Tan"
output: html_document
---

### (a) Logistic regression

```r
library(ISLR)
glm.fit <- glm(default~income+balance,data = Default,family = binomial)
summary(glm.fit)
```

```
## 
## Call:
## glm(formula = default ~ income + balance, family = binomial, 
##     data = Default)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -2.4725  -0.1444  -0.0574  -0.0211   3.7245  
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept) -1.154e+01  4.348e-01 -26.545  < 2e-16 ***
## income       2.081e-05  4.985e-06   4.174 2.99e-05 ***
## balance      5.647e-03  2.274e-04  24.836  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 2920.6  on 9999  degrees of freedom
## Residual deviance: 1579.0  on 9997  degrees of freedom
## AIC: 1585
## 
## Number of Fisher Scoring iterations: 8
```

### (b) New function boot.fn

```r
boot.fn <- function(input,index) {
  glm.fit <- glm(default~income+balance,data = input,family = binomial,subset = index)
  return(coef(glm.fit))
}
```

### (c) Estimate standard errors of the coefficients

```r
library(boot)
set.seed(1)
boot(Default,boot.fn,R=1000)
```

```
## 
## ORDINARY NONPARAMETRIC BOOTSTRAP
## 
## 
## Call:
## boot(data = Default, statistic = boot.fn, R = 1000)
## 
## 
## Bootstrap Statistics :
##          original        bias     std. error
## t1* -1.154047e+01 -8.008379e-03 4.239273e-01
## t2*  2.080898e-05  5.870933e-08 4.582525e-06
## t3*  5.647103e-03  2.299970e-06 2.267955e-04
```

The results are actually very close to each other.

### (d) Compare the estimates

The estimates for the standard errors are actually very close between these two methods. The bootstrap function may be resulting in a little bit smaller estimated standard errors.
