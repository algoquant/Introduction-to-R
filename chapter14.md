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
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
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
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
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
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
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
library(zoo)
library(xts)
library(ggplot2)
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
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
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
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
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
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
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
```

*** =sample_code
```{r}
# load libraries


# create data frame of time series


# plotly syntax using pipes
data_frame %>%
  plot_ly(x=~dates, y=~VTI, fill=?, name=?)
  add_trace(x=~dates, y=~IEF, fill=, name=?)
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

# change code to make plot
data_frame %>%
  plot_ly(x=~dates, y=~VTI, type = "scatter",fill="tozeroy", name="VTI") %>%
  add_trace(x=~dates, y=~IEF, type= "scatter",fill="tonexty", name="IEF") %>%
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
## Subsetting xts Time Series

xts time series can be subset in similar ways to zoo.

In addition, xts time series can be subset using date strings, or date range strings, for example: ["2014-10-15/2015-01-10"], xts time series can be subset by year, week, days, or even seconds.

If only the date is subset, then a comma "," after the date range isn’t necessary, The function `.subset xts()` allows fast subsetting of xts time series, which is at least three times faster than the bracket "[]" notation

*** =instructions
- Subset time series objects according to time span

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
```

*** =sample_code
```{r}
# construct time series


# subset xts using a date range string


# get the first element


# get the last element


# subset Nov 2014 using a date string


# get the first element


# get the last element


# subset all data after Nov 2014


# get the first element


# get the last element


# comma after date range not necessary


# load microbenchmark


# benchmark the speed of subsetting

```

*** =solution
```{r}
# construct time series
st_ox <- as.xts(zoo_stx_adj)

# subset xts using a date range string
stox_sub <- st_ox["2014-10-15/2015-01-10", 1:4]

# get the first element
first(stox_sub)

# get the last element
last(stox_sub)

# subset Nov 2014 using a date string
stox_sub <- st_ox["2014-11", 1:4]

# get the first element
first(stox_sub)

# get the last element
last(stox_sub)

# subset all data after Nov 2014
stox_sub <- st_ox["2014-11/", 1:4]

# get the first element
first(stox_sub)

# get the last element
last(stox_sub)

# comma after date range not necessary
identical(st_ox["2014-11", ], st_ox["2014-11"])

# load microbenchmark
library(microbenchmark)

# benchmark the speed of subsetting
summary(microbenchmark(
  bracket=sapply(10*(10:1000),
  function(in_dex)
    max(SPY[in_dex:(in_dex+10), ])),
  subset=sapply(10*(10:1000),
  function(in_dex)
    max(.subset_xts(SPY, in_dex:(in_dex+10)))),
  times=10))[, c(1, 4, 5)]
```


*** =sct
```{r}
test_error()
success_msg("Carefully use this convenient but slow tool!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:47e9ca9b81
## Subsetting Recurring xts Time Intervals

A recurring time interval is the same time interval every day, xts can be subset on recurring time intervals using the "T" notation。

For example, to subset the time interval from 9:30AM to 4:00PM every day: `["T09:30:00/T16:00:00"]` Warning messages that ”timezone of object is diﬀerent than current timezone” can be suppressed by calling the function `options()` with argument "xts check tz=FALSE"


*** =instructions
- Subset with recurring time span.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
```

*** =sample_code
```{r}
# vector of 1-minute times (ticks)


# xts of 1-minute times (ticks) of random returns


# subset recurring time interval using "T notation",


# first element of day


# last element of day


# suppress timezone warning messages

```

*** =solution
```{r}
# vector of 1-minute times (ticks)
min_ticks <- seq.POSIXt(
  from=as.POSIXct("2015-04-14", tz="America/New_York"),
  to=as.POSIXct("2015-04-16"),
  by="min")

# xts of 1-minute times (ticks) of random returns
x_ts <- xts(rnorm(length(min_ticks)),
               order.by=min_ticks)

# subset recurring time interval using "T notation",
x_ts <- x_ts["T09:30:00/T16:00:00"]

# first element of day
first(x_ts["2015-04-15"])

# last element of day
last(x_ts["2015-04-15"])

# suppress timezone warning messages
options(xts_check_tz=FALSE)
```


*** =sct
```{r}
test_error()
success_msg("Subset for regular daily periods made easy!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:ab3a8365ff
## Properties of xts Time Series

xts series always have a dim attribute, unlike zoo, zoo series with multiple columns have a dim attribute, and are therefore matrices.

But zoo with a single column don’t, and are therefore vectors not matrices, When a zoo is subset to a single column, the dim attribute is dropped, which can create errors.


*** =instructions
- Explore properties of xts object

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
st_ox <- as.xts(zoo_stx_adj)
```

*** =sample_code
```{r}
# display structure of xts


# subsetting zoo


# subsetting zoo to single column drops dim attribute


# zoo with single column are vectors not matrices


# xts always have a dim attribute


# check if it a matrix

```

*** =solution
```{r}
# display structure of xts
str(st_ox)

# subsetting zoo
dim(zoo_stx_adj)

# subsetting zoo to single column drops dim attribute
dim(zoo_stx_adj[, 1])

# zoo with single column are vectors not matrices
c(is.matrix(zoo_stx_adj), is.matrix(zoo_stx_adj[, 1]))

# xts always have a dim attribute
rbind(base=dim(st_ox), subs=dim(st_ox[, 1]))

# check if it a matrix
c(is.matrix(st_ox), is.matrix(st_ox[, 1]))
```


*** =sct
```{r}
test_error()
success_msg("xts is actually a matrix with time index")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:771f2e9f50
## lag() and diff() Operations on xts Time Series

`lag()` and `diff()` operations on xts series diﬀer from those on zoo, `lag()` and `diff()` operations on zoo series shorten the series by one row, By default, the `lag()` operation on xts replaces the present value with values from the past (negative lags replace with values from the future).

By default, the `lag()` and `diff()` operations on xts retain the same number of rows, but substitute NAs for missing data.


*** =instructions
- Use functions to get lag terms in time series.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
st_ox <- as.xts(zoo_stx_adj)
```

*** =sample_code
```{r}
# lag of zoo shortens it by one row


# lag of xts doesn't shorten it


# lag of zoo is in opposite direction from xts


# print the first 4 rows

```

*** =solution
```{r}
# lag of zoo shortens it by one row
rbind(base=dim(zoo_stx_adj), lag=dim(lag(zoo_stx_adj)))

# lag of xts doesn't shorten it
rbind(base=dim(st_ox), lag=dim(lag(st_ox)))

# lag of zoo is in opposite direction from xts
head(lag(zoo_stx_adj), 4)

# print the first 4 rows
head(lag(st_ox), 4)
```


*** =sct
```{r}
test_error()
success_msg("Lag terms are useful for time series analysis. Just be careful to the NA items generated.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:748763cc09
## Converting xts to Lower Periodicity

The function `to.period()` converts a time series to a lower periodicity (for example from hourly to daily periodicity), `to.period()` returns a time series of open, high, low, and close values (OHLC) for the lower period, `to.period()` converts both univariate and OHLC time series to a lower periodicity


*** =instructions
- Use `to.period()` families to adapt time series frequency.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# none
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
st_ox <- as.xts(zoo_stx_adj)
```

*** =sample_code
```{r}
# lower the periodicity to months


# get monthly column names


# change the code to convert colnames to standard OHLC format 
colnames(xts_monthly) <- sapply(
  colnames(xts_monthly),
  function(na_me) na_me[-1]
  )

# print the first 3 rows


# lower the periodicity to years


# change the code to modify column names
colnames(xts_yearly) <- sapply(
  colnames(xts_yearly),
  function(na_me) na_me[-1]
  )

# get head

```

*** =solution
```{r}
# lower the periodicity to months
xts_monthly <- to.period(x=st_ox,
             period="months", name="MSFT")

# get monthly column names
colnames(xts_monthly)

# change the code to convert colnames to standard OHLC format 
colnames(xts_monthly) <- sapply(
  strsplit(colnames(xts_monthly), split=".", fixed=TRUE),
  function(na_me) na_me[-1]
  )

# print the first 3 rows
head(xts_monthly, 3)

# lower the periodicity to years
xts_yearly <- to.period(x=xts_monthly,
             period="years", name="MSFT")

# change the code to modify column names
colnames(xts_yearly) <- sapply(
  strsplit(colnames(xts_yearly), split=".", fixed=TRUE),
  function(na_me) na_me[-1]
  )

# get head
head(xts_yearly)
```


*** =sct
```{r}
test_error()
success_msg("You can use daily data to generate OHLC data of lower frequency now")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:91aa35a650
## Plotting OHLC Time Series Using xts

The method (function) plot.xts() can plot OHLC time series of class xts.


*** =instructions
- Plot OHLC data.

*** =hint
Follow the instruction and introduction

*** =pre_exercise_code
```{r}
# none
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
st_ox <- as.xts(zoo_stx_adj)
```

*** =sample_code
```{r}
# as.xts() creates xts from zoo


# subset xts using a date


# plot OHLC using plot.xts method


# add title

```

*** =solution
```{r}
# as.xts() creates xts from zoo
st_ox <- as.xts(zoo_stx_adj)

# subset xts using a date
stox_sub <- st_ox["2014-11", 1:4]

# plot OHLC using plot.xts method
plot(stox_sub, type="candles", main="")

# add title
title(main="MSFT Prices")
```


*** =sct
```{r}
test_error()
success_msg("OHLC helps generating candle charts!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:ca09ff3670
## Time Series Classes in R

R and other packages contain a number of diﬀerent time series classes: 

Class "ts" from base package stats: native time series class in R, but allows only regular (equally spaced) date-time index, not suitable for sophisticated ﬁnancial applications, 

Class "zoo": allows irregular date-time index, the zoo index can be from any date-time class, 

Class "xts" extension of zoo class: most widely accepted time series class, designed for high-frequency and OHLC data, contains convenient functions for plotting, calculating rolling max, min, etc. 

Class "timeSeries" from the Rmetrics suite

*** =instructions
- Use and compare different time series format.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
library(microbenchmark)
library(zoo)
library(xts)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/zoo_data.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1871/datasets/etf_data.RData"))
```

*** =sample_code
```{r}
# make ts object


# get its class


# see the last few data


# load the xts package


# make xts object


# get its class


# get the last few rows

```

*** =solution
```{r}
# make ts object
ts_stx <- as.ts(zoo_stx)

# get its class
class(ts_stx)

# see the last few data
tail(ts_stx[, 1:4])

# load the xts package
library(xts)

# make xts object
st_ox <- as.xts(zoo_stx)

# get its class
class(st_ox)

# get the last few rows
tail(st_ox[, 1:4])
```


*** =sct
```{r}
test_error()
success_msg("All formats are fine, but you see there're reason we prefer xts")
```
