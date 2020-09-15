Homework 1
================
Rachel Heise

Homework 1 Assignment

# Problem 1

Start by calling the tidyverse package.

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

Create a data frame that will be used to calculate mean values.

``` r
mean_df = tibble(
  num_vector = rnorm(n = 10),
  logical_vector = c(num_vector > 0),
  char_vector = c('this', 'is', 'a', 'character', 'vector', 'of', 'length', 'ten', 'called', 'char_vector'),
  factor_vector = factor(c('cat', 'dog', 'fish', 'cat', 'cat', 'fish', 'dog', 'dog', 'dog', 'fish'))
)
```

Check whether a mean can be calculated for each column of the data
frame.

``` r
mean(mean_df$num_vector)
```

    ## [1] 0.2129172

``` r
mean(mean_df$logical_vector)
```

    ## [1] 0.6

``` r
mean(mean_df$char_vector)
```

    ## Warning in mean.default(mean_df$char_vector): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

``` r
mean(mean_df$factor_vector)
```

    ## Warning in mean.default(mean_df$factor_vector): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

A mean can be calculated for the standard normal column and for the
logical vector, but not for the character vector or the factor vector.

Here, the logical, character, and factor vectors are converted to
numeric vectors.

``` r
as.numeric(mean_df$logical_vector)
```

    ##  [1] 0 0 1 1 1 1 0 1 1 0

The logical vector returns 0 and 1 values.

``` r
as.numeric(mean_df$char_vector)
```

    ## Warning: NAs introduced by coercion

    ##  [1] NA NA NA NA NA NA NA NA NA NA

The character vector returns NA values (not available).

``` r
as.numeric(mean_df$factor_vector)
```

    ##  [1] 1 2 3 1 1 3 2 2 2 3

The factor vector returns values of 1, 2, and 3, based on which factor
was selected. However, you are not able to take a mean of a factor
vector because a value returned for this would have no meaning.

``` r
log_to_num = as.numeric(mean_df$logical_vector)
log_to_num * mean_df$num_vector
```

    ##  [1] 0.00000000 0.00000000 0.53060277 0.02837313 1.94822064 0.15559426
    ##  [7] 0.00000000 0.60587615 1.36997352 0.00000000

``` r
log_to_fact = as.factor(mean_df$logical_vector)
log_to_fact * mean_df$num_vector
```

    ## Warning in Ops.factor(log_to_fact, mean_df$num_vector): '*' not meaningful for
    ## factors

    ##  [1] NA NA NA NA NA NA NA NA NA NA

``` r
log_fact_num = as.numeric(log_to_fact)
log_fact_num * mean_df$num_vector
```

    ##  [1] -1.79036919 -0.07538741  1.06120554  0.05674626  3.89644127  0.31118851
    ##  [7] -0.07997616  1.21175231  2.73994704 -0.56373536

# Problem 2

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
library(ggplot2)

penguin_scatterplot = ggplot(penguins, aes(x = bill_length_mm, y = flipper_length_mm, color = species)) + geom_point()

ggsave("penguin_scatterplot", device = "png")
```

    ## Saving 7 x 5 in image

    ## Warning: Removed 2 rows containing missing values (geom_point).
