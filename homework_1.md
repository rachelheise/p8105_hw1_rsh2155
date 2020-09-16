Homework 1
================
Rachel Heise

P8105 Homework 1

## Problem 1

Start by loading all the required libraries.

``` r
library(tidyverse)
```

    ## -- Attaching packages ------------------------------------ tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.3     v dplyr   1.0.2
    ## v tidyr   1.1.2     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts --------------------------------------- tidyverse_conflicts() --
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

    ## [1] 0.1358661

``` r
mean(pull(mean_df, logical_vector))
```

    ## [1] 0.5

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
as.numeric(pull(mean_df, char_vector))
as.numeric(pull(mean_df, factor_vector))
```

The logical vector returns values of 0 and 1, which is the numeric
version of this boolean. The character vector returns NA values (not
available) because letters or words cannot be converted to numbers.
Finally, the factor vector returns values of 1, 2, and 3, because R
orders the factors numerically.

However, you are not able to take a mean of a factor vector because a
value returned for this would have no meaning.

``` r
as.numeric(pull(mean_df, logical_vector)) * pull(mean_df, num_vector)
```

    ##  [1] 0.61352161 0.00000000 0.00000000 0.00000000 0.00000000 1.31001444
    ##  [7] 0.84182240 0.00000000 0.86237216 0.09496868

``` r
as.factor(pull(mean_df, logical_vector)) * pull(mean_df, num_vector)
```

    ## Warning in Ops.factor(as.factor(pull(mean_df, logical_vector)), pull(mean_df, :
    ## '*' not meaningful for factors

    ##  [1] NA NA NA NA NA NA NA NA NA NA

``` r
as.numeric(as.factor(pull(mean_df, logical_vector))) * pull(mean_df, num_vector)
```

    ##  [1]  1.2270432 -0.2829971 -0.3798851 -0.1612546 -0.3916889  2.6200289
    ##  [7]  1.6836448 -1.1482123  1.7247443  0.1899374

## Problem 2

``` r
data("penguins", package = "palmerpenguins")
```

The Penguins data set contains 8 variables and 344 observations. Several
are quite useful for consideration: flipper\_length\_mm has a mean value
of 200.92 and a standard deviation of 14.06. There are 3 species,
including Adelie, Chinstrap, Gentoo. Finally, the years seen range from
2007 to 2009.

``` r
print(ggplot(penguins, aes(x = bill_length_mm, y = flipper_length_mm, color = species)) + geom_point())
```

![](homework_1_files/figure-gfm/create_scatterplot-1.png)<!-- -->

``` r
ggsave("penguin_scatterplot", device = "png")
```

    ## Saving 7 x 5 in image
