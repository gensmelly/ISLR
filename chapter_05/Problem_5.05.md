---
title: "Problem 5.5"
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

### (b) Validation set approach

```r
set.seed(1)
train <- sample(1:length(Default$default),length(Default$default)/2)
glm.fit <- glm(default~income+balance,data = Default,family = binomial,subset = train)
summary(glm.fit)
```

```
## 
## Call:
## glm(formula = default ~ income + balance, family = binomial, 
##     data = Default, subset = train)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -2.3583  -0.1268  -0.0475  -0.0165   3.8116  
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept) -1.208e+01  6.658e-01 -18.148   <2e-16 ***
## income       1.858e-05  7.573e-06   2.454   0.0141 *  
## balance      6.053e-03  3.467e-04  17.457   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 1457.0  on 4999  degrees of freedom
## Residual deviance:  734.4  on 4997  degrees of freedom
## AIC: 740.4
## 
## Number of Fisher Scoring iterations: 8
```

```r
glm.probs <- predict(glm.fit,Default[-train,],type = "response")
glm.pred <- rep("No",length(glm.probs))
glm.pred[glm.probs>0.5] <- "Yes"
mean(glm.pred!=Default$default[-train])
```

```
## [1] 0.0286
```

### (c) Three more splits of the observations

```r
for (i in 1:3) {
  train <- sample(1:length(Default$default),length(Default$default)/2)
  glm.fit <- glm(default~income+balance,data = Default,family = binomial,subset = train)
  print(summary(glm.fit))
  glm.probs <- predict(glm.fit,Default[-train,],type = "response")
  glm.pred <- rep("No",length(glm.probs))
  glm.pred[glm.probs>0.5] <- "Yes"
  print(mean(glm.pred!=Default$default[-train]))
}
```

```
## 
## Call:
## glm(formula = default ~ income + balance, family = binomial, 
##     data = Default, subset = train)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -2.1891  -0.1573  -0.0605  -0.0226   3.6623  
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept) -1.136e+01  5.982e-01 -18.987  < 2e-16 ***
## income       2.265e-05  6.947e-06   3.259  0.00112 ** 
## balance      5.530e-03  3.142e-04  17.600  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 1483.83  on 4999  degrees of freedom
## Residual deviance:  829.05  on 4997  degrees of freedom
## AIC: 835.05
## 
## Number of Fisher Scoring iterations: 8
## 
## [1] 0.0236
## 
## Call:
## glm(formula = default ~ income + balance, family = binomial, 
##     data = Default, subset = train)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -2.3008  -0.1271  -0.0479  -0.0164   3.5590  
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept) -1.237e+01  6.649e-01 -18.605  < 2e-16 ***
## income       2.566e-05  7.175e-06   3.577 0.000348 ***
## balance      6.042e-03  3.452e-04  17.502  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 1463.7  on 4999  degrees of freedom
## Residual deviance:  739.5  on 4997  degrees of freedom
## AIC: 745.5
## 
## Number of Fisher Scoring iterations: 8
## 
## [1] 0.028
## 
## Call:
## glm(formula = default ~ income + balance, family = binomial, 
##     data = Default, subset = train)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -2.1185  -0.1446  -0.0580  -0.0222   3.6735  
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept) -1.142e+01  6.128e-01 -18.628  < 2e-16 ***
## income       2.383e-05  7.184e-06   3.317 0.000908 ***
## balance      5.471e-03  3.123e-04  17.519  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 1436.67  on 4999  degrees of freedom
## Residual deviance:  780.85  on 4997  degrees of freedom
## AIC: 786.85
## 
## Number of Fisher Scoring iterations: 8
## 
## [1] 0.0268
```

The results are actually very close to each other.

### (d) Validation set approach with the predictor of student

```r
set.seed(1)
train <- sample(1:length(Default$default),length(Default$default)/2)
glm.fit <- glm(default~income+balance+student,data = Default,family = binomial,subset = train)
summary(glm.fit)
```

```
## 
## Call:
## glm(formula = default ~ income + balance + student, family = binomial, 
##     data = Default, subset = train)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -2.2905  -0.1260  -0.0465  -0.0161   3.7715  
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept) -1.147e+01  7.562e-01 -15.164   <2e-16 ***
## income       2.433e-06  1.256e-05   0.194    0.846    
## balance      6.124e-03  3.525e-04  17.373   <2e-16 ***
## studentYes  -5.608e-01  3.473e-01  -1.615    0.106    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 1456.95  on 4999  degrees of freedom
## Residual deviance:  731.81  on 4996  degrees of freedom
## AIC: 739.81
## 
## Number of Fisher Scoring iterations: 8
```

```r
glm.probs <- predict(glm.fit,Default[-train,],type = "response")
glm.pred <- rep("No",length(glm.probs))
glm.pred[glm.probs>0.5] <- "Yes"
mean(glm.pred!=Default$default[-train])
```

```
## [1] 0.0288
```

Including a dummy variable of student won't lead to a reduction in the test error rate.
