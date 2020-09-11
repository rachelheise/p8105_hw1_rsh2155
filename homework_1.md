Homework 1
================
Rachel Heise

Homework 1 Assignment

# Problem 1

Start by calling the tidyverse package.

``` r
library(tidyverse)
```

    ## -- Attaching packages ---------------------------------------------------------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.3     v dplyr   1.0.2
    ## v tidyr   1.1.2     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts ------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

Create a data frame that will be used to calculate mean values.

``` r
mean_df = tibble(
  std_normal = rnorm(n = 10),
  positive_num = c(std_normal > 0),
  char_vector = c('this', 'is', 'a', 'character', 'vector', 'of', 'length', 'ten', 'called', 'char_vector'),
  factor_vector = factor(c('cat', 'dog', 'fish', 'cat', 'cat', 'fish', 'dog', 'dog', 'dog', 'fish'))
)
```

Check whether a mean can be calculated for each column of the data
frame.

``` r
mean(mean_df$std_normal)
```

    ## [1] 0.1328913

``` r
mean(mean_df$positive_num)
```

    ## [1] 0.5

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
as.numeric(mean_df$positive_num)
```

    ##  [1] 1 0 1 0 0 1 1 1 0 0

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

# Problem 2
