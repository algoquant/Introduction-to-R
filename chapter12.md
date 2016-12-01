--- 
title_meta  : Chapter 12
title       : Import and Export
description : Import external data files and export r data objects.


--- type:NormalExercise lang:r xp:100 skills:1 key:f625f0fd8d
## Writing Text Strings

The function `cat()` concatenates strings and writes them to standard output or to ﬁles, `cat()` interprets its argument character string and its escape sequences ("\"), but doesn’t return a value, The function `print()` doesn’t interpret its argument, and simply prints it to standard output and invisibly returns it, Typing the name of an object in R implicitly calls `print()` on that object, The function `save()` writes objects to a binary ﬁle


*** =instructions
- Learn to use `cat()`, `print()` and `save()` to control output and input of data.

*** =hint
Follow the instruction and introduction. 

*** =pre_exercise_code
```{r}
```

*** =sample_code

```{r}
# cat() interprets backslash escape sequences


# simply print


# assign print


# print() returns its argument


# create string
my_text <- "Title: My Text\nSome numbers: 1,2,3,...\nRprofile files contain code executed at R startup,\n"

# write to text file


# write several lines to text file


# write to binary file

```

*** =solution
```{r}
# cat() interprets backslash escape sequences
cat("Enter\ttab")

# simply print
print("Enter\ttab")

# assign print
my_text <- print("hello")

# print() returns its argument
my_text

# create string
my_text <- "Title: My Text\nSome numbers: 1,2,3,...\nRprofile files contain code executed at R startup,\n"

# write to text file
cat(my_text, file="mytext.txt")

# write several lines to text file
cat("Title: My Text",
    "Some numbers: 1,2,3,...",
    "Rprofile files contain code executed at R startup,", 
    file="mytext.txt", sep="\n")

# write to binary file
save(my_text, file="mytext.RData")
```

*** =sct
```{r}
test_error()
success_msg("Forget about your notepad and write files, interpret strings in R")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:d4ddcf9a7d
## Displaying Numeric Data

The function `print()` displays numeric data objects, with the number of digits given by the global option "digits".

The function `sprintf()` returns strings formatted from text strings and numeric data.

*** =instructions
- Display numeric objects in formats.

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
# print pi
print(pi)

# print pi to 10 digits
print(pi, digits=10)

# get system setting on digits
getOption("digits")

# construct numeric variable
foo <- 12

# construct characteristic variable
bar <- "months"

# print in format
sprintf("There are %i %s in the year", foo, bar)
```

*** =sct
```{r}
test_error()
success_msg("Quite smart, isn't it?")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:c8f389fdbd
## Reading Text from Files

The function `scan()` reads text or data from a ﬁle and returns it as a vector or a list.

The function `readLines()` reads lines of text from a connection (ﬁle or console), and returns them as a vector of character strings.

The function `readline()` reads a single line from the console, and returns it as a character string.

The function `file.show()` reads text or data from a ﬁle and displays in editor.

*** =instructions
- Explore txt reading format. 

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sample_code
```{r}
# read text from file
scan(file="mytext.txt", what=character(), sep="\n")

# read lines from file
readLines(con="mytext.txt")

# read text from console
in_put <- readline("Enter a number: ")

# get the class
class(in_put)

# coerce to numeric
in_put <- as.numeric(in_put)
```

*** =solution
```{r}
# read text from file
scan(file="mytext.txt", what=character(), sep="\n")

# read lines from file
readLines(con="mytext.txt")

# read text from console
in_put <- readline("Enter a number: ")

# get the class
class(in_put)

# coerce to numeric
in_put <- as.numeric(in_put)
```

*** =sct
```{r}
success_msg("Good job! Don't worry about the warnings")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:f09c0189ac
## Reading and Writing Data Frames from Text Files

The functions `read.table()` and `write.table()` read and write data frames from text ﬁles, `write.table()` coerces objects to data frames before it writes them, `read.table()` returns a data frame, and coerces non-numeric values to factors (unless the stringsAsFactors=FALSE option is set), `read.table()` and `write.table()` can be used to read and write matrices from text ﬁles, but they have to be coerced back to matrices, `read.table()` and `write.table()` are ineﬃcient for very large data sets.

*** =instructions
- Use standardized function to read and write txt files.

*** =hint
Follow the instruction and introductions

*** =pre_exercise_code
```{r}
data_frame <- data.frame(type=c("rose", "daisy", "tulip"), color=c("red", "white", "yellow"), price=c(1.5, 0.5, 1.0), row.names=c("flower1", "flower2", "flower3"))  # end data.frame
mat_rix <- matrix(sample(1:12), ncol=3, dimnames=list(NULL, c("col1", "col2", "col3")))
rownames(mat_rix) <- paste("row", 1:NROW(mat_rix), sep="")
```

*** =sample_code
```{r}
# write data frame to text file


# read data frame back from file


# print a data frame


# write matrix to text file


# read a matrix back


# write.table() coerced matrix to data frame


# get class of variable


# coerce from data frame back to matrix


# get class of variable

```

*** =solution
```{r}
# write data frame to text file
write.table(data_frame, file="florist.txt")

# read data frame back from file
data_read <- read.table(file="florist.txt")

# print a data frame
data_read

# write matrix to text file
write.table(mat_rix, file="matrix.txt")

# read a matrix back
mat_read <- read.table(file="matrix.txt")

# write.table() coerced matrix to data frame
mat_read

# get class of variable
class(mat_read)

# coerce from data frame back to matrix
mat_read <- as.matrix(mat_read)

# get class of variable
class(mat_read)
```

*** =sct
```{r}
success_msg("Have fun playing these data!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7090dc3538
## Copying Data Frames Between the clipboard and R

Data frames stored in the clipboard can be copied into R using the function `read.table()`.

Data frames in R can be copied into the clipboard using the function `write.table()`.

This allows convenient copying of data frames between Excel and R, Data frames can also be manipulated directly in the R spreadsheet-style data editor.

*** =instructions
- Link your R data with your clipboard.

*** =hint
Follow the instruction and introduction!

*** =pre_exercise_code

```{r}

```

*** =sample_code
```{r}
# create data frame


# write data to your clipboard


# wrapper function for copying data frame from clipboard into R
# complete the code; by default, data is tab delimited, with a header
read_clip <- function(file="clipboard", sep="\t",
              header=TRUE, ...) {
  
}

# run the function


# wrapper function for copying data frame from R into clipboard
# complete the code; by default, data is tab delimited, with a header
write_clip <- function(data, row.names=FALSE,
               col.names=TRUE, ...) {
  
}

# run the function


# launch spreadsheet-style data editor

```

*** =solution
```{r}
# create data frame
data_frame <- data.frame(small=c(3, 5), medium=c(9, 11), large=c(15, 13))

# write data to your clipboard
write.table(x=data_frame, file="clipboard", sep="\t")

# wrapper function for copying data frame from clipboard into R
# complete the code; by default, data is tab delimited, with a header
read_clip <- function(file="clipboard", sep="\t",
              header=TRUE, ...) {
  read.table(file=file, sep=sep, header=header, ...)
}

# run the function
data_frame <- read_clip()

# wrapper function for copying data frame from R into clipboard
# complete the code; by default, data is tab delimited, with a header
write_clip <- function(data, row.names=FALSE,
               col.names=TRUE, ...) {
  write.table(x=data, file="clipboard", sep="\t",
      row.names=row.names, col.names=col.names, ...)
}

# run the function
write_clip(data=data_frame)

# launch spreadsheet-style data editor
data_frame <- edit(data_frame)
```

*** =sct
```{r}
success_msg("Clipboard is your new data import tools now.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:a80ae7fbe8
## Reading and Writing Data Frames from csv Files

The functions `read.csv()` and `write.csv()` read and write data frames from csv format ﬁles.

These functions are wrappers for `read.table()` and `write.table()`, `read.csv()` coerces non-numeric values to factors, unless the `stringsAsFactors=FALSE` option is set, `read.csv()` reads row names as an extra column, unless the row.names=1 argument is used.

The argument "row.names" accepts either the number or the name of the column containing the row names.

The `*.csv()` functions are very ineﬃcient for large data sets.

The functions `read.csv()` and `write.csv()` can read and write data frames from csv format ﬁles without using row names, Row names can be omitted from the output ﬁle by calling `write.csv()` with the argument row.names=FALSE

*** =instructions
- Learn to handle csv files with related functions.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
# no
data_frame <- data.frame(small=c(3, 5), medium=c(9, 11), large=c(15, 13))
```

*** =sample_code
```{r}
# write data frame to CSV file


# write data frame for usage


# the row names are read in as extra column


# restore row names


# remove extra column


# print out data


# read row names from first column


# print out data


# read it back


# a data frame without row names

```

*** =solution
```{r}
# write data frame to CSV file
write.csv(data_frame, file="florist.csv")

# write data frame for usage
data_read <- read.csv(file="florist.csv", 
                 stringsAsFactors=FALSE)

# the row names are read in as extra column
data_read

# restore row names
rownames(data_read) <- data_read[, 1]

# remove extra column
data_read <- data_read[, -1]

# print out data
data_read

# read row names from first column
data_read <- read.csv(file="florist.csv", row.names=1)

# print out data
data_read

# write data frame to CSV file, without row names
write.csv(data_frame, row.names=FALSE, file="florist.csv")

# read it back
data_read <- read.csv(file="florist.csv")

# a data frame without row names
data_read
```

*** =sct
```{r}
success_msg("csv file is a simple and popular format of data file, widely used for various languages")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:b6125af738
## Reading and Writing Matrices from csv Files

The functions `read.csv()` and `write.csv()` can read and write matrices from csv format ﬁles.

If row names can be omitted in the output ﬁle, then `write.csv()` can be called with argument `row.names=FALSE`, If the input ﬁle doesn’t contain row names, then `read.csv()` can be called without the "row.names" argument

*** =instructions
- Input and output matrix object with csv file.

*** =hint
Follow the instruction and introductions. 

*** =pre_exercise_code
```{r}
# no
mat_rix <- matrix(sample(1:12), ncol=3, dimnames=list(NULL, c("col1", "col2", "col3")))
rownames(mat_rix) <- paste("row", 1:NROW(mat_rix), sep="")
```

*** =sample_code
```{r}
# write matrix to csv file, and then read it back


# read the matrix back


# read.csv() reads matrix as data frame


# get the class


# coerce to matrix


# compare the two


# write to csv file without rownames


# read it back


# convert to a matrix


# a matrix without row names
mat_read
```

*** =solution
```{r}
# write matrix to csv file, and then read it back
write.csv(mat_rix, file="matrix.csv")

# read the matrix back
mat_read <- read.csv(file="matrix.csv", row.names=1)

# read.csv() reads matrix as data frame
mat_read
class(mat_read)

# coerce to matrix
mat_read <- as.matrix(mat_read)

# compare the two
identical(mat_rix, mat_read)

# write to csv file without rownames
write.csv(mat_rix, row.names=FALSE, 
    file="matrix_ex_rows.csv")

# read it back
mat_read <- read.csv(file="matrix_ex_rows.csv")

# convert to a matrix
mat_read <- as.matrix(mat_read)

# a matrix without row names
mat_read
```

*** =sct
```{r}
success_msg("Great!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7aa0a94261
## Reading and Writing Matrices (cont.)

There are several ways of reading and writing matrices from csv ﬁles, with tradeoﬀs between simplicity, data size, and speed, The function `write.matrix()` writes a matrix to a text ﬁle, without its row names, `write.matrix()` is part of package MASS.

The advantage of function `scan()` is its speed, but it doesn’t handle row names easily, Removing row names simpliﬁes the reading and writing of matrices.

The function `readLines()` reads whole lines and returns them as single strings.

The function `system.time()` calculates the execution time (in seconds) used to evaluate a given expression.


*** =instructions
- Produce charts to reveal relationships between critial measures and noises.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
library(MASS)
```

*** =sample_code
```{r}
# write to CSV file by row - it's very SLOW!!!


# scan reads faster - skip first line with colnames


# read colnames


# this is a string!


# convert to char vector


# mat_read is a vector, not matrix!


# coerce by row to matrix


# restore colnames


# print the variable

```

*** =solution
```{r}
# write to CSV file by row - it's very SLOW!!!
write.matrix(mat_rix, file="matrix.csv", sep=",")

# scan reads faster - skip first line with colnames
system.time(
  mat_read <- scan(file="matrix.csv", sep=",", 
            skip=1, what=numeric()))

# read colnames
col_names <- readLines(con="matrix.csv", n=1)

# this is a string!
col_names

# convert to char vector
col_names <- strsplit(col_names, s=",")[[1]]

# mat_read is a vector, not matrix!
mat_read

# coerce by row to matrix
mat_read <- matrix(mat_read, ncol=length(col_names), 
            byrow=TRUE)

# restore colnames
colnames(mat_read) <- col_names

# print the variable
mat_read
```

*** =sct
```{r}
success_msg("New tools and new potentials!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:d6245c1bb1
## Reading Matrices Containing Bad Data

Very often data that is read from external sources contains elements with bad data, An example of bad data are character strings in numeric data.

Columns of numeric data that contain strings are coerced to character or factor, when they’re read by `read.csv()`, `as.numeric()` coerces strings that don’t represent numbers into NA values.

*** =instructions
- Deal with strings in numeric columns when importing data. The file name is "matrix_bad.csv"

*** =hint
Follow the instructions and introductions.


*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# read data from a csv file, including row names


# print matrix


# class of matrix


# columns with bad data are character or factor


# copy row names


# sapply loop over columns and coerce to numeric


# restore row names


# replace NAs with zero


# matrix without NAs

```

*** =solution
```{r}
# read data from a csv file, including row names
mat_rix <- read.csv(file="matrix_bad.csv", row.names=1,
               stringsAsFactors=FALSE)

# print matrix
mat_rix

# class of matrix
class(mat_rix)

# columns with bad data are character or factor
sapply(mat_rix, class)

# copy row names
row_names <- row.names(mat_rix)

# sapply loop over columns and coerce to numeric
mat_rix <- sapply(mat_rix, as.numeric)

# restore row names
row.names(mat_rix) <- row_names

# replace NAs with zero
mat_rix[is.na(mat_rix)] <- 0

# matrix without NAs
mat_rix
```

*** =sct
```{r}
success_msg("Looks better, right?")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:c1a08e245c
## Reading and Writing zoo Series From Text Files

The package zoo contains functions `read.zoo()` and `write.zoo()` for reading and writing zoo objects from text and csv ﬁles, `read.zoo()` and `write.zoo()` are wrappers for `read.table()` and `write.table()`.

By default these functions read and write data in space-delimited format, but they can also read and write data to comma-delimited csv ﬁles by passing the parameter sep=",".

*** =instructions
- Read and write zoo objects. "zoo" package is already loaded to your environment.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
set.seed(1121)  # reset random number generator
library(zoo)  # load package zoo
```

*** =sample_code
```{r}
# create index of dates


# create zoo with Date index


# create tail 


# write zoo to text file, and then read it back


# read it back


# get some last elements

```

*** =solution
```{r}
# create index of dates
in_dex <- seq(from=as.Date("2013-06-15"), 
            by="day", length.out=100)

# create zoo with Date index
zoo_series <- zoo(cumsum(rnorm(length(in_dex))), 
            order.by=in_dex)

# create tail 
tail(zoo_series, 3)

# write zoo to text file, and then read it back
write.zoo(zoo_series, file="zoo_series.txt")

# read it back
zoo_series <- read.zoo("zoo_series.txt")

# get some last elements
tail(zoo_series, 3)
```

*** =sct
```{r}
success_msg("Beautiful!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e9ca3eeb99
## Reading and Writing zoo Series With Date-time Index

If the index of a zoo series is a date-time, then `write.zoo()` writes the date and time ﬁelds as separate columns with a space between them.

To properly read separate date and time columns from text ﬁles, `read.zoo()` must be passed arguments "index.column=list(1,2)" and "tz".

*** =instructions
- Index your zoo object with data-time.

*** =hint
Follow the instruction and introductions. Remember to load "lmtest" package.

*** =pre_exercise_code
```{r}
set.seed(1211)
library(zoo)
```

*** =sample_code
```{r}
# create data time index


# create zoo with POSIXct date-time index


# get the last 3 rows


# write zoo to text file, and then read it back


# read it back


# time field was read as a separate column


# read and specify that second column is time field


# get last 3 rows

```

*** =solution
```{r}
# create data time index
in_dex <- seq(from=as.POSIXct("2013-06-15"), 
            by="hour", length.out=1000)

# create zoo with POSIXct date-time index
zoo_series <- zoo(cumsum(rnorm(length(in_dex))), 
            order.by=in_dex)

# get the last 3 rows
tail(zoo_series, 3)

# write zoo to text file, and then read it back
write.zoo(zoo_series, file="zoo_series.txt")

# read it back
zoo_series <- read.zoo("zoo_series.txt")

# time field was read as a separate column
tail(zoo_series, 3)

# read and specify that second column is time field
zoo_series <- read.zoo(file="zoo_series.txt", 
                 index.column=list(1,2), 
                 tz="America/New_York")

# get last 3 rows
tail(zoo_series, 3)
```

*** =sct
```{r}
success_msg("Feels more ordered now!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:8e5ade7078
## Reading and Writing zoo Series From csv Files

Very often csv ﬁles contain custom date-time formats, which need to be passed as parameters into `read.zoo()` for proper formatting.

The "FUN" argument of `read.zoo()` accepts a function for coercing columns of the input data into a date-time object suitable for the zoo index.

*** =instructions
- Deal the zoo object with csv format.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
library(zoo)
set.seed(1211)
in_dex <- seq(from=as.POSIXct("2013-06-15"), 
            by="hour", length.out=1000)
zoo_series <- zoo(cumsum(rnorm(length(in_dex))), 
            order.by=in_dex)
```

*** =sample_code
```{r}
# write zoo to CSV file


# change code to read the data back
zoo_series <- read.zoo(file=?, 
            header=?, sep=?, FUN=?,
            tz="?")

# get last 3 rows
tail(zoo_series, 3)

# read zoo from CSV file, with custom date-time format


# date-time format mm/dd/yyyy hh:mm


# read zoo series


# get last 3 rows

```

*** =solution
```{r}
# write zoo to CSV file
write.zoo(zoo_series, file="zoo_series.csv", sep=",")

# change code to read the data back
zoo_series <- read.zoo(file="zoo_series.csv", 
            header=TRUE, sep=",", FUN=as.POSIXct,
            tz="America/New_York")

# get last 3 rows
tail(zoo_series, 3)

# read zoo from CSV file, with custom date-time format
zoo_frame <- read.table(file="zoo_series2.csv", sep=",")

# date-time format mm/dd/yyyy hh:mm
tail(zoo_frame, 3)

# read zoo series
zoo_series <- read.zoo(file="zoo_series2.csv", 
            header=TRUE, sep=",", FUN=as.POSIXct, 
            tz="America/New_York",
            format="%m/%d/%Y %H:%M")

# get last 3 rows
tail(zoo_series, 3)
```

*** =sct
```{r}
success_msg("Works fine!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:ec87541ef1
## Passing Arguments to the save() Function

The function `save()` writes objects to a binary ﬁle, Object names can be passed into `save()` either through the "..." argument, or the "list" argument, Objects passed through the "..." argument are not evaluated, so they must be either object names or character strings, Object names aren’t surrounded by quotes "", while character strings that represent object names are surrounded by quotes "", Objects passed through the "list" argument are evaluated, so they may be variables containing character strings.


*** =instructions
- Save objects in current environment using `save()`.

*** =hint
Follow the instruction and introduction.

*** =pre_exercise_code
```{r}
set.seed(1121)

```

*** =sample_code
```{r}
# create objects


# another object


# list all objects


# list first object


# list arguments of save function


# save "var1" to a binary file using string argument


# save "var1" to a binary file using object name


# save multiple objects


# save first object in list by passing to "list" argument


# save whole list by passing it to the "list" argument

```

*** =solution
```{r}
# create objects
var1 <- 1

# another object
var2 <- 2

# list all objects
ls()

# list first object
ls()[1]

# list arguments of save function
args(save)

# save "var1" to a binary file using string argument
save("var1", file="my_data.RData")

# save "var1" to a binary file using object name
save(var1, file="my_data.RData")

# save multiple objects
save(var1, var2, file="my_data.RData")

# save first object in list by passing to "list" argument
save(list=ls()[1], file="my_data.RData")

# save whole list by passing it to the "list" argument
save(list=ls(), file="my_data.RData")
```

*** =sct
```{r}
success_msg("Wonderful!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:3d8a9618b9
## Reading and Writing Lists of Objects

The function `load()` reads data from *.RData ﬁles, and invisibly returns a vector of names of objects created in the workspace.

The vector of names can be used to manipulate the objects in loops, or to pass them to functions.

*** =instructions
- Read and write lists of objects with `load()` and other functions.

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec
var1 <- 1
var2 <- 2
save(list=ls(), file="my_data.RData")
```

*** =sample_code
```{r}
# load objects from file


# vector of loaded objects


# list objects


# assign new values to objects in  global environment


# list objects


# assign new values to objects using for loop


# list objects


# save vector of objects


# remove only loaded objects


# remove the object "load_ed"

```

*** =solution
```{r}
# load objects from file
load_ed <- load(file="my_data.RData")

# vector of loaded objects
load_ed

# list objects
ls()

# assign new values to objects in  global environment
sapply(load_ed, function(sym_bol) {
  assign(sym_bol, runif(1), envir=globalenv())
})

# list objects
ls()

# assign new values to objects using for loop
for (sym_bol in load_ed) {
  assign(sym_bol, runif(1))
}

# list objects
ls()

# save vector of objects
save(list=load_ed, file="my_data.RData")

# remove only loaded objects
rm(list=load_ed)

# remove the object "load_ed"
rm(load_ed)
```

*** =sct
```{r}
success_msg("Whoa!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:0326283b29
## Saving Output of R to a File

The function `sink()` diverts R text output (excluding graphics) to a ﬁle, or ends the diversion.

Remember to call `sink()` to end the diversion! 

The function `pdf()` diverts graphics output to a pdf ﬁle (text output isn’t diverted), in vector graphics format.

The functions `png()`, `jpeg()`, `bmp()`, and `tiff()` divert graphics output to graphics ﬁles (text output isn’t diverted), in pixel graphics format.

The function `dev.off()` ends the diversion.

*** =instructions
- Learn to output your data in various format!

*** =hint
Follow the instruction and introductions.

*** =pre_exercise_code
```{r}
# no pec

```

*** =sample_code
```{r}
# load objects from file


# vector of loaded objects


# list objects


# assign new values to objects in  global environment


# list objects


# assign new values to objects using for loop


# list objects


# save vector of objects


# remove only loaded objects


# remove the object "load_ed"

```

*** =solution
```{r}
# redirect text output to file
sink("sinkdata.txt")

# text output
cat("Redirect text output from R\n")

# another text
print(runif(10))

# third text
cat("\nEnd data\nbye\n")

# turn redirect off
sink()

# redirect graphics to pdf file
pdf("Rgraph.pdf", width=7, height=4)


# concate text
cat("Redirect data from R into pdf file\n")

# set up variable
my_var <- seq(-2*pi, 2*pi, len=100)

# plot variable
plot(x=my_var, y=sin(my_var), main="Sine wave", 
   xlab="", ylab="", type="l", lwd=2, col="red")

# concate text
cat("\nEnd data\nbye\n")

# turn pdf output off
dev.off()

# redirect output to png file
png("Rgraph.png")

# concate text
cat("Redirect graphics from R into png file\n")

# plot variable
plot(x=my_var, y=sin(my_var), main="Sine wave", 
 xlab="", ylab="", type="l", lwd=2, col="red")

# concate text
cat("\nEnd data\nbye\n")

# turn png output off
dev.off()
```

*** =sct
```{r}
success_msg("Congrats for your skills!")
```