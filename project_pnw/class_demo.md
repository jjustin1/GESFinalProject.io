---
title: "R Notebook"
subtitle: Census Differences GES 486
output: 
        html_document:
                keep_md: true
author: Dillon Mahmoudi (dillonm@umbc.edu)
date:   2021/02/25
---

# Census Demo
This file 

## Setup
First, we load in the various packages we need. I've added `mapview` here instead of `ggplot` because it allows for easier interactions with `sf`. This chunk of code also sets some defaults for the `tidycensus` package. To use this script, you'll need to sign up for your own census api key. (https://api.census.gov/data/key_signup.html)


```r
# packages
library(tidyverse)
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.3     v purrr   0.3.4
## v tibble  3.1.0     v dplyr   1.0.4
## v tidyr   1.1.2     v stringr 1.4.0
## v readr   1.4.0     v forcats 0.5.1
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(tidycensus)
library(sf)
```

```
## Linking to GEOS 3.8.0, GDAL 3.0.4, PROJ 6.3.1
```

```r
library(ggplot2)

# settings for tidycensus
options(tigris_class = "sf")
options(tigris_use_cache = TRUE)
# census_api_key("yourkeyhere", install=TRUE)

setwd("C://Users//Dillon Mahmoudi//Downloads")
```

## Get Census Data
Then we use the `get_acs` command to get data from the Census specifying which population and housing variables we want to get. Here's the Data Dictionary from Social Explorer. (https://www.socialexplorer.com/data/ACS2019_5yr/metadata/?ds=ACS19_5yr)


```r
# This gets evening and afternoon workers in 2019
bmore_t_worktime_2019 <- get_acs(geography = "tract", 
     variables = c("total_workers" = "B08302_001", # Total workers
                   "workers_eve1" = "B08302_014", # Afternoon departure 1
                   "workers_eve2" = "B08302_015", # Afternoon departure 2
                   "med_hh_inc" = "B19013_001" # Median household income
                   ), 
     year = 2019,
     survey = "acs5",
     state = c(24), 
     county = c(510,5), 
     geometry = TRUE, # download the shapefile with the data
     output = "wide") # need this
```

```
## Getting data from the 2015-2019 5-year ACS
```

```r
# This gets evening and afternoon workers in 2014
bmore_t_worktime_2014 <- get_acs(geography = "tract", 
     variables = c("total_workers" = "B08302_001", # Total workers
                   "workers_eve1" = "B08302_014", # Afternoon departure 1
                   "workers_eve2" = "B08302_015", # Afternoon departure 2
                   "med_hh_inc" = "B19013_001" # Median household income
                   ), 
     year = 2014,
     survey = "acs5",
     state = c(24), 
     county = c(510,5), 
     geometry = FALSE, # download the shapefile with the data
     output = "wide") # need this
```

```
## Getting data from the 2010-2014 5-year ACS
```

```r
# We now have raw data that we should write out to file
# Because we're going to save in geojson, we're going to transform to 3857
#st_write(st_transform(bmore_t_worktime_2019, 3857), "bmore_t_worktime_2019.geojson")

#st_write(bmore_t_worktime_2014, "bmore_t_worktime_2014.csv") # geometry is false!
```

## Compute morning share vs evening share of workers
Add a bunch of explanation here. And talk about my formulas that I used.

```r
# Compute the evening *share* in 2019
bmore_t_worktime_2019$work_evening_share <- (bmore_t_worktime_2019$workers_eve1E + bmore_t_worktime_2019$workers_eve2E) / bmore_t_worktime_2019$total_workersE

# Compute the evening *share* in 2014
bmore_t_worktime_2014$work_evening_share <- (bmore_t_worktime_2014$workers_eve1E + bmore_t_worktime_2014$workers_eve2E) / bmore_t_worktime_2014$total_workersE

# Compute the morning *share* in 2019, as the inverse of the evening share computed above
bmore_t_worktime_2019$work_morning_share <- 1 - bmore_t_worktime_2019$work_evening_share

# Compute the morning *share* in 2014, as the inverse of the evening share computed above
bmore_t_worktime_2014$work_morning_share <- 1 - bmore_t_worktime_2014$work_evening_share
```

## Merge the two time periods

```r
bmore_t_worktime <- left_join(bmore_t_worktime_2019, bmore_t_worktime_2014, 
                              by="GEOID",
                              suffix=c(".19",".14"))

# Compute differences in worktimes
bmore_t_worktime$work_eve_diff <- bmore_t_worktime$work_evening_share.19 -
        bmore_t_worktime$work_evening_share.14

bmore_t_worktime$work_mor_diff <- bmore_t_worktime$work_morning_share.19 -
        bmore_t_worktime$work_morning_share.14

# Compute difference in median household income
bmore_t_worktime$mhhi_diff <- bmore_t_worktime$med_hh_incE.19 -
        bmore_t_worktime$med_hh_incE.14


bmore_t_worktime <- st_transform(bmore_t_worktime, 3857) # reproject into web-mercator because Google owns everything        
```


## Write to file
Here I'm going to use ggplot. Not that I specified the CRS (projection)

```r
st_write(bmore_t_worktime_2019, "bmore_t_worktime_diff.geojson")
```

```
## Writing layer `bmore_t_worktime_diff' to data source `bmore_t_worktime_diff.geojson' using driver `GeoJSON'
## Writing 414 features with 12 fields and geometry type Multi Polygon.
```

