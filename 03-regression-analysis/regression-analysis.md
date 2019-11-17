PROJECT TITLE
================
RTime2Shine
11/20/19

Your regression analysis results go here. At a minimum, the regression
analysis should include the following:

  - Statement of the research question and modeling obejctive
    (prediction, inference, etc.)
  - Description of the response variable
  - Updated exploratory data analysis, incorporating any feedback from
    the proposal
  - Explanation of the modeling process and why you chose those metohds,
    incorporating any feedback from the proposal
  - Output of the final model
  - Discussion of the assumptions for the final model
  - Interpretations / interesting findings from the model coefficients
  - Additional work of other models or analylsis not included in the
    final model.

<!-- end list -->

    ## Warning: 2 parsing failures.
    ##   row     col               expected     actual                                         file
    ## 10473 Reviews no trailing characters M          '/cloud/project/02-data/googleplaystore.csv'
    ## 10473 NA      13 columns             12 columns '/cloud/project/02-data/googleplaystore.csv'

### Research Question:

What are the relevant factors that affect the rating given for apps in
the Google Play store?

### Response Variable:

The response variable in our investigation is `Rating` which is the mean
rating out of 5.0 for an application in the Google Play Store. This is a
numeric variable.

### Updated EDA

Below is some additional exploratory data analysis to further understand
the response variable.

    ## Skim summary statistics
    ##  n obs: 10841 
    ##  n variables: 13 
    ## 
    ## ── Variable type:character ──────────────────────────────────────────────────────────────────
    ##        variable missing complete     n min max empty n_unique
    ##     Android Ver       1    10840 10841   3  18     0       34
    ##             App       0    10841 10841   1 194     0     9660
    ##        Category       0    10841 10841   3  19     0       34
    ##  Content Rating       1    10840 10841   4  12     0        6
    ##     Current Ver       1    10840 10841   1  50     0     2833
    ##          Genres       0    10841 10841   4  37     0      120
    ##        Installs       0    10841 10841   1  13     0       21
    ##    Last Updated       0    10841 10841   6  18     0     1378
    ##           Price       0    10841 10841   1   8     0       93
    ##            Size       0    10841 10841   2  18     0      462
    ##            Type       0    10841 10841   1   4     0        4
    ## 
    ## ── Variable type:numeric ────────────────────────────────────────────────────────────────────
    ##  variable missing complete     n      mean         sd p0 p25    p50
    ##    Rating    1474     9367 10841      4.19       0.54  1   4    4.3
    ##   Reviews       1    10840 10841 444152.9  2927760.6   0  38 2094  
    ##      p75     p100     hist
    ##      4.5 19       ▁▇▁▁▁▁▁▁
    ##  54775.5  7.8e+07 ▇▁▁▁▁▁▁▁

For our predictor variables, it looks like there occasionally one or two
observations missing, which does not raise lots of concern. It is worth
noting, however, that 1474 of our response variable values are missing.
This is roughly 10% of the data. Given that the data was web scrapped,
we will assume that the reason behind the 10% missing is that there was
not a mean rating value for that observation (app), thus we will omit
all of the NA values as we are investigating the apps for which do have
ratings.

We also have a lot of predictors that are characters, so we will recode
them as
factors.

    ## Warning: Removed 2 rows containing missing values (geom_bar).

![](regression-analysis_files/figure-gfm/rating-distribution-1.png)<!-- -->

    ## # A tibble: 1 x 2
    ##   `median(Rating)` `IQR(Rating)`
    ##              <dbl>         <dbl>
    ## 1              4.3           0.5

    ## # A tibble: 33 x 2
    ##    Category          n
    ##    <fct>         <int>
    ##  1 FAMILY         1747
    ##  2 GAME           1097
    ##  3 TOOLS           734
    ##  4 PRODUCTIVITY    351
    ##  5 MEDICAL         350
    ##  6 COMMUNICATION   328
    ##  7 FINANCE         323
    ##  8 SPORTS          319
    ##  9 PHOTOGRAPHY     317
    ## 10 LIFESTYLE       314
    ## # … with 23 more rows

As shown above, qe determined median and IQR as our summary statistics
because the distribution of `rating` appears to be slightly left-skewed.
The median rating of an app is approximately **4.3** and the IQR is
**0.5**.

To conduct a bivariate analysis, we will be making a pairs plot.

Given the above pairs plot, we will be investigating some relationships
more in depth:
![](regression-analysis_files/figure-gfm/category-rating-1.png)<!-- -->

Although there is some variation in rating between app categories, the
most telling aspect of this exploratory model is the outliers. It
appears that some categories are more suspectible to outliers with low
ratings. More over there are notable discrepancies between minimum
boxplot rating among categories.

![](regression-analysis_files/figure-gfm/reviews-rating-1.png)<!-- -->

Based on the scatterplot above, there is likely **not** a relationship
between number of reviews and app rating. As the number of reviews
increased the app rating was concentrated at approximately 4.5 - which
was consistent with apps holding smaller number of reviews.

![](regression-analysis_files/figure-gfm/installs-rating-1.png)<!-- -->

The boxplot above clearly shows a significant relationship between
number of installs and rating. As the number of installs increases the
IQR appears to decrease in conjunction. Moreover median rating also
increases with number of installs.

![](regression-analysis_files/figure-gfm/type-rating-1.png)<!-- -->

The boxplots for free and paid apps sport nearly identical median and
IQR values. This tells us that whether an app is free or paid doesn’t
appear to have a major impact on the rating. Further analysis into the
variation of rating among apps of different price levels is needed.
