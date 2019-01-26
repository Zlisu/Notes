
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

* [Correlation](#correlation)
	* [simple correlation](#simple-correlation)
	* [Non-Parametric](#non-parametric)
	* [Partial correlation](#partial-correlation)
* [Regression](#regression)
	* [R^2^](#r2)
	* [Regression v.s. ANOVA](#regression-vs-anova)
	* [Standardized](#standardized)
	* [Assumptions](#assumptions)
	* [Model](#model)
	* [Check remaining assumptions](#check-remaining-assumptions)
		* [Heteroscedasticity: equal residual variances along regression line](#heteroscedasticity-equal-residual-variances-along-regression-line)
		* [Normality of Residuals](#normality-of-residuals)
	* [Outlier](#outlier)
	* [Leverage](#leverage)
		* [Remove high leverage observations:](#remove-high-leverage-observations)
* [Categorical Predictors](#categorical-predictors)
	* [set base level](#set-base-level)
	* [model](#model-1)
	* [run all pairwise comparison](#run-all-pairwise-comparison)
* [Non-linear trend](#non-linear-trend)
	* [adding higher order fuctions](#adding-higher-order-fuctions)

<!-- /code_chunk_output -->


## Correlation

Covariance

Correlation
One issue with applying a z test is that r is known to not follow a normal distribution which z relies on.

To account for this we can use Fishers method for transforming r to something approaching normality

* Correlation does not imply causality
* Correlation does not tell us directionality

If one wants to use Pearson's r then our data need to be interval: The space between units indicate the same amount

### simple correlation

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
---

## Regression

### R^2^
tells us how much of the variance in y is shared with x: R^2^ is a measure of effect size.

### Regression v.s. ANOVA
ANOVA has two major limitation:
1. The biggest limitation is we cannot really include continuous predictors (Age, Weight, Income, Time, etc.)
2. ANOVA does not build a predictive model it simply tells us where differences exist but does not quantify those differences.

### Standardized
𝜷 is reserved for standardized predictors while b is used for unstandardized.
b  are what we get by default when we use our variables in their raw state. They tell us the unit change in our dependent variable (in its raw units) for a unit change in our predictor variable (in its raw units).
With 𝜷 we see the impact of a 1 SD change in the predictor on the dependent. 
`scale()`
Note standardization ensures all coefficients are on the same scale, we can directly compare them in a multiple regression which is (typically) not possible with b’s

### Assumptions
1. Predictors must be categorical or continuous and unconstrained on their scale.
2. Predictors should be uncorrelated with external variables – model should be well specified.
3. We need variance in our dependent and independent variables. `plot()`
4. We need **multicollinearity** (relationship between predictors) to be minimal.
5. We want a linear relationship between our variables (we can add non-linear trends to deal with non-linear relationships). `scatterplot()`
6. **Heteroscedasticity**: equal residual variances along regression line. `plot(model)` `ncvTest(model)`
7. We need independence of errors (no **auto-correlation**). Essentially the errors of one data point need to be unrelated to those of another (normally only a problem with time series or repeated measurement). We also need our observations to be independent (no repeated measurement).
8. Normally distributed errors – same as ANOVA. `shapiro.test()`
   

### Model

```r
model <- lm(`Percent Income Saved (negative implies debt)`~Income, simplerelationships)
```

### Check remaining assumptions

#### Heteroscedasticity: equal residual variances along regression line
```r
par(mfrow=c(2,2)) # puts all plots in one cavas 2*2
plot(model)


ncvTest(model)
# result: Chi square = 1.418553  p = 0.2336417 
# p value > 0.05 so it's not a significant violation
```
![heteroscedasticity](https://github.com/Zlisu/Notes/blob/master/Images/heteroscedasticity.png?raw=True)
For Heteroscedasticity, check out Residuals vs Fitted and Scale-Location

#### Normality of Residuals
`r
shapiro.test(model$residuals)
`
w should be close to 1 and p should be larger than 0.05; Otherwise it's a violation.

If normality of residuals is violated, we can:
1. check for high leverage observations. 
2. If that fails we would want to find other variables that could make our model better.

### Outlier
Extreme outliers can impact influence coefficient estimates and model fit. We can check for outliers by looking at standardized residuals and try to find points that are extreme relative to others.

Removing an outlier generally means we don’t think that value could possibly exist in the population.


### Leverage
Data points might exert great influence even if they are not outliers.
**Cooks distance** will tell us how much each observation is impacting the model so we can find those data points which are influencing our model more than others.

![Residuals vs Leverage](https://github.com/Zlisu/Notes/blob/master/Images/residuals_leverage.png?raw=True)
Use **Cooks Distance** to identify the potential issuesmore clearly:
```r
cutoff <- 4/((nrow(simplerelationships)-length(model$coefficients)-1))
plot(model, which=4, cook.levels=cutoff)

outlierTest(model)
```
![cook's distance](https://github.com/Zlisu/Notes/blob/master/Images/cooks_distance.png?raw=True)
Observations 41, 61, and 89 have great leverage. An outlier test also shows us 89 is suspicious.

#### Remove high leverage observations:
```r
simplerelationships$number = row.names(simplerelationships)

model1.2 <- lm(`Percent Income Saved (negative implies debt)` ~ Income, data=subset(simplerelationships, number != 89 & number != 61 & number != 41))
```
```
# result:
Estimate Std. Error t value Pr(>|t|)   
(Intercept) -5.037e-03  2.464e-03  -2.044   0.0438 * 
Income       8.224e-08  2.421e-08   3.396   0.0010 **
Multiple R-squared:  0.1093,	Adjusted R-squared:  0.09983 
F-statistic: 11.54 on 1 and 94 DF,  p-value: 0.001002
```
We can see the model “fit” is reduced, but things are more or less the same.
Did this improve our other issues? Doesn’t appear so.

---

## Categorical Predictors

### set base level
```r
Simplerealtionships$variable = relevel(simplerelationships$varaible, ref=level)
```
### model
```r
modelc <- lm(`Percent Income Saved (negative implies debt)` ~ `Motivation Score (rank variable)`, data = simplerelationships)
```
### run all pairwise comparison 
```r
library(multcomp)
tukey <- glht(modelc, linfct = mcp(Motivation= "Tukey"))
```
---

## Non-linear trend

always plot our data first
1. The red lines (by default) is a “smoothed” fit (really only useful for thinking about trend)
2. The green line (by default) plots the best fitting linear trend (regression line).

### adding higher order fuctions
* 1 visible shift: quadratic (x^2^)
* 2 visible shifts: Cubic (x^3^)
  
When we include higher order trends it is important we **do not** remove their lower order components. For example, if we wanted to add a quadratic trend to the model we need to keep the linear trend in as well **even if its not significant**.

To include a cubic trend we must include the quadratic and linear trends as well.

The reason for this is that if we do not include the lower order trends the higher order trends will capture in part these effects which would bias our estimates.

An annoying issue that will pop up as you include trends beyond linear is **multicollinearity** (predictors sharing some of the same predictive variance – Age and Income).

One way to deal with this is to **standardize** your predictors (after transformation).
