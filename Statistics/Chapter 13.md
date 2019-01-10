- [Repeated measure](#repeated-measure)
  - [Asumptions](#asumptions)
    - [sphericity](#sphericity)
      - [Assessing the sphericity](#assessing-the-sphericity)
  - [Theory](#theory)
    - [Partitioning variances](#partitioning-variances)
    - [F-ratio](#f-ratio)
  - [Procedure](#procedure)
    - [data](#data)

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



## One-way repeated-measures designs using R
1. Enter data
2. Expore your data
3. Construct or choose contrasts
4. Compute the ANOVA/multilevel model
5. Compute contrasts or post hoc tests

### data
R requires long format data for the analysis

```r{.line-numbers}
# read data
bushData <- read.delim("Bushtucker.dat", header = TRUE)

# reshape data to long format
longBush <- melt(bushData, id = "participant", measured = c("stick_insect", "kangaroo_testicle", "fish_eye", "witchetty_grub"))

# give the column names
names(longBush) <- c("Participant", "Animal", "Retch")

# desiganate levels to the categorical variable
longBush$Animal <- factor(longBush$Animal, labels = c("Stick Insect", "Kangaroo Testicle", "Fish Eye", "Witchetty Grub"))
```

### ezANOVA

#### model
```r{.line-numbers}
library(ez)
bushModel <- ezANOVA(data = longBush, dv = .(Retch), wid = .(Participant), within = .(Animal), detailed = TRUE, type = 3)
bushModel
```
#### result:
```
$`ANOVA`
       Effect DFn DFd     SSn     SSd          F            p p<.05       ges
1 (Intercept)   1   7 990.125  17.375 398.899281 1.973536e-07     * 0.8529127
2      Animal   3  21  83.125 153.375   3.793806 2.557030e-02     * 0.3274249

$`Mauchly's Test for Sphericity`
  Effect        W          p p<.05
2 Animal 0.136248 0.04684581     *

$`Sphericity Corrections`
  Effect       GGe      p[GG] p[GG]<.05       HFe      p[HF] p[HF]<.05
2 Animal 0.5328456 0.06258412           0.6657636 0.04833061         *
```

- 首先看Sphericity是否被violated。
在此例中，W=0.14， p = 0.047 < 0.05, 因此Sphericity is violated.

- 如果Sphericity is violated，就看correction。
ezANOVA提供了 Greenhouse–Geisser correction $(\hat{\epsilon})$ 和 Huynh–Feldt estimate。(GGe 和 HFe)

- The closer the Greenhouse–Geisser correction, $\hat{\epsilon}$, is to 1, the more homogeneous the variances of differences, and hence the closer the data are to being spherical.
$(\hat{\epsilon})$ 的下限是 1/(k-1), k is the number of levels of the independent variable。如果 $\hat{\epsilon}$ 的值更接近下限而偏离1，那么it represents a substantial deviation from sphericity.
- p[GG] and p[HF] 是修正之后的 p value。因为它们一个significant 一个 insignificant，不能做出conclusive的结论，所以要算一下他俩的平均值看看怎么样。the average of the two p-values is (.063 + .048)/2 = .056.
Therefore, we should probably go with the Greenhouse–Geisser correction and conclude that the F-ratio is non-significant.
- These data illustrate how important it is to use a valid critical value of F: it can potentially mean the difference between making a Type I error and not. **However, it also highlights how arbitrary it is that we use a .05 level of significance**. These two corrections produce significance values that differ by only .015 and yet they lead to completely opposite conclusions. The decision about ‘significance’ has, in some ways, become rather arbitrary. The F, and hence the size of effect, is unaffected by these corrections and so whether the p falls slightly above or slightly below .05 is less important than how big the effect is. **We might be well advised to look at an effect size to see whether the effect is substantive regardless of its significance.**

**备注：p value 是怎么算出来的**
1. Independent variable 的 SSn = 83.125 即为 model sum of squares (SS~M~), DFn = 3 是它的自由度, 相除得 mean square for the experimental effect: MS~M~ = 83.125 / 3 = 27.71；
2. SSd = 153.375 即为 residual sum of squares (SS~R~), DFd = 21 是它的自由度，相除得 error mean squares：MS~R~ = 153.375 / 21 = 7.3。
3. 再用 MS~M~ / MS~R~ = 27.71 / 7.3 = 3.79 即为 F-ratio的值。
4. 再通过 DFn = 3 和 DFd = 21 查表得到 critical value, 即可得到p-value。

#### post hoc tests
```r
pairwise.t.test(longBush$Retch, longBush$Animal, paired = TRUE, p.adjust.method = "bonferroni")
```
Result:
```
	Pairwise comparisons using paired t tests 

data:  longBush$Retch and longBush$Animal 

                   Stick Insect Kangaroo\nTesticle Fish Eye
Kangaroo\nTesticle 0.0121       -                  -       
Fish Eye           0.0056       1.0000             -       
Witchetty Grub     1.0000       1.0000             1.0000
```
p value < 0.05 说明两组之间的 mean 有显著差别；否则就是没有显著差别。



