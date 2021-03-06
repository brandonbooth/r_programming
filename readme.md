# Coding Notes
by [Brandon Booth](https://brandon-booth.com/) - Fall 2021


## Table of Contents
- [GettingStarted](#GettingStarted)


**Helpful links:**
- https://rstudio.cloud/learn/primers/1.2
- https://r4ds.had.co.nz/
- https://ggplot2.tidyverse.org/reference/index.html#geoms


## GettingStarted

R Documentation
A "?" infront of function will display help documentation
?runif()

Read Data from file:

yrbss_2017 <- readRDS("yrbss_2017.rds")


sport_heights <- read.csv("sport_heights.csv")


Using !is.na to remove na values from q88 field and assign remaining values to sleep from 2007 dataset:

sleep_2007 <- yrbss_2007$q88[!is.na(yrbss_2007$q88)]


Check type of an Object:
typeof() 

Check structure of data:
str()

## Generate and assign Normal Distribution to sample vector
sample <- rnorm(n = 10, mean = 2, sd = 4)

## Student's t-Test
**t.test()** – Used to perform one and two sample test on sample from population. The test is based upon the t-distribution which is not the same as normal distribution. It is common that we do not know the values for the entire population so t-distribution is a better approximation.

t.test(x, y = NULL,
       alternative = c("two.sided", "less", "greater"),
       mu = 0, paired = FALSE, var.equal = FALSE,
       conf.level = 0.95, ...)
       
## Proportions Test
**prop.test()** – This test is used when we have a large enough sample size. Since prop.test assumes normal distribution, if nπ ≥ 10 and n(1 − π) ≥ 10, the Normal approximation works 
quite well.


## Binomial Test
**binom.test()** – Can be used instead of prop.test but is computationally expensive. Binom.test is better than prop.test when sample size is small.

**Inference of the median** – We can use binom.test and prop.test to obtain the p-value values that fall within a defined range by labeling them as successes. We cannot use the provided confidence intervals from these tests so must determine confidence interval of median by using the formula  provided in lecture relative to the sample median.


## Welch Two Sample t-test
t.test(x,y)

### R Simulation - Welch Two Sample t-test

Consider two populations:

1. Uniform(0, 5), which has a mean of 2.5
2. Uniform(0, 1), which has a mean of 0.5

a\) **Edit the function `sim_ci()`** from lab to:

* draw a sample of size `n_1` from a population 1, and
* draw a sample of size `n_2` from a population 2, then 

sim_ci <- function(n_1, n_2){
  delta <- 2.5-.5

  1) Generate data

  #Generate uniform distribution
  sample_1 <- runif(n_1, 0, 5)
  sample_2 <- runif(n_2, 0, 1)
  
  2) Run `t.test()`
  test_result <- t.test(x = sample_1, y = sample_2)
  
  3) Extract CI
  ci <- test_result$conf.int
  
  4) Check if delta is in CI
  lower <- ci[1]
  upper <- ci[2]
  lower < delta & upper > delta
  

### Run simulation function (returns TRUE or FALSE)
sim_ci(n_1 = 5, n_2 = 5)


### Replicate simulation and calculate proportion of values within the CI
ci_values_valid <- replicate(50000, sim_ci(n_1 = 5, n_2 = 5))
mean(ci_values_valid)



## Permutation Test
**Permutation Test** – Used when sample sizes are small and can’t reasonably say that the data is from normal populations (t-based procedure probably not valid). May use if lots of zeros when log-transformation is not recommended. Assumes null hypothesis is true and that every outcome/labeling is equally likely.


    #example with data created from scratch
    cold <- c(1, 1, 1, 3) # number of o-ring incidents in launches < 18C
    warm <- c(rep(0, times = 17), 1, 1, 2) # ditto above 18 degrees C

    o_ring_data <- c(cold, warm)
    
    
    #general formula
    perm_tstat <- function(x, n1){
      n <- length(x)
      grp1_indices <- sample(1:n, size = n1, replace = FALSE)
      grp1_perm <- x[grp1_indices] 
      grp2_perm <- x[-grp1_indices] 
      t.test(grp1_perm, grp2_perm)$statistic
    }
    
    perm_tstat(o_ring_data, n1 = 4)

## Wilcoxon Rank-Sum Test (two independent samples)
**Wilcoxon Rank-Sum Test** – Used to assess whether there is a ‘difference’ between two population distributions. Assumes two independent samples. Another way to phrase this is, we are testing if the two samples come from the same population.

wilcox.test(x, y = NULL,
            alternative = c("two.sided", "less", "greater"),
            mu = 0, paired = FALSE, exact = NULL, correct = TRUE,
            conf.int = FALSE, conf.level = 0.95,
            tol.root = 1e-4, digits.rank = Inf, ...)


## Wilcoxon Signed-Rank (single-sample or paired-sample data)
**Wilcoxon Signed-Rank** – Used for single-sample or paired-sample data to assess whether a particular value is the ‘center’ of a distribution of values (one-sample setting) or differences (paired two-sample setting).

wilcox.test(x, y = NULL,
            alternative = c("two.sided", "less", "greater"),
            mu = 0, paired = FALSE, exact = NULL, correct = TRUE,
            conf.int = FALSE, conf.level = 0.95,
            tol.root = 1e-4, digits.rank = Inf, ...)

## Levene's Test
Levene's Test – Used to compare the spreads of two populations. If we’re really interested in whether two populations are the same or different, then we should consider not only their centers but also their spread

library(car)

leveneTest(Lifetime~Diet, data=case0501)

## Bootstrap Methods (independent representative samples)
Bootstrap Methods – Is a method for estimating the sampling distribution from the data at hand. Assumes independent representative samples.



