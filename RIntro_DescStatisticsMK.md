---
title: "R Intro-Descriptive statistics"
output: 
  html_document: 
    keep_md: true
---





```r
#install packages if you did not install them already
#install.packages("modeest")
#install.packages("dplyr")
#install.packages("pastecs")

# Load necessary libraries
library(modeest)    # For mode calculations
library(pastecs)    # For various statistics functions
library(dplyr)      # For data manipulation and summarization
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:pastecs':
## 
##     first, last
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```
This code block loads the necessary R packages to use their functions in the script.

![]()

Basic view options

Here, you load the built-in "iris" dataset into the variable my_data. The "iris" dataset contains information about iris flowers and will be used for demonstrations.

```r
#Load the iris dataset (this dataset is built-in)
my_data <- iris
```


This code displays the first 6 rows of your dataset using the head() function. It helps you get an initial look at the data.

```r
# Display the first 6 rows of the dataset for initial exploration
head(my_data, 6)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

```r
#View(my_data)
```


## Measures of Central Tendency: Mean, median and mode

The code below calculates the mean (average) value of the "Sepal.Length" column in your dataset. The mean is a measure of central tendency that represents the average value of the variable.

```r
# Compute the mean value for sepal length
mean(my_data$Sepal.Length)
```

```
## [1] 5.843333
```


This code calculates the median value of the "Sepal.Length" column. The median is another measure of central tendency that represents the middle value when the data is sorted.

```r
#Compute the median value
median(my_data$Sepal.Length)
```

```
## [1] 5.8
```


This code calculates the mode of the "Sepal.Length" column using the modeest package. The mode is the most frequently occurring value in the dataset.

```r
# Compute the mode, using modeest: mfv!
modeest::mfv(my_data$Sepal.Length)
```

```
## [1] 5
```

## Measures of Variability: Range, min, max, quantiles, variance and standard deviation

Range: minimum & maximum: Range corresponds to biggest value minus the
smallest value. It gives you the full spread of the data.



```r
#Compute the minimum, maximum value and the range
min(my_data$Sepal.Length)
```

```
## [1] 4.3
```

```r
max(my_data$Sepal.Length)
```

```
## [1] 7.9
```

```r
range(my_data$Sepal.Length)
```

```
## [1] 4.3 7.9
```

Quartiles and quantiles 
Recall that, quartiles divide the data into 4
parts. Note that, the interquartile range (IQR) - corresponding to the
difference between the first and third quartiles - is sometimes used as
a robust alternative to the standard deviation. R function:

quantile(x, probs = seq(0, 1, 0.25))

x: numeric vector whose sample quantiles are wanted. probs: numeric
vector of probabilities with values in [0,1].

by default, you will get quartiles

```r
quantile(my_data$Sepal.Length)
```

```
##   0%  25%  50%  75% 100% 
##  4.3  5.1  5.8  6.4  7.9
```

lets compute deciles (0.1, 0.2, 0.3... 0,9)


```r
quantile(my_data$Sepal.Length, seq(0, 1, 0.1))
```

```
##   0%  10%  20%  30%  40%  50%  60%  70%  80%  90% 100% 
## 4.30 4.80 5.00 5.27 5.60 5.80 6.10 6.30 6.52 6.90 7.90
```

To compute the interquartile (IQR) range: IQR means="midspread, middle
50%"


```r
IQR(my_data$Sepal.Length)
```

```
## [1] 1.3
```

Variance and standard deviation 
The variance represents the average
squared deviation from the mean. The standard deviation is the square
root of the variance. It measures the average deviation of the values,
in the data, from the mean value.

Compute the variance


```r
var(my_data$Sepal.Length)
```

```
## [1] 0.6856935
```

Compute the standard deviation


```r
sd(my_data$Sepal.Length)
```

```
## [1] 0.8280661
```

Median absolute deviation The median absolute deviation (MAD) measures
the deviation of the values, in the data, from the median value.

Compute the median


```r
median(my_data$Sepal.Length)
```

```
## [1] 5.8
```

Compute the median absolute deviation


```r
mad(my_data$Sepal.Length)
```

```
## [1] 1.03782
```

## Computing an overall summary of a variable and an entire data frame

summary() function = Can be used for overall summary of dataframe or a
variable

Summary of a single variable.


```r
summary(my_data$Sepal.Length)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   4.300   5.100   5.800   5.843   6.400   7.900
```

Summary of a data frame. Previous function is applied to each column.
Depending on the data in each column, result will differ.

If the column is a numeric variable, mean, median, min, max and
quartiles are returned. If the column is a factor variable, the number
of observations in each group is returned.

Let's use it:


```r
summary(my_data)
```

```
##   Sepal.Length    Sepal.Width     Petal.Length    Petal.Width   
##  Min.   :4.300   Min.   :2.000   Min.   :1.000   Min.   :0.100  
##  1st Qu.:5.100   1st Qu.:2.800   1st Qu.:1.600   1st Qu.:0.300  
##  Median :5.800   Median :3.000   Median :4.350   Median :1.300  
##  Mean   :5.843   Mean   :3.057   Mean   :3.758   Mean   :1.199  
##  3rd Qu.:6.400   3rd Qu.:3.300   3rd Qu.:5.100   3rd Qu.:1.800  
##  Max.   :7.900   Max.   :4.400   Max.   :6.900   Max.   :2.500  
##        Species  
##  setosa    :50  
##  versicolor:50  
##  virginica :50  
##                 
##                 
## 
```

If you do not want to see 3 digits after dot (lets limit it to one
digit):


```r
summary(my_data, digits = 1)
```

```
##   Sepal.Length  Sepal.Width  Petal.Length  Petal.Width        Species  
##  Min.   :4     Min.   :2    Min.   :1     Min.   :0.1   setosa    :50  
##  1st Qu.:5     1st Qu.:3    1st Qu.:2     1st Qu.:0.3   versicolor:50  
##  Median :6     Median :3    Median :4     Median :1.3   virginica :50  
##  Mean   :6     Mean   :3    Mean   :4     Mean   :1.2                  
##  3rd Qu.:6     3rd Qu.:3    3rd Qu.:5     3rd Qu.:1.8                  
##  Max.   :8     Max.   :4    Max.   :7     Max.   :2.5
```

## sapply and apply functions for calculations

It's also possible to use the function sapply() to apply a particular
function over a list or vector. For instance, we can use it, to compute
for each column in a data frame, the mean, sd, var, min, quantile, ...

Compute the mean of each column


```r
sapply(my_data[-5], mean)
```

```
## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
##     5.843333     3.057333     3.758000     1.199333
```

What is "[-5]"? : It means drop the fifth column while doing the
calculation. Why? Because it is not numeric, function cannot calculate
that.

Compute quartiles


```r
sapply(my_data[-5], quantile)
```

```
##      Sepal.Length Sepal.Width Petal.Length Petal.Width
## 0%            4.3         2.0         1.00         0.1
## 25%           5.1         2.8         1.60         0.3
## 50%           5.8         3.0         4.35         1.3
## 75%           6.4         3.3         5.10         1.8
## 100%          7.9         4.4         6.90         2.5
```

We can also use apply(), However, we will need to specify if we want to
work with columns or rows. We'll start with the main function of the
apply group: apply(). It takes a DataFrame, a matrix, or a
multi-dimensional array as input and, depending on the input object type
and the function passed in, outputs a vector, a list, a matrix, or an
array.

The syntax of the apply() function is very simple and has only three
parameters:

apply(X, MARGIN, FUN)

X=dataframe MARGIN=(it can take values 1, 2, or c(1,2), meaning that the
function is applied row-wise, column-wise, or both row- and column-wise,
correspondingly) FUN=function


```r
apply(my_data[,-5], 2, median)
```

```
## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
##         5.80         3.00         4.35         1.30
```

## Pipe (%>%) Operator

The %>% symbol in R is called the pipe operator, and it comes from the
magrittr package, which is also imported by the dplyr package. It is
used to pass the result of one expression as the first argument to the
next expression. This can make your code more readable and reduces the
need for nested function calls.


```r
summarize(
  filter(iris, Species == 'setosa'),
  mean_sepal_length = mean(Sepal.Length),
  mean_sepal_width = mean(Sepal.Width)
)
```

```
##   mean_sepal_length mean_sepal_width
## 1             5.006            3.428
```

For example, code above is identical to code below. However, it is better readable.

```r
library(dplyr)

iris %>%
  filter(Species == 'setosa') %>%
  summarize(
    mean_sepal_length = mean(Sepal.Length),
    mean_sepal_width = mean(Sepal.Width)
  )
```

```
##   mean_sepal_length mean_sepal_width
## 1             5.006            3.428
```

## Descriptive statistics by groups

We want to group the data by Species (using group_by) and then: compute
the number of element in each group. R function: n() compute the mean: R
function mean() and the standard deviation: R function sd() dont forget
to ignore NA values for calculation functions mean and sd

lets use group_by, which takes our data, and groups it by species. Then,
we use summarize()

Quest: group_by Species, count entries for each group etc


```r
group_by(my_data, Species) %>% 
  summarise(
    count = n(), 
    mean = mean(Sepal.Length, na.rm = TRUE),
    standarddeviation = sd(Sepal.Length, na.rm = TRUE)
)
```

```
## # A tibble: 3 × 4
##   Species    count  mean standarddeviation
##   <fct>      <int> <dbl>             <dbl>
## 1 setosa        50  5.01             0.352
## 2 versicolor    50  5.94             0.516
## 3 virginica     50  6.59             0.636
```

We can make it a new variable, so we can manipulate if needed...


```r
sepal_length_table <- group_by(my_data, Species) %>% 
  summarise(
    count = n(), 
    mean = mean(Sepal.Length, na.rm = TRUE),
    standarddeviation = sd(Sepal.Length, na.rm = TRUE),
    median = median(Petal.Length, na.rm = TRUE)
  )
```

The result of this pipeline will be a new data frame where each row
corresponds to a unique Species in the original my_data. Each row will
have the count of observations, the mean of Sepal.Length, and the
standard deviation of Sepal.Length for that Species. This type of
summary is particularly useful for understanding the distribution of
measurements within categories of a categorical variable.

## Let's try a new dataset.


```r
data("ToothGrowth")
head(ToothGrowth)
```

```
##    len supp dose
## 1  4.2   VC  0.5
## 2 11.5   VC  0.5
## 3  7.3   VC  0.5
## 4  5.8   VC  0.5
## 5  6.4   VC  0.5
## 6 10.0   VC  0.5
```

```r
#View(ToothGrowth)
```

len: Tooth length supp: Supplement type (VC or OJ).two delivery methods,
(orange juice or ascorbic acid (a form of vitamin C and coded as VC).
dose: numeric Dose in milligrams/day

Can you group this dataset by dose and calculate mean, count and
standard deviation for each group?


```r
group_by(ToothGrowth, dose) %>%
  summarise(
    count = n(),
    mean = mean(len, na.rm = TRUE),
    stdev = sd(len, na.rm = TRUE),
  )
```

```
## # A tibble: 3 × 4
##    dose count  mean stdev
##   <dbl> <int> <dbl> <dbl>
## 1   0.5    20  10.6  4.50
## 2   1      20  19.7  4.42
## 3   2      20  26.1  3.77
```

Can you group this dataset by supp and calculate mean, count, standard
deviation, median, min and max?


```r
group_by(ToothGrowth, supp) %>%
  summarise(
    count = n(),
    mean = mean(len, na.rm = TRUE),
    stdev = sd(len, na.rm = TRUE),
    median = median(len, na.rm =TRUE),
    min = min(len),
    max = max(len)
  )
```

```
## # A tibble: 2 × 7
##   supp  count  mean stdev median   min   max
##   <fct> <int> <dbl> <dbl>  <dbl> <dbl> <dbl>
## 1 OJ       30  20.7  6.61   22.7   8.2  30.9
## 2 VC       30  17.0  8.27   16.5   4.2  33.9
```
