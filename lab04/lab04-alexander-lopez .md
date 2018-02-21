---
title: "Lab04-alexander-lopez"
author: "Alexander Lopez"
date: "2/15/2018"
output: github_document
---


##Basic Importing 
```{r}
abalone <- read.table("abalone.data", sep = ",")

head(abalone)
tail(abalone)
str(abalone, vec.len <- 1 )##checking the data frame's structure 
```

##Detailed Information about the columns
```{r}
column_names <- c(
    'sex',
    'length',
    'diameter',
    'height',
    'whole_weight',
    'shucked_weight',
    'viscera_weight',
    'shell_weight',
    'rings'
)

column_types <- c(
    'character',
    'real',
    'real',
    'real',
    'real',
    'real',
    'real',
    'real',
    'integer'   
)

column_names
column_types


abalone <- read.table(
  'abalone.data',
  col.names = column_names,
  colClasses = column_types,
  sep =","
)
str(abalone, vec.len = 1)


read.csv(
  file = 'abalone.data',
  sep = "",
  quote = "\"'",
  dec = ".",
  col.names = column_names,
  colClasses = NA,
  nrows = 4
)

library(readr)
read_csv(file = 'abalone.data', col_names = TRUE, col_types = NULL,
  locale = default_locale(), na = c("", "NA"), quoted_na = TRUE, quote = "\"", comment = "", trim_ws = TRUE, skip = 0, n_max = Inf)



```

##Pittsburgh Bridges 
###*Reading the description*

* There are column names; name, type, possible values, and comments.
* The field separator is a space. 
* There are missing values, there are missing attribute values. There are missing values in attribute #'s 2,6,7,8,9,10,11,12,and 13. 
*The character for missing values are specifications and design descriptions. 
*The data type of each variable is nominal or cardinal. 
```{r}
url <- "http://archive.ics.uci.edu/ml/machine-learning-databases/bridges/bridges.data.version1"
pittsburg_bridges <- read.table(url, sep = ",")

pittsburg_bridges

origin_pittbridges <- "http://archive.ics.uci.edu/ml/machine-learning-databases/bridges/bridges.data.version1"
dest <- 'bridges.data'
download.file(origin_pittbridges, dest)

column_pittsburg_names <- c(
    'Identif',
    'River',
    'Location',
    'Erected',
    'Purpose',
    'Length',
    'Lanes',
    'Clear-G',
    'T-or-D',
    'Material',
    'Span',
    'Rel-l',
    'Type')

column_pittsburg_types <- c(
  'character',
  'character',
  'character',
  'character',
  'character',
  'character',
  'character',
  'character',
  'character',
  'character',
  'character',
  'character',
  'character'
)

column_pittsburg_names
column_pittsburg_types

bridges1 <- read.table(
  'bridges.data',
  col.names = column_pittsburg_names,
  colClasses = column_pittsburg_types,
  sep =","
)

bridges2 <- read.csv(
  'bridges.data',
  col.names = column_pittsburg_names,
  colClasses = column_pittsburg_types,
  sep =","
)

bridges3 <- read.table(
  'bridges.data',
  col.names = column_pittsburg_names,
  colClasses = column_pittsburg_types [1:5],
  sep = ","
)

str(bridges1, vec.len = 5)
summary(bridges1)
head(bridges1)
tail(bridges1)
dim(bridges1)
names(bridges1)
colnames(bridges1)
nrow(bridges1)
ncol(bridges1)
tail(bridges1, nrow = 108L)
head(bridges1, n = 1L)

```
#Creating Data Frames 
```{r}
player <- c("Thompson", "Curry","Green","Durant", "Pachulia")
position <- c("SG","PG","PF","SF","C")
salary <- c(16663575, 12112359, 15330435, 26540100, 2898000)
points <- c(1742, 1999, 776, 1555, 426)
ppg <- c(22.3, 25.3, 10.2, 25.1, 6.1)
rookie <- c(FALSE, FALSE, FALSE, FALSE, FALSE)

df <- data.frame(player, position, salary, points, ppg, rookie, stringsAsFactors = FALSE)
df

class(df)

ls(df, pos = 5L, all.names = FALSE, sorted = TRUE)
str(df, max.level <- NA, vec.len <- 20, give.attr <- TRUE)

cbind(df,  deparse.level = 1, stringsAsFactors <- FALSE)


```
# download csv file into working directory 
#Bracket notation and subsetting 
```{r}
csv <- "https://github.com/ucb-stat133/stat133-fall-2017/raw/master/data/nba2017-players.csv"
download.file(url = csv, destfile = 'nba2017-players.csv')

dat <- read.csv('nba2017-players.csv', stringsAsFactors = FALSE)

dim(dat)
head(dat)
tail(dat)
str(dat, vec.len = 1)
summary(dat)

names(dat)

dat[437:441,1:5]
dat[which(dat$height >70),1:5]
dat[which(dat$position == "C"), c(1,9)]
durant <- dat[which(dat$player == "Kevin Durant"),]
durant
ucla <- dat[which(dat$college == "University of California, Los Angeles"),]
ucla
rookies <- dat[which(dat$experience == 0),]
rookies
rookie_centers <- dat[which(dat$position == "C"),]
rookie_centers
top_players <- dat[which(dat$games > 50 & dat$minutes > 100),]
top_players
max(dat$height)
min(dat$height)
mean(dat$height)
dat$player[max(dat$height)]
dat$player[min(dat$height)]
dat$team
dat$player[max(dat$age)]
median(dat$salary)
median(dat$salary[dat$experience >= 10])
median(dat$salary[dat$position == "SG" | dat$position == "PG"])
median(dat$salary[dat$position == "PF" | dat$age >= 29| dat$height >= 79])
dat$player[dat$points <= 4]
dat$player[dat$points == 0]
dat[dat$college == "University of California, Berkeley",]
dat[dat$college == "University of Notre Dame",]
dat[dat$college != "University of",]
dat[dat$points[dat$minutes > 1],]
dat[max(dat$points3[dat$minutes >1]),]
dat[dat$points2[dat$minutes > 1],]
gsw <- dat[which(dat$team == "GSW"), c(1, 4:5)]
gsw

##Group By

aggregate(dat[ ,c('height', 'weight', 'age')], by = list(dat$position), FUN = mean)
aggregate(dat[ ,c('height', 'weight', 'age')], by = list(dat$team), FUN = mean)


```

the argument StringsAsFactors = FALSE is a good practice because the conversion automatically turns the characters into R factors. It is easier to call on specific commands after regarding the analysis of the data. 

