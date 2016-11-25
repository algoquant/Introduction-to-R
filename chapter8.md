---
title_meta  : Chapter 8
title       : Exceptions
description : In this chapter you will learn about several exceptions in R and how to handle with them.

--- type:NormalExercise lang:r xp:100 skills:1 key:f625f0fd8d
## Exception Conditions: Errors and Warnings

Exception conditions are R objects containing information about errors or warnings produced while evaluating expressions, The function warning() produces a warning condition, but doesn’t halt function execution, and returns its message to the warning handler, The function stop() produces an error condition, halts function execution, and returns its message to the error handler.

The handling of warning conditions depends on the value of options("warn"): 

negative then warnings are ignored, 

zero then warnings are stored and printed after the top-level function has completed, 

one - warnings are printed as they occur, two or larger - warnings are turned into errors.

The function suppressWarnings() evaluates its expressions and ignores all warnings.


*** =instructions
- Learn how different exception conditions are handled. Please run the function without argument after you submit the answer for each of the following change

*** =hint
Follow the instruction and introduction. 

*** =pre_exercise_code
```{r}
```

*** =sample_code

```{r}
# global option for "warn"


# global option for "warn"


# global option for "error"


# finish the test function
sqrt_safe <- function(in_put) {

  if (in_put) {
    warning("sqrt_safe: in_put is negative")
    NULL
  } else {
    sqrt(in_put)
  }
}

# input 5


# input -1


# change warning setting to -1


# input -1


# please run the function without argument after you submit the answer for each of the following change
# change warning setting to 0


# change warning setting to 1


# change warning setting to 3

```

*** =solution
```{r}
# global option for "warn"
getOption("warn")

# global option for "warn"
options("warn")

# global option for "error"
getOption("error")

# finish the test function
sqrt_safe <- function(in_put) {

  if (in_put<0) {
    warning("sqrt_safe: in_put is negative")
    NULL
  } else {
    sqrt(in_put)
  }
}

# input 5
sqrt_safe(5)

# input -1
sqrt_safe(-1)

# change warning setting to -1
options(warn=-1)

# input -1
sqrt_safe(-1)

# please run the function without argument after you submit the answer for each of the following change
# change warning setting to 0
options(warn=0)

# change warning setting to 1
options(warn=1)

# change warning setting to 3
options(warn=3)
```

*** =sct
```{r}
test_error()
success_msg("Tired of warnings? You can turn them on or off now")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:d4ddcf9a7d
## Validating Function Arguments

Argument validation consists of ﬁrst determining if any arguments are missing, and then determining if the arguments are of the correct type.

An argument is missing when the formal argument is not bound to an actual value in the function call.

The function `missing()` returns `TRUE` if an argument is missing, and `FALSE` otherwise.

Missing arguments can be detected by: 1. assigning a NULL default value to formal arguments and then calling `is.null()` on them, 2. calling the function `missing()` on the arguments, The argument type can be validated using functions such as `is.numeric()`, `is.character()`, etc. 

The function `return()` returns its argument and terminates futher function execution

*** =instructions
- Evaluate function arguments. Please run the function without argument after you submit the answer for each of the following change.

*** =hint
Follow the instruction and introductions. 

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# function vali_date validates its arguments
vali_date <- function(in_put=NULL) {

# check if argument is valid and return double
  if (?) {
    return("vali_date: in_put is missing")
  } else if (?) {
    2*in_put
  } else cat("vali_date: in_put not numeric")
}

# input 3


# input "a"


# vali_date validates arguments using missing()
vali_date <- function(in_put) {
# check if argument is valid and return double
  if (?) {
    return("vali_date: in_put is missing")
  } else if (?) {
    2*in_put
  } else cat("vali_date: in_put is not numeric")
} 

# input 3


# input "a"

```

*** =solution
```{r}
# function vali_date validates its arguments
vali_date <- function(in_put=NULL) {

# check if argument is valid and return double
  if (is.null(in_put)) {
    return("vali_date: in_put is missing")
  } else if (is.numeric(in_put)) {
    2*in_put
  } else cat("vali_date: in_put not numeric")
}

# input 3
vali_date(3)

# input "a"
vali_date("a")

# vali_date validates arguments using missing()
vali_date <- function(in_put) {
# check if argument is valid and return double
  if (missing(in_put)) {
    return("vali_date: in_put is missing")
  } else if (is.numeric(in_put)) {
    2*in_put
  } else cat("vali_date: in_put is not numeric")
} 

# input 3
vali_date(3)

# input "a"
vali_date("a")
```

*** =sct
```{r}
test_error()
success_msg("Good, now missing arguments can also be handled.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:c8f389fdbd
## Validating Assertions Inside Functions

If assertions about variables inside a function are FALSE, then `stop()` can be called to halt its execution.

Calling `stop()` is preferable to calling `return()`, or inserting `cat()` statements into the code.

Using `stop()` inside a function allows calling the function `traceback()`, if an error was produced, The function `traceback()` prints the call stack, showing the function that produced the error condition, `cat()` statements inside the function body provide information about the state of its variables.

*** =instructions
- Customize error information using `stop()`

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# vali_date() validates its arguments and assertions
vali_date <- function(in_put) {

# change code, check if argument is valid and return double
  if (?) {
    cat("vali_date: in_put is missing")
  } else if (?) {
    cat("in_put=", in_put)
    cat("vali_date: in_put is not numeric")
  } else 2*in_put
}

# input 3
vali_date(3)

# input "a"
vali_date("a")

# call traceback
traceback()
```

*** =solution
```{r}
# vali_date() validates its arguments and assertions
vali_date <- function(in_put) {

# change code, check if argument is valid and return double
  if (missing(in_put)) {
    stop("vali_date: in_put is missing")
  } else if (!is.numeric(in_put)) {
    cat("in_put=", in_put)
    stop("vali_date: in_put is not numeric")
  } else 2*in_put
}

# input 3
vali_date(3)

# input "a"
vali_date("a")

# call traceback
traceback()
```

*** =sct
```{r}
success_msg("Nice work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:f09c0189ac
## Validating Assertions Using stopifnot()  

R provides robust validation and debugging tools through type validation functions, and functions `missing()`, `stop()`, and `stopifnot()`.

If the argument to function `stopifnot()` is FALSE, then it produces an error condition, and halts function execution, `stopifnot()` is a convenience wrapper for `stop()`, and eliminates the need to use `if ()` statements, `stopifnot()` is often used to check the validity of function arguments, `stopifnot()` can be inserted anywhere in the function body in order to check assertions about its variables

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
# define target function
vali_date <- function(in_put) {

# change code, check argument using long form '&&' operator
  !in_put |
      in_put
  2*in_put
}

# check with input 3


# check with input "a"


# modify target function
vali_date <- function(in_put) {

# change code, check argument using logical '&' operator
  !in_put | in_put)
  2*in_put
}

# check with input 

```

*** =solution
```{r}
# define target function
vali_date <- function(in_put) {

# change code, argument using long form '&&' operator
  stopifnot(!missing(in_put) &&
      is.numeric(in_put))
  2*in_put
}

# check with input 3
vali_date(3)

# check with input "a"
vali_date("a")

# modify target function
vali_date <- function(in_put) {

# change code, argument using logical '&' operator
  stopifnot(!missing(in_put) & is.numeric(in_put))
  2*in_put
}

# check with input 
vali_date("a")
```

*** =sct
```{r}
success_msg("Good job!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7090dc3538
## Validating Function Arguments and Assertions

The functions `stop()` and `stopifnot()` halt function execution and produce error conditions if certain assertions are FALSE.

The type validation functions, such as `is.numeric()`, `is.na()`, etc., and `missing()`, allow for validation of arguments and variables inside functions, `cat()` statements can provide information about the state of variables inside a function, `cat()` statements don’t return values, so they provide information even when a function produces an error


*** =instructions
- Utilize all the skills you learnt previously.

*** =hint
Follow the instruction and introduction!

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# sum_two() returns the sum of its two arguments
sum_two <- function(in_put1, in_put2) {

# check if at least one argument is not missing
  stopifnot(!missing(in_put1) &&
      !missing(in_put2))

# both valid      
  if  (&&
      ) {
    in_put1 + in_put2
  } 
  
# in_put1 is valid
  else if () {
    cat("in_put2 is not numeric\n")
    in_put1
  } 
  
# in_put2 is valid
  else if () {
    cat("in_put1 is not numeric\n")
    in_put2
  } else {
  
# otherwise return error message
    
  }
}

# input two numbers


# input a number and a character


# input a character and a number


# input two characters

```

*** =solution
```{r}
# sum_two() returns the sum of its two arguments
sum_two <- function(in_put1, in_put2) {

# check if at least one argument is not missing
  stopifnot(!missing(in_put1) &&
      !missing(in_put2))

# both valid      
  if (is.numeric(in_put1) &&
      is.numeric(in_put2)) {
    in_put1 + in_put2
  } 
  
# in_put1 is valid
  else if (is.numeric(in_put1)) {
    cat("in_put2 is not numeric\n")
    in_put1
  } 
  
# in_put2 is valid
  else if (is.numeric(in_put2)) {
    cat("in_put1 is not numeric\n")
    in_put2
  } else {
  
# otherwise return error message
    stop("none of the arguments are numeric")
  }
}

# input two numbers
sum_two(1, 2)

# input a number and a character
sum_two(5, 'a')

# input a character and a number
sum_two('a', 5)

# input two characters
sum_two('a', 'b')
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
## Omitted Variable Bias

Omitted Variable Bias occurs in a regression model that omits important predictors.

The parameter estimates are biased, even though the t-statistics, p-values, and R-squared all indicate a statistically signiﬁcant regression.

But the Durbin-Watson test shows residuals are autocorrelated, invalidating other tests.

*** =instructions
- Examine the effects of DW test in autocorrelation.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
library(lmtest)
reg_formula <- res_ponse ~ explana_tory
```

*** =sample_code
```{r}
# design matrix


# response depends on both explanatory variables


# mis-specified regression only one explanatory


# get model summary


# get model coefficients


# get model r-square


# Durbin-Watson test shows residuals are autocorrelated


# set plot parameters


# set plot panels


# make plot


# draw a line


# set plot title


# plot just Q-Q

```

*** =solution
```{r}
# design matrix
design_matrix <- data.frame(
  explana_tory=1:30, omit_var=sin(0.2*1:30))

# response depends on both explanatory variables
res_ponse <- with(design_matrix,
  0.2*explana_tory + omit_var + 0.2*rnorm(30))

# mis-specified regression only one explanatory
reg_model <- lm(res_ponse ~ explana_tory, data=design_matrix)

# get model summary
reg_model_sum <- summary(reg_model)

# get model coefficients
reg_model_sum$coefficients

# get model r-square
reg_model_sum$r.squared

# Durbin-Watson test shows residuals are autocorrelated
dwtest(reg_model)$p.value

# set plot parameters
par(oma=c(15, 1, 1, 1), mgp=c(0, 0.5, 0), mar=c(1, 1, 1, 1), cex.lab=0.8, cex.axis=0.8, cex.main=0.8, cex.sub=0.5)

# set plot panels
par(mfrow=c(2,1))

# make plot
plot(reg_formula, data=design_matrix)

# draw a line
abline(reg_model, lwd=2, col="red")

# set plot title
title(main="OVB Regression", line=-1)

# plot just Q-Q
plot(reg_model, which=2, ask=FALSE)
```

*** =sct
```{r}
success_msg("Great!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:ec87541ef1
## Spurious Time Series Regression

Regression of non-stationary time series creates spurious regressions.

The t-statistics, p-values, and R-squared all indicate a statistically signiﬁcant regression, But the Durbin-Watson test shows residuals are autocorrelated, which invalidates the other tests, 

The Q-Q plot also shows that residuals are not normally distributed.


*** =instructions
- Examine several critical measures on spurious regression.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
set.seed(1121)
library(lmtest)
```

*** =sample_code
```{r}
# unit root time series for explanatory variable


# unit root time series for response variable


# construct formula


# perform regression


# summary indicates statistically significant regression


# get model coefficients


# get model r-squared


# Durbin-Watson test shows residuals are autocorrelated


# print DW test results


# set plot parameters


# set plot panels


# plot scatterplot using formula


# set plot title


# add regression line


# plot just Q-Q

```

*** =solution
```{r}
# unit root time series for explanatory variable
explana_tory <- cumsum(rnorm(100))

# unit root time series for response variable
res_ponse <- cumsum(rnorm(100))

# construct formula
reg_formula <- res_ponse ~ explana_tory

# perform regression
reg_model <- lm(reg_formula)

# summary indicates statistically significant regression
reg_model_sum <- summary(reg_model)

# get model coefficients
reg_model_sum$coefficients

# get model r-squared
reg_model_sum$r.squared

# Durbin-Watson test shows residuals are autocorrelated
dw_test <- dwtest(reg_model)

# print DW test results
c(dw_test$statistic[[1]], dw_test$p.value)

# set plot parameters
par(oma=c(15, 1, 1, 1), mgp=c(0, 0.5, 0), mar=c(1, 1, 1, 1), cex.lab=0.8, cex.axis=0.8, cex.main=0.8, cex.sub=0.5)

# set plot panels
par(mfrow=c(2,1))

# plot scatterplot using formula
plot(reg_formula, xlab="", ylab="")

# set plot title
title(main="Spurious Regression", line=-1)

# add regression line
abline(reg_model, lwd=2, col="red")

# plot just Q-Q
plot(reg_model, which=2, ask=FALSE)
```

*** =sct
```{r}
success_msg("Wonderful!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:3d8a9618b9
## Predictions Using Regression Models

The function predict() is a generic function for performing predictions based on a given model, predict.lm() is the predict method for linear models (regressions).

*** =instructions
- Make predictions based on regression models.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
set.seed(1120)
```

*** =sample_code
```{r}
# explanatory variable


# response variable


# construct regression model


# perform regression


# set new data range


# change code to make predictions
predict_lm <- predict(object=reg_model)
              
# convert to data frame


# print the first two lines


# make the plot table

     
# draw the fitted line


# plot points and prediction range

```

*** =solution
```{r}
# explanatory variable
explana_tory <- seq(from=0.1, to=3.0, by=0.1)

# response variable
res_ponse <- 3 + 2*explana_tory + rnorm(30)

# construct regression model
reg_formula <- res_ponse ~ explana_tory

# perform regression
reg_model <- lm(reg_formula)

# set new data range
new_data <- data.frame(explana_tory=0.1*31:40)

# change code to make predictions
predict_lm <- predict(object=reg_model,
              newdata=new_data, level=0.95,
              interval="confidence")
              
# convert to data frame
predict_lm <- as.data.frame(predict_lm)

# print the first two lines
head(predict_lm, 2)

# make the plot table
plot(reg_formula, xlim=c(1.0, 4.0),
     ylim=range(res_ponse, predict_lm),
     main="Regression predictions")
     
# draw the fitted line
abline(reg_model, col="red")

# plot points and prediction range
with(predict_lm, {
  points(x=new_data$explana_tory, y=fit, pch=16, col="blue")
  lines(x=new_data$explana_tory, y=lwr, lwd=2, col="red")
  lines(x=new_data$explana_tory, y=upr, lwd=2, col="red")
})
```

*** =sct
```{r}
success_msg("Brilliant! You've became a statistician now!")
```
