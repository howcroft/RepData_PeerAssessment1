# Reproducible Research: Peer Assessment 1
António Howcroft Ferreira  
Saturday, February 14, 2015  

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:



## Loading and preprocessing the data

<!--- 
setwd("C:/Users/ahf/Desktop/lectures_etc/coursera/jhopkins/represearch/assignment1/RepData_PeerAssessment1")
-->

```r
zipfile <- "activity.zip"
datafile <- "activity.csv"
unzip(zipfile, overwrite = TRUE, exdir = ".", unzip = "internal")
data <- read.csv(datafile)
#Data could be sanitized to only show meaningful means
dataNAsRemoved <- data[complete.cases(data),]
rm(zipfile)
```




## What is mean total number of steps taken per day?
1. Make a histogram of the total number of steps taken each day

```r
library(dplyr)
#Some days are present but have no data (e.g. 2012-10-01 for steps data)
dataNAsRemoved$date <- as.POSIXct(dataNAsRemoved$date)
answer <- summarise_each(group_by(dataNAsRemoved, date), funs(mean, median))
answer <- as.data.frame(answer)[c(1,2,3)]
# as.POSIXct Necessary for knittr limitation
hist(answer[,2], main="Total Steps", xlab = "Total Steps per day", col = "red")
```

![](PA1_template_files/figure-html/first_question-1.png) 
2. Calculate and report the mean and median of the total number of steps taken per day

```r
answer[, c(1,2)]
```

```
##          date steps_mean
## 1  2012-10-02  0.4375000
## 2  2012-10-03 39.4166667
## 3  2012-10-04 42.0694444
## 4  2012-10-05 46.1597222
## 5  2012-10-06 53.5416667
## 6  2012-10-07 38.2465278
## 7  2012-10-09 44.4826389
## 8  2012-10-10 34.3750000
## 9  2012-10-11 35.7777778
## 10 2012-10-12 60.3541667
## 11 2012-10-13 43.1458333
## 12 2012-10-14 52.4236111
## 13 2012-10-15 35.2048611
## 14 2012-10-16 52.3750000
## 15 2012-10-17 46.7083333
## 16 2012-10-18 34.9166667
## 17 2012-10-19 41.0729167
## 18 2012-10-20 36.0937500
## 19 2012-10-21 30.6284722
## 20 2012-10-22 46.7361111
## 21 2012-10-23 30.9652778
## 22 2012-10-24 29.0104167
## 23 2012-10-25  8.6527778
## 24 2012-10-26 23.5347222
## 25 2012-10-27 35.1354167
## 26 2012-10-28 39.7847222
## 27 2012-10-29 17.4236111
## 28 2012-10-30 34.0937500
## 29 2012-10-31 53.5208333
## 30 2012-11-02 36.8055556
## 31 2012-11-03 36.7048611
## 32 2012-11-05 36.2465278
## 33 2012-11-06 28.9375000
## 34 2012-11-07 44.7326389
## 35 2012-11-08 11.1770833
## 36 2012-11-11 43.7777778
## 37 2012-11-12 37.3784722
## 38 2012-11-13 25.4722222
## 39 2012-11-15  0.1423611
## 40 2012-11-16 18.8923611
## 41 2012-11-17 49.7881944
## 42 2012-11-18 52.4652778
## 43 2012-11-19 30.6979167
## 44 2012-11-20 15.5277778
## 45 2012-11-21 44.3993056
## 46 2012-11-22 70.9270833
## 47 2012-11-23 73.5902778
## 48 2012-11-24 50.2708333
## 49 2012-11-25 41.0902778
## 50 2012-11-26 38.7569444
## 51 2012-11-27 47.3819444
## 52 2012-11-28 35.3576389
## 53 2012-11-29 24.4687500
```

## What is the average daily activity pattern?

Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
#plot interval (answer[,1]) column over number of steps (answer[,2]).
answer <- summarise_each(group_by(dataNAsRemoved[,c(1,3)], interval), funs(mean))
answer <- as.data.frame(answer)
plot(answer[,1], answer[,2], type = "l", main="Daily activity pattern", xlab="Interval", ylab="Steps Taken")
```

![](PA1_template_files/figure-html/second_question-1.png) 

Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


```r
answer[which.max(answer$steps),]
```

```
##     interval    steps
## 104      835 206.1698
```


## Imputing missing values
Note that there are a number of days/intervals where there are missing values (coded as NA). The presence of missing days may introduce bias into some calculations or summaries of the data.

Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

```r
#dim(data)[1] - sum(complete.cases(data)) # would be the answer but since we've already have the length of data with NAsRemoved lets use that instead
dim(data)[1] - dim(dataNAsRemoved)[1]
```

```
## [1] 2304
```


Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

Create a new dataset that is equal to the original dataset but with the missing data filled in.

Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?


## Are there differences in activity patterns between weekdays and weekends?





<!---
Clean up Routines.
This is the only part where the assignment rule of echo=true is broken. Please forgive me ;)
-->


