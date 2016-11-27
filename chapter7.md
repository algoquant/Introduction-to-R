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
## Interpreting the Regression Statistics

The regression summary is a list, and its elements can be accessed individually, The standard errors of the regression are the standard deviations of the coeﬃcients, given the residuals as the source of error.

The key assumption in the above formula for the standard error and the p-value is that the residuals are normally distributed, independent, and stationary.

If the residuals are not normally distributed, independent, and stationary, then the standard error and the p-value may be much bigger than reported by `summary.lm()`, and therefore the regression may not be statistically signiﬁcant.

Market return time series are very far from normal, so the small p-values shouldn’t be automatically interpreted as meaning that the regression is statistically signiﬁcant.

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
