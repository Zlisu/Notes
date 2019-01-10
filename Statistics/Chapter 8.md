<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Logistic Regression](#logistic-regression)
	- [Principle](#principle)
		- [Assessing logistic model](#assessing-logistic-model)
			- [log-likelihood statistic](#log-likelihood-statistic)
			- [deviance statistic](#deviance-statistic)
			- [likelihood ratio](#likelihood-ratio)
			- [R and R^2^](#r-and-r2)
				- [R-statistic](#r-statistic)
				- [R^2^](#r2)
			- [Information criteria](#information-criteria)
		- [Assessing the contribution of predictors](#assessing-the-contribution-of-predictors)
			- [z-statisc (Wald statistic)](#z-statisc-wald-statistic)
			- [The odds ratio](#the-odds-ratio)
	- [Assuptions](#assuptions)
		- [Other problems](#other-problems)
			- [Incomplete information from the predictors](#incomplete-information-from-the-predictors)
			- [Complete separation](#complete-separation)
	- [Procedure in R](#procedure-in-r)
		- [Assign base level:](#assign-base-level)
		- [Model](#model)
			- [model chi-square](#model-chi-square)
			- [coefficient and z-statistic](#coefficient-and-z-statistic)
			- [Odds ratio](#odds-ratio)
				- [Calculation](#calculation)
				- [Interpret](#interpret)
				- [Confidence interval](#confidence-interval)

<!-- /code_chunk_output -->

# Logistic Regression

中文： “逻辑回归”或“对数几率回归”。

Dependent varialbe: Categorical 

- two categories: Binary logistic regression
- three or more categories: Multinominal/polychotomous logistic regression

Independent variable: Continuous or Categorical

## Principle

Instead of predicting the value of a variable Y from a predictor variable X~1~ or several predictor variables (X~s~), we predict the probability of Y occurring given known values of X~1~ (or X~s~).

基本：$P(Y) = \frac{1}{1+e^{-(b_0+b_1X_{1i})}}$

扩展：$P(Y) = \cfrac{1}{1+e^{-(b_0+b_1X_{1i}+b_2X_{2i}+...b_nX_{ni})}}$

P(Y) is the **probability** of Y occurring. i.e., the probability that a case belongs in a certain category.

当 dependent variable 是 categorical data 时，independent variable 与 dependent variable 之间不再是现形关系，这违背了 linear regression 的 assumptions，所以不能直接用 linear regression 的公式，需要通过对数来克服这一问题。

The values of the parameters are estimated using **maximum-likelihood estimation**,
which selects coefficients that make the observed values most likely to have occurred.

### Assessing logistic model

#### log-likelihood statistic

In logistic regression, we can use the observed and predicted values to assess the fit of the model.The measure we use is the log-likelihood.

$$log-likelihood = \sum_{i=1}^n[Y_i\ln(P(Y_i))+(1-Y_i)\ln(1-P(Y_i))]$$

The log-likelihood statistic is an indicator of how much **unexplained** information there is after the model has been fitted. The larger the value of the log-likelyhood, the more unexplained observations there are, and that indicates poorly fitting statistcal model.

#### deviance statistic

The deviance is often referred to as _**-2LL**_.
$$ deviance = -2*log{-}likelihood$$

Deviance has chi-square distribution.

To assessing a model, we compare the model against a **baseline model**.
Baseline model: our baseline model isthe model that gives us the best prediction when we know nothing other than the values of the outcome.

- _In linear regression_, the baseline model is the **mean** of all scores (this is our best guess of the outcome when we have no other information)
- _In logistic regression_, the baseline model is the category with the largest number of cases (frequency)

#### likelihood ratio

The improvement of our model is measured by **likelihood ratio**. It is the difference between the deviances of the new model and base model.

$$
\begin{aligned}
\chi^2 &= (-2LL(baseline))-(-2LL(new)) \\
&= 2LL(new) - 2LL(baseline)\\
df &= k_{new} - k_{baseline}
\end{aligned}
$$

The likelihood ratio has chi-square distribution.

The model chi-square is an analogue of the F-test for the linear regression. In an ideal world we would like to see a non-significant overall −2LL (indicating that the
amount of unexplained data is minimal) and a highly significant model chi-square statistic (indicating that the model including the predictors is significantly better than without those predictors). However, in reality it is possible for both statistics to be highly significant.

#### R and R^2^

##### R-statistic

This R-statistic is the partial correlation between the outcome variable and **each** of the predictor variables, and it can vary between −1 and 1.

- A positive value indicates that as the predictor variable increases, so does the likelihood of the event occurring. 
- A negative value implies that as the predictor variable increases, the likelihood of the outcome occurring decreases. 
- If a variable has a small value of R then it contributes only a small amount to the model.

_**It is invalid to square this value and interpret it as you would in linear regression.**_

##### R^2^

Below are several **analogues** to the R^2^ in linear regression

- Hosmer and Lemeshow's ($R^2_L$)
- Cox and Snell's $R^2_{CS}$
- Nagelkerke's $R^2_N$

In terms of interpretation they can be seen as similar to the R2 in linear regression in that they provide a gauge of the substantive significance of the model.

#### Information criteria

R^2^ is flawed because every time we add a variable to the model, R^2^ increases. Information criteria penalizes a model that contains more predictor variables.

- Akaike Information Criterion (AIC)
- Bayes Information Criterion (BIC)

### Assessing the contribution of predictors

#### z-statisc (Wald statistic)

t-statistic and z-statistic are measurements of the individual contribution of predictors. t-statistic is used for linear regression. z-statistic is an analogous statistic used for logistic regression.

Like the t-test in linear regression, the z-statistic tells us whether the b coefficient for that predictor is significantly different from zero. If the coefficient is significantly different from zero then we can assume that the predictor is making a significant contribution to the prediction of the outcome.
$$ z = \frac{b}{SE_b} $$
z statistic follows the normal distribution.

When the regression coefficient (b) is large, the standard error tends to become inflated, resulting in the z-statistic being underestimated (see Menard, 1995). The inflation of the standard error increases the probability of rejecting a predictor as being significant when in reality it is making a significant contribution to
the model

#### The odds ratio

The odds of an event occurring are defined as the probability of an event occurring divided by the probability of that event not occurring.
$$
\begin{aligned}
odds &= \frac{P(event)}{P(no\enspace event)} \\
P(event\enspace Y) &= \frac{1}{1+e^{-(b_0+b_1X_{1i})}} \\
P(no\enspace event\enspace Y) &= 1-P(event\enspace Y)
\end{aligned}
$$

$$
\Delta odds = \frac{odds\enspace after\enspace a\enspace unit\enspace change\enspace in\enspace the\enspace predictor}{original\enspace odds}
$$
This proportionate change in odds is the odds ratio, and we can interpret it in terms of the change in odds: if the value is greater than 1 then it indicates that as the predictor increases, the odds of the outcome occurring increase. Conversely, a value less than 1 indicates that as the predictor increases, the odds of the outcome occurring decrease.

## Assuptions

- **Linerity**: between any continuous predictors and the logit of the outcome variable.
- **Independence of errors**: Basically it means that cases of data should not be related.
- **Multicollinearity**: predictors should not be too highly corelated.

### Other problems

#### Incomplete information from the predictors

As a general point, whenever samples are broken down into categories and one or more combinations are empty it creates problems. These will probably be signalled by coefficients that have unreasonably large standard errors.

#### Complete separation

The outcome variable can be perfectly predicted by one variable or a combination of variables!

## Procedure in R

### Assign base level:

```r
# Variable "Cured" 中包含两个 level: Cured 和 Not Cured
# 把 "not Cured" 指定为 base level

eelData$Cured <- relevel(eelData$Cured, "Not Cured")

```

### Model

```r
# family 用于指定 distribution
# oridinary regression 是 Gaussian distribution, 也就是 normal distribution
# logistic regression 是 binomial distribution

eelModel.1 <- glm(Cured ~ Intervention, data = eelData, family =
binomial())
```

```
Call:
glm(formula = Cured ~ Intervention, family = binomial(), data = eelData)

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-1.5940  -1.0579   0.8118   0.8118   1.3018  

Coefficients:
                         Estimate Std. Error z value Pr(>|z|)   
(Intercept)               -0.2877     0.2700  -1.065  0.28671   
InterventionIntervention   1.2287     0.3998   3.074  0.00212 **
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 154.08  on 112  degrees of freedom
Residual deviance: 144.16  on 111  degrees of freedom
AIC: 148.16

Number of Fisher Scoring iterations: 4
```

* **Null deviance**: the baseline model that contains no predictors other than the constant. It is the -2LL(baseline).
* **Residual deviance**: the model we built. It is the -2LL(new).

_lower values of −2LL indicate that the model is predicting the outcome variable more accurately._

#### model chi-square

Highly significant model chi-square statistic indicates that the model including the predictors is significantly better than without those predictors.

```r
# Calculate the value of chi square
modelChi <- eelModel.1$null.deviance - eelModel.1$deviance

# Calculate the value of df
chidf <- eelModel.1$df.null - eelModel.1$df.residual

# Calculate the probably associated with this chi-square  statistic
chisq.prob <- 1 - pchisq(modelChi, chidf)

```

The result of chisq.prob is 0.001629425. In other words, the p-value is .002; because this probability is less than .05, we can reject the null hypothesis that the model is not better than chance at predicting the outcome.

**This value is the likelihood ratio p-value of the model because we only had one predictor in the model.**

We can report that including Intervention produced a significant improvement in the fit of the model, χ2(1) = 9.93, p = .002.

#### coefficient and z-statistic

The crucial statistic is the z-statistic which has a normal distribution and tells us whether the b coefficient for that predictor is significantly different from zero.6 If the coefficient is significantly different from zero then we can assume that the predictor is making a significant contribution to the prediction of the outcome.

We could say that Intervention was a significant predictor of being cured, b = 1.23, z = 3.07, p < .002.

#### Odds ratio

##### Calculation
```r
exp(eelModel.1$coefficients)

# result:
(Intercept)		InterventionIntervention 
0.750000				3.416667 
```

This is the odds ratio for predictor _Intervention_.

##### Interpret

We can interpret the odds ratio in terms of the change in odds. 

* If the value is greater than 1 then it indicates that as the predictor increases, the odds of the outcome occurring increase. 
* Conversely, a value less than 1 indicates that as the predictor increases, the odds of the outcome occurring decrease. 

In this example, we can say that the odds of a patient who is treated being cured are 3.42 times higher than those of a patient who is not treated.

##### Confidence interval

```r
exp(confint(eelModel.1))

# result:
                             2.5 %   97.5 %
(Intercept)              0.4374531 1.268674
InterventionIntervention 1.5820127 7.625545
```

The important thing about this confidence interval is that it doesn’t cross 1
