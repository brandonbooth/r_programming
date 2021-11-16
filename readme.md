# Coding Notes
by [Brandon Booth](https://brandon-booth.com/) - Fall 2021


## Table of Contents
- [GettingStarted](#GettingStarted)


**Helpful links:**
- https://rstudio.cloud/learn/primers/1.2

> Note: TBD...

## GettingStarted


R Documentation
?factorial. --> will bring you to help page
?runif()





x: ```x```

```sh
x
```

Generate and assign Normal Distribution to sample vector
sample <- rnorm(n = 10, mean = 2, sd = 4)



Student's t-Test
t.test(x, y = NULL,
       alternative = c("two.sided", "less", "greater"),
       mu = 0, paired = FALSE, var.equal = FALSE,
       conf.level = 0.95, ...)
       
       
R Simulation - Welch Two Sample t-test

Consider two populations:

1. Uniform(0, 5), which has a mean of 2.5
2. Uniform(0, 1), which has a mean of 0.5

a\) **Edit the function `sim_ci()`** from lab to:

* draw a sample of size `n_1` from a population 1, and
* draw a sample of size `n_2` from a population 2, then 

sim_ci <- function(n_1, n_2){
  delta <- 2.5-.5

  # 1) Generate data

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
  
  

# Run simulation function (returns TRUE or FALSE)
sim_ci(n_1 = 5, n_2 = 5)


#Replicate simulation and calculate proportion of values within the CI
ci_values_valid <- replicate(50000, sim_ci(n_1 = 5, n_2 = 5))
mean(ci_values_valid)


Permutation Test

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

Wilcoxon Rank-Sum Test (two independent samples)


Wilcoxon Signed-Rank (single-sample or paired-sample data)


Levene's Test


Bootstrap Methods (independent representative samples)









Wi
