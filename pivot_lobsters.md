---
title: "pivot_lobsters.rmd"
author: "Hussain"
date: "04/03/2022"
output:
  html_document: default
  word_document: default
---
## attach libraries
library(tidyverse)
library(readxl)
library(here)
library(skimr) # install.packages('skimr')
library(kableExtra) # install.packages('kableExtra')
#read xlsx file
## read in data
lobsters <- read_xlsx(here("data/lobsters.xlsx"), skip=4)
# explore data
skimr::skim(lobsters) 
#group_by multiple variables
lobsters %>%
  group_by(site, year) %>%
  summarize(count_by_siteyear =  n())
#assign
siteyear_summary <- lobsters %>%
  group_by(year, site) %>%
  summarize(count_by_siteyear =  n(), 
            mean_size_mm = mean(size_mm, na.rm = TRUE), 
            sd_size_mm = sd(size_mm, na.rm = TRUE))
## make a table with our new variable
siteyear_summary %>%
  kable()


```r
summary(lobsters)
```

```
##       year          month           date               site              transect    
##  Min.   :2012   Min.   :8.000   Length:2893        Length:2893        Min.   :1.000  
##  1st Qu.:2014   1st Qu.:8.000   Class :character   Class :character   1st Qu.:2.000  
##  Median :2015   Median :8.000   Mode  :character   Mode  :character   Median :3.000  
##  Mean   :2015   Mean   :8.037                                         Mean   :3.723  
##  3rd Qu.:2016   3rd Qu.:8.000                                         3rd Qu.:5.000  
##  Max.   :2016   Max.   :9.000                                         Max.   :9.000  
##                                                                                      
##   replicate            size_mm      
##  Length:2893        Min.   : 18.00  
##  Class :character   1st Qu.: 62.00  
##  Mode  :character   Median : 72.00  
##                     Mean   : 71.38  
##                     3rd Qu.: 81.00  
##                     Max.   :165.00  
##                     NA's   :5
```

 


