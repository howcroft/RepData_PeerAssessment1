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
#Convert date to proper format
data$date <- strptime(data$date, "YYYY-MM-DD")
rm(zipfile)
```




## What is mean total number of steps taken per day?

```r
library(dplyr)
#all data even ones with no data (like 2012-10-01)
#answer <- summarise_each(group_by(data, date), funs(mean(., na.rm=TRUE)))
#answer
#Data sanitized to only show meaningful means
#dataNAsRemoved <- data[complete.cases(data),]
#answer <- summarise_each(group_by(dataNAsRemoved, date), funs(mean(., na.rm=TRUE)))
#answer
```


## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?





<!---
Clean up Routines.
This is the only part where the assignment rule of echo=true is broken. Please forgive me ;)
-->


