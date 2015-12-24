---
title: "Problem 5.7"
author: "Yuwen Tan"
output: html_document
---

### (a) Logistic regression

```r
library(ISLR)
glm.fit1 <- glm(Direction~Lag1+Lag2,data = Weekly,family = binomial)
```

### (b) Logistic regression except the first observation

```r
glm.fit2 <- glm(Direction~Lag1+Lag2,data = Weekly,family = binomial,subset = c(-1))
```

### (c) Predict the first observation

```r
glm.probs <- predict(glm.fit2,Weekly[1,],type = "response")
if (glm.probs>0.5) glm.pred <- "Up" else glm.pred <- "Down"
glm.pred
```

```
## [1] "Up"
```

```r
toString(Weekly$Direction[1])
```

```
## [1] "Down"
```

### (d) Loop test

```r
error.indicator <- rep(1,length(Weekly$Direction))
for (i in 1:length(Weekly$Direction)) {
  glm.fit2 <- glm(Direction~Lag1+Lag2,data = Weekly,family = binomial,subset = c(-i))
  glm.probs <- predict(glm.fit2,Weekly[i,],type = "response")
  if (glm.probs>0.5) glm.pred <- "Up" else glm.pred <- "Down"
  if (glm.pred == toString(Weekly$Direction[i])) error.indicator[i] <- 0
}
```

### (e) Error rate

```r
mean(error.indicator)
```

```
## [1] 0.4499541
```
