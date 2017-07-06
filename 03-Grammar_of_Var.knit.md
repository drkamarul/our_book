---
output:
  html_document:
    keep_md: yes
---

# Prepare folder and data

## Set the working directory

This can be done in 2 ways:

1. Using codes
2. Using point and click


To use point and click, use the down arrow button next to *More* . Then click 'Set as working directory'

# Read Data


```r
library(foreign)
data_qol<-read.dta('qol.dta',convert.factors = T)
str(data_qol)
```

```
## 'data.frame':	365 obs. of  13 variables:
##  $ id       : num  308 335 94 329 350 22 171 274 332 147 ...
##  $ sex      : Factor w/ 2 levels "female","male": 1 2 1 1 1 2 1 1 2 2 ...
##  $ age      : num  55 41 50 47 67 57 60 54 60 45 ...
##  $ tahundx  : num  14 4 5 10 13 4 4 15 13 3 ...
##  $ tx       : Factor w/ 4 levels "diet only","OHA and diet only",..: 3 4 2 4 4 2 2 2 4 2 ...
##  $ group    : Factor w/ 2 levels "\"group A\"",..: 2 2 1 2 2 1 1 1 2 1 ...
##  $ complica : Factor w/ 2 levels "no","yes": 2 1 1 2 1 2 1 1 2 1 ...
##  $ hba1c    : num  8.1 8 7.5 9.4 11.7 8.1 7.5 9.2 NA NA ...
##  $ fbs      : num  6.9 4.8 8 3.6 12.5 8.5 NA NA NA NA ...
##  $ rbs      : num  16.7 7.4 13.2 7.4 NA 7.8 9.4 7.8 NA 12.4 ...
##  $ tg_total : num  0.92 1.66 0.74 0.94 3.01 1.3 NA 1.9 NA NA ...
##  $ choleste : num  7.09 2.91 5.94 3.27 7.1 3.54 NA 5.7 NA NA ...
##  $ ADDQSCORE: num  0 -0.222 -0.333 -0.36 -0.44 ...
##  - attr(*, "datalabel")= chr ""
##  - attr(*, "time.stamp")= chr ""
##  - attr(*, "formats")= chr  "%10.0g" "%10.0g" "%10.0g" "%10.0g" ...
##  - attr(*, "types")= int  255 255 255 255 255 255 255 255 255 255 ...
##  - attr(*, "val.labels")= chr  "" "sex" "" "" ...
##  - attr(*, "var.labels")= chr  "id_no" "sex" "" "" ...
##  - attr(*, "version")= int 8
##  - attr(*, "label.table")=List of 4
##   ..$ sex     : Named int  0 1
##   .. ..- attr(*, "names")= chr  "female" "male"
##   ..$ tx      : Named int  1 2 3 4
##   .. ..- attr(*, "names")= chr  "diet only" "OHA and diet only" "insulin and diet only" "all"
##   ..$ group   : Named int  1 2
##   .. ..- attr(*, "names")= chr  "\"group A\"" "\"group B\""
##   ..$ complica: Named int  0 1
##   .. ..- attr(*, "names")= chr  "no" "yes"
```

# Browse data

1.  First few rows
2.  Last few rows


```r
head(data_qol)
```

```
##    id    sex age tahundx                    tx     group complica hba1c
## 1 308 female  55      14 insulin and diet only "group B"      yes   8.1
## 2 335   male  41       4                   all "group B"       no   8.0
## 3  94 female  50       5     OHA and diet only "group A"       no   7.5
## 4 329 female  47      10                   all "group B"      yes   9.4
## 5 350 female  67      13                   all "group B"       no  11.7
## 6  22   male  57       4     OHA and diet only "group A"      yes   8.1
##    fbs  rbs tg_total choleste  ADDQSCORE
## 1  6.9 16.7     0.92     7.09  0.0000000
## 2  4.8  7.4     1.66     2.91 -0.2222222
## 3  8.0 13.2     0.74     5.94 -0.3333333
## 4  3.6  7.4     0.94     3.27 -0.3600000
## 5 12.5   NA     3.01     7.10 -0.4400000
## 6  8.5  7.8     1.30     3.54 -0.5000000
```

```r
tail(data_qol)
```

```
##      id  sex age tahundx                tx     group complica hba1c  fbs
## 360  14 male  45      10 OHA and diet only "group A"       no   9.6 12.6
## 361 170 male  57       4 OHA and diet only "group A"       no    NA   NA
## 362 214 male  48       5 OHA and diet only "group A"       no    NA   NA
## 363 174 male  45       2 OHA and diet only "group A"       no   8.5   NA
## 364 130 male  64      16 OHA and diet only "group A"       no   6.1  3.8
## 365 219 male  46       2         diet only "group A"       no   5.9   NA
##      rbs tg_total choleste ADDQSCORE
## 360   NA       NA       NA -8.833333
## 361  9.4       NA       NA -8.833333
## 362 10.7       NA       NA -9.000000
## 363  9.6       NA       NA -9.000000
## 364  7.9       NA       NA -9.000000
## 365  6.3       NA       NA -9.000000
```

# Grammar of variables 

## Select columns

Let us create a new dataframe with only id, sex and hba1c as the variables


```r
data_qol2<-subset(data_qol, select = c('sex', 'age', 'hba1c'))
str(data_qol2)
```

```
## 'data.frame':	365 obs. of  3 variables:
##  $ sex  : Factor w/ 2 levels "female","male": 1 2 1 1 1 2 1 1 2 2 ...
##  $ age  : num  55 41 50 47 67 57 60 54 60 45 ...
##  $ hba1c: num  8.1 8 7.5 9.4 11.7 8.1 7.5 9.2 NA NA ...
```

alternatively, we can use other subsetting functions


```r
data_qol3<-data_qol[,c('sex','age','hba1c')]
str(data_qol3)
```

```
## 'data.frame':	365 obs. of  3 variables:
##  $ sex  : Factor w/ 2 levels "female","male": 1 2 1 1 1 2 1 1 2 2 ...
##  $ age  : num  55 41 50 47 67 57 60 54 60 45 ...
##  $ hba1c: num  8.1 8 7.5 9.4 11.7 8.1 7.5 9.2 NA NA ...
```

## Select rows


```r
data_qol4<-subset(data_qol, age > 30)
str(data_qol4)
```

```
## 'data.frame':	363 obs. of  13 variables:
##  $ id       : num  308 335 94 329 350 22 171 274 332 147 ...
##  $ sex      : Factor w/ 2 levels "female","male": 1 2 1 1 1 2 1 1 2 2 ...
##  $ age      : num  55 41 50 47 67 57 60 54 60 45 ...
##  $ tahundx  : num  14 4 5 10 13 4 4 15 13 3 ...
##  $ tx       : Factor w/ 4 levels "diet only","OHA and diet only",..: 3 4 2 4 4 2 2 2 4 2 ...
##  $ group    : Factor w/ 2 levels "\"group A\"",..: 2 2 1 2 2 1 1 1 2 1 ...
##  $ complica : Factor w/ 2 levels "no","yes": 2 1 1 2 1 2 1 1 2 1 ...
##  $ hba1c    : num  8.1 8 7.5 9.4 11.7 8.1 7.5 9.2 NA NA ...
##  $ fbs      : num  6.9 4.8 8 3.6 12.5 8.5 NA NA NA NA ...
##  $ rbs      : num  16.7 7.4 13.2 7.4 NA 7.8 9.4 7.8 NA 12.4 ...
##  $ tg_total : num  0.92 1.66 0.74 0.94 3.01 1.3 NA 1.9 NA NA ...
##  $ choleste : num  7.09 2.91 5.94 3.27 7.1 3.54 NA 5.7 NA NA ...
##  $ ADDQSCORE: num  0 -0.222 -0.333 -0.36 -0.44 ...
```

```r
summary(data_qol4$age)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   32.00   47.00   53.00   52.91   59.00   80.00
```

alternatively, we can use other subsetting functions


```r
data_qol5<-data_qol[data_qol$age>30,]
str(data_qol5)
```

```
## 'data.frame':	363 obs. of  13 variables:
##  $ id       : num  308 335 94 329 350 22 171 274 332 147 ...
##  $ sex      : Factor w/ 2 levels "female","male": 1 2 1 1 1 2 1 1 2 2 ...
##  $ age      : num  55 41 50 47 67 57 60 54 60 45 ...
##  $ tahundx  : num  14 4 5 10 13 4 4 15 13 3 ...
##  $ tx       : Factor w/ 4 levels "diet only","OHA and diet only",..: 3 4 2 4 4 2 2 2 4 2 ...
##  $ group    : Factor w/ 2 levels "\"group A\"",..: 2 2 1 2 2 1 1 1 2 1 ...
##  $ complica : Factor w/ 2 levels "no","yes": 2 1 1 2 1 2 1 1 2 1 ...
##  $ hba1c    : num  8.1 8 7.5 9.4 11.7 8.1 7.5 9.2 NA NA ...
##  $ fbs      : num  6.9 4.8 8 3.6 12.5 8.5 NA NA NA NA ...
##  $ rbs      : num  16.7 7.4 13.2 7.4 NA 7.8 9.4 7.8 NA 12.4 ...
##  $ tg_total : num  0.92 1.66 0.74 0.94 3.01 1.3 NA 1.9 NA NA ...
##  $ choleste : num  7.09 2.91 5.94 3.27 7.1 3.54 NA 5.7 NA NA ...
##  $ ADDQSCORE: num  0 -0.222 -0.333 -0.36 -0.44 ...
##  - attr(*, "datalabel")= chr ""
##  - attr(*, "time.stamp")= chr ""
##  - attr(*, "formats")= chr  "%10.0g" "%10.0g" "%10.0g" "%10.0g" ...
##  - attr(*, "types")= int  255 255 255 255 255 255 255 255 255 255 ...
##  - attr(*, "val.labels")= chr  "" "sex" "" "" ...
##  - attr(*, "var.labels")= chr  "id_no" "sex" "" "" ...
##  - attr(*, "version")= int 8
##  - attr(*, "label.table")=List of 4
##   ..$ sex     : Named int  0 1
##   .. ..- attr(*, "names")= chr  "female" "male"
##   ..$ tx      : Named int  1 2 3 4
##   .. ..- attr(*, "names")= chr  "diet only" "OHA and diet only" "insulin and diet only" "all"
##   ..$ group   : Named int  1 2
##   .. ..- attr(*, "names")= chr  "\"group A\"" "\"group B\""
##   ..$ complica: Named int  0 1
##   .. ..- attr(*, "names")= chr  "no" "yes"
```

```r
summary(data_qol5$age)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   32.00   47.00   53.00   52.91   59.00   80.00
```

## Select rows and columns together


```r
data_qol6<-subset(data_qol,age>30 & sex=='male', select = c(id, sex, age, group))
str(data_qol6)
```

```
## 'data.frame':	211 obs. of  4 variables:
##  $ id   : num  335 22 332 147 247 185 331 323 314 305 ...
##  $ sex  : Factor w/ 2 levels "female","male": 2 2 2 2 2 2 2 2 2 2 ...
##  $ age  : num  41 57 60 45 59 48 58 69 65 73 ...
##  $ group: Factor w/ 2 levels "\"group A\"",..: 2 1 2 1 1 1 2 2 2 2 ...
```

```r
table(data_qol6$sex)
```

```
## 
## female   male 
##      0    211
```

## Generate a new variable


```r
data_qol$age_cat<-data_qol$age
View(data_qol)
```

## Categorize into new variables

### From a numerical variable


```r
data_qol$age_cat<-cut(data_qol$age_cat,
                      breaks=c(min(data_qol$age),40,60,Inf),
                      labels=c('min-39','40-59','60-above'))
min(data_qol$age)
```

```
## [1] 21
```

```r
table(data_qol$age_cat)
```

```
## 
##   min-39    40-59 60-above 
##       32      259       73
```

```r
str(data_qol$age_cat)
```

```
##  Factor w/ 3 levels "min-39","40-59",..: 2 2 2 2 3 2 2 2 2 2 ...
```

### From a categorical variable


```r
table(data_qol$tx)
```

```
## 
##             diet only     OHA and diet only insulin and diet only 
##                    10                   238                    26 
##                   all 
##                    91
```

```r
str(data_qol$tx)
```

```
##  Factor w/ 4 levels "diet only","OHA and diet only",..: 3 4 2 4 4 2 2 2 4 2 ...
```

Create a variable with 'Diet only' vs 'Diet+Drug'. This is a little bit complicated


```r
data_qol$tx2<-data_qol$tx
str(data_qol$tx2)
```

```
##  Factor w/ 4 levels "diet only","OHA and diet only",..: 3 4 2 4 4 2 2 2 4 2 ...
```

```r
str(data_qol$tx)
```

```
##  Factor w/ 4 levels "diet only","OHA and diet only",..: 3 4 2 4 4 2 2 2 4 2 ...
```

```r
table(data_qol$tx2)
```

```
## 
##             diet only     OHA and diet only insulin and diet only 
##                    10                   238                    26 
##                   all 
##                    91
```

```r
library(plyr)
data_qol$tx2<-revalue(data_qol$tx,c('diet only'='diet', 'OHA and diet only'='med',
                                    'insulin and diet only'='med', 'all'='med'))
table(data_qol$tx2)
```

```
## 
## diet  med 
##   10  355
```


## Dealing with missing data


```r
data_qol$tx3<-data_qol$tx
str(data_qol$tx3)
```

```
##  Factor w/ 4 levels "diet only","OHA and diet only",..: 3 4 2 4 4 2 2 2 4 2 ...
```

```r
str(data_qol$tx)
```

```
##  Factor w/ 4 levels "diet only","OHA and diet only",..: 3 4 2 4 4 2 2 2 4 2 ...
```

```r
table(data_qol$tx3)
```

```
## 
##             diet only     OHA and diet only insulin and diet only 
##                    10                   238                    26 
##                   all 
##                    91
```

### Replace values with 'NA'


```r
data_qol$tx3<-revalue(data_qol$tx,c('diet only'=NA))
table(data_qol$tx3)
```

```
## 
##     OHA and diet only insulin and diet only                   all 
##                   238                    26                    91
```

```r
str(data_qol$tx3)
```

```
##  Factor w/ 3 levels "OHA and diet only",..: 2 3 1 3 3 1 1 1 3 1 ...
```

# Additional package

## Package 'dplyr'

'dplyr' package is a very useful package that encourage users to use proper verb when manipulating variables (columns) and observations (rows)

It has 9 useful functions
1.  filter()
2.  arrange()
3.  select()
4.  distinct()
5.  mutate() and transmute()
6.  summarise()
7.  sample_n() and sample_frac()

Package 'dplyr' is very useful when it is combined with another function that is 'group_by'




