# Reproducible Research: Peer Assessment 1


### Loading and preprocessing the data

I assume that the file `activity.csv` is placed in the same folder as this file (`PA1_template.Rmd`).


```r
data <- read.csv("activity.csv")
data$date <- as.Date(data$date , format = "%Y-%m-%d")
```

### What is mean total number of steps taken per day?

Total number of steps per day:


```r
steps.per.day <- aggregate(data$steps, by = list(data$date), sum)
colnames(steps.per.day) <- c("Date", "Steps")
summary(steps.per.day)
```

```
##       Date                Steps      
##  Min.   :2012-10-01   Min.   :   41  
##  1st Qu.:2012-10-16   1st Qu.: 8841  
##  Median :2012-10-31   Median :10765  
##  Mean   :2012-10-31   Mean   :10766  
##  3rd Qu.:2012-11-15   3rd Qu.:13294  
##  Max.   :2012-11-30   Max.   :21194  
##                       NA's   :8
```


```r
hist(steps.per.day$Steps, breaks = 20, main = "Total number of steps taken each day", xlab = "Steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 

Mean number of steps taken per day (over the days for which data is present):


```r
mean(steps.per.day$Steps, na.rm = TRUE)
```

```
## [1] 10766.19
```

Median number of steps taken per day (over the days for which data is present):


```r
median(steps.per.day$Steps, na.rm = TRUE)
```

```
## [1] 10765
```


### What is the average daily activity pattern?

Time series plot of average number of steps taken over each 5-minute interval, averaged across all days


```r
steps.per.interval <- aggregate(data$steps, by = list(data$interval), mean, na.rm = TRUE)
colnames(steps.per.interval) <- c("Interval", "Steps")
plot(steps.per.interval$Interval, steps.per.interval$Steps, type="l", main = "Average number of steps over 5-minute interval", 
     xlab = "Interval", ylab = "Steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-6-1.png) 

The 5-minute interval that contains the maximum number of steps (on average across all days) is:


```r
steps.per.interval[which.max(steps.per.interval$Steps), ]
```

```
##     Interval    Steps
## 104      835 206.1698
```

### Imputing missing values



### Are there differences in activity patterns between weekdays and weekends?
