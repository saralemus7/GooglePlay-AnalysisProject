Understanding Google Play Application Reviews
================
RTime2Shine
12/7/19

    ## Skim summary statistics
    ##  n obs: 7731 
    ##  n variables: 15 
    ## 
    ## ── Variable type:factor ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
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

## Section 1: Introduction (includes introduction and exploratory data analysis)

Lukengu: relevel categories, log transform and remove the outliers of
reviews

Sanjay: finish EDA,
etc.

## Section 2: Regression Analysis (includes the final model and discussion of assumptions)

## Section 3: Discussion and Limitations

## Section 4: Conclusion

## Section 5: Additional Work
