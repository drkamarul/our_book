
# Introduction to R
This chapter introduces readers to the basics of working with data in R. We will start with installing R in your computer and getting familiar with RStudio interface. These will be followed by the basics of handling data in R.

## R and RStudio
### Installing R and RStudio
Install R base package: http://www.r-project.org/

Install RStudio: http://www.rstudio.com/

### Getting familiar with the interface
Consists of 4 tabs:

1. Source
2. Console
3. Environment & History
4. Misc. Most important Plots, Packages & Help
<img>

### R script
source tab

* important
* everything done here
* keep track what's going on
* not recommended to type in console

### Working with packages
what is package/library

#### Installing packages

```r
install.packages("package.name")
```

#### Loading libraries

```r
library("package.name")
```

## Working with Data
### Setting working directory
general steps

* codes
* point-and-click
<img>

### Data management
concerns reading data from data set, displaying data.

advanced, direct input in the code, esp. useful for tables.

#### Reading data set
Easiest is to read .csv file.

```r
read.csv("file.name")
```

For SPSS file, need `foreign` package

```r
library("foreign")
read.spss("file.name")
```

Can read data in table format from text file.
From text file

```r
read.table("file.name", header = TRUE)
```

#### Viewing data set
Easy, just type the name,

```r
data
```
Nicer, using `View()`

```r
View(data)
```
Important tasks

```r
dim(data)
str(data)
names(data)
```

### More about data management
* subsetting
* new variable
* recoding
* direct input for table
