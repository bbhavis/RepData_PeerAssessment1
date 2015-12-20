---
title: "test"
output: html_document
---

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

###Loading and preprocessing the data

Show any code that is needed to

1. Load the data (i.e. read.csv())

2. Process/transform the data (if necessary) into a format suitable for your analysis


```r
act <- read.table("activity.csv", sep=",", header = TRUE, stringsAsFactors = FALSE)
str(act)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : chr  "2012-10-01" "2012-10-01" "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

```r
act$date1 <- as.Date(act$date, "%Y-%m-%d")
head(act)
```

```
##   steps       date interval      date1
## 1    NA 2012-10-01        0 2012-10-01
## 2    NA 2012-10-01        5 2012-10-01
## 3    NA 2012-10-01       10 2012-10-01
## 4    NA 2012-10-01       15 2012-10-01
## 5    NA 2012-10-01       20 2012-10-01
## 6    NA 2012-10-01       25 2012-10-01
```

###What is mean total number of steps taken per day?

For this part of the assignment, you can ignore the missing values in the dataset.

1. Calculate the total number of steps taken per day

2. If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day

3. Calculate and report the mean and median of the total number of steps taken per day


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following objects are masked from 'package:stats':
## 
##     filter, lag
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
#Calculation of total number of steps taken per day
df <- filter(act, is.na(act$steps) == FALSE)
dfSum <- dplyr::summarise(group_by(df, date1), sum(steps))
names(dfSum) <- c("Date", "TotSteps")
head(names)
```

```
##                      
## 1 .Primitive("names")
```

```r
#Displaying the data on histogram
hist(dfSum$TotSteps, breaks=30, main="Historgram of Number of Steps", xlab="Steps", col="green", las=1)
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-1.png) 

```r
#Calculating mean and median steps taken per day
library(plyr)
```

```
## -------------------------------------------------------------------------
## You have loaded plyr after dplyr - this is likely to cause problems.
## If you need functions from both plyr and dplyr, please load plyr first, then dplyr:
## library(plyr); library(dplyr)
## -------------------------------------------------------------------------
## 
## Attaching package: 'plyr'
## 
## The following objects are masked from 'package:dplyr':
## 
##     arrange, count, desc, failwith, id, mutate, rename, summarise,
##     summarize
```

```r
ddply(df, .(date1), summarize, "mean"=mean(steps), "median"=median(steps))
```

```
##         date1       mean median
## 1  2012-10-02  0.4375000      0
## 2  2012-10-03 39.4166667      0
## 3  2012-10-04 42.0694444      0
## 4  2012-10-05 46.1597222      0
## 5  2012-10-06 53.5416667      0
## 6  2012-10-07 38.2465278      0
## 7  2012-10-09 44.4826389      0
## 8  2012-10-10 34.3750000      0
## 9  2012-10-11 35.7777778      0
## 10 2012-10-12 60.3541667      0
## 11 2012-10-13 43.1458333      0
## 12 2012-10-14 52.4236111      0
## 13 2012-10-15 35.2048611      0
## 14 2012-10-16 52.3750000      0
## 15 2012-10-17 46.7083333      0
## 16 2012-10-18 34.9166667      0
## 17 2012-10-19 41.0729167      0
## 18 2012-10-20 36.0937500      0
## 19 2012-10-21 30.6284722      0
## 20 2012-10-22 46.7361111      0
## 21 2012-10-23 30.9652778      0
## 22 2012-10-24 29.0104167      0
## 23 2012-10-25  8.6527778      0
## 24 2012-10-26 23.5347222      0
## 25 2012-10-27 35.1354167      0
## 26 2012-10-28 39.7847222      0
## 27 2012-10-29 17.4236111      0
## 28 2012-10-30 34.0937500      0
## 29 2012-10-31 53.5208333      0
## 30 2012-11-02 36.8055556      0
## 31 2012-11-03 36.7048611      0
## 32 2012-11-05 36.2465278      0
## 33 2012-11-06 28.9375000      0
## 34 2012-11-07 44.7326389      0
## 35 2012-11-08 11.1770833      0
## 36 2012-11-11 43.7777778      0
## 37 2012-11-12 37.3784722      0
## 38 2012-11-13 25.4722222      0
## 39 2012-11-15  0.1423611      0
## 40 2012-11-16 18.8923611      0
## 41 2012-11-17 49.7881944      0
## 42 2012-11-18 52.4652778      0
## 43 2012-11-19 30.6979167      0
## 44 2012-11-20 15.5277778      0
## 45 2012-11-21 44.3993056      0
## 46 2012-11-22 70.9270833      0
## 47 2012-11-23 73.5902778      0
## 48 2012-11-24 50.2708333      0
## 49 2012-11-25 41.0902778      0
## 50 2012-11-26 38.7569444      0
## 51 2012-11-27 47.3819444      0
## 52 2012-11-28 35.3576389      0
## 53 2012-11-29 24.4687500      0
```

###What is the average daily activity pattern?

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


```r
#Time series plot
df <- filter(act, is.na(act$steps) == FALSE)
dfMean <- dplyr::summarise(group_by(df, interval), mean(steps))
names(dfMean) <- c("Interval", "AverageSteps")
with(dfMean, {plot(Interval, AverageSteps, type="l", main="Time Series Plot")})
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3-1.png) 

```r
#Sorting the data in descending order and selecting the 1st record to idntify the 5-minute average interval with max steps
arrange(dfMean, desc(AverageSteps))[1,]
```

```
## Source: local data frame [1 x 2]
## 
##   Interval AverageSteps
##      (int)        (dbl)
## 1      835     206.1698
```

###Imputing missing values

Note that there are a number of days/intervals where there are missing values (coded as NA). The presence of missing days may introduce bias into some calculations or summaries of the data.

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

2. Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

3. Create a new dataset that is equal to the original dataset but with the missing data filled in.

4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?


```r
#Counting total number of missing values
nrow(filter(act,is.na(steps)==TRUE))
```

```
## [1] 2304
```

```r
#applying a strategy to fill the missing values with the average steps taken for that interval using dfMean calculated earlier
act1 <- filter(act, is.na(steps) == TRUE)
dfMerge <- merge(act1, dfMean, by.x="interval", by.y="Interval", all=TRUE)[,c("AverageSteps", "date", "interval", "date1")]
names(dfMerge) <- c("steps", "date", "interval", "date1")
dfMerge$steps <- trunc(dfMerge$steps)
#Creating the new dataset and checking the counts
dfBind <- rbind(filter(act, is.na(steps)==FALSE), dfMerge)

nrow(act) 
```

```
## [1] 17568
```

```r
nrow(dfMerge) 
```

```
## [1] 2304
```

```r
nrow(filter(dfMerge, is.na(steps)==TRUE)) 
```

```
## [1] 0
```

```r
#Calculating the Total, Mean and Median after fixing the missing data values
dfAll <- ddply(dfBind, .(date1), summarize, "tot"=sum(steps), "mean"=mean(steps), "median"=median(steps))
head(dfAll)
```

```
##        date1   tot     mean median
## 1 2012-10-01 10641 36.94792   33.5
## 2 2012-10-02   126  0.43750    0.0
## 3 2012-10-03 11352 39.41667    0.0
## 4 2012-10-04 12116 42.06944    0.0
## 5 2012-10-05 13294 46.15972    0.0
## 6 2012-10-06 15420 53.54167    0.0
```

```r
#Historgram
hist(dfAll$tot, breaks=30, main="Steps after fixing NA values", xlab="Steps", col="green", las=1)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-1.png) 

```r
hist(dfSum$TotSteps, breaks=30, main="Steps before fixing NA values", xlab="Steps", col="green", las=1)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-2.png) 

```r
#Conclusion: 
#(a) Total number of steps for certain days has drastrically went up. This due to non-availability of steps taken for certain days (b) Median for certain days has gone up from 0 which can be clearly noticed when comparing the values before & after fixing the data (c) There is not much of change in Mean for the days where median has been 0 before & after fixing the data which also demonstrates the quality of data collection
```

###Are there differences in activity patterns between weekdays and weekends?

For this part the weekdays() function may be of some help here. Use the dataset with the filled-in missing values for this part.

1. Create a new factor variable in the dataset with two levels – “weekday” and “weekend” indicating whether a given date is a weekday or weekend day.

2. Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.


```r
#Adding new variables for Day and Weekday/Weekend indicator
dfBind$Day <- weekdays(dfBind$date1)
dfBind$WDay <- ifelse (weekdays(dfBind$date1) %in% c("Saturday", "Sunday"), "Weekend", "Weekday")
dfFinalGrp <- dplyr::summarize(group_by(dfBind, interval, WDay), mean(steps))
names(dfFinalGrp) <- c("Interval","WDay", "Steps")
head(dfFinalGrp)
```

```
## Source: local data frame [6 x 3]
## 
##   Interval    WDay     Steps
##      (int)   (chr)     (dbl)
## 1        0 Weekday 2.1555556
## 2        0 Weekend 0.1250000
## 3        5 Weekday 0.4000000
## 4        5 Weekend 0.0000000
## 5       10 Weekday 0.1555556
## 6       10 Weekend 0.0000000
```

```r
#plot created using lattice library
library(lattice)
attach(dfFinalGrp)
days.f <- factor(dfFinalGrp$WDay, levels=c("Weekday", "Weekend"), labels=c("Weekday", "Weekend"))
xyplot(dfFinalGrp$Steps~dfFinalGrp$Interval|days.f, 
        main="Panel Plot of Steps by Interval for Weekend/Weekday", 
        ylab="Number of Steps", xlab="Interval", type="l", layout=c(1,2))
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-1.png) 
