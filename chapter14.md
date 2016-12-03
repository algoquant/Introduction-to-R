--- 
title_meta  : Chapter 14
title       : Time Series
description : Present and investigate time series data in R.


--- type:NormalExercise lang:r xp:100 skills:1 key:b1b1305012
## xts Time Series Objects

The package xts deﬁnes time series objects of class "xts", Class "xts" is an extension of the zoo class (derived from zoo), "xts" is the most widely accepted time series class, "xts" is designed for high-frequency and OHLC data, "xts" contains many convenient functions for plotting, calculating rolling max, min, etc. 


The function `xts()` creates a xts object from a numeric vector or matrix, and an associated date-time index, The xts index is a vector of date-time objects, and can be from any date-time class, The xts class can manage irregular time series whose date-time index isn’t equally spaced


*** =instructions
- Explore basic features and operations on xts objects.

*** =hint
Follow instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# load package xts


# create date index


# create xts time series of random returns


# name the series


# print the series


# get last few elements


# get first element


# get last element


# class 'xts'


# get attributes

```

*** =solution
```{r}
# load package xts
library(xts)

# create date index
in_dex <- Sys.Date() + 0:3

# create xts time series of random returns
x_ts <- xts(rnorm(length(in_dex)),
         order.by=in_dex)

# name the series
names(x_ts) <- "random"

# print the series
x_ts

# get last few elements
tail(x_ts, 3)

# get first element
first(x_ts)

# get last element
last(x_ts)

# class 'xts'
class(x_ts)

# get attributes
attributes(x_ts)
```


*** =sct
```{r}
test_error()
success_msg("Great!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:05697caf6a
## Coercing zoo Time Series Into Class xts

The function `as.xts()` coerces time series (including zoo) into xts time series, `as.xts()` preserves the index attributes of the original time series, xts can be plotted using the generic function `plot()`, which dispatches the `plot.xts()` method


*** =instructions
- Print and plot time series data.

*** =hint
Follow the instruction and introductions

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# as.xts() creates xts from zoo


# get dimension of xts


# get first 4 lines and first 4 columns


# set parameters


# plot using plot.xts method


# add title

```

*** =solution
```{r}
# as.xts() creates xts from zoo
st_ox <- as.xts(zoo_stx_adj)

# get dimension of xts
dim(st_ox)

# get first 4 lines and first 4 columns
head(st_ox[, 1:4], 4)

# set parameters
par(mar=c(7, 2, 1, 2), mgp=c(2, 1, 0), cex.lab=0.8, cex.axis=0.8, cex.main=0.8, cex.sub=0.5)

# plot using plot.xts method
plot(st_ox[, "AdjClose"], xlab="", ylab="", main="")

# add title
title(main="MSFT Prices")
```


*** =sct
```{r}
test_error()
success_msg("Excellent!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:b99299073f
## Plotting Multiple xts Using Packages xts and quantmod

The quantmod package has some useful function to generate fancy stock charts.

*** =instructions
- Make use of functions in quantmod package to visualize time series data.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# load xts


# load lubridate


# coerce EuStockMarkets into class xts


# set colors


# complete the code to plot all columns in single panel
plot(x_ts, main="EuStockMarkets using xts",
     col=?, major.ticks=?,
     minor.ticks=TRUE)

# make legends


# plot only first column


# plot remaining columns


# load quantmod package


# select theme


# select color


# plot using quantmod


# set legends

```

*** =solution
```{r}
# load xts
library(xts)

# load lubridate
library(lubridate)

# coerce EuStockMarkets into class xts
x_ts <- xts(coredata(EuStockMarkets),
      order.by=date_decimal(index(EuStockMarkets)))

# set colors
col_ors <- rainbow(NCOL(x_ts))

# complete the code to plot all columns in single panel
plot(x_ts, main="EuStockMarkets using xts",
     col=col_ors, major.ticks="years",
     minor.ticks=FALSE)

# make legends
legend("topleft", legend=colnames(EuStockMarkets),
 inset=0.2, cex=0.7, , lty=rep(1, NCOL(x_ts)),
 lwd=3, col=col_ors, bg="white")

# plot only first column
plot(x_ts[, 1], main="EuStockMarkets using xts",
     col=col_ors[1], major.ticks="years",
     minor.ticks=FALSE)

# plot remaining columns
for(col_umn in 2:NCOL(x_ts))
  lines(x_ts[, col_umn], col=col_ors[col_umn])
  
# load quantmod package
library(quantmod)

# select theme
plot_theme <- chart_theme()

# select color
plot_theme$col$line.col <- col_ors

# plot using quantmod
chart_Series(x=x_ts, theme=plot_theme,
       name="EuStockMarkets using quantmod")

# set legends
legend("topleft", legend=colnames(EuStockMarkets),
 inset=0.2, cex=0.7, , lty=rep(1, NCOL(x_ts)),
 lwd=3, col=col_ors, bg="white")
```


*** =sct
```{r}
test_error()
success_msg("Excellent!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:ab03e239aa
## Plotting xts Using Package ggplot2

xts time series can be plotted using the package ggplot2.

The function `qplot()` is the simplest function in the ggplot2 package, and allows creating line and bar plots.

The function `theme()` customizes plot objects

*** =instructions
- Use ggplot package to create beautiful time series charts.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
load("etf_data.Rdata")
load("etf_data_new.Rdata")
```

*** =sample_code
```{r}
# complete code to create ggplot object
etf_gg <- qplot(x=env_etf$price_s[, 1],
          y=env_etf$price_s[, 2],
          geom="points",
          main=env_etf$price_s[, 1]) +
  xlab("") + ylab("") +
  theme(

# add legend and title
    legend.position=c(0.1, 0.5),
    plot.title=element_text(vjust=-2.0),
    plot.background=element_blank()
  )

# render ggplot object
etf_gg
```

*** =solution
```{r}
# complete code to create ggplot object
etf_gg <- qplot(x=index(env_etf$price_s[, 1]),
          y=as.numeric(env_etf$price_s[, 1]),
          geom="line",
          main=names(env_etf$price_s[, 1])) +
  xlab("") + ylab("") +
  theme(

# add legend and title
    legend.position=c(0.1, 0.5),
    plot.title=element_text(vjust=-2.0),
    plot.background=element_blank()
  )

# render ggplot object
etf_gg
```


*** =sct
```{r}
test_error()
success_msg("GGplot is the most popular plot library in R. Learn more on datacamp or other online sources")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:540b8c57a5
## Plotting Multiple xts Using Package ggplot2

Multiple xts time series can be plotted using the function `ggplot()` from package ggplot2.

But ggplot2 functions don’t accept time series objects, so time series must be ﬁrst formatted into data frames


*** =instructions
- Plot various time serieses at once in ggplot2.

*** =hint
In order to plot various time series at once, you need to combine time serieses into one data frame.

*** =pre_exercise_code
```{r}
# no pec
load("etf_data.Rdata")
load("etf_data_new.Rdata")
```

*** =sample_code
```{r}
# load reshape2


# load ggplot2


# create data frame of time series


# reshape data into a single column


# change the code to ggplot the melted data_frame
ggplot(data=data_frame,
 mapping=aes()) +
 geom_line() +
  xlab("") + ylab("") +
  ggtitle("VTI and IEF") +
  theme(

# add legend and title

  )
```

*** =solution
```{r}
# load reshape2
library(reshape2)

# load ggplot2
library(ggplot2)

# create data frame of time series
data_frame <-
  data.frame(dates=index(env_etf$price_s),
    coredata(env_etf$price_s[, c("VTI", "IEF")]))

# reshape data into a single column
data_frame <- reshape2::melt(data_frame, id="dates")

# change the code to ggplot the melted data_frame
ggplot(data=data_frame,
 mapping=aes(x=dates, y=value, colour=variable)) +
 geom_line() +
  xlab("") + ylab("") +
  ggtitle("VTI and IEF") +
  theme(

# add legend and title
    legend.position=c(0.2, 0.8),
    plot.title=element_text(vjust=-2.0)
  )
```


*** =sct
```{r}
test_error()
success_msg("Beautiful Charts! Tune the parameters to make your own style!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:5a2dc65a8a
## Interactive Time Series Plots Using Package dygraphs

The function `dygraph()` from package dygraphs creates interactive, zoomable plots from xts time series.

The function `dyOptions()` adds options (like colors, etc.) to a dygraph plot.

The function `dyRangeSelector()` adds a date range selector to the bottom of a dygraphs plot.

`%>%` the pipe operator is widely used in R data analysis to transfer function outcome to another function.

*** =instructions
- Make interactive time series plots.

*** =hint
Follow the instructions and introductions.

*** =pre_exercise_code
```{r}
# no pec
load("etf_data.Rdata")
load("etf_data_new.Rdata")
```

*** =sample_code
```{r}
# load dygraphs package


# load magrittr package


# generate data object


# cahnge the code to plot dygraph with date range selector
dygraph()
  dyOptions()
  dyRangeSelector()
```

*** =solution
```{r}
# load dygraphs package
library(dygraphs)

# load magrittr package
library(magrittr)

# generate data object
x_ts <- env_etf$price_s[, c("VTI", "IEF")]

# cahnge the code to plot dygraph with date range selector
dygraph(x_ts, main="VTI and IEF prices") %>%
  dyOptions(colors=c("blue","green")) %>%
  dyRangeSelector()
```


*** =sct
```{r}
test_error()
success_msg("Amazing interactive charts!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:2635635720
## Interactive Time Series Plots Using Package plotly

The function `plot_ly()` from package plotly creates interactive plots from data residing in data frames.

The function `add_trace()` adds elements to a plotly plot.

The function `layout()` modiﬁes the layout of a plotly plot.

*** =instructions
- Use plotly packge for another interactive charts.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no pec
load("etf_data.Rdata")
load("etf_data_new.Rdata")
```

*** =sample_code
```{r}
# load libraries


# create data frame of time series


# plotly syntax using pipes
data_frame %>%
  plot_ly(x=dates, y=VTI, fill=?, name=?)
  add_trace(x=dates, y=IEF, fill=, name=?)
  layout(title="VTI and IEF prices",
   xaxis=list(title="Time"),
   yaxis=list(title="Stock Prices"),
   legend=list(x=0.1, y=0.9))
```

*** =solution
```{r}
# load libraries
suppressMessages(suppressWarnings(library(magrittr)))
suppressMessages(suppressWarnings(library(plotly)))

# create data frame of time series
data_frame <-
  data.frame(dates=index(env_etf$price_s),
    coredata(env_etf$price_s[, c("VTI", "IEF")]))

# plotly syntax using pipes
data_frame %>%
  plot_ly(x=dates, y=VTI, fill="tozeroy", name="VTI") %>%
  add_trace(x=dates, y=IEF, fill="tonexty", name="IEF") %>%
  layout(title="VTI and IEF prices",
   xaxis=list(title="Time"),
   yaxis=list(title="Stock Prices"),
   legend=list(x=0.1, y=0.9))
```


*** =sct
```{r}
test_error()
success_msg("This is very modern chart!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:e2b1d979f4
## Subsetting Vectors

Vector elements can be subset (indexed, dereferenced) using the "[]" operator.

Vectors can be subset using vectors of:
positive integers, 
negative integers, 
characters (names),
boolean vectors. 

Negative integers remove the vector elements.
Subsetting with zero returns a zero-length vector.
A named vector can be subset using element names.

*** =instructions
Vec_tor has been recreated in this exercise. 
Use "[]" combined with integers, characters and boolean vectors to subset a vector.

*** =hint
Check if object names and function names are correctly typed.

*** =pre_exercise_code
```{r}
vec_tor <- c(pi_const=pi, euler=exp(1), gamma=-digamma(1))
```

*** =sample_code
```{r}
# extract second element


# extract all elements, except the second element


# extract zero elements - returns zero-length vector


# extract second and third elements by boolean vector


# extract a element using its name "eulery"


# extract multiple elements using a vector of their names


# now create a boolean vector comparing vec_tor to 2, name it as "bool"
bool <- vec_tor > 2

# subset vec_tor with bool to see which element is bigger than 2

```

*** =solution
```{r}
# extract second element
vec_tor[2]

# extract all elements, except the second element
vec_tor[-2]

# extract zero elements - returns zero-length vector
vec_tor[0]

# extract second and third elements by boolean vector
vec_tor[c(FALSE, TRUE, TRUE)]

# extract a element using its name "eulery"
vec_tor["eulery"]

# extract multiple elements using a vector of their names
vec_tor[c("pie", "gammy")]

# now create a boolean vector comparing vec_tor to 2, name it as "bool"
bool <- vec_tor > 2

# subset vec_tor with bool to see which element is bigger than 2
vec_tor[bool]
```


*** =sct
```{r}
test_error()
success_msg("The subsetting provides support for filtering")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:47e9ca9b81
## Filtering Vectors

Filtering means extracting elements from a vector that satisfy a logical condition.
When logical comparison operators are applied to vectors, they produce boolean vectors.
Boolean vectors can then be applied to subset the original vectors, to extract their elements.
The function which() returns the indices of the TRUE elements of a boolean vector or array.


*** =instructions
Vec_tor has been recreated in this exercise. 
Use "[]"  or "which()" to filter vector elements.

*** =hint
Check if object names and function names are correctly typed.

*** =pre_exercise_code
```{r}
vec_tor <- runif(5)
```

*** =sample_code
```{r}
# first, print the vec_tor


# compare vec_tor to 0.5


# boolean vector of elements equal to the second one


# extract all elements equal to the second one


# extract all elements greater than 0.5


# get index of elements > 0.5


# combine which() and "[]" to extract elements greater than 0.5

```

*** =solution
```{r}
# first, print the vec_tor
vec_tor

# compare vec_tor to 0.5
vec_tor > 0.5

# boolean vector of elements equal to the second one
vec_tor == vec_tor[2]

# extract all elements equal to the second one
vec_tor[vec_tor == vec_tor[2]]

# extract all elements greater than 0.5
vec_tor[vec_tor > 0.5]

# get index of elements > 0.5
which(vec_tor > 0.5)

# combine which() and "[]" to extract elements greater than 0.5
vec_tor[which(vec_tor > 0.5)]
```


*** =sct
```{r}
test_error()
success_msg("Now you can filter a vector with '[]' and which()!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:ab3a8365ff
## Factors

Factors are similar to vectors, but their elements can only take values from a set of levels.
Factors are designed for categorical data which can only take certain values.

The function factor() converts a vector into a factor, Factors have two attributes: class (equal to "factor") and levels (the allowed values).
Although factors aren’t vectors, the data underlying a factor is an integer vector, called an encoding vector.
The function as.numeric() extracts the encoding vector (indices) of a factor.
The function as.vector() coerces a factor to a character vector.

*** =instructions
Create factors with factor(). 
See attributes of factor using attributes() and levels().
Coerce factor using as.numeric() and as.vector().

*** =hint
Check if object names and function names are correctly typed.

*** =pre_exercise_code
```{r}
fac_tor <- factor(c('b', 'c', 'd', 'a', 'c', 'b'))
```

*** =sample_code
```{r}
# print the factor vector 'fac_tor'
fac_tor

# subset fac_tor for the third element


# get factor attributes


# get factor levels


# get encoding vector


# coerce factor to character vector

```

*** =solution
```{r}
# print the factor vector 'fac_tor'
fac_tor

# subset fac_tor for the third element
fac_tor[3]

# get factor attributes
attributes(fac_tor)

# get factor levels
levels(fac_tor)

# get encoding vector
as.numeric(fac_tor)

# coerce factor to character vector
as.vector(factor(1:5))
```


*** =sct
```{r}
test_error()
success_msg("See! The numeric vector turned to be a character vector!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:771f2e9f50
## Tables of Categorical Data

The function table() calculates the frequency distribution of categorical data.
A contingency table is a matrix that contains the frequency distribution of variables (factors) contained in a set of data, sapply() applies a function to a vector or a list of objects and returns a vector or a list,


*** =instructions
Use functions and variables as insturcted in the comment.

*** =hint
Check if object names and function names are correctly typed.

*** =pre_exercise_code
```{r}
fac_tor <- factor(c('b', 'c', 'd', 'a', 'c', 'b'))
```

*** =sample_code
```{r}
# have a look at the factor vector
fac_tor

# get encoding vector


# get unique values


# change the code below to get contingency table
sapply(fac_tor, 
 function(le_vel) {
   sum(fac_tor=le_vel)
 })

# get contingency (frequency) table

```

*** =solution
```{r}
# have a look at the factor vector
fac_tor

# get encoding vector
as.numeric(fac_tor)

# get unique values
unique(fac_tor)

# change the code below to get contingency table using sapply 
sapply(levels(fac_tor), 
 function(le_vel) {
   sum(fac_tor==le_vel)
 })

# get contingency (frequency) table
table(fac_tor)
```


*** =sct
```{r}
test_error()
success_msg("Compared the results you get with sapply() and table()")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:748763cc09
## Classifying Continuous Numeric Data Into Categories

Numeric data that represents a magnitude, intensity, or score can be classiﬁed into categorical data, given a vector of breakpoints.

The breakpoints create intervals that correspond to diﬀerent categories.

The categories combine elements that have a similar numeric magnitude, findInterval() returns the indices of the intervals speciﬁed by "vec" that contain the elements of "x".
If there’s an exact match, then findInterval() returns the same index as function match().
If there’s no exact match, then findInterval() ﬁnds the element of "vec" that is closest to, but not greater than, the element of "x".
If all the elements of "vec" are greater than the element of "x", then findInterval() returns zero,


*** =instructions
Use functions and variables as insturcted in the comment.

*** =hint
Check if object names and function names are correctly typed.

*** =pre_exercise_code
```{r}
# none
```

*** =sample_code
```{r}
# see how we can tweak the outcome findInterval() function with five parameters
str(findInterval)

# get index of the element of "vec" c(3,5,7) that matches 5


# use match()


# no exact match


# use match()


# indices of "vec" that match elements of "x"


# return only indices of inside intervals


# make rightmost interval inclusive

```

*** =solution
```{r}
# see how we can tweak the outcome findInterval() function with five parameters
str(findInterval)

# get index of the element of "vec" c(3,5,7) that matches 5
findInterval(x=5, vec=c(3, 5, 7))

# use match()
match(5, c(3, 5, 7))

# no exact match
findInterval(x=6, vec=c(3, 5, 7))

# use match()
match(6, c(3, 5, 7))

# indices of "vec" that match elements of "x"
findInterval(x=1:8, vec=c(3, 5, 7))

# return only indices of inside intervals
findInterval(x=1:8, vec=c(3, 5, 7), all.inside=TRUE)

# make rightmost interval inclusive
findInterval(x=1:8, vec=c(3, 5, 7), rightmost.closed=TRUE)
```


*** =sct
```{r}
test_error()
success_msg("Congrats! This is the very first step in dividing continuous values")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:91aa35a650
## Classifying Continuous Numeric Data Into Categories, Continued

Temperature can be categorized into ”cold”, ”warm”, ”hot”, etc. 
A named numeric vector of breakpoints can be used to convert a temperature into one of the categories.
Breakpoints correspond to categories of the data.
The ﬁrst breakpoint should correspond to the lowest category, and should have a value less than any of the data.


*** =instructions
Use functions and variables as insturcted in the comment.

*** =hint
Check if object names and function names are correctly typed.

*** =pre_exercise_code
```{r}
# none
```

*** =sample_code
```{r}
# creat named numeric vector of breakpoints
brea_ks <- c("freezing"=0, "very_cold"=30,
       "cold"=50, "pleasant"=60,
       "warm"=80, "hot"=90)

# print out the breakpoints vector
brea_ks

# create a vector of temperatures
tempe_ratures <- runif(10, min=10, max=100)

# change the code to name values according to breakpoints
feels_like <- names(
  brea_ks,findInterval(x=tempe_ratures,
                 vec=brea_ks))

names(tempe_ratures) <- feels_like

# print the categorized vector

```

*** =solution
```{r}
# creat named numeric vector of breakpoints
brea_ks <- c("freezing"=0, "very_cold"=30,
       "cold"=50, "pleasant"=60,
       "warm"=80, "hot"=90)

# print out the breakpoints vector
brea_ks

# create a vector of temperatures
tempe_ratures <- runif(10, min=10, max=100)

# change the code to name values according to breakpoints
feels_like <- names(
  brea_ks[findInterval(x=tempe_ratures,
                 vec=brea_ks)])

names(tempe_ratures) <- feels_like

# print the categorized vector
tempe_ratures
```


*** =sct
```{r}
test_error()
success_msg("Congrats! This is the your first value categorization results!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:ca09ff3670
## Converting Numeric Data Into Factors Using cut()

The function cut() converts a numeric vector into a vector of factors, representing the intervals to which the numeric values belong, cut() divides the range of values into intervals, based on a vector of breaks, cut() then assigns factors to the numeric values, representing the intervals to which the numeric values belong. 
The argument "breaks" is a numeric vector of break points that divide the range of values into intervals.
The argument "labels" is a vector of labels for the intervals.
The argument "right" is a boolean indicating if the intervals should be closed on the right (and open on the left), or vice versa, cut() can produce the same classiﬁcation as findInterval(), but findInterval() is faster than cut(), because it’s a compiled function,

The library microbenchmark is already loaded to the environment

*** =instructions
Use functions and variables as insturcted in the comment.

*** =hint
Check if object names and function names are correctly typed.

*** =pre_exercise_code
```{r}
library(microbenchmark)
```

*** =sample_code
```{r}
# create a vector of random value
foo <- sample(0:6) + 0.1

# print the vector foo


# use cut to vector
cut(x=foo, breaks=c(2, 4, 6, 8))

# bind the cutted vector with rbind()
rbind(foo, cut(x=foo, breaks=c(2, 4, 6, 8)))

# cut the vector with findInterval()
findInterval(x=1:8, vec=c(2, 4, 6, 8))

# findInterval() is a compiled function, so it is faster than cut()
# change the code to compare their speed
vec_tor <- rnorm(1000)
summary(microbenchmark(
  find_interval=
    findInterval(vec=c(3, 5, 7)),
  cuut=
    cut(breaks=c(3, 5, 7)),
  times=10))[, c(1, 4, 5)]
```

*** =solution
```{r}
# create a vector of random value
foo <- sample(0:6) + 0.1

# print the vector foo
foo

# use cut to vector
cut(x=foo, breaks=c(2, 4, 6, 8))

# bind the cutted vector with rbind()
rbind(foo, cut(x=foo, breaks=c(2, 4, 6, 8)))

# cut the vector with findInterval()
findInterval(x=1:8, vec=c(2, 4, 6, 8))

# findInterval() is a compiled function, so it is faster than cut()
# change the code to compare their speed
vec_tor <- rnorm(1000)
summary(microbenchmark(
  find_interval=
    findInterval(x=vec_tor, vec=c(3, 5, 7)),
  cuut=
    cut(x=vec_tor, breaks=c(3, 5, 7)),
  times=10))[, c(1, 4, 5)]
```


*** =sct
```{r}
test_error()
success_msg("Althogh slower and a little bit different, cut() has similar functionality as findInternval()")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:cd32ce976a
## Matrices

The function matrix() creates a matrix from a vector, and the matrix dimensions.
By default matrix() creates matrices column-wise, unless the argument byrow=TRUE is used.
The elements of matrices can be subset (dereferenced) using the "[]" operator.
The functions nrow() and ncol() return the number of rows and columns of a matrix.
The functions NROW() and NCOL() also return the number of rows or columns of a matrix, but they can also be applied to vectors, and treat vectors as single column matrices.

*** =instructions
Use matrix() to construct matrices, and nrow(), ncol() and NROW(), NCOL().

*** =hint
Check if object names and function names are correctly typed.

*** =pre_exercise_code
```{r}
vec_tor <- runif(5)
```

*** =sample_code
```{r}
# create a matrix
mat_rix <- matrix(5:10, nrow=2, ncol=3)

# by default matrices are constructed column-wise
mat_rix

# create a matrix row-wise
matrix(5:10, nrow=2, byrow=TRUE)

# extract third element from second row


# extract second row


# now try to extract third column


# extract first and third column


# remove second column


# get the number of rows or columns
nrow(mat_rix); ncol(mat_rix)
NROW(mat_rix); NCOL(mat_rix)

# apply nrow() and NROW() on vec_tor

```

*** =solution
```{r}
# create a matrix
mat_rix <- matrix(5:10, nrow=2, ncol=3)

# by default matrices are constructed column-wise
mat_rix

# create a matrix row-wise
matrix(5:10, nrow=2, byrow=TRUE)

# extract third element from second row
mat_rix[2, 3]

# extract second row
mat_rix[2, ]

# now try to extract third column
mat_rix[, 3]

# extract first and third column
mat_rix[, c(1,3)]

# remove second column
mat_rix[, -2]

# get the number of rows or columns
nrow(mat_rix); ncol(mat_rix)
NROW(mat_rix); NCOL(mat_rix)

# apply nrow() and NROW() on vec_tor
nrow(vec_tor)
NROW(vec_tor)
```


*** =sct
```{r}
test_error()
success_msg("So the capitalized functions can be applied to vectors and matrixes")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:9cb7dccabe
## Matrix attributes

Arrays are vectors with a dimension attribute.
Matrices are two-dimensional arrays.
The dimension attribute of a matrix is an integer vector of length 2 (nrow, ncol).
The dimnames attribute is a list, with vector elements containing row and column names.
A named matrix can be subset using row and column names.


*** =instructions
Use attributes(), dim(), rownames(), colnames() and rownames() as instructed.

*** =hint
Check if object names and function names are correctly typed.

*** =pre_exercise_code
```{r}
mat_rix <- matrix(5:10, nrow=2, ncol=3)
```

*** =sample_code
```{r}
# get matrix attributes


# get dimension attribute


# get class attribute


# change the code to assign rownames and colnames attribute
c("row1", "row2")
c("col1", "col2", "col3")

# use dimnames() to see row and column names


# get the name attributes of mat_rix

```

*** =solution
```{r}
# get matrix attributes
attributes(mat_rix)

# get dimension attribute
dim(mat_rix)

# get class attribute
class(mat_rix)

# rownames and colnames attribute
rownames(mat_rix) <- c("row1", "row2")
colnames(mat_rix) <- c("col1", "col2", "col3")

# use dimnames() to see row and column names
dimnames(mat_rix)

# get the name attributes of mat_rix
names(mat_rix)
```


*** =sct
```{r}
test_error()
success_msg("dimname and name is different!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:cb0ddb5306
## Matrix Subsetting

Matrices can be subset in a similar way as Vectors, either by indices (integers), by characters (names), or boolean vectors.
Subsetting a matrix to a single row or column produces a vector, unless the parameter "drop=FALSE" is used.
Subsetting with the parameter "drop=FALSE" prevents the implicit coercion and preserves the matrix class.
This is an example of implicit coercion in R, which can cause diﬃcult to trace bugs.


*** =instructions
Use "[]" for matrix subsetting, beware of the parameter "drop=FALSE"

*** =hint
Check if object names and function names are correctly typed.

*** =pre_exercise_code
```{r}
mat_rix <- matrix(5:10, nrow=2, ncol=3)
rownames(mat_rix) <- c("row1", "row2")
colnames(mat_rix) <- c("col1", "col2", "col3")
```

*** =sample_code
```{r}
# subset column1 by name 
mat_rix[, "col1"]

# subset columns 1,3 by boolean vector
mat_rix[, c(TRUE, FALSE, TRUE)]

# get subset of row 1 by index
mat_rix[1, ]

# drop=FALSE preserves matrix
mat_rix[1, , drop=FALSE]

# revise the code to create two subsets with and without drop = FALSE argument
mat_1 <- mat_rix[1, ]
mat_2 <- mat_rix[1, ]

# check if the two subsets are matrix using is.matrix()

```

*** =solution
```{r}
# subset column1 by name 
mat_rix[, "col1"]

# subset columns 1,3 by boolean vector
mat_rix[, c(TRUE, FALSE, TRUE)]

# get subset of row 1 by index
mat_rix[1, ]

# drop=FALSE preserves matrix
mat_rix[1, , drop=FALSE]

# revise the code to create two subsets with and without drop = FALSE argument
mat_1 <- mat_rix[1, ]
mat_2 <- mat_rix[1, , drop=FALSE]

# check if the two subsets are matrix using is.matrix()
is.matrix(mat_1)
is.matrix(mat_2)
```


*** =sct
```{r}
test_error()
success_msg("Add or drop the 'drop = FALSE' argument does make differences!")
```

