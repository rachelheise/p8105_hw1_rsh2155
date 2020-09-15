Homework 1
================
Rachel Heise

Homework 1 Assignment

## Problem 1

Start by loading all the required libraries.

``` r
library(tidyverse)
```

    ## -- Attaching packages ------------------------------------------------------------------------------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.3     v dplyr   1.0.2
    ## v tidyr   1.1.2     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts ---------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(ggplot2)
```

Create a data frame that will be used to calculate mean values.

``` r
mean_df <-
  tibble(
    num_vector = rnorm(10),
    logical_vector = num_vector > 0,
    char_vector = c("a", "b", "c", "d", "e", "f", "g", "h", "i", "j"),
    factor_vector = factor(c("cat", "dog", "fish", "cat", "cat", "fish", "dog", "dog", "dog", "fish"))
  )
```

Check whether a mean can be calculated for each column of the data
frame.

``` r
mean(pull(mean_df, num_vector))
```

    ## [1] -0.3812174

``` r
mean(pull(mean_df, logical_vector))
```

    ## [1] 0.2

``` r
mean(pull(mean_df, char_vector))
```

    ## Warning in mean.default(pull(mean_df, char_vector)): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

``` r
mean(pull(mean_df, factor_vector))
```

    ## Warning in mean.default(pull(mean_df, factor_vector)): argument is not numeric
    ## or logical: returning NA

    ## [1] NA

A mean can be calculated for the numerical vector and for the logical
vector, but not for the character vector or the factor vector. Type
coercion occurs for the logical vector which is important to understand.

Next, the logical, character, and factor vectors are converted to
numeric vectors.

``` r
as.numeric(pull(mean_df, logical_vector))
```

    ##  [1] 0 0 0 1 0 0 0 1 0 0

``` r
as.numeric(pull(mean_df, char_vector))
```

    ## Warning: NAs introduced by coercion

    ##  [1] NA NA NA NA NA NA NA NA NA NA

``` r
as.numeric(pull(mean_df, factor_vector))
```

    ##  [1] 1 2 3 1 1 3 2 2 2 3

The logical vector returns values of 0 and 1. The character vector
returns NA values (not available). The factor vector returns values of
1, 2, and 3.

However, you are not able to take a mean of a factor vector because a
value returned for this would have no meaning.

``` r
as.numeric(pull(mean_df, logical_vector)) * pull(mean_df, num_vector)
```

    ##  [1] 0.0000000 0.0000000 0.0000000 1.2536753 0.0000000 0.0000000 0.0000000
    ##  [8] 0.2811225 0.0000000 0.0000000

``` r
as.factor(pull(mean_df, logical_vector)) * pull(mean_df, num_vector)
```

    ## Warning in Ops.factor(as.factor(pull(mean_df, logical_vector)), pull(mean_df, :
    ## '*' not meaningful for factors

    ##  [1] NA NA NA NA NA NA NA NA NA NA

``` r
as.numeric(as.factor(pull(mean_df, logical_vector))) * pull(mean_df, num_vector)
```

    ##  [1] -1.017478656 -0.302048027 -0.428577039  2.507350689 -1.112701206
    ##  [6] -0.011952192 -1.270673630  0.562244944 -1.194879685 -0.008661552

## Problem 2

``` r
data("penguins", package = "palmerpenguins")

nrow(penguins)
```

    ## [1] 344

``` r
ncol(penguins)
```

    ## [1] 8

``` r
mean_flip_length = mean(penguins$flipper_length_mm, na.rm = TRUE)
```

The Penguins data set contains 8 variables. Some of the most useful ones
for consideration are flipper\_length\_mm which has a mean value of
200.92 and a standard deviation of 14.06.

``` r
ggplot(penguins, aes(x = bill_length_mm, y = flipper_length_mm, color = species)) + geom_point()
```

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](homework_1_files/figure-gfm/create_scatterplot-1.png)<!-- -->

``` r
ggsave("penguin_scatterplot", device = "png")
```

    ## Saving 7 x 5 in image

    ## Warning: Removed 2 rows containing missing values (geom_point).
