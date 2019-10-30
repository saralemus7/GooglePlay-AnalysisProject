PROJECT TITLE
================
RTime2Shine
October 29, 2019

## Section 1. Introduction

## Section 2. Analysis plan

``` r
library(tidyverse)
```

    ## ── Attaching packages ────────────────────────────────────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.2.1     ✔ purrr   0.3.2
    ## ✔ tibble  2.1.3     ✔ dplyr   0.8.3
    ## ✔ tidyr   0.8.3     ✔ stringr 1.4.0
    ## ✔ readr   1.3.1     ✔ forcats 0.4.0

    ## ── Conflicts ───────────────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(broom)
library(knitr) 
library(ggplot2)
```

``` r
apps <- read_csv("/cloud/project/02-data/googleplaystore.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   App = col_character(),
    ##   Category = col_character(),
    ##   Rating = col_double(),
    ##   Reviews = col_double(),
    ##   Size = col_character(),
    ##   Installs = col_character(),
    ##   Type = col_character(),
    ##   Price = col_character(),
    ##   `Content Rating` = col_character(),
    ##   Genres = col_character(),
    ##   `Last Updated` = col_character(),
    ##   `Current Ver` = col_character(),
    ##   `Android Ver` = col_character()
    ## )

    ## Warning: 2 parsing failures.
    ##   row     col               expected     actual                                         file
    ## 10473 Reviews no trailing characters M          '/cloud/project/02-data/googleplaystore.csv'
    ## 10473 NA      13 columns             12 columns '/cloud/project/02-data/googleplaystore.csv'

## Section 3. Regression Analysis Plan

## Section 4. References

## The Data

``` r
glimpse(apps)
```

    ## Observations: 10,841
    ## Variables: 13
    ## $ App              <chr> "Photo Editor & Candy Camera & Grid & ScrapBook…
    ## $ Category         <chr> "ART_AND_DESIGN", "ART_AND_DESIGN", "ART_AND_DE…
    ## $ Rating           <dbl> 4.1, 3.9, 4.7, 4.5, 4.3, 4.4, 3.8, 4.1, 4.4, 4.…
    ## $ Reviews          <dbl> 159, 967, 87510, 215644, 967, 167, 178, 36815, …
    ## $ Size             <chr> "19M", "14M", "8.7M", "25M", "2.8M", "5.6M", "1…
    ## $ Installs         <chr> "10,000+", "500,000+", "5,000,000+", "50,000,00…
    ## $ Type             <chr> "Free", "Free", "Free", "Free", "Free", "Free",…
    ## $ Price            <chr> "0", "0", "0", "0", "0", "0", "0", "0", "0", "0…
    ## $ `Content Rating` <chr> "Everyone", "Everyone", "Everyone", "Teen", "Ev…
    ## $ Genres           <chr> "Art & Design", "Art & Design;Pretend Play", "A…
    ## $ `Last Updated`   <chr> "January 7, 2018", "January 15, 2018", "August …
    ## $ `Current Ver`    <chr> "1.0.0", "2.0.0", "1.2.4", "Varies with device"…
    ## $ `Android Ver`    <chr> "4.0.3 and up", "4.0.3 and up", "4.0.3 and up",…
