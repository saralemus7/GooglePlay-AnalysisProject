Understanding Google Play Application Reviews
================
RTime2Shine
12/7/19

## Section 1: Introduction (includes introduction and exploratory data analysis)

### Motivaton

As technology has become increasingly prevalent around the world, there
has been a change in the consumption of media. One of these ways is via
the purchase of applications (apps) for various smartphones and other
devices. Several technology companies, including Apple and Google, run
virtual stores for these apps in which a person can download an app for
their device. These apps can be for various purposes like socializing,
playing games, or watching television and movies, among others. While
any user of a phone can agree that apps hold an important effect on how
one interacts with technology on a daily basis, the weight of the impact
becomes even more shocking when one looks at the figures- in 2018,
global app downloads topped 194 billion (Dignan).

Our motivation for this project is to understand what makes apps (from
the Google Play store specifically) have favorable ratings.
Understanding the ratings of an app is important for several reasons.
First, ratings can be important to the provider- in this case Google-
who can decide whether an app should continue to be sold to maintain
their quality standards. Ratings are additionally useful as a direct
line of communication between the user and the developers- often,
developers are made aware of changes that need to be made to their apps
through user feedback. Lastly, reviews serve to inform potential users
of an app whether or not it is worth their time and can affect future
downloads. Considering that app users are predicted to spend about $120
billion in app stores in 2019, understanding which apps do well on the
Play Store and what factors affect app performance is an immensely
important question to gain more insight into.

### Research Question & Hypothesis

Our ultimate goal is to create a model which most accurately and
concisely predicts the Rating of an app given the predictors in the
dataset. This will enable us to see which predictor variables interact
with each other to effect the rating for a given app. We posit that
examining such relationships will help developers understand what
factors may influence an app’s rating and use that information to create
better applications for consumers. As well, conglomerates such as Google
(whom this dataset is from) can use this information to more accurately
display or promote apps that meet these characteristics or promote ads
related to these apps and generate revenue.

This leads us to introduce our main research question: What are the
relevant factors that affect the rating given for apps in the Google
Play store? Although this project will give a detailed attempt to answer
this question, our preliminary hypothesis is that the variables
Category, Price, Installs, and Content Rating are the predictor
variables that will most affect a given app rating and popularity, as
measured by the number of installs of the app. We believe that these
variables are indicative of an apps useability and likeness (as
determined by variables like content rating and categories in how people
may be drawn to an app) as well as its accessibility (price).
Furthermore, once we test our hypothesis and determine which factors are
relevant, we will attempt to use that information to predict the success
of an app as measured by its rating.

### The Data

The dataset was obtained from Kaggle. According to Kaggle, the dataset
was scraped directly from the Google Play Store in August 2018. Each
observation represents one individual app on the Google Play Store. This
particular dataset has 13 variables with 10841 observations. The
variables consist of various information collected about each
application (which represents a row) in the dataset. This information
includes the apps category in the app store, its average rating, price,
content rating, the number of installs, among other metrics. In our
Exploratory Data Analysis, we will further explain the use of each of
these variables and determine which of these may be significant for and
relevant in our analysis. The response variable in our investigation is
`Rating` which is the mean rating out of 5.0 for an application in the
Google Play Store. This is a numeric variable.

### Exploratory Data Analysis

    ## Skim summary statistics
    ##  n obs: 10841 
    ##  n variables: 13 
    ## 
    ## ── Variable type:character ─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
    ##        variable missing complete     n min max empty n_unique
    ##     Android Ver       1    10840 10841   3  18     0       34
    ##             App       0    10841 10841   1 194     0     9660
    ##        Category       0    10841 10841   3  19     0       34
    ##  Content Rating       1    10840 10841   4  15     0        6
    ##     Current Ver       1    10840 10841   1  50     0     2833
    ##          Genres       0    10841 10841   4  37     0      120
    ##        Installs       0    10841 10841   1  14     0       22
    ##    Last Updated       0    10841 10841   6  18     0     1378
    ##           Price       0    10841 10841   1   8     0       93
    ##            Size       0    10841 10841   3  18     0      462
    ##            Type       0    10841 10841   1   4     0        4
    ## 
    ## ── Variable type:numeric ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
    ##  variable missing complete     n      mean         sd p0 p25    p50
    ##    Rating    1474     9367 10841      4.19       0.54  1   4    4.3
    ##   Reviews       1    10840 10841 444152.9  2927760.6   0  38 2094  
    ##      p75     p100     hist
    ##      4.5 19       ▁▇▁▁▁▁▁▁
    ##  54775.5  7.8e+07 ▇▁▁▁▁▁▁▁

#### Data Wrangling

Upon examining our predictor variables, it looks like there are
occasionally one or two observations missing in the dataset, which does
not raise lots of concern. It is worth noting, however, that 1474 of our
response variable values are missing. This is roughly 10% of the data.
Given that the data was web scraped, we will assume that the reason
behind these missing values is that there was not a mean rating value
for those particular observations (app). Thus, we will omit all of the
NA values and continue to investigate only those apps for which we have
ratings.

Furthermore, here it is worth noting that the variable, `Genres`
contains the same information in the `category` variable - the only
difference being that the data is just displayed a bit differently.
Therefore, as to avoid being redundant, we will only be using `category`
in our analysis. As well, the information contained in the variable
`Type` is also contained in `Price`. Since `Price` provides the prices
of an app and `Type` simply denotes wether or not an app is paid or
free. There is mostly likely a large linear dependency between these two
variables as they measure the same thing, so we will use `Price` instead
of `Type.` We will not deleting theese variables from the dataset as to
maintain integrity, but will not examine them in our analysis.

As well, we also have many of predictors that are coded as characters in
the dataset, so we decided to recode them as factors. We also have some
variables that are coded as characters due to the existence of a
particular a symbol (ex. $), we will recoded these into a format which
will be usable for our analysis.

Looking at the data, there are two variables related to the version, or
iteration of the app as provided by the developers: `Current Ver` and
`Android Ver`. Given that Google owns both Android and the Google Play
Store, the company would likely be more interested in the Android
version of the app. Furthermore, Android users are unlikely to be using
other operating system’s application stores, so a developer who is
interested in creating apps for the Android market would gain more
information through an examination of the compatibility of certain apps
with a particular version of Android. Some data wrangling was necessary
to make this variable suitable for analysis.

We also created a variable called `date_since`, which marks the number
of days that the app has been updated since the day that the data was
scraped on August 8, 2018. This will allow us to determine how recent
the last update was for a particular app and provides some information
related to the relative frequency of updates and how that may affect an
app’s rating.

There are also a number of variables which required releveling. Many of
our predictors have multiple levels and these may have made our model
too complicated. To reduce the probabiltiy that the model overfits the
data and is too complicated, we will relevel our variables as follows:

Since our variable `Price` is currently not numeric and isn’t coded into
categories, we will relevel price into 3 categories: Free, Between 0 and
4.99 dollars, and greater than 5 dollars.

Since our variable `Size` is currently very widely distributed, we will
relevel size into 3 categories: Varies with Device, Less than 100, and
Greater than 100.

Since our variable `Installs` is currently very widely distributed, we
will relevel installs into 3 categories: Less than 100, Between 100 and
1,000, Between 1,000 and 10,000, Between 10,000 and 100,000, and 100,000
or Greater.

Our variable `Category` is extremely large and has many levels as shown
in the graphiic below. To simplify this, we will create a new variable
called `category_simp` with two levels: one for the top 6 categories
(“FAMILY”,“GAME”, “TOOLS”,“MEDICAL”, “LIFESTYLE”, and “FINANCE”) and
another for all the other categories.

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

As shown in the above table, we can see that the top 6 cateogies are in
one level and the others are stored in another
    level.

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
    ## 3 "Mature "        Mature         355
    ## 4 "Everyone "      Everyone       271
    ## 5 "Adults only "   Adults only      3
    ## 6 Unrated          Unrated          1

#### Univariate Analysis

![](final-writeup_files/figure-gfm/rating-distribution-1.png)<!-- -->

    ## # A tibble: 1 x 2
    ##   `median(Rating)` `IQR(Rating)`
    ##              <dbl>         <dbl>
    ## 1              4.2           0.6

![](final-writeup_files/figure-gfm/log%20reviews-1.png)<!-- -->

    ## # A tibble: 1 x 3
    ##   `median(log_reviews)` `max(log_reviews)` `IQR(log_reviews)`
    ##                   <dbl>              <dbl>              <dbl>
    ## 1                  7.55               12.2               5.44

Above is the plot of the logged number of reviews for each application.
We decided to log, due to an extreme skew seen in the plot of the
original variable.

FOR OTHER UNIVARIATE PLOTS ONLY INCLUDE THOSE IN FULL MODEL

Arrange the bars in the barplot of Categories in order of frequency.
This will help the reader more easily distinguish which categories are
the most common.

Which app has 78 million reviews?

Change the bin width on the histogram of date\_since. It should be fine
to just use the default bin width by R.

#### Bivariate Analysis

A bivariate analysis between variables will help understand the
interaction between indidivual predictor variables and the response.

![](final-writeup_files/figure-gfm/category-rating-1.png)<!-- -->

Although there is some variation in rating between app categories, the
most telling aspect of this exploratory model is the outliers. It
appears that some categories are more susceptible to outliers with low
ratings. More over there are notable discrepancies between minimum
boxplot rating among categories.

![](final-writeup_files/figure-gfm/reviews-rating-1.png)<!-- -->

Based on the scatterplot above, there is likely a relationship between
number of reviews and app rating. As the number of reviews increased the
app rating was concentrated at approximately 4.5 - which was consistent
with apps holding smaller number of reviews. IS THIS RIGHT??

![](final-writeup_files/figure-gfm/installs-rating-1.png)<!-- -->

The boxplot above clearly shows a significant relationship between
number of installs and rating. As the number of installs increases the
IQR appears to decrease in conjunction. Moreover median rating also
increases with number of installs.

![](final-writeup_files/figure-gfm/type-rating-1.png)<!-- -->

The boxplots for free and paid apps sport nearly identical median and
IQR values. This tells us that whether an app is free or paid doesn’t
appear to have a major impact on the rating. Further analysis into the
variation of rating among apps of different price levels is needed.

#### Possible Interactions

ONLY INCLUDE THOSE IN FULL
MODEL

## Section 2: Regression Analysis (includes the final model and discussion of assumptions)

### Model Process

The regression modeling technique we will use will be Multiple Linear
Regression (MLR). Since we are exploring the effect of multiple
predictor variables on our response, `rating`, it is apt that we use MLR
to model our data. MLR allows us to see the effect of multiple
predictors on a response and explore both the significance of each
predictor on the response as well as the effect of each predictor on the
response. As opposed to Simple Linear Regression, MLR allows us to
measure the effect of multiple predictors on your response in one model
- SLR only allows us to measure the effect of one predictor on the
response in one model. This is very taxing and inefficient for the
number of predictors we want to measure. As well, there may be
interactions between these predictors that we will be unable to view
using SLR. MLR allows us to both model and view the amalgamation of
these predictors in their effects on the response variable. MLR from
both an efficiency and relevancy perspective is much better suited to
model our data as opposed to other methods.

Our ultimate goal is to create the model which most accurately and
concisely predicts the Rating of an app given the predictors in the
dataset. We will attempt to choose a model using a minimization of both
BIC and AIC as our criteria as this will allow us to calculate a precise
prediction of our response variable while also removing extraneous
predictors. We will use BIC and AIC as our selection criteria as it
penalizes more for erroneous predictors as compared to adj. R-Squared.
We will not use R-squared as a criteria for model selection. R squared
increases strictly as the number of predictors increases and does not
tell us if these additional predictors are significant or not. If we
used r-squared we would always choose models with the largest numbers of
predictors, which would not always produce the simplest, most accurate
model. Unlike R squared, AIC, BIC, and adjusted R squared do penalize
for insignificant predictors and can give us a better idea of which
predictors actually contribute to the response variable.

In order to find our final model, we will use a process of both forwards
and backwards selection slowly adding a combination of relevant
predictors into our model. We will then check the BIC and AIC values for
each of these models and find the model with the lowest value overall,
or the fewest predictors - this will be the model that most accurately
predicts our response with the fewest number of predictors. We will then
plot each predictor on the response to determine if the effect is
relevant or if there are possible interactions between other variables.
As well, we will need to consider potential outliers and extraneous
values in our model. Using the distributions of standardized residuals
and a calculation of Cook’s distance, we will attempt to determine those
observations with high standardized residuals or cook’s distance and
determine if those observations have a significant effect on our model.
Lastly, we will need to find the VIF factor for each of our final
predictors to see if there is any collinearity between them. A VIF
greater than 10 would require us to explore possible ways to mitigate
interactions between variables or consider dropping predictors are are
too heavily
correlated.

### Model Selection

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
|     PriceBetween $0 and $4.99      |  0.1112532  | 0.0255464 |  4.3549494   | 0.0000135 |
|        PriceGreater than $5        |  0.0741875  | 0.0461754 |  1.6066454   | 0.1081732 |
|      `Content Rating`Everyone      | \-0.0548353 | 0.3039831 | \-0.1803892  | 0.8568518 |
|      `Content Rating`Everyone      | \-0.0677175 | 0.3055862 | \-0.2215989  | 0.8246321 |
|       `Content Rating`Mature       | \-0.1521919 | 0.3051383 | \-0.4987637  | 0.6179601 |
|        `Content Rating`Teen        | \-0.0740591 | 0.3044898 | \-0.2432235  | 0.8078387 |
|      `Content Rating`Unrated       |  0.1279921  | 0.6088736 |  0.2102113   | 0.8335083 |
|        androidver\_simp5-8         | \-0.0572665 | 0.0227200 | \-2.5205266  | 0.0117380 |
| androidver\_simpVaries with Device | \-0.0249248 | 0.0378446 | \-0.6586090  | 0.5101666 |
|            date\_since             | \-0.0001225 | 0.0000159 | \-7.7033322  | 0.0000000 |

    ##                        (Intercept)                        log_reviews 
    ##                       4.4912514453                       0.0758591553 
    ##      InstallsBetween 100 and 1,000   InstallsBetween 1,000 and 10,000 
    ##                      -0.3194153798                      -0.6723565620 
    ## InstallsBetween 10,000 and 100,000         Installs100,000 or Greater 
    ##                      -0.8289290318                      -1.0026226107 
    ##          PriceBetween $0 and $4.99            `Content Rating`Mature  
    ##                       0.1046628972                      -0.0878715403 
    ##                         date_since 
    ##                      -0.0001177867

    ##                        (Intercept)                        log_reviews 
    ##                       4.4912514453                       0.0758591553 
    ##      InstallsBetween 100 and 1,000   InstallsBetween 1,000 and 10,000 
    ##                      -0.3194153798                      -0.6723565620 
    ## InstallsBetween 10,000 and 100,000         Installs100,000 or Greater 
    ##                      -0.8289290318                      -1.0026226107 
    ##          PriceBetween $0 and $4.99            `Content Rating`Mature  
    ##                       0.1046628972                      -0.0878715403 
    ##                         date_since 
    ##                      -0.0001177867

Given the BIC forwards and backwards selection our reduced linear model
is:

hat(mean rating) = 4.5124715854 x exp(0.0744108983(log\_reviews)) -
0.3447278672(InstallsBetween 100 and 1,000) -0.6891663588
(InstallsBetween 1,000 and 10,000) - 0.8405412693(InstallsBetween 10,000
and 100,000) -1.0072240860(Installs 100,000 or Greater) +
0.0978316624(PriceBetween 0 and 4.99) -0.0001211124(date\_since)

    ## Start:  AIC=-9894.63
    ## Rating ~ category_simp + log_reviews + Size + Installs + Price + 
    ##     `Content Rating` + androidver_simp + date_since
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## - Size              2     0.599 2132.3 -9896.5
    ## - category_simp     1     0.463 2132.1 -9895.0
    ## <none>                          2131.7 -9894.6
    ## - `Content Rating`  5     3.325 2135.0 -9892.6
    ## - androidver_simp   2     1.808 2133.5 -9892.1
    ## - Price             2     5.701 2137.4 -9878.0
    ## - date_since        1    16.428 2148.1 -9837.4
    ## - log_reviews       1    95.566 2227.2 -9558.1
    ## - Installs          4   122.381 2254.1 -9471.7
    ## 
    ## Step:  AIC=-9896.46
    ## Rating ~ category_simp + log_reviews + Installs + Price + `Content Rating` + 
    ##     androidver_simp + date_since
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## - category_simp     1     0.425 2132.7 -9896.9
    ## <none>                          2132.3 -9896.5
    ## - `Content Rating`  5     3.280 2135.6 -9894.6
    ## - androidver_simp   2     3.889 2136.2 -9886.4
    ## - Price             2     5.686 2138.0 -9879.9
    ## - date_since        1    18.913 2151.2 -9830.3
    ## - log_reviews       1    95.136 2227.4 -9561.5
    ## - Installs          4   122.250 2254.5 -9474.1
    ## 
    ## Step:  AIC=-9896.93
    ## Rating ~ log_reviews + Installs + Price + `Content Rating` + 
    ##     androidver_simp + date_since
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## <none>                          2132.7 -9896.9
    ## - `Content Rating`  5     3.149 2135.8 -9895.5
    ## - androidver_simp   2     3.654 2136.3 -9887.7
    ## - Price             2     5.520 2138.2 -9881.0
    ## - date_since        1    19.387 2152.1 -9829.1
    ## - log_reviews       1    95.482 2228.2 -9560.9
    ## - Installs          4   122.549 2255.2 -9473.7

    ## Start:  AIC=-9224.82
    ## Rating ~ 1
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + Installs          4    63.534 2272.2 -9429.7
    ## + log_reviews       1    34.937 2300.8 -9339.2
    ## + date_since        1    28.974 2306.8 -9319.2
    ## + Price             2     9.927 2325.8 -9253.7
    ## + Size              2     6.307 2329.5 -9241.7
    ## + category_simp     1     1.723 2334.1 -9228.5
    ## + androidver_simp   2     1.773 2334.0 -9226.7
    ## <none>                          2335.8 -9224.8
    ## + `Content Rating`  5     2.784 2333.0 -9224.0
    ## 
    ## Step:  AIC=-9429.69
    ## Rating ~ Installs
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + log_reviews       1   113.172 2159.1 -9822.1
    ## + date_since        1    22.116 2250.1 -9503.2
    ## + Price             2    12.007 2260.2 -9466.6
    ## + Size              2     3.529 2268.7 -9437.7
    ## + category_simp     1     0.793 2271.4 -9430.4
    ## + `Content Rating`  5     3.065 2269.2 -9430.1
    ## <none>                          2272.2 -9429.7
    ## + androidver_simp   2     0.844 2271.4 -9428.6
    ## 
    ## Step:  AIC=-9822.05
    ## Rating ~ Installs + log_reviews
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + date_since        1   14.4627 2144.6 -9871.9
    ## + Size              2    3.6109 2155.5 -9831.0
    ## + Price             2    3.0574 2156.0 -9829.0
    ## + androidver_simp   2    1.5735 2157.5 -9823.7
    ## <none>                          2159.1 -9822.1
    ## + category_simp     1    0.3084 2158.8 -9821.2
    ## + `Content Rating`  5    2.2798 2156.8 -9820.2
    ## 
    ## Step:  AIC=-9871.93
    ## Rating ~ Installs + log_reviews + date_since
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + Price             2    5.4111 2139.2 -9887.4
    ## + androidver_simp   2    3.1047 2141.5 -9879.1
    ## + Size              2    2.1523 2142.5 -9875.7
    ## + `Content Rating`  5    2.9777 2141.6 -9872.7
    ## <none>                          2144.6 -9871.9
    ## + category_simp     1    0.0417 2144.6 -9870.1
    ## 
    ## Step:  AIC=-9887.43
    ## Rating ~ Installs + log_reviews + date_since + Price
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + androidver_simp   2    3.3511 2135.8 -9895.5
    ## + Size              2    2.3133 2136.9 -9891.8
    ## + `Content Rating`  5    2.8459 2136.3 -9887.7
    ## <none>                          2139.2 -9887.4
    ## + category_simp     1    0.1137 2139.1 -9885.8
    ## 
    ## Step:  AIC=-9895.54
    ## Rating ~ Installs + log_reviews + date_since + Price + androidver_simp
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + `Content Rating`  5   3.14927 2132.7 -9896.9
    ## <none>                          2135.8 -9895.5
    ## + category_simp     1   0.29422 2135.6 -9894.6
    ## + Size              2   0.52198 2135.3 -9893.4
    ## 
    ## Step:  AIC=-9896.93
    ## Rating ~ Installs + log_reviews + date_since + Price + androidver_simp + 
    ##     `Content Rating`
    ## 
    ##                 Df Sum of Sq    RSS     AIC
    ## <none>                       2132.7 -9896.9
    ## + category_simp  1   0.42456 2132.3 -9896.5
    ## + Size           2   0.56026 2132.1 -9895.0

    ## Start:  AIC=-9224.82
    ## Rating ~ 1
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + Installs          4    63.534 2272.2 -9429.7
    ## + log_reviews       1    34.937 2300.8 -9339.2
    ## + date_since        1    28.974 2306.8 -9319.2
    ## + Price             2     9.927 2325.8 -9253.7
    ## + Size              2     6.307 2329.5 -9241.7
    ## + category_simp     1     1.723 2334.1 -9228.5
    ## + androidver_simp   2     1.773 2334.0 -9226.7
    ## <none>                          2335.8 -9224.8
    ## + `Content Rating`  5     2.784 2333.0 -9224.0
    ## 
    ## Step:  AIC=-9429.69
    ## Rating ~ Installs
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + log_reviews       1   113.172 2159.1 -9822.1
    ## + date_since        1    22.116 2250.1 -9503.2
    ## + Price             2    12.007 2260.2 -9466.6
    ## + Size              2     3.529 2268.7 -9437.7
    ## + category_simp     1     0.793 2271.4 -9430.4
    ## + `Content Rating`  5     3.065 2269.2 -9430.1
    ## <none>                          2272.2 -9429.7
    ## + androidver_simp   2     0.844 2271.4 -9428.6
    ## - Installs          4    63.534 2335.8 -9224.8
    ## 
    ## Step:  AIC=-9822.05
    ## Rating ~ Installs + log_reviews
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + date_since        1    14.463 2144.6 -9871.9
    ## + Size              2     3.611 2155.5 -9831.0
    ## + Price             2     3.057 2156.0 -9829.0
    ## + androidver_simp   2     1.573 2157.5 -9823.7
    ## <none>                          2159.1 -9822.1
    ## + category_simp     1     0.308 2158.8 -9821.2
    ## + `Content Rating`  5     2.280 2156.8 -9820.2
    ## - log_reviews       1   113.172 2272.2 -9429.7
    ## - Installs          4   141.770 2300.8 -9339.2
    ## 
    ## Step:  AIC=-9871.93
    ## Rating ~ Installs + log_reviews + date_since
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + Price             2     5.411 2139.2 -9887.4
    ## + androidver_simp   2     3.105 2141.5 -9879.1
    ## + Size              2     2.152 2142.5 -9875.7
    ## + `Content Rating`  5     2.978 2141.6 -9872.7
    ## <none>                          2144.6 -9871.9
    ## + category_simp     1     0.042 2144.6 -9870.1
    ## - date_since        1    14.463 2159.1 -9822.1
    ## - log_reviews       1   105.519 2250.1 -9503.2
    ## - Installs          4   137.869 2282.5 -9399.0
    ## 
    ## Step:  AIC=-9887.43
    ## Rating ~ Installs + log_reviews + date_since + Price
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + androidver_simp   2     3.351 2135.8 -9895.5
    ## + Size              2     2.313 2136.9 -9891.8
    ## + `Content Rating`  5     2.846 2136.3 -9887.7
    ## <none>                          2139.2 -9887.4
    ## + category_simp     1     0.114 2139.1 -9885.8
    ## - Price             2     5.411 2144.6 -9871.9
    ## - date_since        1    16.816 2156.0 -9829.0
    ## - log_reviews       1    94.083 2233.3 -9557.2
    ## - Installs          4   121.169 2260.4 -9470.1
    ## 
    ## Step:  AIC=-9895.54
    ## Rating ~ Installs + log_reviews + date_since + Price + androidver_simp
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## + `Content Rating`  5     3.149 2132.7 -9896.9
    ## <none>                          2135.8 -9895.5
    ## + category_simp     1     0.294 2135.6 -9894.6
    ## + Size              2     0.522 2135.3 -9893.4
    ## - androidver_simp   2     3.351 2139.2 -9887.4
    ## - Price             2     5.657 2141.5 -9879.1
    ## - date_since        1    18.541 2154.4 -9830.8
    ## - log_reviews       1    96.003 2231.8 -9558.2
    ## - Installs          4   122.523 2258.4 -9473.0
    ## 
    ## Step:  AIC=-9896.93
    ## Rating ~ Installs + log_reviews + date_since + Price + androidver_simp + 
    ##     `Content Rating`
    ## 
    ##                    Df Sum of Sq    RSS     AIC
    ## <none>                          2132.7 -9896.9
    ## + category_simp     1     0.425 2132.3 -9896.5
    ## - `Content Rating`  5     3.149 2135.8 -9895.5
    ## + Size              2     0.560 2132.1 -9895.0
    ## - androidver_simp   2     3.654 2136.3 -9887.7
    ## - Price             2     5.520 2138.2 -9881.0
    ## - date_since        1    19.387 2152.1 -9829.1
    ## - log_reviews       1    95.482 2228.2 -9560.9
    ## - Installs          4   122.549 2255.2 -9473.7

### Interactions & Our Updated Model

(finish this)

### Assumptions

(finish this)

### Model Assesment

(c/p code from regressions wehn we finish stuff)

### Model Interpretation

Will finish after we get model

## Section 3: Discussion and Limitations

## Section 4: Conclusion

## Section 5: Additional Work

### References

Gupta, Lavanya. Kaggle. Jan. 2019,
www.kaggle.com/lava18/google-play-store-apps?fbclid=IwAR36EMS2jg5fhPi-BQlX6Mv4MCk8YUm2XmyOLt0zsKkNyc9JK-JD7aLy-6I.
Accessed 30 Oct. 2019.

Dignan, Larry. “App Economy Expected to Be $120 Billion in 2019 as Small
Screen Leads Digital Transformation Efforts.” ZDNet, ZDNet, 16
Jan. 2019,
www.zdnet.com/article/app-economy-expected-to-be-120-billion-in-2019-as-small-screen-leads-digital-transformation-efforts/
