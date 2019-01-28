# Guess the analysis

1. Over the period of a month we tallied the number of customers who entered each of our ten stores each day. Everyday each store randomly used 1 of 3 banners to draw customers in. How can we determine which banner works best? 

repeated measurement
lmer(count ~banner*day + (1|store))

2. We presented one of five versions of our Facebook ad to Facebook users at random. We have data on whether 100,000 users clicked or did not click on our ad. How should we determine which ad works best?

chi-square test independence
logistic regression

3. We have multiple demographic variables and we seek to predict an individuals income using those variables. How might we build such a model?

multiple regression
select predictors: a. half-normal plot to see which one has impact or b. elastic net

4. One-thousand out-patient patients at 50 drug rehabilitation clinics across five states were randomly assigned to one of three treatment methods to aid in their abstinence from drugs and/or alcohol. Success was determined by whether a patient had not used any substance over a 6 month period. How might we determine which program works best?

glmer(outcome ~ treatment + (treatment|states/clinics), family = "binomial")

5. We suspect that the positive effect of empathy/sympathy on the amount donated to victims of natural disasters is actually driven by the donators perceptions that donating will make them feel good. How might we test 

mediation


6. Event attendees indicated how much they enjoyed the event on 7-point Likert scale as well as their gender. How can we find out if gender impacted enjoyment?

ordinal logistic regression using gender as the predictor

7. We find income and years of education are correlated with ratings of attractiveness and want to determine the unique relationship each has with attractiveness. How might we accomplish this?

partial correlation cor.test

8. We graph our data and find that age appears to show a convex relationship with income. How might we capture this relationship?




9. We are trying to build a predictive model and we have multiple potential predictors to include and no theory of what to include. How might we proceed?

elastic net


# Fix

1. positive skew: log. Negative skew: ^2
   
2. We suspect a few of our predictors are ~ the same.
identify multicorrelinearity. drop variable/merge the two, take average

3. We have count data with lots of 0 counts.
zero inflation / negative binomial

4. We are performing and RANOVA and encounter violations of sphericity.
correction

5. We find one observation is both an outlier and has very high leverage.
run, remove, re-run the model, compare result. If new model reports pretty much the same thing (coefficients stay significant/insignificant), keep it.

6. We find an odd (non-normal) pattern in our residuals.

try different trend? interaction?
non parametric
collect data again

7. We wish to compare two models using the same data but containing unique predictors.
AIC/BIC

8. We are running a logistic regression with several continuous predictors and the model will not converge, what might help it converge?
scalling

# Assumptions

1. If we wish to include random slopes/effects for our sources of  repeated measurement what must our data have?
replications

2. If we use multiple predictors what should we check for?
multicollinearity

3. What is a unique assumption of repeated measures ANOVA?
sphericity

4. What is an assumption shared by logistic and linear regression? What is an assumption that linear regression has that logistic does not?
multicollinearity and independence of errors

difference: normal distributed residuals (only for linear regression)

5. What assumption is violated by repeated measurement and how are we correcting for it in a mixed effect model?


6. We generate a model based on data available to us. In regards to the constraints of the predictive power of the model what is true?


7. What are the unique assumptions of ANCOVA?
no interaction between cocariate and predictor