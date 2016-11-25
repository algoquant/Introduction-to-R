---
title_meta  : Chapter 10
title       : Logistic regression
description : Have a taste of the machine learning techniques in R!

--- type:NormalExercise lang:r xp:100 skills:1 key:36ba783482
## The Logistic Function

The logistic function expresses the cumulative probability of a numerical variable ranging over the whole interval of real numbers.

Where λ is the scale (dispersion) parameter, The logistic function can be inverted to obtain the Odds Ratio (the ratio of probabilities for favorable to unfavorable outcomes).

The function `plogis()` gives the cumulative probability of the Logistic distribution.

*** =instructions
- Discover shapes of logistic regression.

*** =hint
Follow the instructions and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# setting lambda value


# setting colors


# change the code to plot three curves in loop
for (in_dex in 1:3) {
  expr=plogis(x, scale=lamb_da),
xlim=c(0, 0), type="l",
xlab="", ylab="", lwd=100,
col=col_ors, add=(in_dex>20))
}

# add title


# change the code to add legend
legend("bottomright", title="Scale parameters",
       paste("lambda", lamb_da, sep="="),
       inset=50, cex=80, lwd=2,
       lty=c(1, 1, 1), col=col_ors)
```

*** =solution
```{r}
# setting lambda value
lamb_da <- c(0.5, 1, 1.5)

# setting colors
col_ors <- c("red", "black", "blue")

# change the code to plot three curves in loop
for (in_dex in 1:3) {
  curve(expr=plogis(x, scale=lamb_da[in_dex]),
xlim=c(-4, 4), type="l",
xlab="", ylab="", lwd=2,
col=col_ors[in_dex], add=(in_dex>1))
}

# add title
title(main="Logistic function", line=0.5)

# change the code to add legend
legend("topleft", title="Scale parameters",
       paste("lambda", lamb_da, sep="="),
       inset=0.05, cex=0.8, lwd=2,
       lty=c(1, 1, 1), col=col_ors)
```

*** =sct
```{r}
success_msg("Great!");
```


--- type:NormalExercise lang:r xp:100 skills:1 key:56d9d5409e
## Performing Logistic Regression Using the Function glm()

Linear regression isn’t suitable when the response variable represents categorical data (factor), But logistic regression (logit) can be used to model data with a categorical response variable.

The function `glm()` ﬁts generalized linear models, including logistic regressions, `glm()` can ﬁt two diﬀerent types of response variables: categorical data (factors) from individual observations, or counts of categorical data (integers) from groups of observations.

The family object binomial(link="logit") speciﬁes a binomial distribution of residuals in the logistic regression model.

*** =instructions
- Utilize `glm()` for logistic regression.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# simulate categorical data


# probability threshold


# product tags


# Wilcoxon test for sco_re predictor


# perform logit regression


# regression summary


# change the code to make plot
plot(x=sco_re, y=log_it, type="l", lwd=3,
     main="Category densities and logistic function",
     xlab="score", ylab="probability")

# get density of active group


# scale y value


# add line


# change code to produce polygon


# get density of not active group


# scale y value


# add line


# change code to produce polygon
polygon(c(den_sity, den_sity, den_sity), c(den_sity, den_sity, den_sity), col=rgb(0, 0, 1, 0.2), border=NA)

# add legend

```

*** =solution
```{r}
# simulate categorical data
sco_re <- sort(runif(100))

# probability threshold
thresh_old <- 0.5

# product tags
ac_tive <- ((sco_re + rnorm(100, sd=0.1)) > thresh_old)

# Wilcoxon test for sco_re predictor
wilcox.test(sco_re[ac_tive], sco_re[!ac_tive])

# perform logit regression
log_it <- glm(ac_tive ~ sco_re, family=binomial(logit))

# regression summary
summary(log_it)

# change the code to make plot
plot(x=sco_re, y=log_it$fitted.values, type="l", lwd=3,
     main="Category densities and logistic function",
     xlab="score", ylab="probability")

# get density of active group
den_sity <- density(sco_re[ac_tive])

# scale y value
den_sity$y <- den_sity$y/max(den_sity$y)

# add line
lines(den_sity, col="red")

# change code to produce polygon
polygon(c(min(den_sity$x), den_sity$x, max(den_sity$x)), c(min(den_sity$y), den_sity$y, min(den_sity$y)), col=rgb(1, 0, 0, 0.2), border=NA)

# get density of not active group
den_sity <- density(sco_re[!ac_tive])

# scale y value
den_sity$y <- den_sity$y/max(den_sity$y)

# add line
lines(den_sity, col="blue")

# change code to produce polygon
polygon(c(min(den_sity$x), den_sity$x, max(den_sity$x)), c(min(den_sity$y), den_sity$y, min(den_sity$y)), col=rgb(0, 0, 1, 0.2), border=NA)

# add legend
legend(x="top", bty="n", lty=c(1, NA, NA), lwd=c(3, NA, NA), pch=c(NA, 15, 15),
 legend=c("logistic fit", "active", "non-active"),
 col=c("black", "red", "blue"),
 text.col=c("black", "red", "blue"))
```

*** =sct
```{r}
success_msg("Wow!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e09996c475
## Package ISLR With Datasets for Machine Learning

The package ISLR contains datasets used in the book ”Introduction to Statistical Learning”: 

Trevor Hastie Robert Tibshirani Gareth James Daniela Witten. An Introduction to Statistical Learning with Applications in R. . First Edition. Springer, 2013. url: http://www-bcf.usc.edu/∼gareth/ISL/index.html


*** =instructions
- Take a look at the ISLR pacakage, which mainly contains datasets.

*** =hint
Follow the instructions and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# load package ISLR


# get documentation for package tseries


# load help page


# load package ISLR


# list all datasets in ISLR


# list all objects in ISLR


# remove ISLR from search path

```

*** =solution
```{r}
# load package ISLR
library(ISLR)

# get documentation for package tseries
packageDescription("ISLR")

# load help page
help(package="ISLR")

# load package ISLR
library(ISLR)

# list all datasets in ISLR
data(package="ISLR")

# list all objects in ISLR
ls("package:ISLR")

# remove ISLR from search path
detach("package:ISLR")
```

*** =sct
```{r}
success_msg("Now you can manipulate all these data.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:f6eb0a5c5f
## The Default Dataset

The Default dataset is a data frame in package ISLR, with credit default data.

The Default data frame contains two columns of binary categorical data (factors): 

default and student, and two columns of numerical data: balance and income.

The columns student, balance, and income can be used as predictors to predict the default column.

*** =instructions
- Explore and visualize the dataset. 

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# load package ISLR


# load credit default data


# summary of dataset


# class of each column


# dimension of dataset


# head of dataset


# range of balance value


# range of income value


# select the defaulted record
default_ed <- (default=="Yes")

# change the code to plot data points for non-defaulters
plot(income ~ balance,
     main="Default dataset from package ISLR",
     xlim=x_lim, ylim=y_lim,
     data=Default,
     pch=40, col="blueandred")

# plot data points for defaulters


# change code to add legend
legend(x="bottomright", bty="l",
 legend=c("non-defaulters", "defaulters"),
 col=c("blue", "red"), lty=10, pch=40)
```

*** =solution
```{r}
# load package ISLR
library(ISLR)

# load credit default data
attach(Default)

# summary of dataset
summary(Default)

# class of each column
sapply(Default, class)

# dimension of dataset
dim(Default)

# head of dataset
head(Default)

# range of balance value
x_lim <- range(balance)

# range of income value
y_lim <- range(income)

# select the defaulted record
default_ed <- (default=="Yes")

# change the code to plot data points for non-defaulters
plot(income ~ balance,
     main="Default dataset from package ISLR",
     xlim=x_lim, ylim=y_lim,
     data=Default[!default_ed, ],
     pch=4, col="blue")

# plot data points for defaulters
points(income ~ balance,
 data=Default[default_ed, ],
 pch=4, col="red")

# change code to add legend
legend(x="topright", bty="n",
 legend=c("non-defaulters", "defaulters"),
 col=c("blue", "red"), lty=1, pch=4)
```

*** =sct
```{r}
success_msg("Interesting points! Seems like defaulted and non-defaulted records can be seperated somehow.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:d65e71390a
## Boxplots of the Default Dataset

A Box Plot (box-and-whisker plot) is a graphical display of a distribution of values.

The box represents the upper and lower quartiles, the vertical lines (whiskers) represent values beyond the quartiles, and open circles represent values beyond the nominal range (outliers).

The function boxplot() plots a box-and-whisker plot for a distribution of values, boxplot() has two methods: one for formula objects (involving categorical variables), and another for data frames.

The Wilcoxon test shows that the balance column provides a strong separation between defaulters and non-defaulters, but the income column doesn't.

*** =instructions
- Produce `boxplot()` to see differences between defaulted and non-default group.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no pec
library(ISLR)  # load package ISLR
# load credit default data
attach(Default)
summary(Default)
sapply(Default, class)
dim(Default); head(Default)
x_lim <- range(balance)
y_lim <- range(income)
# plot data points for non-defaulters
default_ed <- (default=="Yes")
```

*** =sample_code
```{r}
# set default tag


# Wilcoxon test for balance predictor


# Wilcoxon test for income predictor


# load package ISLR


# load credit default data


# set plot panels


# balance boxplot


# income boxplot

```

*** =solution
```{r}
# set default tag
default_ed <- (default=="Yes")

# Wilcoxon test for balance predictor
wilcox.test(balance[default_ed], balance[!default_ed])

# Wilcoxon test for income predictor
wilcox.test(income[default_ed], income[!default_ed])

# load package ISLR
library(ISLR)

# load credit default data
attach(Default)

# set plot panels
par(mfrow=c(1,2))

# balance boxplot
boxplot(formula=balance ~ default,
  col="lightgrey",
  main="balance", xlab="default")

# income boxplot
boxplot(formula=income ~ default,
  col="lightgrey",
  main="income", xlab="default")
```

*** =sct
```{r}
success_msg("So you have a clearer idea about how to seperate two groups.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e23011c42b
## Modeling Credit Defaults Using Logistic Regression

The balance column can be used to calculate the probability of default using logistic regression.

The residuals in logistic regression are the diﬀerences betweeen the actual response values (0 and 1), and the calculated probabilities of default.

The logit residuals are not normally distributed, so the data is ﬁtted using the maximum-likelihood method, instead of least squares.

The family object binomial(link="logit") speciﬁes a binomial distribution of residuals in the logistic regression model.

*** =instructions
- Run logistic regression on Defaulted dataset.

*** =hint
Balance seems to have a bigger effect on default rate.

*** =pre_exercise_code
```{r}
# no pec
library(ISLR)  # load package ISLR
# load credit default data
attach(Default)
summary(Default)
sapply(Default, class)
dim(Default); head(Default)
x_lim <- range(balance)
y_lim <- range(income)
# plot data points for non-defaulters
default_ed <- (default=="Yes")
```

*** =sample_code
```{r}
# fit logistic regression model

        
# regression summary


# make plot


# make the balance in order


# make lines


# make legend

```

*** =solution
```{r}
# fit logistic regression model
log_it <- glm(default ~ balance,
        family=binomial(logit))
        
# regression summary
summary(log_it)

# make plot
plot(x=balance, y=default_ed,
     main="Logistic regression of credit defaults", col="orange",
     xlab="credit balance", ylab="defaults")

# make the balance in order
or_der <- order(balance)

# make lines
lines(x=balance[or_der], y=log_it$fitted.values[or_der],
col="blue", lwd=2)

# make legend
legend(x="topleft", inset=0.1,
 legend=c("defaults", "logit fitted values"),
 col=c("orange", "blue"), lty=c(NA, 1), pch=c(1, NA), lwd=c(3, 3))
```

*** =sct
```{r}
success_msg("Bellissimo!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:59a81e117a
## Modeling Cumulative Defaults Using Logistic Regression

The cumulative count of defaults with respect to a single predictor can be modelled as a logistic function, using the function `glm()`, The response variable should be speciﬁed as a matrix with two columns, one containing the number of defaults, and other the number of non-defaults.


*** =instructions
- Fit data into logistic model.

*** =hint
Always call data object as the first argument of apply, second arguemnt is the dimension, and function name as following arguments.

*** =pre_exercise_code
```{r}
# no pec
library(ISLR)  # load package ISLR
# load credit default data
attach(Default)
summary(Default)
sapply(Default, class)
dim(Default); head(Default)
x_lim <- range(balance)
y_lim <- range(income)
```

*** =sample_code
```{r}
# subset dataset


# sum of default


# calculate cumulative defaults


# perform logit regression


# summary of regression model


# make plot


# order the balance


# make lines


# make legend

```

*** =solution
```{r}
# subset dataset
default_ed <- (default=="Yes")

# sum of default
to_tal <- sum(default_ed)

# calculate cumulative defaults
default_s <- sapply(balance, function(ba_lance) {
    sum(default_ed[balance <= ba_lance])
})

# perform logit regression
log_it <- glm(
  cbind(default_s, to_tal-default_s) ~
    balance,
  family=binomial(logit))

# summary of regression model
summary(log_it)

# make plot
plot(x=balance, y=default_s/to_tal, col="orange", lwd=1,
     main="Cumulative defaults versus balance",
     xlab="credit balance", ylab="cumulative defaults")

# order the balance
or_der <- order(balance)

# make lines
lines(x=balance[or_der], y=log_it$fitted.values[or_der],
col="blue", lwd=2)

# make legend
legend(x="topleft", inset=0.1,
 legend=c("cumulative defaults", "fitted values"),
 col=c("orange", "blue"), lty=c(NA, 1), pch=c(1, NA), lwd=c(3, 3))
```

*** =sct
```{r}
success_msg("Outstanding!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:8debcc371a
## Multifactor Logistic Regression

Logistic regression calculates the probability of categorical variables, from the Odds Ratio of continuous explanatory variables.

The generic function summary() produces a list of regression model summary and diagnostic statistics: 

    coeﬃcients: matrix with estimated coeﬃcients, their z-values, and p-values, 

    Null deviance: measures the diﬀerences betweeen the response values and the probabilities calculated using only the intercept, 

    Residual deviance: measures the diﬀerences betweeen the response values and the model probabilities.

The balance and student columns are statistically signiﬁcant, but the income column is not

*** =instructions
- Perform logistic regression for multifactor situation.

*** =hint
Follow the instruction and introduction. 

*** =pre_exercise_code
```{r}
# no pec
library(ISLR)  # load package ISLR
# load credit default data
attach(Default)
summary(Default)
sapply(Default, class)
dim(Default); head(Default)
x_lim <- range(balance)
y_lim <- range(income)
# plot data points for non-defaulters
default_ed <- (default=="Yes")
```

*** =sample_code
```{r}
# get column names


# make formula


# fit multifactor logistic regression model


# model summary

```

*** =solution
```{r}
# get column names
col_names <- colnames(Default)

# make formula
for_mula <- as.formula(paste(col_names[1], 
  paste(col_names[-1], collapse="+"), sep=" ~ "))

# fit multifactor logistic regression model
log_it <- glm(for_mula, data=Default, 
        family=binomial(logit))

# model summary
summary(log_it)
```

*** =sct
```{r}
success_msg("Doskonały!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:c1a08e245c
## Confounding Variables in Multifactor Logistic Regression

The student column is a confounding variable since it’s correlated with the balance column, Students are less likely to default than non-students with the same balance, But on average students have higher balances than non-students, which makes them more likely to default, That’s why the multifactor regression coeﬃcient for student is negative, while the single factor coeﬃcient for student is positive.

*** =instructions
- Examine the confounding effects of multicollinearity in logistic regression.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no prec
```

*** =sample_code
```{r}
# load package ISLR


# load credit default data


# subset defaulted 


# subset student


# complete the code and calculate cumulative defaults
default_s <- sapply(balance,
  function(ba_lance) {
    c(stu_dent=?),
non_student=?))
})

# sum of default rate


# scale and transpose


# set plot panels


# make ordered balance


# plot cumulative defaults

     
# draw line


# make legend


# balance boxplot for student factor

```

*** =solution
```{r}
# load package ISLR
library(ISLR)

# load credit default data
attach(Default)

# subset defaulted 
default_ed <- (default=="Yes")

# subset student
stu_dent <- (student=="Yes")

# complete the code and calculate cumulative defaults
default_s <- sapply(balance,
  function(ba_lance) {
    c(stu_dent=sum(default_ed[stu_dent & (balance <= ba_lance)]),
non_student=sum(default_ed[(!stu_dent) & (balance <= ba_lance)]))
})

# sum of default rate
to_tal <- c(sum(default_ed[stu_dent]), sum(default_ed[!stu_dent]))

# scale and transpose
default_s <- t(default_s / to_tal)

# set plot panels
par(mfrow=c(1,2))

# make ordered balance
or_der <- order(balance)

# plot cumulative defaults
plot(x=balance[or_der], y=default_s[or_der, 1],
     col="red", t="l", lwd=2,
     main="Cumulative defaults of\n students and non-students",
     xlab="credit balance", ylab="")
     
# draw line
lines(x=balance[or_der], y=default_s[or_der, 2],
col="blue", lwd=2)

# make legend
legend(x="topleft", bty="n",
 legend=c("students", "non-students"),
 col=c("red", "blue"), text.col=c("red", "blue"),
 lwd=c(3, 3))

# balance boxplot for student factor
boxplot(formula=balance ~ student,
  col="lightgrey",
  main="balance", xlab="student")
```

*** =sct
```{r}
success_msg("Multicollinearity is a headache for many regression.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e9ca3eeb99
## Forecasting of Credit Defaults using Logistic Regression

The function `predict()` is a generic function for forecasting based on a given model.

Logistic regression calculates the probability of categorical variables, based on continuous explanatory variables.

A type I error is the incorrect rejection of a TRUE case (i.e. a ”false positive”), That is, a type I error is when there is no default, but it’s classiﬁed as a default, A type II error is the incorrect acceptance of a FALSE case (i.e. a ”false negative”), That is, a type II error is when there is a default, but it’s classiﬁed as no default.

A confusion matrix is a table that summarizes the performance of a classiﬁcation model on a set of test data for which the true values are known.


*** =instructions
- Get prediction from models you trained.

*** =hint
Follow the instruction and introductions. 

*** =pre_exercise_code
```{r}
# no
```

*** =sample_code
```{r}
# fit full logistic regression model


# run logistic model

        
# make prediction using existing model and explanatory variable


# get length


# look at first ten elements


# probability threshold


# calculate confusion matrix


# sum up


# random select data


# make training dataset


# fit logistic regression over training data


# make training dataset


# forecast over test data


# calculate confusion matrix

```

*** =solution
```{r}
# fit full logistic regression model
for_mula <- as.formula(paste(col_names[1],
  paste(col_names[-1], collapse="+"), sep=" ~ "))

# run logistic model
log_it <- glm(for_mula, data=Default,
        family=binomial(logit))
        
# make prediction using existing model and explanatory variable
fore_casts <- predict(log_it, type="response")

# get length
length(fore_casts)

# look at first ten elements
fore_casts[1:10]

# probability threshold
thresh_old <- 0.5

# calculate confusion matrix
table((fore_casts>thresh_old), default_ed)

# sum up
sum(default_ed)

# random select data
sam_ple <- sample(x=1:NROW(Default), size=NROW(Default)/2)

# make training dataset
train_data <- Default[sam_ple, ]

# fit logistic regression over training data
log_it <- glm(for_mula, data=train_data,
        family=binomial(link="logit"))

# make training dataset
test_data <- Default[-sam_ple, ]

# forecast over test data
fore_casts <- predict(log_it, newdata=test_data, type="response")

# calculate confusion matrix
table((fore_casts>thresh_old), test_data$default=="Yes")
```

*** =sct
```{r}
success_msg("Congrats on finishing your first machine learning tiny project!")
```

