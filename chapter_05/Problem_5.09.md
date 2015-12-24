---
title: "Problem 5.9"
author: "Yuwen Tan"
output: html_document
---

### (a) Estimate the population mean of medv

```r
library(MASS)
mean(Boston$medv)
```

```
## [1] 22.53281
```

### (b) Estimate the standard error

```r
sd(Boston$medv)/sqrt(length(Boston$medv))
```

```
## [1] 0.4088611
```

### (c) Estimate the standard error by bootstrap

```r
library(boot)
mean.fn <- function(data,index) {
  return(mean(data[index]))
}
set.seed(1)
Boot <- boot(Boston$medv,mean.fn,R=1000)
Boot
```

```
## 
## ORDINARY NONPARAMETRIC BOOTSTRAP
## 
## 
## Call:
## boot(data = Boston$medv, statistic = mean.fn, R = 1000)
## 
## 
## Bootstrap Statistics :
##     original      bias    std. error
## t1* 22.53281 0.008517589   0.4119374
```

The result is close to the answer in (b), but bootstrap is a little larger.

### (d) Confidence interval

```r
Boot$t0-2*sd(Boot$t)
```

```
## [1] 21.70893
```

```r
Boot$t0+2*sd(Boot$t)
```

```
## [1] 23.35668
```

```r
t.test(Boston$medv)
```

```
## 
## 	One Sample t-test
## 
## data:  Boston$medv
## t = 55.111, df = 505, p-value < 2.2e-16
## alternative hypothesis: true mean is not equal to 0
## 95 percent confidence interval:
##  21.72953 23.33608
## sample estimates:
## mean of x 
##  22.53281
```

These results are close, but bootstrap is a little larger.

### (e) Estimate the population median of medv

```r
median(Boston$medv)
```

```
## [1] 21.2
```

### (f) Estimate the standard error by bootstrap

```r
median.fn <- function(data,index) {
  return(median(data[index]))
}
set.seed(1)
boot(Boston$medv,median.fn,R=1000)
```

```
## 
## ORDINARY NONPARAMETRIC BOOTSTRAP
## 
## 
## Call:
## boot(data = Boston$medv, statistic = median.fn, R = 1000)
## 
## 
## Bootstrap Statistics :
##     original   bias    std. error
## t1*     21.2 -0.01615   0.3801002
```

### (g) Estimate the tenth percentile of medv

```r
quantile(Boston$medv,0.1)
```

```
##   10% 
## 12.75
```

### (h) Estimate the standard error by bootstrap

```r
quantile.fn <- function(data,index) {
  return(quantile(data[index],0.1))
}
set.seed(1)
boot(Boston$medv,quantile.fn,R=1000)
```

```
## 
## ORDINARY NONPARAMETRIC BOOTSTRAP
## 
## 
## Call:
## boot(data = Boston$medv, statistic = quantile.fn, R = 1000)
## 
## 
## Bootstrap Statistics :
##     original  bias    std. error
## t1*    12.75 0.01005    0.505056
```
