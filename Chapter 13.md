# Repeated measure

‘Repeated measures’ is a term used when the same entities participate in all conditions of an experiment or provide data at multiple time points.

## Asumptions

### sphericity

Sphericity refers to the equality of variances of the differences between treatment levels. So, if you were to take each pair of treatment levels, and calculate the differences between each pair of scores, then it is necessary that these differences have approximately equal variances. As such, you need at least three conditions for sphericity to be an issue.

#### Assessing the sphericity
Violations of sphericity affect the accuracy of _F_. When sphericity is violated, the **Bonferroni** method seems to be generally the most robust of the univariate techniques, especially in terms of power and control of the Type I error rate. When sphericity is definitely not violated, **Tukey’s** test can be used.

**Mauchly's test**
- if Mauchly’s test statistic is significant (i.e., p < .05) we should conclude
that there are significant differences between the variances of differences and, therefore, the condition of sphericity is not met.
- Mauchly’s test statistic is non-significant (i.e., p > .05) then it is reasonable to conclude that the variances of differences are not significantly different (i.e., they are roughly equal)


## Theory

### Partitioning variances



In an independent ANOVA (section 10.2) the within-participant variance is our residual variance (SSR); it is the variance created by individual differences in performance.

In a repeated-measures ANOVA the effect of our experiment is shown up in the withinparticipant variance (rather than in the between-group variance)

![enter image description here](https://github.com/Zlisu/Notes/blob/master/Images/Partitioning.png?raw=True)


Within-person (or within-subject) effects represent the variability of a particular value for individuals in a sample. a within person effect is a measure of how much an individual in your sample tends to change (or vary) over time. In other words, it is the mean of the change for the average individual case in your sample.
同一个人在不同的实验条件下得到的结果不同，其原因一部分是由于实验条件之变化对实验结果的影响，即 Effect of Experiment, **SS<sub>M<sub>**.

另一部份是不受控的随机因素，即 Error (variation not explained by the experiment), **SS<sub>R<sub>**.

Between-persons (or between-subjects) effects, by contrast, examine differences between individuals. This can be between groups of cases when the independent variable (IV) is categorical or between individuals when the (IV) is continuous. **SS<sub>B<sub>**.

Because both of these values are summed values the number of scores that were summed influences them. We eliminate this bias by calculating the average sum of squares (known as the mean squares, MS), which is simply the sum of squares divided by the degrees of freedom:

$$MS_M = \frac{SS_M}{df_M}$$
$$MS_R = \frac{SS_R}{df_R}$$

### F-ratio
As in independent ANOVA, we use an F-ratio that compares the size of the variation due to our experimental manipulations to the size of the variation due to random factors, the only difference being how we calculate these variances. If the variance due to our manipulations is big relative to the variation due to random factors, we get a big value of F, and we can conclude that the observed results are unlikely to have occurred if there was no effect in the population.

$$ F = \frac{MS_M}{MS_R}$$

This value is greater than 1, which indicates that the experimental manipulation had some effect above and beyond the effect of extraneous factors.



## Procedure
### Libraries

