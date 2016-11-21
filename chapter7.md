--- 
title_meta  : Chapter 7
title       : Regression and tests
description : Utilize R for statistical analysis.


--- type:NormalExercise lang:r xp:100 skills:1 key:f625f0fd8d
## Hypothesis Testing

Hypothesis Testing is designed to test the validity of a null hypothesis.

A Hypothesis Test consists of: 

null hypothesis, 
test statistic (from sample), 
signiﬁcance level α, determining whether to accept or reject the null hypothesis, 
p-value (probability of observing the test statistic value, assuming the null hypothesis is TRUE).

If the p-value is less than the signiﬁcance level α, then the null hypothesis is rejected, The objective of Hypothesis Testing is to invalidate the null hypothesis, In statistics we cannot prove that a hypothesis is TRUE; we can only conclude that it’s very unlikely to be FALSE (given the data).

*** =instructions
- Compare p-values with certain significance value.

*** =hint
Follow the instruction and introduction. Perform two-tailed test that sample is from Standard Normal Distribution (mean=0, SD=1)

*** =pre_exercise_code
```{r}
```

*** =sample_code

```{r}
# generate vector of samples and store in data frame
test_frame <- data.frame(samples=rnorm(1000))

# significance level, two-tailed test, critical value=2*SD
signif_level

# print significance level


# change the code to get p-values for all the samples
test_frame$p_values <-
  sapply(test_frame$samples, rnorm)
test_frame$p_values <-
  abs(test_frame$p_values-0.5)

# compare p_values to significance level
test_frame$result <- test_frame$p_values > signif_level

# number of null rejections
sum(!test_frame$result)

# show null rejections
head(test_frame[!test_frame$result, ])
```

*** =solution
```{r}
# generate vector of samples and store in data frame
test_frame <- data.frame(samples=rnorm(1000))

# significance level, two-tailed test, critical value=2*SD
signif_level <- 2*(1-pnorm(2))

# print significance level
signif_level

# change the code to get p-values for all the samples
test_frame$p_values <-
  sapply(test_frame$samples, pnorm)
test_frame$p_values <-
  2*(0.5-abs(test_frame$p_values-0.5))

# compare p_values to significance level
test_frame$result <- test_frame$p_values > signif_level

# number of null rejections
sum(!test_frame$result)

# show null rejections
head(test_frame[!test_frame$result, ])
```

*** =sct
```{r}
test_error()
success_msg("First step to statistics!")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:d4ddcf9a7d
## Formula Objects

Formulas in R are deﬁned using the `~` operator followed by a series of terms separated by the `+` operator.

Formulas can be deﬁned as separate objects, manipulated, and passed to functions, The formula `z ~ x` means the response variable z is explained by the explanatory variable x, The formula `z ~ x + y` represents a linear model: z = ax + by + c, The formula `z ~ x - 1` or `z ~ x + 0` represents a linear model with zero intercept: z = ax

The function update() modiﬁes existing formulas

The `.` symbol represents either all the remaining data, or the variable that was in this part of the formula

*** =instructions
- Construct and modify formula objects

*** =hint
Follow the instruction and introductions. Formula objects are firstly constructed like a string, then turned to formula objects.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# formula of linear model with zero intercept


# print the formula object


# collapsing a character vector into a text string


# add `+` between elements


# creating formula from text string
lin_formula <- as.formula(
          paste(paste0("x", 1:5), collapse="+")
      )

# get the class of object


# print the object


# modify the formula using "update"

```

*** =solution
```{r}
# formula of linear model with zero intercept
lin_formula <- z ~ x + y - 1

# print the formula object
lin_formula

# collapsing a character vector into a text string
paste0("x", 1:5)

# add `+` between elements
paste(paste0("x", 1:5), collapse="+")

# add codes to create formula from text string
lin_formula <- as.formula(
        paste("z ~ ",
          paste(paste0("x", 1:5), collapse="+")
          )
      )

# get the class of object
class(lin_formula)

# print the object
lin_formula

# modify the formula using "update"
update(lin_formula, log(.) ~ . + beta)
```

*** =sct
```{r}
test_error()
success_msg("Wonderful!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:c8f389fdbd
## Linear Regression Using lm()

Let the data generating process for the response variable be given as: 
z = αlat + βlatx + εlat 

Where αlat and βlat are latent (unknown) coeﬃcients, and εlat is an unknown vector of random noise (error terms)

The error terms are the diﬀerence between the measured values of the response minus the (unknown) actual response values.

The function `lm()` ﬁts a linear model into a set of data, and returns an object of class "lm", which is a list containing the results of ﬁtting the model: call - the model formula, coeﬃcients - the ﬁtted model coeﬃcients (α, βj), residuals - the model residuals (response minus ﬁtted values),.

he regression residuals are not the same as the error terms, because the regression coeﬃcients are not equal to the coeﬃcients of the data generating process

*** =instructions
- Run OLS regression with lm()

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# initialize random number generator
set.seed(1121)

# define explanatory variable


# define random noise


# response equals linear form plus error terms


# specify regression formula


# perform regression


# regressions have class lm


# get attributes


# regression formula


# regression coefficients


# get coefficients in another way

```

*** =solution
```{r}
# initialize random number generator
set.seed(1121)

# define explanatory variable
explana_tory <- rnorm(100, mean=2)

# define random noise
noise <- rnorm(100)

# response equals linear form plus error terms
res_ponse <- -3 + explana_tory + noise

# specify regression formula
reg_formula <- res_ponse ~ explana_tory

# perform regression
reg_model <- lm(reg_formula)

# regressions have class lm
class(reg_model)

# get attributes
attributes(reg_model)

# regression formula
eval(reg_model$call$formula)

# regression coefficients
reg_model$coefficients

# get coefficients in another way
coef(reg_model)
```

*** =sct
```{r}
success_msg("Nice work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:f09c0189ac
## The Regression Scatterplot

The generic function `plot()` produces a scatterplot when it’s called on the regression formula, `abline()` plots a straight line corresponding to the regression coeﬃcients, when it’s called on the regression object.

The ﬁtted (predicted) values are the values of the response variable obtained from applying the regression model to the explanatory variables

*** =instructions
- Plot the underlying data as well as your OLS model to the plot!

*** =hint
Follow the instruction and introductions

*** =pre_exercise_code
```{r}
set.seed(1121)  # initialize random number generator
# define explanatory variable
explana_tory <- rnorm(100, mean=2)
noise <- rnorm(100)
# response equals linear form plus error terms
res_ponse <- -3 + explana_tory + noise
# specify regression formula
reg_formula <- res_ponse ~ explana_tory
reg_model <- lm(reg_formula)  # perform regression
```

*** =sample_code
```{r}
# set parameters for plot


# plot scatterplot using formula


# set title and position


# add regression line


# plot fitted (predicted) response values

```

*** =solution
```{r}
# set parameters for plot
par(oma=c(1, 2, 1, 0), mgp=c(2, 1, 0), mar=c(5, 1, 1, 1), cex.lab=0.8, cex.axis=1.0, cex.main=0.8, cex.sub=0.5)

# plot scatterplot using formula
plot(reg_formula)

# set title and position
title(main="Simple Regression", line=-1)

# add regression line
abline(reg_model, lwd=2, col="red")

# plot fitted (predicted) response values
points(x=explana_tory, y=reg_model$fitted.values, pch=16, col="blue")
```

*** =sct
```{r}
success_msg("Great job!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7090dc3538
## Regression Summary

The function `summary.lm()` produces a list of regression model summary statistics: 

coeﬃcients: matrix with estimated coeﬃcients, their t-statistics, and p-values, r

.squared: fraction of response variance explained by the model (correlation between response and explanatory), 

adj.r.squared: r.squared adjusted for higher model complexity, 

fstatistic: ratio of variance explained by model divided by unexplained variance.

The regression null hypothesis is that the regression coeﬃcients are zero, The t-statistic (t-value) is the ratio of the estimated value divided by its standard error, The p-value is the probability of obtaining the observed value of the t-statistic, or even more extreme values, under the null hypothesis, A small p-value is often interpreted as meaning that the coeﬃcients are very unlikely to be zero (given the data),


*** =instructions
- Check regression results in detail.

*** =hint
Follow the instruction and introduction!

*** =pre_exercise_code
```{r}
# no pec
set.seed(1121)  # initialize random number generator
# define explanatory variable
explana_tory <- rnorm(100, mean=2)
noise <- rnorm(100)
# response equals linear form plus error terms
res_ponse <- -3 + explana_tory + noise
# specify regression formula
reg_formula <- res_ponse ~ explana_tory
reg_model <- lm(reg_formula)  # perform regression
```

*** =sample_code
```{r}
# copy regression summary
reg_model_sum <- summary(reg_model)

# print the summary to console
reg_model_sum

# get summary elements

```

*** =solution
```{r}
# copy regression summary
reg_model_sum <- summary(reg_model)

# print the summary to console
reg_model_sum

# get summary elements
attributes(reg_model_sum)$names
```

*** =sct
```{r}
success_msg("There's so much beyond a simple print!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:a80ae7fbe8
## Benchmarking the Speed of R Code

The function system.time() calculates the execution time (in seconds) used to evaluate a given expression, system.time() returns the ”user time” (execution time of user instructions), the ”system time” (execution time of operating system calls), and ”elapsed time” (total execution time, including system latency waiting), The function microbenchmark() from package microbenchmark calculates and compares the execution time of R expressions (in milliseconds), and is more accurate than system.time(), microbenchmark() executes the expression many times, and returns the distribution of total execution times.

*** =instructions
- Get the details about model coefficients

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
set.seed(1121)  # initialize random number generator
# define explanatory variable
explana_tory <- rnorm(100, mean=2)
noise <- rnorm(100)
# response equals linear form plus error terms
res_ponse <- -3 + explana_tory + noise
# specify regression formula
reg_formula <- res_ponse ~ explana_tory
reg_model <- lm(reg_formula)  # perform regression
reg_model_sum <- summary(reg_model)
```

*** =sample_code
```{r}
# get coefficients in model summary


# get r-squre in model summary


# get adjusted r-square in model summary


# get f-statistic in model summary


# standard error of beta


# get sd error of beta by hand


# get model anova analysis

```

*** =solution
```{r}
# get coefficients in model summary
reg_model_sum$coefficients

# get r-squre in model summary
reg_model_sum$r.squared

# get adjusted r-square in model summary
reg_model_sum$adj.r.squared

# get f-statistic in model summary
reg_model_sum$fstatistic

# standard error of beta
reg_model_sum$coefficients["explana_tory", "Std. Error"]

# get sd error of beta by hand
sd(reg_model_sum$residuals)/sd(explana_tory)/sqrt(unname(reg_model_sum$fstatistic[3]))

# get model anova analysis
anova(reg_model)
```

*** =sct
```{r}
success_msg("Bravo!")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:b6125af738
## Weak Regression

If the relationship between the response and explanatory variables is weak compared to the error terms (noise), then the regression will have low statistical signiﬁcance

*** =instructions
- See results from a regression with weak linear relationships underneath.

*** =hint
Follow the instruction and introductions. 

*** =pre_exercise_code
```{r}
set.seed(1121)  # initialize random number generator
# define explanatory variable
explana_tory <- rnorm(100, mean=2)
noise <- rnorm(100)
# response equals linear form plus error terms
res_ponse <- -3 + explana_tory + noise
# specify regression formula
reg_formula <- res_ponse ~ explana_tory
reg_model <- lm(reg_formula)  # perform regression
reg_model_sum <- summary(reg_model)
```

*** =sample_code
```{r}
# initialize random number generator
set.seed(1121)

# high noise compared to coefficient
res_ponse <- 3 + 2*explana_tory + rnorm(30, sd=8)

# perform regression


# estimate of regression coefficient is not statistically significant

```

*** =solution
```{r}
# initialize random number generator
set.seed(1121)

# high noise compared to coefficient
res_ponse <- 3 + 2*explana_tory + rnorm(30, sd=8)

# perform regression
reg_model <- lm(reg_formula)

# estimate of regression coefficient is not statistically significant
summary(reg_model)
```

*** =sct
```{r}
success_msg("Great!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7aa0a94261
## Inﬂuence of Noise on Regression

Generally speaking, noise will hinder regressions from producing accurate, or sensible results. We will spend the exercises on this effect.


*** =instructions
- Produce charts to reveal relationships between critial measures and noises.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# noisy regression
reg_stats <- function(std_dev) {

# initialize number generator


# create explanatory and response variables
  explana_tory
  res_ponse

# specify regression formula


# perform regression and get summary
  

# extract regression statistics


}

# produce a vector of standard deviation


# create x-axis labels


# apply reg_stats() to vector of std dev values


# change the code to plot in loop
par(mfrow, 1))
for (in_dex in 1:NCOL(mat_stats)) {
  plot(mat_stats, type="o",
 xaxt="l", xlab="n", ylab="s", main="False")
  title(main=colnames(mat_stats), line=1.0)
  axis(2, at=1:(NROW(mat_stats)),
 labels=rownames(mat_stats))
}
```

*** =solution
```{r}
# noisy regression
reg_stats <- function(std_dev) {

# initialize number generator
  set.seed(1121)

# create explanatory and response variables
  explana_tory <- seq(from=0.1, to=3.0, by=0.1)
  res_ponse <- 3 + 0.2*explana_tory +
    rnorm(30, sd=std_dev)

# specify regression formula
  reg_formula <- res_ponse ~ explana_tory

# perform regression and get summary
  reg_model_sum <- summary(lm(reg_formula))

# extract regression statistics
  with(reg_model_sum, c(pval=coefficients[2, 4],
   adj_rsquared=adj.r.squared,
   fstat=fstatistic[1]))
}

# produce a vector of standard deviation
vec_sd <- seq(from=0.1, to=0.5, by=0.1)

# create x-axis labels
names(vec_sd) <- paste0("sd=", vec_sd)

# apply reg_stats() to vector of std dev values
mat_stats <- t(sapply(vec_sd, reg_stats))

# change the code to plot in loop
par(mfrow=c(NCOL(mat_stats), 1))
for (in_dex in 1:NCOL(mat_stats)) {
  plot(mat_stats[, in_dex], type="l",
 xaxt="n", xlab="", ylab="", main="")
  title(main=colnames(mat_stats)[in_dex], line=-1.0)
  axis(1, at=1:(NROW(mat_stats)),
 labels=rownames(mat_stats))
}
```

*** =sct
```{r}
success_msg("Press on for your conquest!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:d6245c1bb1
## Inﬂuence of Noise on Regression Another Method

Learn to investigate the influence of regressions on methods in another way round.

*** =instructions
- Learn to investigate the influence of regressions on methods in another way round.

*** =hint
Follow the instructions and introductions.


*** =pre_exercise_code
```{r}
library(microbenchmark)
```

*** =sample_code
```{r}
# get regression
reg_stats <- function(da_ta) {

# perform regression and get summary
  col_names
  reg_formula <- paste(sep="~")
  reg_model_sum <- summary(lm(reg_formula, data))
                        
# extract regression statistics
  with(reg_model_sum)
}

# apply reg_stats() to vector of std dev values


# create x-axis labels


# apply reg_stats() to vector of std dev values
mat_stats <-
  t(sapply(vec_sd, function (std_dev) {

# initialize number generator
    

# create explanatory and response variables
    
    reg_stats(data.frame(explana_tory, res_ponse))
    }))

# change the code to plot in loop
par(mfrow=c(NCOL(mat_stats), 1))
for (in_dex in 1:NCOL(mat_stats)) {
  plot(mat_stats, type="o",
 xaxt="l", xlab="n", ylab="", main="False")
  title(main=colnames(mat_stats), line=1.0)
  axis(2, at=1:(NROW(mat_stats)),
 labels=rownames(mat_stats))
}
```

*** =solution
```{r}
# get regression
reg_stats <- function(da_ta) {

# perform regression and get summary
  col_names <- colnames(da_ta)
  reg_formula <-
    paste(col_names[2], col_names[1], sep="~")
  reg_model_sum <- summary(lm(reg_formula,
                        data=da_ta))
                        
# extract regression statistics
  with(reg_model_sum, c(pval=coefficients[2, 4],
   adj_rsquared=adj.r.squared,
   fstat=fstatistic[1]))
}

# apply reg_stats() to vector of std dev values
vec_sd <- seq(from=0.1, to=0.5, by=0.1)

# create x-axis labels
names(vec_sd) <- paste0("sd=", vec_sd)

# apply reg_stats() to vector of std dev values
mat_stats <-
  t(sapply(vec_sd, function (std_dev) {

# initialize number generator
    set.seed(1121)

# create explanatory and response variables
    explana_tory <- seq(from=0.1, to=3.0, by=0.1)
    res_ponse <- 3 + 0.2*explana_tory +
rnorm(30, sd=std_dev)
    reg_stats(data.frame(explana_tory, res_ponse))
    }))

# change the code to plot in loop
par(mfrow=c(NCOL(mat_stats), 1))
for (in_dex in 1:NCOL(mat_stats)) {
  plot(mat_stats[, in_dex], type="l",
 xaxt="n", xlab="", ylab="", main="")
  title(main=colnames(mat_stats)[in_dex], line=-1.0)
  axis(1, at=1:(NROW(mat_stats)),
 labels=rownames(mat_stats))
}
```

*** =sct
```{r}
success_msg("Nice work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:c1a08e245c
## Regression Diagnostic Plots

`plot()` produces diagnostic scatterplots for the residuals, when called on the regression object.

The diagnostic scatterplots allow for visual inspection to determine the quality of the regression ﬁt, ”Residuals vs Fitted” is a scatterplot of the residuals vs. the predicted responses, ”Scale-Location” is a scatterplot of the square root of the standardized residuals vs. the predicted responses, The residuals should be randomly distributed around the horizontal line representing zero residual error.

A pattern in the residuals indicates that the model was not able to capture the relationship between the variables, or that the variables don’t follow the statistical assumptions of the regression model.

”Normal Q-Q” is the standard Q-Q plot, and the points should fall on the diagonal line, indicating that the residuals are normally distributed, ”Residuals vs Leverage” is a scatterplot of the residuals vs. their leverage, Leverage measures the amount by which the predicted response would change if the observed response were shifted by a small amount, Cook’s distance measures the inﬂuence of a single observation on the predicted values, and is proportional.

*** =instructions
- Use various plots to investigate model fit.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
set.seed(1121)  # initialize random number generator
# define explanatory variable
explana_tory <- rnorm(100, mean=2)
noise <- rnorm(100)
# response equals linear form plus error terms
res_ponse <- -3 + explana_tory + noise
# specify regression formula
reg_formula <- res_ponse ~ explana_tory
reg_model <- lm(reg_formula)
```

*** =sample_code
```{r}
# plot 2x2 panels
par(mfrow=c(2, 2))

# plot diagnostic scatterplots
plot(reg_model)

# plot just Q-Q
plot(reg_model, which=2)
```

*** =solution
```{r}
# plot 2x2 panels
par(mfrow=c(2, 2))

# plot diagnostic scatterplots
plot(reg_model)

# plot just Q-Q
plot(reg_model, which=2)
```

*** =sct
```{r}
success_msg("Beautiful!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e9ca3eeb99
## Durbin-Watson Test of Autocorrelation of Residuals

The Durbin-Watson test is designed to test the null hypothesis that the autocorrelations of regression residuals are equal to zero.

The value of the Durbin-Watson statistic DW is close to zero for large positive autocorrelations, and close to four for large negative autocorrelations, The DW is close to two for autocorrelations close to zero, The p-value for the reg model regression is large, and we conclude that the null hypothesis is TRUE, and the regression residuals are uncorrelated.

*** =instructions
- Conduct DW test on regression results.

*** =hint
Follow the instruction and introductions. Remember to load "lmtest" package.

*** =pre_exercise_code
```{r}
set.seed(1121)  # initialize random number generator
# define explanatory variable
explana_tory <- rnorm(100, mean=2)
noise <- rnorm(100)
# response equals linear form plus error terms
res_ponse <- -3 + explana_tory + noise
# specify regression formula
reg_formula <- res_ponse ~ explana_tory
reg_model <- lm(reg_formula)
```

*** =sample_code
```{r}
# load lmtest


# perform Durbin-Watson test

```

*** =solution
```{r}
# load lmtest
library(lmtest)

# perform Durbin-Watson test
dwtest(reg_model)
```

*** =sct
```{r}
success_msg("Nice one!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:8e5ade7078
## Vectorized Functions for Matrix Computations

`apply()` loops are very ineﬃcient for calculating statistics over rows and columns of very large matrices, R has very fast vectorized compiled functions for calculating sums and means of rows and columns: 
````
rowSums(),
colSums(),
rowMeans(),
colMeans()
````
These vectorized functions are also compiled functions, so they’re very fast because they pass their data to compiled C++ code, which performs the loop calculations

*** =instructions
- Utilize compiled functions dedicated for matrix to save additional time. Compare their speed with `*apply()` family.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
library(microbenchmark)
```

*** =sample_code
```{r}
# matrix with 5,000 rows
big_matrix <- matrix(rnorm(10000), ncol=2)

# calculate row sums two different ways

```

*** =solution
```{r}
# matrix with 5,000 rows
big_matrix <- matrix(rnorm(10000), ncol=2)

# calculate row sums two different ways
summary(microbenchmark(
  row_sums=rowSums(big_matrix),
  ap_ply=apply(big_matrix, 1, sum),
  times=10))[, c(1, 4, 5)]
```

*** =sct
```{r}
success_msg("Great!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:ec87541ef1
## Fast R Code for Matrix Computations

The functions `pmax()` and `pmin()` calculate the ”parallel” maxima (minima) of multiple vector arguments, `pmax()` and `pmin()` return a vector, whose n-th element is equal to the maximum (minimum) of the n-th elements of the arguments, with shorter vectors recycled if necessary, `pmax.int()` and `pmin.int()` are methods of generic functions `pmax()` and `pmin()`, designed for atomic vectors, `pmax()` can be used to quickly calculate the maximum values of rows of a matrix, by ﬁrst converting the matrix columns into a list, and then passing them to `pmax()`, `pmax.int()` and `pmin.int()` are very fast because they are compiled functions (compiled from C++ code).


*** =instructions
- Use `pmax()` and `pmin()` family to search through the matrix.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
big_matrix <- matrix(rnorm(10000), ncol=2)
```

*** =sample_code
```{r}
# load the microbenchmark package


# see the structure of pmax function


# calculate row maximums two different ways
summary(microbenchmark(
  p_max=
    do.call(pmax.int,big_matrix),
  l_apply=
    lapply(seq_along(big_matrix[, 1]),
  function(in_dex) max(big_matrix[in_dex, ])),
  times=10)[, c(1, 4, 5)]
```

*** =solution
```{r}
# load the microbenchmark package
library(microbenchmark)

# see the structure of pmax function
str(pmax)

# calculate row maximums two different ways
summary(microbenchmark(
  p_max=
    do.call(pmax.int,
lapply(seq_along(big_matrix[1, ]),
  function(in_dex) big_matrix[, in_dex])),
  l_apply=unlist(
    lapply(seq_along(big_matrix[, 1]),
  function(in_dex) max(big_matrix[in_dex, ]))),
  times=10))[, c(1, 4, 5)]
```

*** =sct
```{r}
success_msg("Wonderful!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:3d8a9618b9
## Package matrixStats for Fast Matrix Computations

The package matrixStats contains functions for calculating aggregations over matrix columns and rows, and other matrix computations, such as: estimating location and scale: `rowRanges()`, `colRanges()`, and `rowMaxs()`, `rowMins()`, etc., testing and counting values: `colAnyMissings()`, `colAnys()`, etc., cumulative functions: `colCumsums()`, `colCummins()`, etc., binning and diﬀerencing: `binCounts()`, `colDiffs()`, etc.

A summary of matrixStats functions can be found under: "https://cran.r-project.org/web/packages/matrixStats/ vignettes/matrixStats-methods.html"

The matrixStats functions are very fast because they are compiled functions (compiled from C++ code)

*** =instructions
- Explore the functions in `matrixStats` package.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
library(microbenchmark)
big_matrix <- matrix(rnorm(10000), ncol=2)
```

*** =sample_code
```{r}
# load package matrixStats


# calculate row min values three different ways
summary(microbenchmark(
  row_mins=rowMins(big_matrix),
  p_min=
    do.call(pmin.int, big_matrix[, in_dex])),
  as_data_frame=
    do.call(pmin.int, big_matrix),
  ))[, c(1, 4, 5)]
```

*** =solution
```{r}
# load package matrixStats
library(matrixStats)

# calculate row min values three different ways
summary(microbenchmark(
  row_mins=rowMins(big_matrix),
  p_min=
    do.call(pmin.int,
      lapply(seq_along(big_matrix[1, ]),
             function(in_dex)
               big_matrix[, in_dex])),
  as_data_frame=
    do.call(pmin.int,
      as.data.frame.matrix(big_matrix)),
  times=10))[, c(1, 4, 5)]
```

*** =sct
```{r}
success_msg("Great!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:7b69825576
## Writing Fast R Code Using Vectorized Operations

R-style code is code that relies on vectorized compiled functions, instead of `for()` loops, `for()` loops in R are slow because they call functions multiple times, and individual function calls are compute-intensive and slow, The brackets `[]` operator is a vectorized compiled function, and is therefore very fast, Vectorized assignments using brackets `[]` and boolean or integer vectors to subset vectors or matrices are therefore preferable to `for()` loops, R code that uses vectorized compiled functions can be as fast as C++ code, R-style code is also very expressive, i.e. it allows performing complex operations with very few lines of code

*** =instructions
- Utilize vectorized operations.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
library(microbenchmark)
big_matrix <- matrix(rnorm(10000), ncol=2)
```

*** =sample_code
```{r}
# assign values to vector three different ways
summary(microbenchmark(

# fast vectorized assignment loop performed in C using brackets "[]"
  brack_ets={vec_tor <- numeric(10)
    vec_tor <- 2},
    
# slow because loop is performed in R
  for_loop={vec_tor <- numeric(10)
    for (in_dex in vec_tor)
      vec_tor[in_dex] <- 2},
      
# very slow because no memory is pre-allocated
# "vec_tor" is "grown" with each new element
  grow_vec={vec_tor <- numeric(0)
    for (in_dex in 1:10)
    
# add new element to "vec_tor" ("grow" it)
      vec_tor[in_dex] <- 2},
  times=10))[, c(1, 4, 5)]
```

*** =solution
```{r}
# assign values to vector three different ways
summary(microbenchmark(

# fast vectorized assignment loop performed in C using brackets "[]"
  brack_ets={vec_tor <- numeric(10)
    vec_tor[] <- 2},
    
# slow because loop is performed in R
  for_loop={vec_tor <- numeric(10)
    for (in_dex in seq_along(vec_tor))
      vec_tor[in_dex] <- 2},
      
# very slow because no memory is pre-allocated
# "vec_tor" is "grown" with each new element
  grow_vec={vec_tor <- numeric(0)
    for (in_dex in 1:10)
    
# add new element to "vec_tor" ("grow" it)
      vec_tor[in_dex] <- 2},
  times=10))[, c(1, 4, 5)]
```

*** =sct
```{r}
success_msg("The speed difference can be enormous!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:cd816481aa
## Vectorized Functions

Functions which use vectorized operations and functions are automatically vectorized themselves, Functions which only call other compiled C vectorized functions, are also very fast, But not all functions are vectorized, or they’re not vectorized with respect to their parameters, Some vectorized functions perform their calculations in R code, and are therefore slow, but convenient to use.


*** =instructions
- Utilize vectorized functions.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
library(microbenchmark)
```

*** =sample_code
```{r}
# define function vectorized automatically
my_fun <- function(in_put, pa_ram) {
  pa_ram*in_put
}

# "in_put" is vectorized


# "pa_ram" is vectorized


# define vectors of parameters of rnorm()
std_devs <-
  structure(1:3, names=paste0("sd=", 1:3))
me_ans <-
  structure(-1:1, names=paste0("mean=", -1:1))

# "sd" argument of rnorm() isn't vectorized


# "mean" argument of rnorm() isn't vectorized

```

*** =solution
```{r}
# define function vectorized automatically
my_fun <- function(in_put, pa_ram) {
  pa_ram*in_put
}

# "in_put" is vectorized
my_fun(in_put=1:3, pa_ram=2)

# "pa_ram" is vectorized
my_fun(in_put=10, pa_ram=2:4)

# define vectors of parameters of rnorm()
std_devs <-
  structure(1:3, names=paste0("sd=", 1:3))
me_ans <-
  structure(-1:1, names=paste0("mean=", -1:1))

# "sd" argument of rnorm() isn't vectorized
rnorm(1, sd=std_devs)

# "mean" argument of rnorm() isn't vectorized
rnorm(1, mean=me_ans)
```

*** =sct
```{r}
success_msg("Flexibility of R code helps with vectorized functions!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:d8823d128f
## Performing sapply() Loops Over Function Parameters

Many functions aren’t vectorized with respect to their parameters, Performing `sapply()` loops over a function’s parameters produces vector output

*** =instructions
- Utilize `sapply()` for vectorized parameter input.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
std_devs <-
  structure(1:3, names=paste0("sd=", 1:3))
me_ans <-
  structure(-1:1, names=paste0("mean=", -1:1))
```

*** =sample_code
```{r}
# sapply produces desired vector output
set.seed(1121)
sapply(std_devs, function(std_dev) rnorm(n=2, sd=std_dev))

# reset seed


# vectorize on rnorm


# reset seed


# vectorize on rnorm


# reset seed


# vectorize on rnorm

```

*** =solution
```{r}
# sapply produces desired vector output
set.seed(1121)
sapply(std_devs, function(std_dev) rnorm(n=2, sd=std_dev))

# reset seed
set.seed(1121)

# vectorize on rnorm
sapply(std_devs, rnorm, n=2, mean=0)

# reset seed
set.seed(1121)

# vectorize on rnorm
sapply(me_ans, function(me_an) rnorm(n=2, mean=me_an))

# reset seed
set.seed(1121)

# vectorize on rnorm
sapply(me_ans, rnorm, n=2)
```

*** =sct
```{r}
success_msg("Applause for your continued performance!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:737ea4a5e4
## Creating Vectorized Functions

In order to vectorize a function with respect to one of its parameters, it’s necessary to perform a loop over it, The function `Vectorize()` performs an `apply()` loop over the arguments of a function, and returns a vectorized version of the function, `Vectorize()` vectorizes the arguments passed to "vectorize.args", `Vectorize()` is an example of a higher-order function: it accepts a function as its argument and returns a function as its value, Functions that are vectorized using `Vectorize()` or `apply()` loops are just as slow as `apply()` loops, but convenient to use

*** =instructions
- `Vectorize()` can also make your functions vectorized.

*** =hint
Follow the instruction and introductions. Assign vectorized function back to the same function name and input results to it.

*** =pre_exercise_code
```{r}
# no pec
std_devs <-
  structure(1:3, names=paste0("sd=", 1:3))
me_ans <-
  structure(-1:1, names=paste0("mean=", -1:1))
```

*** =sample_code
```{r}
# rnorm() vectorized with respect to "std_dev"
vec_rnorm <- function(n, mean=0, sd=1) {
  if (length(sd)==1)
    rnorm(n=n, mean=mean, sd=sd)
  else
    sapply(sd, rnorm, n=n, mean=mean)
}

# reset seed


# run unvectorized function


# rnorm() vectorized with respect to "mean" and "sd"
vec_rnorm 

# reset seed


# run vectorized function, change sd


# reset seed


# run vectorized function, change mean

```

*** =solution
```{r}
# rnorm() vectorized with respect to "std_dev"
vec_rnorm <- function(n, mean=0, sd=1) {
  if (length(sd)==1)
    rnorm(n=n, mean=mean, sd=sd)
  else
    sapply(sd, rnorm, n=n, mean=mean)
}

# reset seed
set.seed(1121)

# run unvectorized function
vec_rnorm(n=2, sd=std_devs)

# rnorm() vectorized with respect to "mean" and "sd"
vec_rnorm <- Vectorize(FUN=rnorm,
        vectorize.args=c("mean", "sd")
)

# reset seed
set.seed(1121)

# run vectorized function, change sd
vec_rnorm(n=2, sd=std_devs)

# reset seed
set.seed(1121)

# run vectorized function, change mean
vec_rnorm(n=2, mean=me_ans)
```

*** =sct
```{r}
success_msg("Use the Vectorize() and save more time!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:530c1e1c92
## The mapply() Functional

The `mapply()` functional is a multivariate version of `sapply()`, that allows calling a non-vectorized function in a vectorized way, `mapply()` accepts a multivariate function passed to the "FUN" argument and any number of vector arguments passed to the dots "...", `mapply()` calls "FUN" on the vectors passed to the dots "...", one element at a time:
````
mapply(FUN = fun,vec1,vec2,...) = [fun(vec1,1,vec2,1,...),..., fun(vec1,i,vec2,i,...),...]
````
`mapply()` passes the ﬁrst vector to the ﬁrst argument of "FUN", the second vector to the second argument, etc. The ﬁrst element of the output vector is equal to "FUN" called on the ﬁrst elements of the input vectors, the second element is "FUN" called on the second elements, etc.

The output of mapply() is a vector of length equal to the longest vector passed to the dots "..." argument, with the elements of the other vectors recycled if necessary.

*** =instructions
- Utilize `mapply()` on matrix.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
std_devs <-
  structure(1:3, names=paste0("sd=", 1:3))
me_ans <-
  structure(-1:1, names=paste0("mean=", -1:1))
```

*** =sample_code
```{r}
# get the structure of sum()


# na.rm is bound by name


# get the structure of rnorm


# mapply vectorizes both arguments "mean" and "sd"


# mapply vectorizes anonymous function


# rnorm() vectorized with respect to "mean" and "sd", dealing with single value as well
vec_rnorm <- function(n, mean=0, sd=1) {
    mapply(rnorm, n=n, mean=mean, sd=sd)
}

# call vec_rnorm() on vector of "sd"


# call vec_rnorm() on vector of "mean"

```

*** =solution
```{r}
# get the structure of sum()
str(sum)

# na.rm is bound by name
mapply(sum, 6:9, c(5, NA, 3), 2:6, na.rm=TRUE)

# get the structure of rnorm
str(rnorm)

# mapply vectorizes both arguments "mean" and "sd"
mapply(rnorm, n=5, mean=me_ans, sd=std_devs)

# mapply vectorizes anonymous function
mapply(function(in_put, e_xp) in_put^e_xp, 1:5, seq(from=1, by=0.2, length.out=5))

# rnorm() vectorized with respect to "mean" and "sd", dealing with single value as well
vec_rnorm <- function(n, mean=0, sd=1) {
  if (length(mean)==1 && length(sd)==1)
    rnorm(n=n, mean=mean, sd=sd)
  else
    mapply(rnorm, n=n, mean=mean, sd=sd)
}

# call vec_rnorm() on vector of "sd"
vec_rnorm(n=2, sd=std_devs)

# call vec_rnorm() on vector of "mean"
vec_rnorm(n=2, mean=me_ans)
```

*** =sct
```{r}
success_msg("Vectorization gets higher dimension!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:944a839cd1
## Vectorized if-else Statements Using Function ifelse()

The function ifelse() performs vectorized if-else statements on vectors, ifelse() is much faster than performing an element-wise loop in R.

*** =instructions
- Use `ifelse()` for vectorized comparison.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# create two numeric vectors
vec_tor1 <- sin(0.25*pi*1:10)
vec_tor2 <- cos(0.25*pi*1:10)

# create third vector using 'ifelse'


# cbind all three together


# set plotting parameters
par(mar=c(7, 2, 1, 2), mgp=c(2, 1, 0),
    cex.lab=0.8, cex.axis=0.8, cex.main=0.8,
    cex.sub=0.5)

# plot matrix
matplot(type="l", lty="solid",
col=c("green", "blue", "red"), xlab="", ylab="")

# add legend
legend(title="", inset=0.05, cex=0.8, lwd=2,
       col=c("green", "blue", "red"))
```

*** =solution
```{r}
# create two numeric vectors
vec_tor1 <- sin(0.25*pi*1:10)
vec_tor2 <- cos(0.25*pi*1:10)

# create third vector using 'ifelse'
vec_tor3 <- ifelse(vec_tor1 > vec_tor2, vec_tor1, vec_tor2)

# cbind all three together
vec_tor4 <- cbind(vec_tor1, vec_tor2, vec_tor3)

# set plotting parameters
par(mar=c(7, 2, 1, 2), mgp=c(2, 1, 0),
    cex.lab=0.8, cex.axis=0.8, cex.main=0.8,
    cex.sub=0.5)

# plot matrix
matplot(vec_tor4, type="l", lty="solid",
col=c("green", "blue", "red"),
lwd=c(2, 2, 2), xlab="", ylab="")

# add legend
legend(x="bottomright", legend=colnames(vec_tor4),
       title="", inset=0.05, cex=0.8, lwd=2,
       lty=c(1, 1, 1), col=c("green", "blue", "red"))
```

*** =sct
```{r}
success_msg("Welcome to a colorful new world!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:75657a12ba
## Monte Carlo Simulation

Monte Carlo simulation consists of generating random samples from a given probability distribution, The Monte Carlo data samples can then used to calculate diﬀerent parameters of the probability distribution (moments, quantiles, etc.), and its functionals.

*** =instructions
- Generate large random numbers to simulate.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# reset random number generator
set.seed(1121)

# set length of simulated sample
sample_length <- 1000

# sample from Standard Normal Distribution


# sample mean - MC estimate


# sample standard deviation - MC estimate


# MC estimate of cumulative probability


# probability of values no bigger than 1


# frequency of less than 1


# MC estimate of 3rd quantile


# find the 75% value in sample

```

*** =solution
```{r}
# reset random number generator
set.seed(1121)

# set length of simulated sample
sample_length <- 1000

# sample from Standard Normal Distribution
sam_ple <- rnorm(sample_length)

# sample mean - MC estimate
mean(sam_ple)

# sample standard deviation - MC estimate
sd(sam_ple)

# MC estimate of cumulative probability
sam_ple <- sort(sam_ple)

# probability of values no bigger than 1
pnorm(1)

# frequency of less than 1
sum(sam_ple<1)/sample_length

# MC estimate of 3rd quantile
qnorm(0.75)

# find the 75% value in sample
sam_ple[0.75*sample_length]
```

*** =sct
```{r}
success_msg("Congrats! Monte Carlo starts with random value!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:a974740ed7
## Simulating Brownian Motion Using while() Loops

while() loops are often used in simulations, when the number of required loops is unknown in advance.

*** =instructions
- Use `while()` loop for specific conditions.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# reset random number generator
set.seed(1121)

# barrier level
lev_el <- 20

# number of simulation steps
len_gth <- 1000

# allocate path vector


# initialize path


# change the code to initialize simulation index
in_dex <- 0
while ((in_dex <= len_gth) &&
 (pa_th[in_dex - 1] < lev_el)) {
 
# change the code to simulate next step
  pa_th[in_dex] <- pa_th[in_dex - 1]
    
# change the code to advance in_dex
  in_dex <- in_dex
}

# fill remaining pa_th after it crosses lev_el


# create daily time series starting 2011


# create plot


# add horizontal line


# set title


# set other parameters
par(oma=c(1, 1, 1, 1), mgp=c(2, 1, 0), mar=c(5, 1, 1, 1), cex.lab=0.8, cex.axis=0.8, cex.main=0.8, cex.sub=0.5)
```

*** =solution
```{r}
# reset random number generator
set.seed(1121)

# barrier level
lev_el <- 20

# number of simulation steps
len_gth <- 1000

# allocate path vector
pa_th <- numeric(len_gth)

# initialize path
pa_th[1] <- 0

# change the code to initialize simulation index
in_dex <- 2
while ((in_dex <= len_gth) &&
 (pa_th[in_dex - 1] < lev_el)) {
 
# simulate next step
  pa_th[in_dex] <-
    pa_th[in_dex - 1] + rnorm(1)
    
# advance in_dex
  in_dex <- in_dex + 1
}

# fill remaining pa_th after it crosses lev_el
if (in_dex <= len_gth) pa_th[in_dex:len_gth] <- pa_th[in_dex - 1]

# create daily time series starting 2011
ts_var <- ts(data=pa_th, frequency=365, start=c(2011, 1))

# create plot
plot(ts_var, type="l", col="black", 
     lty="solid", xlab="", ylab="")

# add horizontal line
abline(h=lev_el, lwd=2, col="red")

# set title
title(main="Brownian motion crossing a barrier level", line=0.5)

# set other parameters
par(oma=c(1, 1, 1, 1), mgp=c(2, 1, 0), mar=c(5, 1, 1, 1), cex.lab=0.8, cex.axis=0.8, cex.main=0.8, cex.sub=0.5)
```

*** =sct
```{r}
success_msg("Hooray! Your first simulated stock path is produced!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:2f39aa9fee
## Simulating Brownian Motion Using Vectorized Functions

Simulations in R can be accelerated by pre-computing a vector of random numbers, instead of generatng them one at a time in a loop, Vectors of random numbers allow using vectorized functions, instead of ineﬃcient (slow) while() loops

*** =instructions
- Use vectorized function to speed up your simulation.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# reset random number generator
set.seed(1121)

# barrier level
lev_el <- 20

# number of simulation steps
len_gth <- 1000

# simulate path of Brownian motion


# find index when pa_th crosses lev_el


# fill remaining pa_th after it crosses lev_el


# create daily time series starting 2011


# create plot with horizontal line


# add horizontal line


# create title

```

*** =solution
```{r}
# reset random number generator
set.seed(1121)

# barrier level
lev_el <- 20

# number of simulation steps
len_gth <- 1000

# simulate path of Brownian motion
pa_th <- cumsum(rnorm(len_gth))

# find index when pa_th crosses lev_el
cro_ss <- which(pa_th > lev_el)

# fill remaining pa_th after it crosses lev_el
if (length(cro_ss)>0) {
  pa_th[(cro_ss[1]+1):len_gth] <-pa_th[cro_ss[1]]
}

# create daily time series starting 2011
ts_var <- ts(data=pa_th, frequency=365, start=c(2011, 1))

# create plot with horizontal line
plot(ts_var, type="l", col="black", lty="solid", xlab="", ylab="")

# add horizontal line
abline(h=lev_el, lwd=2, col="red")

# create title
title(main="Brownian motion crossing a barrier level", line=0.5)
```

*** =sct
```{r}
success_msg("Your first simulated stock path is even faster!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:3452f1b7d3
## Standard Errors of Estimators Using Bootstrap Simulation

The standard errors of estimators can be calculated using a bootstrap simulation.

The bootstrap procedure generates new data by randomly sampling with replacement from the observed data set.

The bootstrapped data is then used to re-calculate the estimator many times, producing a vector of values.

The bootstrapped estimator values can then be used to calculate the probability distribution of the estimator and its standard error.

Bootstrapping doesn’t provide accurate estimates for estimators that are sensitive to the ordering and correlations in the data.

*** =instructions
- Check if the simulated standard deviation is consistent to hypothesis.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# reset random number generator
set.seed(1121)

# number of simualated steps
sample_length <- 1000

# sample from Standard Normal Distribution


# sample mean


# sample standard deviation


# change the code to bootstrap of sample mean and median
boot_strap <- sapply(1:10000, function(x) {
  boot_sample <-
    sam_ple[sample_length, replace=TRUE]
  c(mean=mean(boot_sample),
    median=median(boot_sample))
})

# check first three result


# standard error from formula


# standard error of mean from bootstrap


# standard error of median from bootstrap

```

*** =solution
```{r}
# reset random number generator
set.seed(1121)

# number of simualated steps
sample_length <- 1000

# sample from Standard Normal Distribution
sam_ple <- rnorm(sample_length)

# sample mean
mean(sam_ple)

# sample standard deviation
sd(sam_ple)

# change the code to bootstrap of sample mean and median
boot_strap <- sapply(1:10000, function(x) {
  boot_sample <-
    sam_ple[sample.int(sample_length, replace=TRUE)]
  c(mean=mean(boot_sample),
    median=median(boot_sample))
})

# check first three result
boot_strap[, 1:3]

# standard error from formula
sd(sam_ple)/sqrt(sample_length)

# standard error of mean from bootstrap
sd(boot_strap["mean", ])

# standard error of median from bootstrap
sd(boot_strap["median", ])
```

*** =sct
```{r}
success_msg("Yes! The simulation has no problem with its variation!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:194a77a838
## Standard Errors of Regression Coeﬃcients Using Bootstrap

The standard errors of the regression coeﬃcients can be calculated using a bootstrap simulation.

The bootstrap procedure creates new design matrices by randomly sampling with replacement from the design matrix.

Regressions are performed on the bootstrapped design matrices, and the regression coeﬃcients are saved into a matrix of bootstrapped coeﬃcients.

*** =instructions
- Check the bootstrapped results!

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# define explanatory variable
explana_tory <- rnorm(100, mean=2)

# produce random noise
noise <- rnorm(100)

# produce response variable


# define design matrix and regression formula


# produce formula


# change the code to bootstrap the regression
boot_strap <- sapply(1:100, function(x) {
  boot_sample <-
    sample(dim(design_matrix)[1], replace=TRUE)
  reg_model <- lm(reg_formula)
})
```

*** =solution
```{r}
# define explanatory variable
explana_tory <- rnorm(100, mean=2)

# produce random noise
noise <- rnorm(100)

# produce response variable
res_ponse <- -3 + explana_tory + noise

# define design matrix and regression formula
design_matrix <- data.frame(res_ponse, explana_tory)

# produce formula
reg_formula <- paste(colnames(design_matrix)[1],
  paste(colnames(design_matrix)[-1], collapse="+"),sep=" ~ ")

# change the code to bootstrap the regression
boot_strap <- sapply(1:100, function(x) {
  boot_sample <-
    sample.int(dim(design_matrix)[1], replace=TRUE)
  reg_model <- lm(reg_formula,
          data=design_matrix[boot_sample, ])
  reg_model$coefficients
})
```

*** =sct
```{r}
success_msg("Remember to see the result! Mont Carlo is powerful!")
```