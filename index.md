---
title       : Sample size calculator
subtitle    : Two independent means
author      : Marc Mari-Dell'Olmo
job         : CIBERESP
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---



## Shiny app description

* This Shiny app provides sample size calculations for two-sided two-sample t-tests when the variances of the two groups (populations) are assumed to be equal.

* This is the traditional two-sample t-test (Fisher, 1925). In this procedure, the assumed difference between means is specified by entering the difference directly. The design corresponding to this test procedure is sometimes referred to as a parallel-groups design.

* This design is used in situations such as the comparison of the income level of two regions, the nitrogen content of two lakes, or the effectiveness of two drugs. 

* There are several statistical tests available for the comparison of the center of two populations. This procedure is specific to the two-sample t-test assuming equal variance. 

---  

## Parameters values to enter

1. Alpha: This is the probability of obtaining a false positive with the statistical test. That is, it is the probability of rejecting a true null hypothesis. The null hypothesis is that the means are equal.
2. Beta: This is the probability of obtaining a false negative with the statistical test. That is, it is the probability of accepting a false null hypothesis.).
3. Group 2 size/Group 1 size ratio: set a value for the ratio of Group 2 size to Group 1 size, and then this calculator determines the needed Group 1 and Group 2 size, with this ratio, to obtain the desired power.
4. Estimated common standard deviation: This is the assumed standard deviation for both the Group 1 population and the Group 2 population.
5. Minimun expected difference: Enter a value for the assumed difference between the means of Groups 1 and 2. This difference is the difference at which the design is powered to reject equal means.
6. Dropout rate: Percentage of the expected number of subjects dropped out at the end of the study. For example, if you enter 0.1 the final adjusted taking into account a dropout rate of 10%.

---


## Example

* With these values: Alpha = 0.05, Beta = 0.2, Ratio = 2, Common Standard deviation = 10, Minimum expected difference = 1, Dropout rate = 0.1

* This Shiny app uses the following R syntax:


```r
library(samplesize)
power = 1-0.2
sample <- n.ttest(power = power, alpha = 0.05, mean.diff = 1, sd1 = 10, k = 2, design = "unpaired", 
                  fraction = "unbalanced", variance = "equal")
ceiling(sample[[2]]/(1-0.1))
```

```
## [1] 1309
```

```r
ceiling(sample[[3]]/(1-0.1))
```

```
## [1] 2618
```

---

## Result

The result is the folowing paragraph that you can copy-paste to your project documentation or paper:

Accepting an alpha risk of 0.05 and a beta risk of 0.2 in a two-sided test, __1309__ subjects are necessary in first group and __2618__ in the second to recognize as statistically significant a difference greater than or equal to 1 units. The common standard deviation is assumed to be 10. It has been anticipated a drop-out rate of 10%.



