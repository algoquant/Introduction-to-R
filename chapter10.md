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
## Performing Loops Using the apply() Functionals

An important example of functionals are the apply() functions, The function apply() returns the result of applying a function to the rows or columns of an array or matrix, If MARGIN=1 then the function will be applied over the matrix rows, If MARGIN=2 then the function will be applied over the matrix columns, apply() performs a loop over the list of objects, and can replace "for" loops in R.


*** =instructions
Use `apply()` to execute function in loops.

*** =hint
Always call data object as the first argument of apply, second arguemnt is the dimension, and function name as following arguments.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# get list of arguments


# create a matrix
mat_rix <- matrix(6:1, nrow=2, ncol=3)

# print the matrix


# sum the rows


# sum the columns


# change the code define a matrix of sums and original matrix
mat_rix <- c(sum(row_sums), col_sums)
dimnames(mat_rix) <- list(c("col_sums", "row1", "row2"),
                 c("row_sums", "col1", "col2", "col3"))

# print the matrix

```

*** =solution
```{r}
# get list of arguments
str(apply)

# create a matrix
mat_rix <- matrix(6:1, nrow=2, ncol=3)

# print the matrix
mat_rix

# sum the rows
row_sums <- apply(mat_rix, 1, sum)

# sum the columns
col_sums <- apply(mat_rix, 2, sum)

# change the code define a matrix of sums and original matrix
mat_rix <- cbind(c(sum(row_sums), row_sums),
          rbind(col_sums, mat_rix))
dimnames(mat_rix) <- list(c("col_sums", "row1", "row2"),
                 c("row_sums", "col1", "col2", "col3"))

# print the matrix
mat_rix
```

*** =sct
```{r}
success_msg("Groß!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:8debcc371a
## The apply() Functional with dots "..." Argument

The dots "..." argument in apply() is designed to pass additional arguments to the function being called by apply(), The additional arguments to apply() must be bound by their full (complete) names.


*** =instructions
Use `apply()` to execute function in loops with additional arguments.

*** =hint
Always call data object as the first argument of apply, second arguemnt is the dimension, and function name as following arguments. More arguments can be passed as dot arguments.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# get list of arguments


# create a matrix
mat_rix <- matrix(sample(12), nrow=3, ncol=4)

# print the code


# sort matrix columns


# sort decreasing order


# introduce NA value


# print the matrix


# calculate median of columns


# calculate median of columns with na.rm=TRUE

```

*** =solution
```{r}
# get list of arguments
str(apply)

# create a matrix
mat_rix <- matrix(sample(12), nrow=3, ncol=4)

# print the code
mat_rix

# sort matrix columns
apply(mat_rix, 2, sort)

# sort decreasing order
apply(mat_rix, 2, sort, decreasing=TRUE)

# introduce NA value
mat_rix[2, 2] <- NA

# print the matrix
mat_rix

# calculate median of columns
apply(mat_rix, 2, median)

# calculate median of columns with na.rm=TRUE
apply(mat_rix, 2, median, na.rm=TRUE)
```

*** =sct
```{r}
success_msg("Doskonały!")
```
