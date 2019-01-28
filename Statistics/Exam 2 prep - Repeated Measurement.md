# Repeated Measurement

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Repeated Measurement](#repeated-measurement)
  - [Concepts](#concepts)
  - [Analysis](#analysis)
    - [Description](#description)
    - [Factoring](#factoring)
    - [Check Distribution](#check-distribution)
    - [Check outlier](#check-outlier)
    - [Check balanced design](#check-balanced-design)
    - [Model](#model)
    - [Check Residuals](#check-residuals)
    - [Post hoc comparison](#post-hoc-comparison)
    - [means and standard deviation](#means-and-standard-deviation)
    - [Summary](#summary)

<!-- /code_chunk_output -->


## Concepts

## Analysis

### Description

We have heart rate measurements over 5 exercises with two sources of repeated measurement – the subjects which we have 22 of and locations which we have 2 of. We also note the subjects are coming from one of the two locations, thus subjects are **nested in** locations. 

### Factoring

```r
HeartRateData$testinglocation <- factor(HeartRateData$testinglocation)
HeartRateData$subject <- factor(HeartRateData$subject)
HeartRateData$exercise <- factor(HeartRateData$exercise)
```

### Check Distribution
```r
library(moments)
agostino.test(HeartRateData$heartrate)

# if p < 0.05 then we got skewness
# take log to fix positive skew
# take square to fix negative skew
```

### Check outlier
```
outlier(HeartRateData$heartrate)
```

### Check balanced design

```
table(HeartRateData$testinglocation)
table(HeartRateData$subject)
table(HeartRateData$subject, HeartRateData$testinglocation)
table(HeartRateData$subject, HeartRateData$exercise)
```
Perfect balance, but we note that for each subject they only undergo each exercise once so we know we cant look for random “slopes” of exercise by subject as we would need at least 2 of each exercise level to do so. 

### Model

```r
library(lmerTest)
model <- lmer(heartrate ~ exercise + (1|testinglocation/subject) + (exercise|testinglocation), data = HeartRateData)
```
* (1|testinglocation/subject): random intercepts for testing location and subject nested in testing location 
* (exercise|testinglocation): random slopes for exercise routines by testing location

Result:
```
Random effects:
 Groups                  Name        Variance Std.Dev. Corr                   
 subject.testinglocation (Intercept)  2.980   1.726                           
 testinglocation         (Intercept)  0.000   0.000                           
 testinglocation.1       (Intercept)  9.445   3.073                           
                         exercise2   27.701   5.263    -1.00                  
                         exercise3   64.854   8.053    -1.00  1.00            
                         exercise4   22.999   4.796    -1.00  1.00  1.00      
                         exercise5   40.079   6.331    -1.00  1.00  1.00  1.00
 Residual                            51.152   7.152                           
Number of obs: 110, groups:  subject:testinglocation, 22; testinglocation, 2
Fixed effects:
            Estimate Std. Error     df t value Pr(>|t|)  
(Intercept)   74.636      2.680  1.127  27.848   0.0154 *
exercise2     19.254      4.301  1.061   4.476   0.1291  
exercise3     27.229      6.089  1.009   4.472   0.1384  
exercise4     48.730      4.019  1.084  12.126   0.0432 *
exercise5     13.955      4.969  1.030   2.808   0.2118  
Correlation of Fixed Effects:
          (Intr) exrcs2 exrcs3 exrcs4
exercise2 -0.903                     
exercise3 -0.901  0.898              
exercise4 -0.900  0.865  0.884       
exercise5 -0.905  0.888  0.919  0.877
```
we find only one difference is significant (exercise 4 seems to lead to a higher heartrate than 1). 

### Check Residuals
```r
qqnorm(resid(model))
qqline(resid(model))
shapiro.test(resid(model))
```

### Post hoc comparison
```r
difflsmeans(model, test.effs = "exercise")
```
```
               Estimate Standard Error    DF t-value Lower CI Upper CI p-value    
exercise 1 - 2    -19.3           4.30   1.1   -4.48  -66.999    28.49   0.129    
exercise 1 - 3    -27.2           6.09   1.0   -4.47 -103.020    48.56   0.138    
exercise 1 - 4    -48.7           4.02   1.1  -12.13  -91.314    -6.14   0.043 *  
exercise 1 - 5    -14.0           4.97   1.0   -2.81  -72.884    44.98   0.212    
exercise 2 - 3     -8.0           2.92   1.4   -2.73  -27.200    11.25   0.161    
exercise 2 - 4    -29.5           2.18  17.6  -13.51  -34.067   -24.89  <2e-16 ***
exercise 2 - 5      5.3           2.28   4.6    2.32   -0.717    11.32   0.072 .  
exercise 3 - 4    -21.5           3.16   1.3   -6.81  -46.092     3.09   0.059 .  
exercise 3 - 5     13.3           2.48   2.3    5.36    3.888    22.66   0.024 *  
exercise 4 - 5     34.8           2.41   2.7   14.40   26.574    42.98   0.001 **
```
```r
library(emmeans)
emmeans(model, list(pairwise ~ exercise), adjust = "holm")
```
```
emmeans of exercise
 exercise    emmean       SE df lower.CL upper.CL
 1         74.63591 2.680106  1 40.58194 108.6899
 2         93.88955 2.204177  1 65.88282 121.8963
 3        101.86500 3.854948  1 52.88325 150.8468
 4        123.36545 1.985937  1 98.13173 148.5992
 5         88.59045 2.786808  1 53.18070 124.0002
Degrees-of-freedom method: kenward-roger 
Confidence level used: 0.95 
pairwise differences of exercise
 contrast   estimate       SE df t.ratio p.value
 1 - 2    -19.253636 4.301234  1  -4.476  0.7045
 1 - 3    -27.229091 6.089121  1  -4.472  0.7045
 1 - 4    -48.729545 4.018646  1 -12.126  0.4413
 1 - 5    -13.954545 4.968861  1  -2.808  0.7045
 2 - 3     -7.975455 2.922743  1  -2.729  0.7045
 2 - 4    -29.475909 2.181619  1 -13.511  0.4413
 2 - 5      5.299091 2.284755  1   2.319  0.7045
 3 - 4    -21.500455 3.155306  1  -6.814  0.6494
 3 - 5     13.274545 2.476611  1   5.360  0.7045
 4 - 5     34.775000 2.414217  1  14.404  0.4413
```
We see that using the Satterthwaite we get exercise 4 being more or less better than all others, while using the Kenward roger methods we find nothing is significant. The truth is probably somewhere between the two but its hard to get perfect estimates of contrast effects with a nested design. Will take the testing to show exercise 4 is likely better than the others and summarize.

### means and standard deviation

```r
tapply(HeartRateData$heartrate, HeartRateData$exercise, mean)
```
```
        1         2         3         4         5 
 74.63591  93.88955 101.86500 123.36545  88.59045 
```
```r
tapply(HeartRateData$heartrate, HeartRateData$exercise, sd)
```
```
       1        2        3        4        5 
7.609115 7.622254 8.729368 6.936912 7.609340
```

### Summary

We performed a hierarchical (mixed effects) linear regression predicting heart rate by exercise routine (exercise one as the default level), with **random intercepts for testing location** and **subject nested in testing location**, and **random slopes for exercise routines by testing location**. 

Analysis revealed that exercise 4 (M = 123.37; SD = 6.94) led to a higher heartrate than exercise 1 (M = 74.64; SD = 7.61) (见 tapply 的结果), β = 48.73, t(1.08) = 12.13, p = .04 (见 model 的结果 fixed effects 部分); no other differences reached significance, ps > .12). 

Post-Hoc analysis revealed exercise 4 led to higher hear rates than exercise 2 (M = 93.89; SD = 7.62; p < .001) and 5 (M = 88.59; SD = 7.61; p = .001), and marginally more than exercise 3 (M = 101.87; SD = 8.79; p = .059). Exercise 3 led to higher heart rate than 5 (p = .02) and exercise 2 led to marginally more than 5, p = .07. (见difflsmeans(model, test.effs = "exercise")的结果) We note however, that these post hoc tests are probably overestimates of the true significance of the effect (见emmeans(model, list(pairwise ~ exercise), adjust = "holm")的结果). In short, it appears that exercise 4 led to the highest heart rates, and likely higher heartrates than many of the other routines.
