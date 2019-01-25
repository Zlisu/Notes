## Concepts

### Fixed effects vs Random effects

Fixed effects: Main effect and their interaction.
The easiest way to think about a fixed effect is that it measures some variable of direct interest and the variable itself comprises all levels/ranges of interest.

If we have designed an experiment with several conditions, we are directly interested in those conditions and the differences between them.

Using age as a fixed effect implies we are interested in the slope of age and the range of ages we have is a range of the population we are interested in.


Random Effects: our source of repeated measurement
Random effects are variables we aren’t directly interested in and where the levels or range we have are not the levels/range we are interested in but some sub-sample from the population.

Repeated measurement fits here because we aren’t interested in the sources of repeated measurement and they don’t normally comprise the entire population they are drawn from (they are samples).

So too would experimental confounds like blocks comprising month run or session number.

Sometimes a variable could be fixed or random depending on our goals.

### Comparing model

anova(model1, model2, …) 
requires shared structure
requires ML rather than restricted ML 

AIC/BIC
more flexible

## Analysis

### factor
```r
DrugsData$subject <- factor(DrugsData$subject)
DrugsData$location <- factor(DrugsData$location)
DrugsData$drug <- factor(DrugsData$drug)
```

### distribution
```r
plot(density(DrugsData$levels))
library(moments)
agostino.test(DrugsData$levels)

# fix positive skewness
agostino.test(log(DrugsData$levels))
DrugsData$l2 <- log(DrugsData$levels)
```

### data distribution
```
table(DrugsData$subject)
 1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 
 3  3  3  3  3  3  3  3  3  3  3  3  3  3  3  3  3  3  3  3  3 
table(DrugsData$location)
 1  2  3  4  5  6 
 9 12 12  9  9 12 
table(DrugsData$drug)
 1  2  3 
21 21 21 

table(DrugsData$subject, DrugsData$drug)
    
     1 2 3
  1  1 1 1
  2  1 1 1
  3  1 1 1
  4  1 1 1
  5  1 1 1
  6  1 1 1
  7  1 1 1
  8  1 1 1
  9  1 1 1
  10 1 1 1
  11 1 1 1
  12 1 1 1
  13 1 1 1
  14 1 1 1
  15 1 1 1
  16 1 1 1
  17 1 1 1
  18 1 1 1
  19 1 1 1
  20 1 1 1
  21 1 1 1
```
### Model
Fullest model:
```r
model <- lmer(l2 ~ drug + (drug|location/subject), data = DrugsData)

# Error: number of observations (=63) <= number of random effects (=63) for term (drug | subject:location); the random-effects parameters and the residual variance (or scale parameter) are probably unidentifiable
```
Don't have enough replication for random slope for each location and each subjuct at each location.

Reduced model:
```r
model <- lmer(l2 ~ drug + (1|location/subject) + (drug|location), data = DrugsData)
summary(model)
```
```
Random effects:
 Groups           Name        Variance Std.Dev. Corr     
 subject.location (Intercept) 0.129511 0.35988           
 location         (Intercept) 0.000000 0.00000           
 location.1       (Intercept) 0.003080 0.05550           
                  drug2       0.002668 0.05166  1.00     
                  drug3       0.022475 0.14992  1.00 1.00
 Residual                     0.045849 0.21412           
Number of obs: 63, groups:  subject:location, 21; location, 6

Fixed effects:
            Estimate Std. Error       df t value Pr(>|t|)    
(Intercept)  8.20238    0.09417 17.98279  87.099   <2e-16 ***
drug2       -0.06404    0.06939 15.33113  -0.923   0.3704    
drug3       -0.30542    0.09026  5.58399  -3.384   0.0165 *  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Correlation of Fixed Effects:
      (Intr) drug2 
drug2 -0.260       
drug3 -0.092  0.557
convergence code: 0
singular fit
```

### residuals
```r
qqnorm(resid(model))
qqline(resid(model))
shapiro.test(resid(model))
```

### Post hoc comparison
```r
difflsmeans(model, test.effs = "drug")
```
```
Least Squares Means table:

               Estimate Std. Error   df t value     lower     upper Pr(>|t|)  
drug1 - drug2  0.064040   0.069393 15.3  0.9229 -0.083590  0.211670  0.37038  
drug1 - drug3  0.305422   0.090259  5.6  3.3838  0.080515  0.530329  0.01652 *
drug2 - drug3  0.241382   0.077399  8.3  3.1187  0.064055  0.418709  0.01360 *
```
```r
library(emmeans)
emmeans(model, list(pairwise ~ drug), adjust = "tukey")
emmeans(model, list(pairwise ~ drug), adjust = "holm")
# 因为 p value 很接近0.05 所以用了两种方法tukey和holm来确认
```
```
emmeans of drug
 drug emmean     SE   df lower.CL upper.CL
 1      8.20 0.0957 4.86     7.95     8.45
 2      8.14 0.1027 4.89     7.87     8.40
 3      7.90 0.1251 4.95     7.57     8.22

Degrees-of-freedom method: kenward-roger 
Confidence level used: 0.95 

pairwise differences of drug
 contrast estimate     SE   df t.ratio p.value
 1 - 2       0.064 0.0704 4.87 0.909   0.6590 
 1 - 3       0.305 0.0908 4.95 3.364   0.0451 
 2 - 3       0.241 0.0782 4.91 3.086   0.0612 

P value adjustment: tukey method for comparing a family of 3 estimates 
```

### means and standard deviation
```r
tapply(DrugsData$levels, DrugsData$drug, mean)
```
```
       1        2        3 
3967.805 3737.676 3065.195 
```
```r
tapply(DrugsData$levels, DrugsData$drug, sd)
       1        2        3 
1651.838 1637.590 1631.897
```

### Summary
We performed a hierarchical (mixed effects) linear regression predicting enzyme levels (skew corrected by taking the log) by drug taken (drug one as the default level), with random intercepts for hospital and subject nested in testing hospital, and random slopes for drugs by hospital. 

Analysis revealed that drug 3 (M = 3065.19; SD = 1631.84) led to a lower enzyme levels than drug 1 (M = 3967.81; SD = 1651.84), β = -.31, t(5.58) = -3.38, p = .02; drugs 1 and 2 (M = 3737.68; SD = 1637.59) were not found to significantly differ, p = .37). 

Post-Hoc analysis revealed drug 2 likely led to higher hear rates enzyme rates than drug 3, p ~ .06. In short, it appears drugs 1 and 2 are about equally effective in raising enzyme levels while drug 3 does not perform well (因为3的平均值最低且significant).