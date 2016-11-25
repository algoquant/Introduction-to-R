---
title_meta  : Chapter 11
title       : Optimization
description : Use various optimization functions to get your best result!

--- type:NormalExercise lang:r xp:100 skills:1 key:36ba783482
## One-dimensional Optimization

The function `optimize()` performs one-dimensional optimization over a single independent variable, `optimize()` searches for the minimum of the objective function with respect to its ﬁrst argument, in the speciﬁed interval.

`optimize()` returns a list containing the location of the minimum and the objective function value

*** =instructions
- Use `optimize()` to find the minimum, or maximum (after some modification) value.

*** =hint
Follow the instructions and introductions. The `optimize()` function returns a list.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# function structure


# objective function with multiple minima


# get optimized value


# get optimized value in another range


# modify devices


# make plot parameters


# plot the objective function


# add title

```

*** =solution
```{r}
# function structure
str(optimize)

# objective function with multiple minima
object_ive <- function(in_put, param1=0.01) {
  sin(0.25*pi*in_put) + param1*(in_put-1)^2
}

# get optimized value
unlist(optimize(f=object_ive, interval=c(-4, 2)))

# get optimized value in another range
unlist(optimize(f=object_ive, interval=c(0, 8)))

# modify devices
options(width=60, dev='pdf')

# make plot parameters
par(oma=c(1, 1, 1, 1), mgp=c(2, 1, 0), mar=c(5, 1, 1, 1), cex.lab=0.8, cex.axis=0.8, cex.main=0.8, cex.sub=0.5)

# plot the objective function
curve(expr=object_ive, type="l", xlim=c(-8, 9),
xlab="", ylab="", lwd=2)

# add title
title(main="Objective Function", line=-1)
```

*** =sct
```{r}
success_msg("Great!");
```


--- type:NormalExercise lang:r xp:100 skills:1 key:56d9d5409e
## The Log-likelihood Function

The likelihood function L(θ|¯ x) is a function of the parameters of a statistical model (θ), given a sample of observed values (¯ x), taken under the model’s probability distribution.

The likelihood function measures how likely are the parameters of a statistical model, given a sample of observed values (¯ x), The maximum-likelihood estimate (MLE) of the model’s parameters are those that maximize the likelihood function.

In practice the logarithm of the likelihood log(L) is maximized, instead of the likelihood itself, The function `outer()` calculates the outer product of two matrices, and by default multiplies the elements of its arguments.

*** =instructions
- Use vectorized function to produce optimized value in a matrix.

*** =hint
Use `outer()` to produce matrix, and apply vectorized function on it.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# sample of normal variables
sam_ple <- rnorm(1000, mean=4, sd=2)

# objective function is log-likelihood
object_ive <- function(pa_r, sam_ple) {
  sum(2*log(pa_r[2]) +
    ((sam_ple - pa_r[1])/pa_r[2])^2)
}

# vectorize objective function


# objective function on parameter grid


# get sequence


# outer product


# grid search

  
# print index


# mean


# sd


# print result


# complete the code to print adjacent area
objective_grid[(objective_min),
       (objective_min)]
```

*** =solution
```{r}
# sample of normal variables
sam_ple <- rnorm(1000, mean=4, sd=2)

# objective function is log-likelihood
object_ive <- function(pa_r, sam_ple) {
  sum(2*log(pa_r[2]) +
    ((sam_ple - pa_r[1])/pa_r[2])^2)
}

# vectorize objective function
vec_objective <- Vectorize(
  FUN=function(mean, sd, sam_ple)
    object_ive(c(mean, sd), sam_ple),
  vectorize.args=c("mean", "sd")
)

# objective function on parameter grid
par_mean <- seq(1, 6, length=50)

# get sequence
par_sd <- seq(0.5, 3.0, length=50)

# outer product
objective_grid <- outer(par_mean, par_sd,
vec_objective, sam_ple=sam_ple)

# grid search
objective_min <- which(
  objective_grid==min(objective_grid),
  arr.ind=TRUE)
  
# print index
objective_min

# mean
par_mean[objective_min[1]]

# sd
par_sd[objective_min[2]]

# print result
objective_grid[objective_min]

# complete the code to print adjacent area
objective_grid[(objective_min[, 1] + -1:1),
       (objective_min[, 2] + -1:1)]
```

*** =sct
```{r}
success_msg("1D world to 2D world!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e09996c475
## Perspective Plot of Likelihood Function

The function `persp()` plots a 3d perspective surface plot of a function speciﬁed over a grid of argument values.

The argument "z" accepts a matrix containing the function values, `persp()` belongs to the base graphics package, and doesn’t create interactive plots, The function `persp3d()` plots an interactive 3d surface plot of a function or a matrix, rgl is an R package for 3d and perspective plotting, based on the OpenGL framework


*** =instructions
- Optimize and visualize results in 3D.

*** =hint
Follow the instructions and introductions. 3D plot requires 3 parameters.

*** =pre_exercise_code
```{r}
# no pec
# objective function is log-likelihood
object_ive <- function(pa_r, sam_ple) {
  sum(2*log(pa_r[2]) +
    ((sam_ple - pa_r[1])/pa_r[2])^2)
}  # end object_ive
# vectorize objective function
vec_objective <- Vectorize(
  FUN=function(mean, sd, sam_ple)
    object_ive(c(mean, sd), sam_ple),
  vectorize.args=c("mean", "sd")
)  # end Vectorize
# objective function on parameter grid
par_mean <- seq(1, 6, length=50)
par_sd <- seq(0.5, 3.0, length=50)
objective_grid <- outer(par_mean, par_sd,
vec_objective, sam_ple=sam_ple)
objective_min <- which(  # grid search
  objective_grid==min(objective_grid),
  arr.ind=TRUE)
objective_min
par_mean[objective_min[1]]  # mean
par_sd[objective_min[2]]  # sd
objective_grid[objective_min]
objective_grid[(objective_min[, 1] + -1:1),
       (objective_min[, 2] + -1:1)]
sam_ple <- rnorm(1000, mean=4, sd=2)
```

*** =sample_code
```{r}
# set parameter


# perspective plot of log-likelihood function


# load package rgl


# scale text by factor of 2


# plot 3D

```

*** =solution
```{r}
# set parameter
par(cex.lab=2.0, cex.axis=2.0, cex.main=2.0, cex.sub=2.0)

# perspective plot of log-likelihood function
persp(z=-objective_grid,
theta=45, phi=30, shade=0.5,
border="green", zlab="objective",
main="objective function")

# load package rgl
library(rgl)

# scale text by factor of 2
par3d(cex=2.0)

# plot 3D
persp3d(z=-objective_grid, zlab="objective",
  col="green", main="objective function")
```

*** =sct
```{r}
success_msg("Welcome to the 3D world!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:f6eb0a5c5f
## Optimization of Objective Function

The function `optim()` performs optimization of an objective function.

The function `fitdistr()` from package MASS ﬁts a univariate distribution to a sample of data, by performing maximum likelihood optimization.

*** =instructions
- Fit data and visualize. 

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
# objective function is log-likelihood
object_ive <- function(pa_r, sam_ple) {
  sum(2*log(pa_r[2]) +
    ((sam_ple - pa_r[1])/pa_r[2])^2)
}
sam_ple <- rnorm(1000, mean=4, sd=2)
```

*** =sample_code
```{r}
# initial parameters


# complete the code to perform optimization using optim()
optim_fit <- optim()

# optimal parameters


# perform optimization using MASS::fitdistr()


# get estimate


# get standard deviation


# plot histogram


# make plot


# make legend

```

*** =solution
```{r}
# initial parameters
par_init <- c(mean=0, sd=1)

# complete the code to perform optimization using optim()
optim_fit <- optim(par=par_init,
  fn=object_ive,
  sam_ple=sam_ple,
  method="L-BFGS-B",
  upper=c(10, 10),
  lower=c(-10, 0.1))

# optimal parameters
optim_fit$par

# perform optimization using MASS::fitdistr()
optim_fit <- MASS::fitdistr(sam_ple, densfun="normal")

# get estimate
optim_fit$estimate

# get standard deviation
optim_fit$sd

# plot histogram
histo_gram <- hist(sam_ple, plot=FALSE)

# make plot
plot(histo_gram, freq=FALSE,
     main="histogram of sample")
curve(expr=dnorm(x, mean=optim_fit$par["mean"],
           sd=optim_fit$par["sd"]),
add=TRUE, type="l", lwd=2, col="red")

# make legend
legend("topright", inset=0.0, cex=0.8, title=NULL,
 leg="optimal parameters",
 lwd=2, bg="white", col="red")
```

*** =sct
```{r}
success_msg("Interesting points! Seems like defaulted and non-defaulted records can be seperated somehow.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:d65e71390a
## Mixture Model Likelihood Function

Fit mixed datasets with likelihood function. 

*** =instructions
- Utilize skills you learned to fit a mixed dataset into models.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# sample from mixture of normal distributions


# complete the code to get objective function is log-likelihood
object_ive <- function(pa_r, sam_ple) {
  likelihood <- pa_r/pa_r *
  sam_ple +
  (1-pa_r)/pa_r*(sam_ple*pa_r[4])+par)
  if (any(likelihood <= 0)) Inf else
    sum(log(likelihood))
}

# vectorize objective function


# objective function on parameter grid


# parameter of standard deviation


# get grid


# set rownames


# set colnames


# find the objective


# print the index


# get the value


# get adjacent area


# perspective plot of objective function

```

*** =solution
```{r}
# sample from mixture of normal distributions
sam_ple <- c(rnorm(100, sd=1.0),
             rnorm(100, mean=4, sd=1.0))

# complete the code to get objective function is log-likelihood
object_ive <- function(pa_r, sam_ple) {
  likelihood <- pa_r[1]/pa_r[3] *
  dnorm((sam_ple-pa_r[2])/pa_r[3]) +
  (1-pa_r[1])/pa_r[5]*dnorm((sam_ple-pa_r[4])/pa_r[5])
  if (any(likelihood <= 0)) Inf else
    -sum(log(likelihood))
}

# vectorize objective function
vec_objective <- Vectorize(
  FUN=function(mean, sd, w, m1, s1, sam_ple)
    object_ive(c(w, m1, s1, mean, sd), sam_ple),
  vectorize.args=c("mean", "sd")
)

# objective function on parameter grid
par_mean <- seq(3, 5, length=50)

# parameter of standard deviation
par_sd <- seq(0.5, 1.5, length=50)

# get grid
objective_grid <- outer(par_mean, par_sd,
    vec_objective, sam_ple=sam_ple,
    w=0.5, m1=2.0, s1=2.0)

# set rownames
rownames(objective_grid) <- round(par_mean, 2)

# set colnames
colnames(objective_grid) <- round(par_sd, 2)

# find the objective
objective_min <- which(objective_grid==
  min(objective_grid), arr.ind=TRUE)

# print the index
objective_min

# get the value
objective_grid[objective_min]

# get adjacent area
objective_grid[(objective_min[, 1] + -1:1),
         (objective_min[, 2] + -1:1)]

# perspective plot of objective function
persp(par_mean, par_sd, -objective_grid,
theta=45, phi=30,
shade=0.5,
col=rainbow(50),
border="green",
main="objective function")
```

*** =sct
```{r}
success_msg("Excellent for overcome all these difficulties!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e23011c42b
## Optimization of Mixture Model

Optimized fitting a mixed model.

*** =instructions
- Optimize on mixed data and visualize.

*** =hint
Follow instruction and introduction.

*** =pre_exercise_code
```{r}
# objective function is log-likelihood
object_ive <- function(pa_r, sam_ple) {
  sum(2*log(pa_r[2]) +
    ((sam_ple - pa_r[1])/pa_r[2])^2)
}
sam_ple <- rnorm(1000, mean=4, sd=2)
```

*** =sample_code
```{r}
# initial parameters


# perform optimization


# optimize parameter


# plot histogram


# make plot


# change code to get fit function
fit_func <- function(x, pa_r) {
  pa_r *
    pnorm(x, mean=pa_r["m1"], sd=pa_r["s1"]) +
  (1-pa_r) *
    pnorm(x, mean=pa_r["m2"], sd=pa_r["s2"])
}

# draw fitted curve


# make legend

```

*** =solution
```{r}
# initial parameters
par_init <- c(weight=0.5, m1=0, s1=1, m2=2, s2=1)

# perform optimization
optim_fit <- optim(par=par_init,
      fn=object_ive,
      sam_ple=sam_ple,
      method="L-BFGS-B",
      upper=c(1,10,10,10,10),
      lower=c(0,-10,0.2,-10,0.2))

# optimize parameter
optim_fit$par

# plot histogram
histo_gram <- hist(sam_ple, plot=FALSE)

# make plot
plot(histo_gram, freq=FALSE,
     main="histogram of sample")

# change code to get fit function
fit_func <- function(x, pa_r) {
  pa_r["weight"] *
    dnorm(x, mean=pa_r["m1"], sd=pa_r["s1"]) +
  (1-pa_r["weight"]) *
    dnorm(x, mean=pa_r["m2"], sd=pa_r["s2"])
}

# draw fitted curve
curve(expr=fit_func(x, pa_r=optim_fit$par), add=TRUE,
type="l", lwd=2, col="red")

# make legend
legend("topright", inset=0.0, cex=0.8, title=NULL,
 leg="optimal parameters",
 lwd=2, bg="white", col="red")
```

*** =sct
```{r}
success_msg("Problem solved! Bellissimo!")
```
