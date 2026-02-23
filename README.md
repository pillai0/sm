# sm

# Practical no:- 1
   Aim: Plotting PDF and CDF for Uniform and Exponential Distributions
Objective: To understand and visualize the Probability Density Function (PDF) and Cumulative
Distribution Function (CDF) for given parameters of Uniform and Exponential distributions.

r codes:-

 # for uniform distribution 
codes:-

# Uniform Distribution Parameters
a <- 0
b <- 1

x <- seq(a - 1, b + 1, length.out = 200)

# PDF
pdf_uniform <- dunif(x, min = a, max = b)

# CDF
cdf_uniform <- punif(x, min = a, max = b)

# Plot PDF
plot(x, pdf_uniform, type = "l", lwd = 2, col = "blue",
     main = "PDF of Uniform(0, 1)",
     xlab = "x", ylab = "Density")

# Plot CDF
plot(x, cdf_uniform, type = "l", lwd = 2, col = "red",
     main = "CDF of Uniform(0, 1)",
     xlab = "x", ylab = "Probability")

# for Exponential Distribution
codes:-

# Exponential Distribution Parameter
lambda <- 1

x <- seq(0, 10, length.out = 200)

# PDF
pdf_exp <- dexp(x, rate = lambda)

# CDF
cdf_exp <- pexp(x, rate = lambda)

# Plot PDF
plot(x, pdf_exp, type = "l", lwd = 2, col = "blue",
     main = "PDF of Exponential(λ = 1)",
     xlab = "x", ylab = "Density")

# Plot CDF
plot(x, cdf_exp, type = "l", lwd = 2, col = "red",
     main = "CDF of Exponential(λ = 1)",
     xlab = "x", ylab = "Probability")


# Practical no:- 3

Aim: Computing Mean, Variance, and Median (Uniform and Exponential)
Objective : To compute and compare theoretical and simulated (Excel-generated) Mean, Variance,
and Median

# in Excel

Step 1: Generate random data
In Excel, in Column A, type heading → Uniform Random Values. →In A2, enter: =RAND()(This
generates numbers between 0 and 1) →Drag the formula down till A21 → Copy → Right-click →
Paste Special → Values.

Step 2: Compute simulated statistics
Mean: =AVERAGE(A2:A21)
Variance: =VAR.P(A2:A21)
Median : =MEDIAN(A2:A21)

Step 3: Compute theoretical statistics for Uniform(0,1)

Here a=0 & b=1
Mean: =(a + b) / 2

Variance :=(b − a)² /12

Median : =(a + b) / 2

# Exponential Distribution

Step 1: Generate exponential random values
Formula to generate exponential random variable:

where and In Column C, heading → Exponential Values. → In C2, enter:=-LN(1-RAND()) →Drag till
C101.

Copy → Paste Special → Values to freeze them.Step 2: Compute simulated statistics
Mean =AVERAGE(C2:C101)

Variance =VAR.P(C2:C101)

Median :=MEDIAN(C2:C101)

Step 3: Compute theoretical
Mean: = 1/λ
Variance:= 1/λ²
Median:= 1/λ²

# in R 
  # for uniform distribution

 # Set seed for same output every time
set.seed(123)

# Sample size
n <- 1000

# Generate Uniform(0,1) random values
u <- runif(n, min = 0, max = 1)

# Simulated statistics
sim_mean_u <- mean(u)
sim_var_u <- var(u)
sim_median_u <- median(u)

# Print results
sim_mean_u
sim_var_u
sim_median_u

# for Exponential Distribution

# Set seed
set.seed(123)

# Sample size
n <- 1000

# Rate parameter λ
lambda <- 2

# Generate Exponential random values
e <- rexp(n, rate = lambda)

# Simulated statistics
sim_mean_e <- mean(e)
sim_var_e <- var(e)
sim_median_e <- median(e)

# Print results
sim_mean_e
sim_var_e
sim_median_e

# Practical no:- 3
Aim: Plotting and Interpreting Normal Distribution

r codes:-

# Step 1: parameters
mean_value <- 0
sd_value <- 1

# Step 2: plot the normal curve
curve(dnorm(x, mean = mean_value, sd = sd_value),
      from = mean_value - 4*sd_value,
      to = mean_value + 4*sd_value,
      main = "Normal Distribution Curve",
      xlab = "x",
      ylab = "Density")

# Step 3: add vertical line at mean
abline(v = mean_value, col = "red", lwd = 2)

# Step 4: Example probabilities
pnorm(1, mean_value, sd_value)        # P(X ≤ 1)
1 - pnorm(1, mean_value, sd_value)    # P(X > 1)
pnorm(1) - pnorm(-1)                  # P(-1 < X < 1)

# Step 5: Z-distribution
curve(dnorm(x),
      from = -4, to = 4,
      main = "Standard Normal Curve (Z)",
      xlab = "Z-score",
      ylab = "Density")

abline(v = 0, col = "blue", lwd = 2)

# Practical no:- 4
Aim: Solving a real-life problem using the Normal distribution

A class has exam marks that are approximately normally distributed with mean= 70
and standard deviation=8 .

1. What is the probability that a randomly chosen student scores more than
85?
2. What is the minimum score required to be in the top 10% of the class?

# Excel (cell formulas)

   Z-score for 85: =STANDARDIZE(85,70,8)
   Probability : =1 - NORM.DIST(85, 70, 8, TRUE) .
   90th percentile (top 10% cutoff): =NORM.INV(0.90, 70, 8)


#  R codes 
codes:-

mu <- 70          # mean
sigma <- 8        # standard deviation

# 1. Probability that a student scores more than 85
x <- 85

# Convert to Z-score
z <- (x - mu) / sigma
z

prob_more_than_85 <- pnorm(x, mean = mu, sd = sigma, lower.tail = FALSE)
prob_more_than_85

# 2. Find the minimum score required for top 10%
# i.e. 90th percentile

cutoff_top_10 <- qnorm(0.90, mean = mu, sd = sigma)

# Practical no:-5
Aim: Simulation of Sampling Distribution of Sample Mean and Proportion

a. Sampling Distribution of Sample Mean
codes:-

population_mean <- 1:100
n_mean <- 10

sample_means <- replicate(1000,
                           mean(sample(population_mean, n_mean, replace = TRUE)))

hist(sample_means,
     main = "Sampling Distribution of Sample Mean",
     xlab = "Sample Mean",
     col = "lightblue",
     breaks = 20)

mean(sample_means)
sd(sample_means)


b. Sampling Distribution of Sample Proportion
codes:-
mean(sample_means)
sd(sample_means)

# (p = 0.6)
population_prop <- rbinom(10000, 1, 0.6)
n_prop <- 20

sample_props <- replicate(1000,
                           mean(sample(population_prop, n_prop, replace = TRUE)))

hist(sample_props,
     main = "Sampling Distribution of Sample Proportion",
     xlab = "Sample Proportion",
     col = "lightgreen",
     breaks = 20)

mean(sample_props)

# Practical no:- 6

Aim: Computing Bias and Standard Error

Parameter Value
Assume
Population Mean (μ) =50
Population SD (σ) =10
Sample Size (n) =30
No. of Simulations= 100

codes:-

mu <- 50
sigma <- 10
n <- 30
B <- 100

estimates <- replicate(B, mean(rnorm(n, mu, sigma)))

bias <- mean(estimates) - mu
print(bias)

se <- sd(estimates)
print(se)

# Practical no:- 7
Aim: To verify the Central Limit Theorem by drawing samples from a non-normal distribution and
checking the normality of sample means.

codes:-
set.seed(1)

x <- runif(10000, min = 0, max = 1)
n <- 30

sample_means <- replicate(1000, mean(sample(x, n)))

hist(sample_means,
     main = "Verification of Central Limit Theorem",
     xlab = "Sample Means",
     col = "lightblue",
     border = "black")

# Practical no:-8
Aim: To calculate covariance and correlation between two variables.

#Using Excel
          x       Y
          2       4
          4       8
          6       12
          8       16
          10      20    
          12      24
          14      28

Covariance: =COVARIANCE.P(A2:A8,B2:B8)
Correlation: =CORREL(A2:A8,B2:B8)

# Using R
codes:-
x <- c(2, 4, 6, 8, 10)
y <- c(4, 8, 12, 16, 20)

# Covariance
cov(x, y)

# Correlation
cor(x, y)

# Practical no:-9 Confidence Interval for Single Mean / Proportion
Aim : To construct a confidence interval for a single population mean using Excel and R.

Sample mean
Sample standard deviation
Sample size
Confidence level = 95%

Excel :
Standard Error: =SD/SQRT(n)
Lower Limit: =Mean - 1.96*(SD/SQRT(n))
Upper Limit: =Mean + 1.96*(SD/SQRT(n))

# in R
codes:-
mean <- 50
sd <- 8
n <- 64
z <- qnorm(0.975)

lower <- mean - z*(sd/sqrt(n))
upper <- mean + z*(sd/sqrt(n))

print(lower)
print(upper)

# Practical no:- 10 Confidence Interval for Difference in Means

Aim : To construct a confidence interval for the difference between two population means using Excel and R.

x1= 60,       n1= 50
x2= 55,       n2= 50
s1= 10,       s2= 8

Excel:
lower limit:- =(x1-x2)-1.96*SQRT((s1*s1/n1)+(s2*s2/n2)
upper limit:- =(x1-x2)+1.96*SQRT((s1*s1/n1)+(s2*s2/n2)

# in R 
codes:-

x1 <- 60; x2 <- 55
s1 <- 10; s2 <- 8
n1 <- 50; n2 <- 50

SE <- sqrt((s1^2/n1) + (s2^2/n2))
z <- qnorm(0.975)

lower <- (x1 - x2) - z*SE
upper <- (x1 - x2) + z*SE

print(lower)
print(upper)
