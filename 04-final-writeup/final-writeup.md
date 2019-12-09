Understanding Google Play Application Reviews
================
RTime2Shine
12/7/19

    ## Skim summary statistics
    ##  n obs: 7731 
    ##  n variables: 15 
    ## 
    ## ── Variable type:factor ──────────────────────────────────────────────────────────────────────────────
    ##  variable missing complete    n n_unique
    ##  Installs       0     7731 7731        5
    ##                                 top_counts ordered
    ##  100: 4462, Bet: 1477, Bet: 1145, Bet: 510   FALSE

![](final-writeup_files/figure-gfm/rating-distribution-1.png)<!-- -->

![](final-writeup_files/figure-gfm/log%20reviews-1.png)<!-- -->

    ## # A tibble: 1 x 3
    ##   `median(log_reviews)` `max(log_reviews)` `IQR(log_reviews)`
    ##                   <dbl>              <dbl>              <dbl>
    ## 1                  7.55               12.2               5.44

    ## # A tibble: 33 x 3
    ##    Category            n   freq
    ##    <fct>           <int>  <dbl>
    ##  1 FAMILY           1543 0.200 
    ##  2 GAME              671 0.0868
    ##  3 TOOLS             646 0.0836
    ##  4 MEDICAL           350 0.0453
    ##  5 LIFESTYLE         301 0.0389
    ##  6 FINANCE           299 0.0387
    ##  7 BUSINESS          289 0.0374
    ##  8 PERSONALIZATION   275 0.0356
    ##  9 SPORTS            269 0.0348
    ## 10 PRODUCTIVITY      262 0.0339
    ## # … with 23 more rows

    ## # A tibble: 33 x 3
    ##    Category        category_simp        n
    ##    <fct>           <chr>            <int>
    ##  1 FAMILY          Top 6 Categories  1543
    ##  2 GAME            Top 6 Categories   671
    ##  3 TOOLS           Top 6 Categories   646
    ##  4 MEDICAL         Top 6 Categories   350
    ##  5 LIFESTYLE       Top 6 Categories   301
    ##  6 FINANCE         Top 6 Categories   299
    ##  7 BUSINESS        Others             289
    ##  8 PERSONALIZATION Others             275
    ##  9 SPORTS          Others             269
    ## 10 PRODUCTIVITY    Others             262
    ## # … with 23 more rows

    ## Warning: Factor `Android Ver` contains implicit NA, consider using
    ## `forcats::fct_explicit_na`

    ## # A tibble: 10 x 2
    ##    `Android Ver`          n
    ##    <fct>              <int>
    ##  1 4                   4972
    ##  2 2                   1085
    ##  3 Varies with device   735
    ##  4 5                    512
    ##  5 3                    229
    ##  6 1                    103
    ##  7 7                     45
    ##  8 6                     43
    ##  9 8                      5
    ## 10 <NA>                   2

    ## # A tibble: 9 x 3
    ##   `Android Ver`      androidver_simp        n
    ##   <fct>              <chr>              <int>
    ## 1 4                  1-4                 4964
    ## 2 2                  1-4                 1085
    ## 3 Varies with device Varies with Device   735
    ## 4 5                  5-8                  510
    ## 5 3                  1-4                  229
    ## 6 1                  1-4                  103
    ## 7 7                  5-8                   45
    ## 8 6                  5-8                   43
    ## 9 8                  5-8                    5

    ## # A tibble: 6 x 3
    ##   `Content Rating` content_simp     n
    ##   <chr>            <chr>        <int>
    ## 1 Everyone         Everyone      6319
    ## 2 Teen             Teen           770
    ## 3 "Mature "        <NA>           355
    ## 4 "Everyone "      <NA>           271
    ## 5 "Adults only "   <NA>             3
    ## 6 Unrated          Unrated          1

# Model Selection

|                term                |  estimate   | std.error |  statistic   |  p.value  |
| :--------------------------------: | :---------: | :-------: | :----------: | :-------: |
|            (Intercept)             |  4.5292030  | 0.3096396 |  14.6273362  | 0.0000000 |
|   category\_simpTop 6 Categories   | \-0.0159527 | 0.0123302 | \-1.2937976  | 0.1957741 |
|            log\_reviews            |  0.0778565  | 0.0041904 |  18.5796391  | 0.0000000 |
|        SizeLess than 100 MB        |  0.0284119  | 0.0386195 |  0.7356863   | 0.4619440 |
|       SizeVaries with device       | \-0.0157805 | 0.0516131 | \-0.3057456  | 0.7598066 |
|   InstallsBetween 100 and 1,000    | \-0.3192573 | 0.0508854 | \-6.2740419  | 0.0000000 |
|  InstallsBetween 1,000 and 10,000  | \-0.6745975 | 0.0488864 | \-13.7992792 | 0.0000000 |
| InstallsBetween 10,000 and 100,000 | \-0.8324958 | 0.0510458 | \-16.3087943 | 0.0000000 |
|     Installs100,000 or Greater     | \-1.0058440 | 0.0582761 | \-17.2599790 | 0.0000000 |
|              TypePaid              |  0.0741875  | 0.0461754 |  1.6066454   | 0.1081732 |
|     PriceBetween $0 and $4.99      |  0.0370657  | 0.0510218 |  0.7264680   | 0.4675740 |
|      `Content Rating`Everyone      | \-0.0548353 | 0.3039831 | \-0.1803892  | 0.8568518 |
|      `Content Rating`Everyone      | \-0.0677175 | 0.3055862 | \-0.2215989  | 0.8246321 |
|       `Content Rating`Mature       | \-0.1521919 | 0.3051383 | \-0.4987637  | 0.6179601 |
|        `Content Rating`Teen        | \-0.0740591 | 0.3044898 | \-0.2432235  | 0.8078387 |
|      `Content Rating`Unrated       |  0.1279921  | 0.6088736 |  0.2102113   | 0.8335083 |
|        androidver\_simp5-8         | \-0.0572665 | 0.0227200 | \-2.5205266  | 0.0117380 |
| androidver\_simpVaries with Device | \-0.0249248 | 0.0378446 | \-0.6586090  | 0.5101666 |
|            date\_since             | \-0.0001225 | 0.0000159 | \-7.7033322  | 0.0000000 |

    ## Warning: 'tidy.numeric' is deprecated.
    ## See help("Deprecated")

    ## # A tibble: 19 x 2
    ##    names                                  x
    ##    <chr>                              <dbl>
    ##  1 category_simpTop 6 Categories         NA
    ##  2 log_reviews                           NA
    ##  3 SizeLess than 100 MB                  NA
    ##  4 SizeVaries with device                NA
    ##  5 InstallsBetween 100 and 1,000         NA
    ##  6 InstallsBetween 1,000 and 10,000      NA
    ##  7 InstallsBetween 10,000 and 100,000    NA
    ##  8 Installs100,000 or Greater            NA
    ##  9 TypePaid                              NA
    ## 10 PriceBetween $0 and $4.99             NA
    ## 11 PriceGreater than $5                  NA
    ## 12 `Content Rating`Everyone              NA
    ## 13 "`Content Rating`Everyone "           NA
    ## 14 "`Content Rating`Mature "             NA
    ## 15 `Content Rating`Teen                  NA
    ## 16 `Content Rating`Unrated               NA
    ## 17 androidver_simp5-8                    NA
    ## 18 androidver_simpVaries with Device     NA
    ## 19 date_since                            NA

    ## Warning in leaps.setup(x, y, wt = wt, nbest = nbest, nvmax = nvmax,
    ## force.in = force.in, : 1 linear dependencies found

    ## Reordering variables and trying again:

    ##                        (Intercept)                        log_reviews 
    ##                        4.452498547                        0.079337732 
    ##      InstallsBetween 100 and 1,000   InstallsBetween 1,000 and 10,000 
    ##                       -0.333550472                       -0.692616919 
    ## InstallsBetween 10,000 and 100,000         Installs100,000 or Greater 
    ##                       -0.856770609                       -1.025709369 
    ##                           TypePaid               `Content Rating`Teen 
    ##                        0.079420275                       -0.009976861 
    ##               PriceGreater than $5 
    ##                       -0.022538797

    ## Warning in leaps.setup(x, y, wt = wt, nbest = nbest, nvmax = nvmax,
    ## force.in = force.in, : 1 linear dependencies found

    ## Reordering variables and trying again:

    ##                        (Intercept)                        log_reviews 
    ##                        4.452498547                        0.079337732 
    ##      InstallsBetween 100 and 1,000   InstallsBetween 1,000 and 10,000 
    ##                       -0.333550472                       -0.692616919 
    ## InstallsBetween 10,000 and 100,000         Installs100,000 or Greater 
    ##                       -0.856770609                       -1.025709369 
    ##                           TypePaid               `Content Rating`Teen 
    ##                        0.079420275                       -0.009976861 
    ##               PriceGreater than $5 
    ##                       -0.022538797

## Section 1: Introduction (includes introduction and exploratory data analysis)

Lukengu: relevel categories, log transform and remove the outliers of
reviews

Sanjay: finish EDA,
etc.

## Section 2: Regression Analysis (includes the final model and discussion of assumptions)

## Section 3: Discussion and Limitations

## Section 4: Conclusion

## Section 5: Additional Work
