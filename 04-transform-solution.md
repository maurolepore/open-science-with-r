Transform
================

<https://github.com/maurolepore/open-science-with-r>

## Setup

It’s common to start a script using required packages and importing the
data. Use the dplyr package with `library(dplyr)`, or all tidyverse
packages with

``` r
library(tidyverse)
```

    ## ── Attaching packages ──────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.0
    ## ✓ tidyr   1.1.0     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ─────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

Import `gapminder`: A global dataset of life-expectancy through time.

``` r
gapminder <- read_csv("data/gapminder.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   country = col_character(),
    ##   year = col_double(),
    ##   pop = col_double(),
    ##   continent = col_character(),
    ##   lifeExp = col_double(),
    ##   gdpPercap = col_double()
    ## )

Preview the `gapminder` dataset with

``` r
gapminder
```

    ## # A tibble: 1,704 x 6
    ##    country      year      pop continent lifeExp gdpPercap
    ##    <chr>       <dbl>    <dbl> <chr>       <dbl>     <dbl>
    ##  1 Afghanistan  1952  8425333 Asia         28.8      779.
    ##  2 Afghanistan  1957  9240934 Asia         30.3      821.
    ##  3 Afghanistan  1962 10267083 Asia         32.0      853.
    ##  4 Afghanistan  1967 11537966 Asia         34.0      836.
    ##  5 Afghanistan  1972 13079460 Asia         36.1      740.
    ##  6 Afghanistan  1977 14880372 Asia         38.4      786.
    ##  7 Afghanistan  1982 12881816 Asia         39.9      978.
    ##  8 Afghanistan  1987 13867957 Asia         40.8      852.
    ##  9 Afghanistan  1992 16317921 Asia         41.7      649.
    ## 10 Afghanistan  1997 22227415 Asia         41.8      635.
    ## # … with 1,694 more rows

## The pipe operator (`%>%`)

Tidyverse functions work well with the pipe operator (`%>%`). The pipe
makes it easier to understand multiple transformations on the same data.

When you apply a single function to a dataset, the pipe is needless.

``` r
# `f` of `x`.
f(x)

# Take `x`, then apply `f`.
x %>% 
  f()
```

When you apply multiple functions to a dataset, the pipe is more
readable.

``` r
# Hard to read: `h` of `g` of `f` of `x`
h(g(f(x)))

# Easy to read: Take `x`, then apply `f`, then apply `g`, then apply `h`.
x %>% 
  f() %>% 
  g() %>% 
  h()
```

## Your turn

This is one other way to view the `gapminder` data.

``` r
glimpse(gapminder)
```

    ## Rows: 1,704
    ## Columns: 6
    ## $ country   <chr> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan",…
    ## $ year      <dbl> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997,…
    ## $ pop       <dbl> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 1…
    ## $ continent <chr> "Asia", "Asia", "Asia", "Asia", "Asia", "Asia", "Asia", "As…
    ## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.…
    ## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134,…

  - Rewrite the code above to produce the same output but this time use
    the pipe.
  - Insert the pipe with *Ctrl+Shift+M* on Windows, or *Cmd+Shift+M* on
    Mac.

<!-- end list -->

``` r
gapminder %>% glimpse()
```

    ## Rows: 1,704
    ## Columns: 6
    ## $ country   <chr> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan",…
    ## $ year      <dbl> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997,…
    ## $ pop       <dbl> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 1…
    ## $ continent <chr> "Asia", "Asia", "Asia", "Asia", "Asia", "Asia", "Asia", "As…
    ## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.…
    ## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134,…

## The five main verzs

Solve the most common data manipulation challenges with the five main
verbs:

  - `mutate()` add columns.
  - `select()` picks columns.
  - `filter()` picks rows.
  - `arrange()` changes the ordering of the rows.
  - `summarise()` summarizes multiple values.

They all input a data frame (spreadsheet) and output a modified data
frame.

## `mutate()` adds new columns that are a function of existing columns

  - Take `gapminder` and then add a new column `gdp` from `pop` times
    `gdpPercap`.

<!-- end list -->

``` r
gapminder %>%
  mutate(gdp = pop * gdpPercap)
```

    ## # A tibble: 1,704 x 7
    ##    country      year      pop continent lifeExp gdpPercap          gdp
    ##    <chr>       <dbl>    <dbl> <chr>       <dbl>     <dbl>        <dbl>
    ##  1 Afghanistan  1952  8425333 Asia         28.8      779.  6567086330.
    ##  2 Afghanistan  1957  9240934 Asia         30.3      821.  7585448670.
    ##  3 Afghanistan  1962 10267083 Asia         32.0      853.  8758855797.
    ##  4 Afghanistan  1967 11537966 Asia         34.0      836.  9648014150.
    ##  5 Afghanistan  1972 13079460 Asia         36.1      740.  9678553274.
    ##  6 Afghanistan  1977 14880372 Asia         38.4      786. 11697659231.
    ##  7 Afghanistan  1982 12881816 Asia         39.9      978. 12598563401.
    ##  8 Afghanistan  1987 13867957 Asia         40.8      852. 11820990309.
    ##  9 Afghanistan  1992 16317921 Asia         41.7      649. 10595901589.
    ## 10 Afghanistan  1997 22227415 Asia         41.8      635. 14121995875.
    ## # … with 1,694 more rows

## `select()` picks columns based on their names

  - Take `gapminder` and then select only `country`, `year`, and
    `lifeExp`.

<!-- end list -->

``` r
gapminder %>% 
  select(country, year, lifeExp)
```

    ## # A tibble: 1,704 x 3
    ##    country      year lifeExp
    ##    <chr>       <dbl>   <dbl>
    ##  1 Afghanistan  1952    28.8
    ##  2 Afghanistan  1957    30.3
    ##  3 Afghanistan  1962    32.0
    ##  4 Afghanistan  1967    34.0
    ##  5 Afghanistan  1972    36.1
    ##  6 Afghanistan  1977    38.4
    ##  7 Afghanistan  1982    39.9
    ##  8 Afghanistan  1987    40.8
    ##  9 Afghanistan  1992    41.7
    ## 10 Afghanistan  1997    41.8
    ## # … with 1,694 more rows

We can instead find all columns in a dataset and drop the irrelevant
ones.

  - Take `gapminder`, and then find the name of all columns with
    `names()`.

<!-- end list -->

``` r
gapminder %>% 
  names()
```

    ## [1] "country"   "year"      "pop"       "continent" "lifeExp"   "gdpPercap"

  - Now take `gapminder`, and then drop each irrelevant column with
    `-column`.

<!-- end list -->

``` r
gapminder %>% 
  select(-continent, -pop, -gdpPercap)
```

    ## # A tibble: 1,704 x 3
    ##    country      year lifeExp
    ##    <chr>       <dbl>   <dbl>
    ##  1 Afghanistan  1952    28.8
    ##  2 Afghanistan  1957    30.3
    ##  3 Afghanistan  1962    32.0
    ##  4 Afghanistan  1967    34.0
    ##  5 Afghanistan  1972    36.1
    ##  6 Afghanistan  1977    38.4
    ##  7 Afghanistan  1982    39.9
    ##  8 Afghanistan  1987    40.8
    ##  9 Afghanistan  1992    41.7
    ## 10 Afghanistan  1997    41.8
    ## # … with 1,694 more rows

## `filter()` pick rows based on their values

  - Take `gapminder`, then `filter()` with the logical expression `year
    == 2002`.

<!-- end list -->

``` r
gapminder %>% 
  filter(year == 2002)
```

    ## # A tibble: 142 x 6
    ##    country      year       pop continent lifeExp gdpPercap
    ##    <chr>       <dbl>     <dbl> <chr>       <dbl>     <dbl>
    ##  1 Afghanistan  2002  25268405 Asia         42.1      727.
    ##  2 Albania      2002   3508512 Europe       75.7     4604.
    ##  3 Algeria      2002  31287142 Africa       71.0     5288.
    ##  4 Angola       2002  10866106 Africa       41.0     2773.
    ##  5 Argentina    2002  38331121 Americas     74.3     8798.
    ##  6 Australia    2002  19546792 Oceania      80.4    30688.
    ##  7 Austria      2002   8148312 Europe       79.0    32418.
    ##  8 Bahrain      2002    656397 Asia         74.8    23404.
    ##  9 Bangladesh   2002 135656790 Asia         62.0     1136.
    ## 10 Belgium      2002  10311970 Europe       78.3    30486.
    ## # … with 132 more rows

`filter()` can take multiple logical expressions separated by “,” or
“&”.

  - Take `gapminder`, and then `filter()` with two logical expressions
    to find the life expectancy of Afghanistan in 1962.

  - Remember the logical operators: `==`, `!=`, `<`, `>`, `<=`, `=>`.

<!-- end list -->

``` r
gapminder %>% 
  filter(country == "Afghanistan" & year == 1962)
```

    ## # A tibble: 1 x 6
    ##   country      year      pop continent lifeExp gdpPercap
    ##   <chr>       <dbl>    <dbl> <chr>       <dbl>     <dbl>
    ## 1 Afghanistan  1962 10267083 Asia         32.0      853.

One way to understand filter is to visualize the logical expressions it
uses.

  - Predict what this code returns; then run it. Explain to yourself
    this result.

<!-- end list -->

``` r
gapminder %>%
  # Drop irrelevant columns
  select(-continent, -pop, -gdpPercap) %>%
  # Add column to see the result of a logical expression I want to use
  mutate(to_pick = country == "Afghanistan" & year == 1962) %>%
  # The logical expression looks good, so I use it
  filter(to_pick)
```

    ## # A tibble: 1 x 4
    ##   country      year lifeExp to_pick
    ##   <chr>       <dbl>   <dbl> <lgl>  
    ## 1 Afghanistan  1962    32.0 TRUE

## `arrange()` changes the ordering of the rows

Where and when was the lowest life expectancy?

  - Take `gapminder`, then arrange it by (ascending) `lifeExp`.

<!-- end list -->

``` r
gapminder %>%
  arrange(lifeExp) %>% 
  select(country, year, lifeExp)
```

    ## # A tibble: 1,704 x 3
    ##    country       year lifeExp
    ##    <chr>        <dbl>   <dbl>
    ##  1 Rwanda        1992    23.6
    ##  2 Afghanistan   1952    28.8
    ##  3 Gambia        1952    30  
    ##  4 Angola        1952    30.0
    ##  5 Sierra Leone  1952    30.3
    ##  6 Afghanistan   1957    30.3
    ##  7 Cambodia      1977    31.2
    ##  8 Mozambique    1952    31.3
    ##  9 Sierra Leone  1957    31.6
    ## 10 Burkina Faso  1952    32.0
    ## # … with 1,694 more rows

Where and when was the highest life expectancy?

  - Take `gapminder`, then arrange it by descending `lifeExp` (see
    `?desc()`).

<!-- end list -->

``` r
gapminder %>%
  arrange(desc(lifeExp)) %>% 
  select(country, year, lifeExp)
```

    ## # A tibble: 1,704 x 3
    ##    country          year lifeExp
    ##    <chr>           <dbl>   <dbl>
    ##  1 Japan            2007    82.6
    ##  2 Hong Kong China  2007    82.2
    ##  3 Japan            2002    82  
    ##  4 Iceland          2007    81.8
    ##  5 Switzerland      2007    81.7
    ##  6 Hong Kong China  2002    81.5
    ##  7 Australia        2007    81.2
    ##  8 Spain            2007    80.9
    ##  9 Sweden           2007    80.9
    ## 10 Israel           2007    80.7
    ## # … with 1,694 more rows

## `summarize()` reduces multiple values to a single summary.

  - Take `gapminder` and then summarize it by computing the mean life
    expectancy.

<!-- end list -->

``` r
gapminder %>% 
  summarize(mean_lifeExp = mean(lifeExp))
```

    ## # A tibble: 1 x 1
    ##   mean_lifeExp
    ##          <dbl>
    ## 1         59.5

This is not terribly useful; `summarize()` is best combined with
`group_by()`.

## group\_by() perform any operation “by group”

Improve the summary you just did:

  - Now calculate life expectancy for each continent.

<!-- end list -->

``` r
gapminder %>%
  group_by(continent) %>% 
  summarize(mean_lifeExp = mean(lifeExp))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 5 x 2
    ##   continent mean_lifeExp
    ##   <chr>            <dbl>
    ## 1 Africa            48.9
    ## 2 Americas          64.7
    ## 3 Asia              60.1
    ## 4 Europe            71.9
    ## 5 Oceania           74.3

## Putting it together

Compare continents before 2000: Did life expectancy increase with total
`gdp`?

``` r
gapminder %>% 
  group_by(continent) %>%
  mutate(gdp = pop * gdpPercap) %>%
  filter(year < 2000) %>% 
  summarize(mean_gdp = mean(gdp), mean_lifeExp = mean(lifeExp)) %>% 
  arrange(desc(mean_lifeExp), desc(mean_gdp))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 5 x 3
    ##   continent      mean_gdp mean_lifeExp
    ##   <chr>             <dbl>        <dbl>
    ## 1 Oceania   150935133957.         73.1
    ## 2 Europe    230367289746.         70.8
    ## 3 Americas  311317615303.         63.0
    ## 4 Asia      164124888658.         58.1
    ## 5 Africa     16977531186.         47.8

## Takeaways

  - The pipe makes it easier to read multiple transformations on the
    same data.

  - You can solve most data manipulation challenges with five dplyr
    verbs:
    
      - `mutate()` adds new variables that are functions of existing
        variables
      - `select()` picks variables based on their names.
      - `filter()` picks cases based on their values.
      - `summarise()` reduces multiple values down to a single summary.
      - `arrange()` changes the ordering of the rows.

  - Combine the main verbs with `group_by()` to perform any operation
    “by group”.
