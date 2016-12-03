--- 
title_meta  : Chapter 13
title       : Numbers and Dates
description : A bit more details about numeric variables and date-time objects.


--- type:NormalExercise lang:r xp:100 skills:1 key:f625f0fd8d
## Floating Point Numbers

Real numbers which have an infinite number of significant digits can only be represented approximately inside a computer.

Floating point numbers are approximate representations of real numbers inside a computer.

Machine precision is a number that specifies the accuracy of floating point numbers in a computer.

The representation of floating point numbers in R depends on the machine precision of the computer operating system.

R prints floating point numbers without showing their full internal representation, which can cause confusion about their true value.

The function `all.equal()` tests the equality of two objects to within the square root of the machine precision.

The generic function `format()` formats R objects for printing and display


*** =instructions
- Evaluate numeric value within and out of machine precision.

*** =hint
Follow the instruction and introduction. 

*** =pre_exercise_code
```{r}
```

*** =sample_code

```{r}
# assign value


# printed as "0.1"


# foo is not equal to "0.1"


# foo is not equal to "0.1"


# print with 10 digit precision


# print with 16 digit precision


# foo is equal to "0.1" within machine precision


# assign by deduct


# print with 20 digit precision


# machine precision

```

*** =solution
```{r}
# assign value
foo <- 0.3/3

# printed as "0.1"
foo

# foo is not equal to "0.1"
foo - 0.1

# foo is not equal to "0.1"
foo == 0.1

# print with 10 digit precision
format(foo, digits=10)

# print with 16 digit precision
format(foo, digits=16)

# foo is equal to "0.1" within machine precision
all.equal(foo, 0.1)

# assign by deduct
foo <- (3-2.9)

# print with 20 digit precision
format(foo, digits=20)

# machine precision
.Machine$double.eps
```

*** =sct
```{r}
test_error()
success_msg("Mind Blown! 0 is actually not 0!")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:d4ddcf9a7d
## Floating Point Calculations

Calculations with floating point numbers are subject to numerical error (they’re not perfectly accurate).

Rounding a number means replacing it with the closest number of a given precision.

The IEC 60559 convention is to round to the nearest even number (1.5 to 2, and also 2.5 to 2), which preserves the mean of a sequence,

The function `round()` rounds a number to the specified number of decimal places,

Truncating a number means replacing it with the largest integer which is less than the given number, The function `trunc()` truncates a number,

The function `ceiling()` returns the smallest integer which is greater than the given number

*** =instructions
- Deal with number precision and calculate floating point numbers.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# assign variable


# printed as "2"


# foo^2 is not equal to "2"


# print with 20 digit precision


# foo^2 is equal to "2" within machine precision


# numbers with precision 0.1


# round to precision 0.1


# round to precision 1.0


# round to nearest even number


# round to nearest even number


# truncate

```

*** =solution
```{r}
# assign variable
foo <- sqrt(2)

# printed as "2"
foo^2

# foo^2 is not equal to "2"
foo^2 == 2

# print with 20 digit precision
format(foo^2, digits=20)

# foo^2 is equal to "2" within machine precision
all.equal(foo^2, 2)

# numbers with precision 0.1
0.1*(1:10)

# round to precision 0.1
round(3.675, 1)

# round to precision 1.0
round(3.675)

# round to nearest even number
c(round(2.5), round(3.5), round(4.5))

# round to nearest even number
round(4:20/2)

# truncate
trunc(3.675)
```

*** =sct
```{r}
test_error()
success_msg("Now you don't worry that much about precision!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:c8f389fdbd
## Modular Arithmetic Operators

R has two modular arithmetic operators:
`%/%` performs modulo division,
`%%` calculates remainder of modulo division.


Modulo division of floating point (non-integer) numbers sometimes produces incorrect results because of limited machine precision of floating point numbers.


For example, the number 0.2 is stored as a binary number slightly larger than 0.2, so the result of calculating 0.6 %/% 0.2 is 2 instead of 3

*** =instructions
- Learn the differences between modulo division and traditional division.

*** =hint
Follow the instruction and introduction. Be careful to the modulo operators.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# modulo division


# remainder of modulo division


# reversing modulo division usually returns the original number


# modulo division of non-integer numbers can produce incorrect results


# use integers to get correct result


# 0.2 stored as binary number slightly larger than 0.2

```

*** =solution
```{r}
# modulo division
4.7 %/% 0.5

# remainder of modulo division
4.7 %% 0.5

# reversing modulo division usually returns the original number
(4.7 %% 0.5) + 0.5 * (4.7 %/% 0.5)

# modulo division of non-integer numbers can produce incorrect results
0.6 %/% 0.2  # produces 2 instead of 3

# use integers to get correct result
6 %/% 2

# 0.2 stored as binary number slightly larger than 0.2
format(0.2, digits=22)
```

*** =sct
```{r}
success_msg("Miracle again!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:944a839cd1
## Determining the Memory Usage of R Objects

The function object.size() displays the amount of memory (in bytes) allocated to R objects,


The generic function format() formats R objects for printing and display,


The method format.object size() defines a megabyte as 1,048,576 bytes (220), not 1,000,000 bytes,


The function `get()` accepts a character string and returns the value of the corresponding object in a specified environment,


`get()` retrieves objects that are referenced using
character strings, instead of their names,


The function `mget()` accepts a vector of strings and returns a list of the corresponding objects,


The function `ll()` from package gdata displays the amount of memory (in bytes) allocated to R objects


*** =instructions
- Measure size of object in your environment.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
big_obj <- matrix(1:1e6, ncol = 1e3)
foo <- sqrt(2)
```

*** =sample_code
```{r}
# get size of an object


# get size in MB



# get sizes of objects in workspace


# get sizes of objects in workspace


# change to display in KB


# get sizes of objects in env_etf environment

# get sizes of objects in env_etf environment


# get total size of all objects in workspace

```

*** =solution
```{r}
# get size of an object
object.size(runif(1e6))

# get size in MB
format(object.size(runif(1e6)), units="MB")


# get sizes of objects in workspace
sort(sapply(ls(),
  function(ob_ject) {
    format(object.size(get(ob_ject)), units="KB")}))

# get sizes of objects in workspace
sort(sapply(mget(ls()), object.size))

# change to display in KB
sort(sapply(mget(ls()),
function(ob_ject) {
  format(object.size(ob_ject), units="KB")}
))

# get sizes of objects in env_etf environment
sort(sapply(ls(env_etf),
  function(ob_ject) {
    object.size(get(ob_ject, env_etf))}))

# get sizes of objects in env_etf environment
sort(sapply(mget(ls(env_etf), env_etf),
      object.size))

# get total size of all objects in workspace
format(object.size(x=mget(ls())), units="MB")
```

*** =sct
```{r}
success_msg("Know your objects helps you manage your memory.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:f09c0189ac
## Date Object

R has a Date class for date objects (but without time). The function `as.Date()` parses a character string into a date object.

R stores Date objects as the number of days since the epoch (January 1, 1970), The function `difftime()` calculates the difference between Date objects, and returns a time interval object of class difftime.

The "+" and "-" arithmetic operators and the "<" and ">" logical comparison operators are overloaded to allow these operations directly on Date objects, numeric year-fraction dates can be coerced to Date objects using the functions `attributes()` and `structure()`.

*** =instructions
- Construct and convert date objects.

*** =hint
Recall previous exercises. Date objects can be constructed explicitly and implicitly.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# get today's date


# "%Y-%m-%d" or "%Y/%m/%d"


# print the object


# Date object class


# specify format


# add 20 days


# extract internal representation to integer


# convert string to date


# print the result


# difference between dates


# get day of the week


# coerce numeric into date-times


# change attributes to create date object


# "Date" object


# "Date" object with structure()

```

*** =solution
```{r}
# get today's date
Sys.Date()

# "%Y-%m-%d" or "%Y/%m/%d"
date_time <- as.Date("2014-07-14")

# print the object
date_time

# Date object class
class(date_time)

# specify format
as.Date("07-14-2014", "%m-%d-%Y")

# add 20 days
date_time + 20

# extract internal representation to integer
as.numeric(date_time)

# convert string to date
date_old <- as.Date("07/14/2013", "%m/%d/%Y")

# print the result
date_old

# difference between dates
difftime(date_time, date_old, units="weeks")

# get day of the week
weekdays(date_time)

# coerce numeric into date-times
date_time <- 0

# change attributes to create date object
attributes(date_time) <- list(class="Date")

# "Date" object
date_time

# "Date" object with structure()
structure(0, class="Date")
```

*** =sct
```{r}
success_msg("Great job!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7090dc3538
## POSIXct Date-time Objects

The POSIXct class in R represente date-time objects, that can store both the date and time,


The clock time is the time (number of hours, minutes and seconds) in the local time zone,

The moment of time is the clock time in the UTC time zone, POSIXct objects are stored as the number of seconds that have elapsed since the epoch (January 1, 1970) in the UTC time zone,

POSIXct objects are stored as the moment of time, but are printed out as the clock time in the local time zone, A clock time together with a time zone uniquely specifies a moment of time,

The function `as.POSIXct()` can parse a character string (representing the clock time) and a time zone into a POSIXct object

*** =instructions
- Explore the POSIXct object attributes and functionalities.

*** =hint
Follow the instruction and introduction!

*** =pre_exercise_code
```{r}
# no pec
split_cars <- split(mtcars, mtcars$cyl)
```

*** =sample_code
```{r}
# get today's date and time


# print the object


# POSIXct object


# POSIXct stored as integer moment of time


# parse character string "%Y-%m-%d %H:%M:%S" to POSIXct object


# change time zones to eastern time


# change time zone to UTC


# format argument allows parsing different date-time string formats

```

*** =solution
```{r}
# get today's date and time
date_time <- Sys.time()

# print the object
date_time

# POSIXct object
class(date_time)

# POSIXct stored as integer moment of time
as.numeric(date_time)

# parse character string "%Y-%m-%d %H:%M:%S" to POSIXct object
date_time <- as.POSIXct("2014-07-14 13:30:10")

# change time zones to eastern time
as.POSIXct("2014-07-14 13:30:10", tz="America/New_York")

# change time zone to UTC
as.POSIXct("2014-07-14 13:30:10", tz="UTC")

# format argument allows parsing different date-time string formats
as.POSIXct("07/14/2014 13:30:10", format="%m/%d/%Y %H:%M:%S",
     tz="America/New_York")
```

*** =sct
```{r}
success_msg("POSIXct is a more precise format of date-time.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:a80ae7fbe8
## Operations on POSIXct Objects

The "+" and "-" arithmetic operators are overloaded to allow addition and subtraction operations on POSIXct objects.

The "<" and ">" logical comparison operators are also overloaded to allow direct comparisons between POSIXct objects.

Operations on POSIXct objects are equivalent to the same operations on the internal integer representation of POSIXct (number of seconds since the
epoch).

Subtracting POSIXct objects creates a time interval object of class difftime.

The method `seq.POSIXt` creates a vector of POSIXct date-times

*** =instructions
- Test ordinary operations on POSIXct objects and learn their attributes.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# same moment of time in eastern time


# same moment of time in UTC


# add five hours to POSIXct


# subtract POSIXct


# class of difference


# compare POSIXct


# create vector of POSIXct times during trading hours


# get first 3 elements


# get last 3 elements

```

*** =solution
```{r}
# same moment of time in eastern time
time_ny <- as.POSIXct("2014-07-14 13:30:10", tz="America/New_York")

# same moment of time in UTC
time_ldn <- as.POSIXct("2014-07-14 13:30:10", tz="UTC")

# add five hours to POSIXct
time_ny + 5*60*60

# subtract POSIXct
time_ny - time_ldn

# class of difference
class(time_ny - time_ldn)

# compare POSIXct
time_ny > time_ldn

# create vector of POSIXct times during trading hours
trading_times <- seq(
  from=as.POSIXct("2014-07-14 09:30:00", tz="America/New_York"),
  to=as.POSIXct("2014-07-14 16:00:00", tz="America/New_York"),
  by="10 min")

# get first 3 elements
head(trading_times, 3)

# get last 3 elements
tail(trading_times, 3)
```

*** =sct
```{r}
success_msg("They can be liken to integers!")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:b6125af738
## Moment of Time and Clock Time

`as.POSIXct()` can also coerce integer objects into POSIXct, given an origin in time.

The same moment of time corresponds to different clock times in different time zones.

The same clock times in different time zones correspond to different moments of time.

*** =instructions
- Explore moments of POSIXct objects.

*** =hint
Follow the instruction and introductions. 

*** =pre_exercise_code
```{r}
date_time <- Sys.time()
```

*** =sample_code
```{r}
# POSIXct is stored as integer moment of time


# same moment of time of eastern time


# same moment of time of UTC time


# same clock time of eastern time

  
# same clock time of time of UTC time


# add 20 seconds to POSIXct


# print the date time

```

*** =solution
```{r}
# POSIXct is stored as integer moment of time
int_time <- as.numeric(date_time)

# same moment of time of eastern time
as.POSIXct(int_time, origin="1970-01-01", tz="America/New_York")

# same moment of time of UTC time
as.POSIXct(int_time, origin="1970-01-01", tz="UTC")

# same clock time of eastern time
as.POSIXct("2014-07-14 13:30:10", tz="America/New_York")
  
# same clock time of time of UTC time
as.POSIXct("2014-07-14 13:30:10", tz="UTC")

# add 20 seconds to POSIXct
date_time + 20

# print the date time
date_time
```

*** =sct
```{r}
success_msg("POSIXct date adds up by seconds!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7aa0a94261
## Methods for Manipulating POSIXct Objects

The generic function `format()` formats R objects for printing and display. The method `format.POSIXct()` parses POSIXct objects into a character string representing the clock time in a given time zone,

The method `as.POSIXct.Date()` parses Date objects into POSIXct, and assigns to them the moment of time corresponding to midnight UTC, POSIX is an acronym for ”Portable Operating System Interface”


*** =instructions
- Learn to use functions to manipulate POSIXct objects.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
date_time <- Sys.time()
```

*** =sample_code
```{r}
# parse POSIXct to string representing the clock time


# character string


# get clock times in east coast


# get clock times in London


# format to month-date


# format to hours


# trunc to hour


# Date converted to midnight UTC moment of time

```

*** =solution
```{r}
# parse POSIXct to string representing the clock time
format(date_time)

# character string
class(format(date_time))

# get clock times in east coast
format(date_time, tz="America/New_York")

# get clock times in London
format(date_time, tz="UTC")

# format to month-date
format(date_time, "%m/%Y")

# format to hours
format(date_time, "%m-%d-%Y %H hours")

# trunc to hour
format(date_time, "%m-%d-%Y %H:00:00")

# Date converted to midnight UTC moment of time
as.POSIXct(as.numeric(as.POSIXct(Sys.Date())),
     origin="1970-01-01",
     tz="UTC")
```

*** =sct
```{r}
success_msg("The POSIXct object becomes handy now!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:d6245c1bb1
## POSIXlt Date-time Objects

The POSIXlt class in R represents date-time objects, that are stored internally as a list, The function `as.POSIXlt()` can parse a character string (representing the clock time) and a time zone into a POSIXlt object.


The method `format.POSIXlt()` parses POSIXlt objects into a character string representing the clock time in a given time zone, The function as.POSIXlt() can also parse a POSIXct object into a POSIXlt object, and `as.POSIXct()` can perform the reverse,


Adding a number to POSIXlt causes implicit coercion to POSIXct, POSIXct and POSIXlt are two derived classes from the POSIXt class, The methods `round.POSIXt()` and `trunc.POSIXt()` round and truncate POSIXt objects, and return POSIXlt

*** =instructions
- Manipulate POSIXct object in a manner similar to floating point numbers

*** =hint
Similar-named functions provide similar functionalities.


*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# parse character string "%Y-%m-%d %H:%M:%S" to POSIXlt object


# print object


# print class


# coerce to POSIXct object


# extract internal list representation to vector


# add 20 seconds


# implicit coercion to POSIXct


# truncate to closest hour


# truncate to closest day


# trunc methods


# look at function structure

```

*** =solution
```{r}
# parse character string "%Y-%m-%d %H:%M:%S" to POSIXlt object
date_time <- as.POSIXlt("2014-07-14 18:30:10")

# print object
date_time

# print class
class(date_time)

# coerce to POSIXct object
as.POSIXct(date_time)

# extract internal list representation to vector
unlist(date_time)

# add 20 seconds
date_time + 20

# implicit coercion to POSIXct
class(date_time + 20)

# truncate to closest hour
trunc(date_time, units="hours")

# truncate to closest day
trunc(date_time, units="days")

# trunc methods
methods(trunc)

# look at function structure
trunc.POSIXt
```

*** =sct
```{r}
success_msg("Nice work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:c1a08e245c
## Time Zones and Date-time Conversion

date-time objects require a time zone to be uniquely specified, UTC stands for ”Universal Time Coordinated”, and is synonymous with GMT, but doesn’t change with Daylight Saving Time, EST stands for ”Eastern Standard Time”, and is UTC - 5 hours, EDT stands for ”Eastern Daylight Time”, and is UTC - 4 hours, 

The function `Sys.setenv()` can be used to set the default time zone, butthe environment variable "TZ" must be capitalized


*** =instructions
- Alter time zone attribute for POSIXct object.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# get time-zone


# set time-zone to UTC


# get time-zone


# Standard Time in effect


# Daylight Savings Time in effect


# today's date and time


# convert to character in different TZ


# parse back to POSIXct


# difference between New_York time and UTC


# set time-zone to New York

```

*** =solution
```{r}
# get time-zone
Sys.timezone()

# set time-zone to UTC
Sys.setenv(TZ="UTC")

# get time-zone
Sys.timezone()


# Standard Time in effect
as.POSIXct("2013-03-09 11:00:00", tz="America/New_York")

# Daylight Savings Time in effect
as.POSIXct("2013-03-10 11:00:00", tz="America/New_York")

# today's date and time
date_time <- Sys.time()

# convert to character in different TZ
format(date_time, tz="UTC")

# parse back to POSIXct
as.POSIXct(format(date_time, tz="America/New_York"))

# difference between New_York time and UTC
as.POSIXct(format(Sys.time(), tz="UTC")) -
  as.POSIXct(format(Sys.time(), tz="America/New_York"))

# set time-zone to New York
Sys.setenv(TZ="America/New_York")
```

*** =sct
```{r}
success_msg("POSIXct value do differ due to time zone!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e9ca3eeb99
## Manipulating Date-time Objects Using lubridate

The package lubridate contains functions for manipulating POSIXct date-time objects,

The `ymd()`, `dmy()`, etc. functions parse character and numeric year-fraction dates into POSIXct objects,

The `mday()`, `month()`, `year()`, etc. accessor functions extract date-time components,

The function decimal `date()` converts POSIXct objects into numeric year-fraction dates,

The function date `decimal()` converts numeric year-fraction dates into POSIXct objects

*** =instructions
- Utilize lubridate package to expedite your date-time operations

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# load lubridate


# parse strings into date-times


# construct date time object


# print object


# POSIXct object class


# construct by different format


# parse numeric into date-times


# use methods in lubridate package


# parse decimal to date-times


# parse decimal to date-times of a year


# parse back

```

*** =solution
```{r}
# load lubridate
library(lubridate)

# parse strings into date-times
as.POSIXct("07-14-2014", format="%m-%d-%Y", tz="America/New_York")

# construct date time object
date_time <- mdy("07-14-2014", tz="America/New_York")

# print object
date_time

# POSIXct object class
class(date_time)

# construct by different format
dmy("14.07.2014", tz="America/New_York")

# parse numeric into date-times
as.POSIXct(as.character(14072014), format="%d%m%Y",
                  tz="America/New_York")

# use methods in lubridate package
dmy(14072014, tz="America/New_York")

# parse decimal to date-times
decimal_date(date_time)

# parse decimal to date-times of a year
date_decimal(2014.25, tz="America/New_York")

# parse back
date_decimal(decimal_date(date_time), tz="America/New_York")
```

*** =sct
```{r}
success_msg("Good one!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:8e5ade7078
## Time Zones Using lubridate

lubridate simplifies time zone calculations, lubridate uses the UTC time zone as default.

The function with `tz()` creates a date-time object with the same moment of time in a different time zone.

The function force `tz()` creates a date-time object with the same clock time in a different time zone.

*** =instructions
- Add or force a time zone attributes to date-time objects.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec

```

*** =sample_code
```{r}
# load lubridate


# create date-time


# print


# get moment of time in "UTC" time zone


# get the same moment of time in "UTC" time zone


# get clock time in "UTC" time zone


# get clock time in "UTC" time zone


# same moment of time


# different moments of time

```

*** =solution
```{r}
# load lubridate
library(lubridate)

# create date-time
date_time <- ymd_hms(20140714142010,
               tz="America/New_York")

# print
date_time

# get moment of time in "UTC" time zone
with_tz(date_time, "UTC")

# get the same moment of time in "UTC" time zone
as.POSIXct(format(date_time, tz="UTC"), tz="UTC")

# get clock time in "UTC" time zone
force_tz(date_time, "UTC")

# get clock time in "UTC" time zone
as.POSIXct(format(date_time, tz="America/New_York"),
     tz="UTC")

# same moment of time
date_time - with_tz(date_time, "UTC")

# different moments of time
date_time - force_tz(date_time, "UTC")
```

*** =sct
```{r}
success_msg("Great!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:ec87541ef1
## lubridate Time Span Objects

lubridate has two time span classes: 
durations and periods,
durations specify exact time spans, such as numbers of seconds, hours,
days, etc.

The functions `ddays()`, `dyears()`, etc. return duration objects, periods specify relative time spans

that don’t have a fixed length, such as months, years, etc. periods account for variable days in the months, for Daylight Savings

Time, and for leap years, The functions `days()`, `months()`, `years()`, etc. return period objects.

periods allow calculating future dates with the same day of the month, or month of the year.


*** =instructions
- Add or subtract time span from date-time objects.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# load lubridate


# Daylight Savings Time handling periods vs durations


# print date-time


# add duration


# add period


# leap year


# create date-time object with time zone


# print objects


# add duration


# add period


# create date-time objects


# print date-time 


# add periods to a date-time


# create vectors of dates


# monthly dates


# add a vector of months


# bi-monthly dates


# add a vector of months


# create a sequence of dates

```

*** =solution
```{r}
# load lubridate
library(lubridate)

# Daylight Savings Time handling periods vs durations
date_time <- as.POSIXct("2013-03-09 11:00:00",
                  tz="America/New_York")

# print date-time
date_time

# add duration
date_time + ddays(1)

# add period
date_time + days(1)

# leap year
leap_year(2012)

# create date-time object with time zone
date_time <- dmy(01012012, tz="America/New_York")

# print objects
date_time

# add duration
date_time + dyears(1)

# add period
date_time + years(1)

# create date-time objects
date_time <- ymd_hms(20140714142010, tz="America/New_York")

# print date-time 
date_time

# add periods to a date-time
c(date_time + seconds(1), date_time + minutes(1),
date_time + days(1), date_time + months(1))

# create vectors of dates
date_time <- ymd(20140714, tz="America/New_York")

# monthly dates
date_time + 0:2 * months(1)

# add a vector of months
date_time + months(0:2)

# bi-monthly dates
date_time + 0:2 * months(2)

# add a vector of months
date_time + seq(0, 5, by=2) * months(1)

# create a sequence of dates
seq(date_time, length=3, by="2 months")
```

*** =sct
```{r}
success_msg("Feels like simple calculation!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:3d8a9618b9
## End-of-month Dates

Adding monthly periods can create invalid dates,


The operators %m+% and %m-% add or subtract monthly periods to account for the varible number of days per month,


This allows creating vectors of end-of-month dates.

*** =instructions
- Get the end date of each month.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
library(lubridate)
```

*** =sample_code
```{r}
# adding monthly periods can create invalid dates


# get dates of 0, 1, 2 months later


# get date one month later


# get date two months later


# create vector of end-of-month dates

```

*** =solution
```{r}
# adding monthly periods can create invalid dates
date_time <- ymd(20120131, tz="America/New_York")

# get dates of 0, 1, 2 months later
date_time + 0:2 * months(1)

# get date one month later
date_time + months(1)

# get date two months later
date_time + months(2)

# create vector of end-of-month dates
date_time %m-% months(13:1)
```

*** =sct
```{r}
success_msg("Smart enough to help you find the last day of each month!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:7b69825576
## RQuantLib Calendar Functions

The package RQuantLib contains a large library of functions for pricing fixed-income instruments and options, and for risk management calculations,


The package RQuantLib contains calendar functions for determining holidays and business days in many different jurisdictions.

*** =instructions
- Utilize vectorized operations.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
library(zoo)  # load zoo
```

*** =sample_code
```{r}
# load RQuantLib


# create daily date series of class 'Date'


# print date index


# create Boolean vector of business days


# create daily series of business days


# print business day

```

*** =solution
```{r}
# load RQuantLib
library(RQuantLib)

# create daily date series of class 'Date'
in_dex <- Sys.Date() + -5:2

# print date index
in_dex

# create Boolean vector of business days
is_busday <- isBusinessDay(
  calendar="UnitedStates/GovernmentBond", in_dex)

# create daily series of business days
bus_index <- in_dex[is_busday]

# print business day
bus_index
```

*** =sct
```{r}
success_msg("Clever date get even cleverer! It's very useful for determining trading days")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:cd816481aa
## Review of Date-time Classes in R

The Date class from the base package is suitable for daily time series,


The POSIXct class from the base package is suitable for intra-day time series,


The yearmon and yearqtr classes from the zoo package are suitable for quarterly and monthly time series


*** =instructions
- Review all you've learnt about date-time objects.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
library(zoo)
```

*** =sample_code
```{r}
# create date series of class 'Date'


# daily series over one year


# print first few dates


# print first few dates


# create daily date-time series of class 'POSIXct'


# print first few dates


# print first few dates


# create series of monthly dates of class 'zoo'


# print first few dates


# create series of quarterly dates of class 'zoo'


# print first few dates


# parse quarterly 'zoo' dates to POSIXct


# convert to index

```

*** =solution
```{r}
# create date series of class 'Date'
date_time <- Sys.Date()

# daily series over one year
in_dex <- date_time + 0:365

# print first few dates
head(in_dex, 4)

# print first few dates
format(head(in_dex, 4), "%m/%d/%Y")

# create daily date-time series of class 'POSIXct'
in_dex <- seq(Sys.time(), by="days", length.out=365)

# print first few dates
head(in_dex, 4)

# print first few dates
format(head(in_dex, 4), "%m/%d/%Y %H:%M:%S")

# create series of monthly dates of class 'zoo'
monthly_index <- yearmon(2010+0:36/12)

# print first few dates
head(monthly_index, 4)

# create series of quarterly dates of class 'zoo'
qrtly_index <- yearqtr(2010+0:16/4)

# print first few dates
head(qrtly_index, 4)

# parse quarterly 'zoo' dates to POSIXct
Sys.setenv(TZ="UTC")

# convert to index
as.POSIXct(head(qrtly_index, 4))
```

*** =sct
```{r}
success_msg("You've quite learnt a lot!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:d8823d128f
## EuStockMarkets Data

R includes a number of base packages that are already installed and loaded, datasets is a base package containing various datasets, for example: EuStockMarkets,

The EuStockMarkets dataset contains daily closing prices of european stock indices

*** =instructions
- Explore the EuStockMarkets data.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# multiple ts object


# get dimension info


# get first three rows


# EuStockMarkets index is equally spaced


# plot all the columns


# add title

```

*** =solution
```{r}
# multiple ts object
class(EuStockMarkets)

# get dimension info
dim(EuStockMarkets)

# get first three rows
head(EuStockMarkets, 3)

# EuStockMarkets index is equally spaced
diff(tail(time(EuStockMarkets), 4))

# plot all the columns
plot(EuStockMarkets, main="", xlab="")

# add title
title(main="EuStockMarkets", line=-2)
```

*** =sct
```{r}
success_msg("This is an pretty interesting and real-life dataset you can work on.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:737ea4a5e4
## Boxplots

A Box Plot (box-and-whisker plot) is a graphical display of a distribution of values,


The box represents the upper and lower quartiles, the vertical lines (whiskers) represent values beyond the quartiles, and open circles represent values beyond the nominal range (outliers)


The function boxplot() plots a box-and-whisker plot for a distribution of values, `boxplot()` has two methods: one for formula objects (involving categorical variables), and another for data frames

*** =instructions
- Use boxplot to feature data distributions.

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
# boxplot method for formula in cars dataset


# calculate EuStockMarkets percentage returns


# boxplot method for data frame

```

*** =solution
```{r}
# boxplot method for formula
boxplot(formula=mpg ~ cyl, data=mtcars,
  main="Mileage by number of cylinders",
  xlab="Cylinders", ylab="Miles per gallon")

# calculate EuStockMarkets percentage returns
eu_rets <- diff(log(EuStockMarkets))

# boxplot method for data frame
boxplot(x=eu_rets)
```

*** =sct
```{r}
success_msg("Wierd? Useful!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:530c1e1c92
## Managing NA Values

Operations on time series can produce NA values. There are two dedicated functions for managing NA values in time series: 

`na.omit()` removes observations containing NA values, 
`na.locf()` carries the last non-NA observation forward

*** =instructions
- Handle NA with given functions.

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
# create zoo time series


# add NA


# print series


# replace NA's using locf


# remove NA's using omit

```

*** =solution
```{r}
# create zoo time series
zoo_series <- zoo(sample(4),
            order.by=(Sys.Date() + 0:3))

# add NA
zoo_series[3] <- NA

# print series
zoo_series

# replace NA's using locf
na.locf(zoo_series)

# remove NA's using omit
na.omit(zoo_series)
```

*** =sct
```{r}
success_msg("Looks familiar right? Similar to an early example in previous chapters.")
```
