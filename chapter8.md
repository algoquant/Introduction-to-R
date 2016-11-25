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
## The R Debugger Facility

The function `debug()` ﬂags a function for future debugging, but doesn’t invoke the debugger.

After a function is ﬂagged for debugging with the call "debug(my func)", then the function call "my func()" automatically invokes the debugger (browser).

When the debugger is ﬁrst invoked, it prints the function code to the console, and produces a browser prompt: "Browse[2]>".

Once inside the debugger, the user can execute the function code one command at a time by pressing the Enter key.

The user can examine the function arguments and variables with standard R commands, and can also change the values of objects or create new ones.

The command "c" executes the remainder of the function code without pausing.

The command "Q" exits the debugger (browser), The call "undebug(my func)" at the R prompt unﬂags the function for debugging.

*** =instructions
- Experiment on debug functionality of R. 

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
sum_two <- function(in_put1, in_put2) {
  stopifnot(!missing(in_put1) &&
      !missing(in_put2))
  if (is.numeric(in_put1) &&
      is.numeric(in_put2)) {
    in_put1 + in_put2
  } 
  else if (is.numeric(in_put1)) {
    cat("in_put2 is not numeric\n")
    in_put1
  } 
  else if (is.numeric(in_put2)) {
    cat("in_put1 is not numeric\n")
    in_put2
  } else {
    stop("none of the arguments are numeric")
  }
}


vali_date <- function(in_put) {
  stopifnot(!missing(in_put) & is.numeric(in_put))
  2*in_put
}

```

*** =sample_code
```{r}
# flag "vali_date" for debugging
debug(vali_date)

# calling "vali_date" starts debugger
vali_date(3)

# unflag "vali_date" for debugging
undebug(vali_date)
```

*** =solution
```{r}
# flag "vali_date" for debugging
debug(vali_date)

# calling "vali_date" starts debugger
vali_date(3)

# unflag "vali_date" for debugging
undebug(vali_date)
```

*** =sct
```{r}
success_msg("Bravo!")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:b6125af738
## Debugging Using browser()

As an alternative to ﬂagging a function for debugging, the user can insert the function `browser()` into the function body.

`browser()` pauses the execution of a function and invokes the debugger (browser) at the point where browser() was called.

Once inside the debugger, the user can execute all the same browser commands as when using `debug()`, `browser()` is usually inserted just before the command that is suspected of producing an error condition.

Another alternative to ﬂagging a function for debugging, or inserting `browser()` calls, is setting the "error" option equal to "recover", Setting the "error" option equal to "recover" automatically invokes the debugger when an error condition is produced

*** =instructions
- Utilize `browser()` for debugging.

*** =hint
Follow the instruction and introductions. Please invoke `vali_date()` without arguments after submitting this exercise. 

*** =pre_exercise_code
```{r}
# no prec
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
# define function
vali_date <- function(in_put) {

# pause and invoke browser
  browser()

# check argument using long form '&&' operator
  stopifnot(!missing(in_put) &&
      is.numeric(in_put))
  2*in_put
}

# show default NULL "error" option
options("error")

# set "error" option to "recover"
options(error=recover)

# set back to default "error" option
options(error=NULL)
```

*** =sct
```{r}
success_msg("Excellent!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7aa0a94261
## Handling Exception Conditions

The function `tryCatch()` can be used as a wrapper around functions or expressions, to handle conditions produced when they are evaluated, `tryCatch()` ﬁrst evaluates its "expression" argument.

If no error or warning condition is produced then `tryCatch()` just returns the value of the expression.

If a condition is produced then `tryCatch()` invokes error and warning handlers and executes other expressions to provide information about the condition.

If a handler is provided to `tryCatch()` then the error is captured by the handler, instead of being broadcast to the console.

At the end, `tryCatch()` evaluates the expression provided to the finally argument.


*** =instructions
- Use `tryCatch()` to handle exceptions.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# get arguments of tryCatch()


# with error handler
tryCatch(
  {  

# evaluate expressions

    
# produce error

  },
  error=function(error_cond)  # handler captures error condition
    print(paste("error handler: ", error_cond)),
  finally=print(paste("num_var=", num_var))
)
```

*** =solution
```{r}
# get arguments of tryCatch()
str(tryCatch)

# with error handler
tryCatch(
  {  

# evaluate expressions
num_var <- 101
    
# produce error
stop('my error')
  },
  error=function(error_cond)  # handler captures error condition
    print(paste("error handler: ", error_cond)),
  finally=print(paste("num_var=", num_var))
)
```

*** =sct
```{r}
success_msg("Nice catch!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:d6245c1bb1
## Error Conditions and Exception Handling in Loops

If an error occurs in an `apply()` loop, then the loop exits without returning any result, `apply()` collects the values returned by the function supplied to its FUN argument, and returns them only after the loop is ﬁnished.

If one of the function calls produces an error, then the loop is interrupted and `apply()` exits without returning any result, The function `tryCatch()` captures errors, allowing loops to continue after the error condition.

If the body of the function supplied to the FUN argument is wrapped in `tryCatch()`, then the loop can ﬁnish without interruption and return its results.

The messages produced by errors and warnings can be caught by handlers (functions) that are supplied to `tryCatch()`, The error and warning messages are bound (passed) to the formal arguments of the handler functions that are supplied to `tryCatch()`, `tryCatch()` always evaluates the expression provided to the finally argument, even after an error occurs.

*** =instructions
- Learn to handle exceptions in loops. Complete the code listed.

*** =hint
Follow the instructions and introductions.


*** =pre_exercise_code
```{r}
```

*** =sample_code
```{r}
# apply loop with tryCatch
apply(as.matrix(1:?), 1, function(num_var) {

# with error handler
    tryCatch(
{

# check for error


# broadcast


# return value

},

# handler captures error condition


  paste("handler: ", error_cond),
finally=print(paste("(finally) num_var =", num_var))
    )
  }
)
```

*** =solution
```{r}
# apply loop with tryCatch
apply(as.matrix(1:5), 1, function(num_var) {

# with error handler
    tryCatch(
{

# check for error
stopifnot(num_var != 3)

# broadcast
cat("(cat) num_var =", num_var, "\t")

# return value
paste("(return) num_var =", num_var)
},

# handler captures error condition
error=function(error_cond)

  paste("handler: ", error_cond),
finally=print(paste("(finally) num_var =", num_var))
    )
  }
)
```

*** =sct
```{r}
success_msg("Nice work!")
```
