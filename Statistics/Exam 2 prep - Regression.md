## Concepts

Covariance

Correlation
One issue with applying a z test is that r is known to not follow a normal distribution which z relies on.

To account for this we can use Fishers method for transforming r to something approaching normality

* Correlation does not imply causality
* Correlation does not tell us directionality

If one wants to use Pearson's r then our data need to be interval: The space between units indicate the same amount

### simple regression

```r
cor.test(simplerelationships$Income, simplerelationships$`Percent Income Saved (negative implies debt)`, method = "pearson", conf.level = .99)
library(car)
scatterplot(simplerelationships$Income, simplerelationships$`Percent Income Saved (negative implies debt)`)
```
### Non-Parametric
use non-parametric correlation coefficient when:
1. violate the assumption of normality greatly 
2. the variables we wish to examine will be **ordinal** (ranked data)

Spearman's is the most common, we will usually only turn to Kendall's when we have a smaller data set and there are a lot of ties in rank.

```r
# relationship between a persons percent savings and their score on the motivation scale
cor.test(simplerelationships$`Percent Income Saved (negative implies debt)`, simplerelationships$`Motivation Score (rank variable)`, method = "spearman", conf.level = .99)
cor.test(simplerelationships$`Percent Income Saved (negative implies debt)`, simplerelationships$`Motivation Score (rank variable)`, method = “kendall", conf.level = .99)
```

### Partial correlation

With partial correlation what we are trying to do is find out the “unique” relationship between x and y that cannot be explained by other x’s.

```r
cor.test(simplerelationships$`Percent Income Saved (negative implies debt)`, simplerelationships$Income, method = "pearson")
# t = 4.2858, df = 97, p-value = 4.296e-05, r = 0.3990131 

cor.test(simplerelationships$`Percent Income Saved (negative implies debt)`, simplerelationships$Age, method = "pearson") 
# t = 5.4674, df = 97, p-value = 3.548e-07, r = 0.4853564 

cor.test(simplerelationships$Income, simplerelationships$Age, method = "pearson")
# t = 101.92, df = 97, p-value < 2.2e-16, cor = 0.9953638

# 对 Percent Income Saved (negative implies debt)， Income 和 Age 这三个变量分别算 correlation，发现它们互相之间都是 highly correlated, 
# 所以it extremely likely a lot of the relationship is shared
# Given the high probability that a lot of the income effect on savings is shared with age we should run a partial correlation
pcor.test(simplerelationships$Income, simplerelationships$`Percent Income Saved (negative implies debt)`, simplerelationships$Age, method = "pearson")
```

