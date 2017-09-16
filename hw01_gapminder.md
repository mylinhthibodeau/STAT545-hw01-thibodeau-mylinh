HW1-Gapminder-Exercises
================
My Linh Thibodeau
2017-09-16

Learn how to access gapminder data with RStudio
-----------------------------------------------

Resources used: <http://rstudio-pubs-static.s3.amazonaws.com/116038_0ebe7e3db5dd4f29ac10e0c994373f99.html> <https://github.com/jennybc/googlesheets>

``` r
library("googlesheets")
suppressPackageStartupMessages(library("dplyr"))
gs_gap() %>%
  gs_copy(to = "Gapminder")
```

    ## Successful copy! New sheet is titled "Gapminder".

``` r
gap <- gs_title("Gapminder")
```

    ## Sheet successfully identified: "Gapminder"

``` r
gap %>% gs_browse()
gap %>% gs_browse(ws = "Europe")
africa <- gs_read(gap)
```

    ## Accessing worksheet titled 'Africa'.

    ## Parsed with column specification:
    ## cols(
    ##   country = col_character(),
    ##   continent = col_character(),
    ##   year = col_integer(),
    ##   lifeExp = col_double(),
    ##   pop = col_integer(),
    ##   gdpPercap = col_double()
    ## )

``` r
glimpse(africa)
```

    ## Observations: 624
    ## Variables: 6
    ## $ country   <chr> "Algeria", "Algeria", "Algeria", "Algeria", "Algeria...
    ## $ continent <chr> "Africa", "Africa", "Africa", "Africa", "Africa", "A...
    ## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992...
    ## $ lifeExp   <dbl> 43.077, 45.685, 48.303, 51.407, 54.518, 58.014, 61.3...
    ## $ pop       <int> 9279525, 10270856, 11000948, 12760499, 14760787, 171...
    ## $ gdpPercap <dbl> 2449.008, 3013.976, 2550.817, 3246.992, 4182.664, 49...

``` r
gap %>% gs_read(ws="Americas", range = cell_rows(3:6))
```

    ## Accessing worksheet titled 'Americas'.

    ## Parsed with column specification:
    ## cols(
    ##   Argentina = col_character(),
    ##   Americas = col_character(),
    ##   `1957` = col_integer(),
    ##   `64.399` = col_double(),
    ##   `19610538` = col_integer(),
    ##   `6856.856` = col_double()
    ## )

    ## # A tibble: 3 x 6
    ##   Argentina Americas `1957` `64.399` `19610538` `6856.856`
    ##       <chr>    <chr>  <int>    <dbl>      <int>      <dbl>
    ## 1 Argentina Americas   1962   65.142   21283783   7133.166
    ## 2 Argentina Americas   1967   65.634   22934225   8052.953
    ## 3 Argentina Americas   1972   67.065   24779799   9443.039
