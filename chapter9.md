---
title_meta  : Chapter 9
title       : Parallel Computing
description : Learn to ride the powerful technique in R!


--- type:NormalExercise lang:r xp:100 skills:1 key:c1a08e245c
## Parallel Computing Using Package parallel

The package parallel provides functions for parallel computing using multiple cores of CPUs, The package parallel is part of the standard R distribution, so it doesn’t need to be installed, Diﬀerent functions from package parallel need to be called depending on the operating system (Windows, Mac-OSX, or Linux).

*** =instructions
- Understand the package "parallel.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no prec
```

*** =sample_code
```{r}
# load package parallel


# get short description


# load help page


# list all objects in "parallel"

```

*** =solution
```{r}
# load package parallel
library(parallel)

# get short description
packageDescription("parallel")

# load help page
help(package="parallel")

# list all objects in "parallel"
ls("package:parallel")
```

*** =sct
```{r}
success_msg("This is a first step to parallel, but big leap to speed!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e9ca3eeb99
## Performing Parallel Loops Using Package parallel

Some computing tasks naturally lend themselves to parallel computing, like for example performing loops.

Diﬀerent functions from package parallel need to be called depending on the operating system (Windows, Mac-OSX, or Linux).

The function `mclapply()` performs apply loops (similar to `lapply()`) using parallel computing on several CPU cores under Mac-OSX or Linux, Under Windows, a cluster of R processes (one per each CPU core) need to be started ﬁrst, by calling the function `makeCluster()`, Mac-OSX and Linux don’t require calling the function `makeCluster()`.

The function `parLapply()` is similar to `lapply()`, and performs apply loops under Windows, using parallel computing on several CPU cores.

The function `stopCluster()` stops the R processes running on several CPU cores

*** =instructions
- Conduct parallel computation and compare speed.

*** =hint
Follow the instruction and introductions. Remember to stop parallel after computing is finished.

*** =pre_exercise_code
```{r}
# no
```

*** =sample_code
```{r}
# load package parallel


# calculate number of available cores


# define function that pauses execution
paws <- function(x, sleep_time) {

}

# perform parallel loop under Mac-OSX or Linux
foo <- mclapply()

# initialize compute cluster


# perform parallel loop under Windows
foo <- parLapply()

# load package microbenchmark


# compare speed of lapply versus parallel computing
summary(microbenchmark(
  l_apply=,
  parl_apply=
    ,
  times=10)
)

# stop R processes over cluster

```

*** =solution
```{r}
# load package parallel
library(parallel)

# calculate number of available cores
num_cores <- detectCores() - 1

# define function that pauses execution
paws <- function(x, sleep_time) {
  Sys.sleep(sleep_time)
  x
}

# perform parallel loop under Mac-OSX or Linux
foo <- mclapply(1:10, paws, mc.cores=num_cores,
          sleep_time=0.01)

# initialize compute cluster
clus_ter <- makeCluster(num_cores)

# perform parallel loop under Windows
foo <- parLapply(clus_ter, 1:10, paws,
           sleep_time=0.01)

# load package microbenchmark
library(microbenchmark)

# compare speed of lapply versus parallel computing
summary(microbenchmark(
  l_apply=lapply(1:10, paws, sleep_time=0.01),
  parl_apply=
    parLapply(clus_ter, 1:10, paws, sleep_time=0.01),
  times=10)
)[, c(1, 4, 5)]

# stop R processes over cluster
stopCluster(clus_ter)
```

*** =sct
```{r}
success_msg("Feels like a flash!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:8e5ade7078
## Computing Overhead of Parallel Computing

Parallel computing requires additional resources and time for distributing the computing tasks and collecting the output, which produces a computing overhead.

Therefore parallel computing can actually be slower for small computations, or for computations that can’t be naturally separated into sub-tasks.

*** =instructions
- Examine the effects of overheads.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
library(microbenchmark)
library(parallel)
num_cores <- detectCores() - 1
clus_ter <- makeCluster(num_cores)
paws <- function(x, sleep_time) {
  Sys.sleep(sleep_time)
  x
}

```

*** =sample_code
```{r}
# load package parallel


# compare speed of lapply with parallel computing


# complete code to compare speed
compute_times <- sapply(iter_ations,
  function(max_iterations, sleep_time) {
    out_put <- summary(microbenchmark(
lapply=?,
parallel=?,
times=10))
    structure(out_put[, 2],
        names=vector(out_put[, 2]))
    }, sleep_time=1)

# transpose


# name rows


# complete the code to make plot
plot(x=?,
     y=?,
     type="l", lwd=2, col="blue",
     main="Compute times",
     xlab="number of iterations in loop", ylab="",
     ylim=c(0, max(compute_times[, "lapply"])))
     
# add lines


# modify legend
legend(x="bottomright", legend=?,
 inset=0.1, cex=1.0, bg="white",
 lwd=2, lty=c(1, 1), col=c("blue", "green"))
```

*** =solution
```{r}
# load package parallel
library(parallel)

# compare speed of lapply with parallel computing
iter_ations <- 3:10

# complete code to compare speed
compute_times <- sapply(iter_ations,
  function(max_iterations, sleep_time) {
    out_put <- summary(microbenchmark(
lapply=lapply(1:max_iterations, paws,
              sleep_time=sleep_time),
parallel=parLapply(clus_ter, 1:max_iterations,
        paws, sleep_time=sleep_time),
times=10))[, c(1, 4)]
    structure(out_put[, 2],
        names=as.vector(out_put[, 1]))
    }, sleep_time=0.01)

# transpose
compute_times <- t(compute_times)

# name rows
rownames(compute_times) <- iter_ations

# complete the code to make plot
plot(x=rownames(compute_times),
     y=compute_times[, "lapply"],
     type="l", lwd=2, col="blue",
     main="Compute times",
     xlab="number of iterations in loop", ylab="",
     ylim=c(0, max(compute_times[, "lapply"])))
     
# add lines
lines(x=rownames(compute_times),
y=compute_times[, "parallel"], lwd=2, col="green")

# modify legend
legend(x="topleft", legend=colnames(compute_times),
 inset=0.1, cex=1.0, bg="white",
 lwd=2, lty=c(1, 1), col=c("blue", "green"))
```

*** =sct
```{r}
success_msg("Cool!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:ec87541ef1
## Parallel Computing Over Matrices

Very often we need to perform time consuming calculations over columns of matrices.

The function `parCapply()` performs an apply loop over columns of matrices using parallel computing on several CPU cores.


*** =instructions
- Deploy parallel computing on matrices.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# load package parallel


# calculate number of available cores


# initialize compute cluster


# define large matrix


# change the code to define aggregation function over column of matrix
agg_regate <- function(col_umn) {
  out_put
  for (in_dex in 1:length(in_dex))
    out_put <- out_put / col_umn[in_dex]
  out_put
}

# perform parallel aggregations over columns of matrix


# complete the code to compare speed of apply with parallel computing
summary(microbenchmark(
  ap_ply=?,
  parl_apply=
    ?,
  times=10)
)

# stop R processes over cluster

```

*** =solution
```{r}
# load package parallel
library(parallel)

# calculate number of available cores
num_cores <- detectCores() - 1

# initialize compute cluster
clus_ter <- makeCluster(num_cores)

# define large matrix
mat_rix <- matrix(rnorm(7*10^5), ncol=7)

# change the code to define aggregation function over column of matrix
agg_regate <- function(col_umn) {
  out_put <- 0
  for (in_dex in 1:length(col_umn))
    out_put <- out_put + col_umn[in_dex]
  out_put
}

# perform parallel aggregations over columns of matrix
agg_regations <-
  parCapply(clus_ter, mat_rix, agg_regate)

# complete the code to compare speed of apply with parallel computing
summary(microbenchmark(
  ap_ply=apply(mat_rix, MARGIN=2, agg_regate),
  parl_apply=
    parCapply(clus_ter, mat_rix, agg_regate),
  times=10)
)[, c(1, 4, 5)]

# stop R processes over cluster
stopCluster(clus_ter)
```

*** =sct
```{r}
success_msg("Wonderful!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:3d8a9618b9
## Standard Errors of Regression Coeﬃcients Using Bootstrap

The standard errors of the regression coeﬃcients can be calculated using a bootstrap simulation.

The bootstrap procedure creates new design matrices by randomly sampling with replacement from the design matrix.

Regressions are performed on the bootstrapped design matrices, and the regression coeﬃcients are saved into a matrix of bootstrapped coeﬃcients. 

*** =instructions
- Use bootstrap methods on regression.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
set.seed(1121)
```

*** =sample_code
```{r}
# define explanatory and response variables


# generate random noise


# construct response variable


# define design matrix and regression formula


# regression formula


# chage the code to bootstrap the regression
boot_strap <- sapply(1:10, function(x) {
  boot_sample <-
    sample(dim(design_matrix), replace=TRUE)
  reg_model <- lm(reg_formula,
          data=design_matrix)
  reg_model$coefficients
})
```

*** =solution
```{r}
# define explanatory and response variables
explana_tory <- rnorm(100, mean=2)

# generate random noise
noise <- rnorm(100)

# construct response variable
res_ponse <- -3 + explana_tory + noise

# define design matrix and regression formula
design_matrix <- data.frame(res_ponse, explana_tory)

# regression formula
reg_formula <- paste(colnames(design_matrix)[1],
  paste(colnames(design_matrix)[-1], collapse="+"),
  sep=" ~ ")

# chage the code to bootstrap the regression
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
success_msg("Cornerstone for greater projects!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:b0b3b7fe27
## Distribution of Bootstrapped Regression Coeﬃcients

The bootstrapped coeﬃcient values can be used to calculate the probability distribution of the coeﬃcients and their standard errors.

*** =instructions
- Visualize bootstrapped errors.

*** =hint
Follow the instruction and introduction. 

*** =pre_exercise_code
```{r}
set.seed(1121)
# define explanatory and response variables
explana_tory <- rnorm(100, mean=2)

# generate random noise
noise <- rnorm(100)

# construct response variable
res_ponse <- -3 + explana_tory + noise

# define design matrix and regression formula
design_matrix <- data.frame(res_ponse, explana_tory)

# regression formula
reg_formula <- paste(colnames(design_matrix)[1],
  paste(colnames(design_matrix)[-1], collapse="+"),
  sep=" ~ ")

# chage the code to bootstrap the regression
boot_strap <- sapply(1:100, function(x) {
  boot_sample <-
    sample.int(dim(design_matrix)[1], replace=TRUE)
  reg_model <- lm(reg_formula,
          data=design_matrix[boot_sample, ])
  reg_model$coefficients
})
```

*** =sample_code

```{r}
# means and standard errors from bootstrap


# means and standard errors from regression summary


# get regression coefficients


# look at standard error


# plot results


# add a line

```

*** =solution
```{r}
# means and standard errors from bootstrap
apply(boot_strap, MARGIN=1,
      function(x) c(mean=mean(x), sd=sd(x)))

# means and standard errors from regression summary
reg_model <- lm(reg_formula, data=design_matrix)

# get regression coefficients
reg_model$coefficients

# look at standard error
summary(reg_model)$coefficients[, "Std. Error"]

# plot results
plot(density(boot_strap["explana_tory", ]),
     lwd=2, xlab="regression slopes",
     main="Bootstrapped regression slopes")

# add a line
abline(v=mean(boot_strap["explana_tory", ]),
       lwd=2, col="red")
```

*** =sct
```{r}
test_error()
success_msg("One step closer to some statistical learning methods!")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:eb77d79f8a
## Bootstrapping Regressions Using Parallel Computing

A list of vectors can be ﬂattened into a matrix using the functions `do.call()` and either `rbind()` or `cbind()`, If the list contains vectors of diﬀerent lengths, then R applies the recycling rule, If the list contains a NULL element, that element is skipped,


*** =instructions
- Apply parallel computing on bootstrapping.

*** =hint
Follow the instruction and introduction. 

*** =pre_exercise_code
```{r}
```

*** =sample_code

```{r}
# load package parallel


# number of cores


# initialize compute cluster


# change code to bootstrap the regression under Windows
boot_strap <- parLapply(clus_ter, 1:10,
  function(x, reg_formula, design_matrix) {
    boot_sample <-
sample(dim(design_matrix)[2], replace=TRUE)
    reg_model <- lm(reg_formula,
data=design_matrix)
    reg_model$coefficients
  },
  reg_formula=reg_formula,
  design_matrix=design_matrix)

# change code to bootstrap the regression under Mac-OSX or Linux
boot_strap <- mclapply(1:10,
  function(x) {
    boot_sample <-
sample(length(design_matrix)[1], replace=FALSE)
    lm(reg_formula,
data=design_matrix[boot_sample, ])$coefficients
  }, mc.cores=num_cores)
  
# stop R processes over cluster  


# convert to a matrix


# means and standard errors from bootstrap


# change code to make plot
plot(boot_strap[, "explana_tory"],
     lwd=20, xlab="regression slopes",
     main="Bootstrapped regression slopes")

# add a line

```

*** =solution
```{r}
# load package parallel
library(parallel)

# number of cores
num_cores <- detectCores() - 1

# initialize compute cluster
clus_ter <- makeCluster(num_cores)

# change code to bootstrap the regression under Windows
boot_strap <- parLapply(clus_ter, 1:1000,
  function(x, reg_formula, design_matrix) {
    boot_sample <-
sample.int(dim(design_matrix)[1], replace=TRUE)
    reg_model <- lm(reg_formula,
data=design_matrix[boot_sample, ])
    reg_model$coefficients
  },
  reg_formula=reg_formula,
  design_matrix=design_matrix)

# change code to bootstrap the regression under Mac-OSX or Linux
boot_strap <- mclapply(1:1000,
  function(x) {
    boot_sample <-
sample.int(dim(design_matrix)[1], replace=TRUE)
    lm(reg_formula,
data=design_matrix[boot_sample, ])$coefficients
  }, mc.cores=num_cores)
  
# stop R processes over cluster  
stopCluster(clus_ter)

# convert to a matrix
boot_strap <- do.call(rbind, boot_strap)

# means and standard errors from bootstrap
apply(boot_strap, MARGIN=2,
function(x) c(mean=mean(x), sd=sd(x)))

# change code to make plot
plot(density(boot_strap[, "explana_tory"]),
     lwd=2, xlab="regression slopes",
     main="Bootstrapped regression slopes")

# add a line
abline(v=mean(boot_strap[, "explana_tory"]),
 lwd=2, col="red")
```

*** =sct
```{r}
test_error()
success_msg("Very brilliant solution! Enjoy this journey!`")
```
