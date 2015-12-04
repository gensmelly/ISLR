---
title: "Problem 3.12"
author: "Yuwen Tan"
output: html_document
---

### (a) To make the coefficient estimates the same, we need to have sum(x\*x) equal to sum(y\*y)

### (b) Example of different coefficient estimates

```r
x <- seq(1,100,length.out = 100)
y <- seq(101,200,length.out = 100)
lm.fit.x <- lm(y ~ x+0)
summary(lm.fit.x)
```

```
## 
## Call:
## lm(formula = y ~ x + 0)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -49.25 -12.31  24.63  61.57  98.51 
## 
## Coefficients:
##   Estimate Std. Error t value Pr(>|t|)    
## x  2.49254    0.08574   29.07   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 49.88 on 99 degrees of freedom
## Multiple R-squared:  0.8951,	Adjusted R-squared:  0.8941 
## F-statistic:   845 on 1 and 99 DF,  p-value: < 2.2e-16
```

```r
lm.fit.y <- lm(x ~ y+0)
summary(lm.fit.y)
```

```
## 
## Call:
## lm(formula = x ~ y + 0)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -35.272 -19.410  -3.548  12.313  28.175 
## 
## Coefficients:
##   Estimate Std. Error t value Pr(>|t|)    
## y  0.35912    0.01235   29.07   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 18.93 on 99 degrees of freedom
## Multiple R-squared:  0.8951,	Adjusted R-squared:  0.8941 
## F-statistic:   845 on 1 and 99 DF,  p-value: < 2.2e-16
```

### (c) Example of same coefficient estimates

```r
x <- seq(1,100,length.out = 100)
y <- seq(-100,-1,length.out = 100)
lm.fit.x <- lm(y ~ x+0)
summary(lm.fit.x)
```

```
## 
## Call:
## lm(formula = y ~ x + 0)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -99.49 -62.18 -24.87  12.44  49.75 
## 
## Coefficients:
##   Estimate Std. Error t value Pr(>|t|)    
## x  -0.5075     0.0866   -5.86 6.09e-08 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 50.37 on 99 degrees of freedom
## Multiple R-squared:  0.2575,	Adjusted R-squared:   0.25 
## F-statistic: 34.34 on 1 and 99 DF,  p-value: 6.094e-08
```

```r
lm.fit.y <- lm(x ~ y+0)
summary(lm.fit.y)
```

```
## 
## Call:
## lm(formula = x ~ y + 0)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -49.75 -12.44  24.87  62.18  99.49 
## 
## Coefficients:
##   Estimate Std. Error t value Pr(>|t|)    
## y  -0.5075     0.0866   -5.86 6.09e-08 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 50.37 on 99 degrees of freedom
## Multiple R-squared:  0.2575,	Adjusted R-squared:   0.25 
## F-statistic: 34.34 on 1 and 99 DF,  p-value: 6.094e-08
```
