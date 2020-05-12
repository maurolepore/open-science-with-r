Visualization
================

Explore <https://ggplot2.tidyverse.org/> and try what it says under
Usage.

``` r
library(ggplot2)

ggplot(mpg, aes(displ, hwy, colour = class)) +
  geom_point()
```

![](03-visualize_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

## Setup

The setup chunk always runs before anything else.

``` r
# install.packages("tidyverse")
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ tibble  3.0.1     ✓ dplyr   0.8.5
    ## ✓ tidyr   1.0.3     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0
    ## ✓ purrr   0.3.4

    ## ── Conflicts ────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

## Data

Copy-paste.

``` r
# National Parks in California
ca <- read_csv("https://bit.ly/03-data-ca")
```

    ## Parsed with column specification:
    ## cols(
    ##   region = col_character(),
    ##   state = col_character(),
    ##   code = col_character(),
    ##   park_name = col_character(),
    ##   type = col_character(),
    ##   visitors = col_double(),
    ##   year = col_double()
    ## )

``` r
# Acadia National Park
acadia <- read_csv("https://bit.ly/03-data-acadia")
```

    ## Parsed with column specification:
    ## cols(
    ##   region = col_character(),
    ##   state = col_character(),
    ##   code = col_character(),
    ##   park_name = col_character(),
    ##   type = col_character(),
    ##   visitors = col_double(),
    ##   year = col_double()
    ## )

``` r
# Southeast US National Parks
se <- read_csv("https://bit.ly/03-data-se")
```

    ## Parsed with column specification:
    ## cols(
    ##   region = col_character(),
    ##   state = col_character(),
    ##   code = col_character(),
    ##   park_name = col_character(),
    ##   type = col_character(),
    ##   visitors = col_double(),
    ##   year = col_double()
    ## )

``` r
# 2016 Visitation for all Pacific West National Parks
visit_16 <- read_csv("https://bit.ly/03-data-visit-16")
```

    ## Parsed with column specification:
    ## cols(
    ##   region = col_character(),
    ##   state = col_character(),
    ##   code = col_character(),
    ##   park_name = col_character(),
    ##   type = col_character(),
    ##   visitors = col_double(),
    ##   year = col_double()
    ## )

``` r
# All Nationally designated sites in Massachusetts
mass <- read_csv("https://bit.ly/03-data-mass")
```

    ## Parsed with column specification:
    ## cols(
    ##   region = col_character(),
    ##   state = col_character(),
    ##   code = col_character(),
    ##   park_name = col_character(),
    ##   type = col_character(),
    ##   visitors = col_double(),
    ##   year = col_double()
    ## )

Preview the data with `View()` and `head()`.

``` r
head(ca)
```

    ## # A tibble: 6 x 7
    ##   region state code  park_name                     type          visitors  year
    ##   <chr>  <chr> <chr> <chr>                         <chr>            <dbl> <dbl>
    ## 1 PW     CA    CHIS  Channel Islands National Park National Park     1200  1963
    ## 2 PW     CA    CHIS  Channel Islands National Park National Park     1500  1964
    ## 3 PW     CA    CHIS  Channel Islands National Park National Park     1600  1965
    ## 4 PW     CA    CHIS  Channel Islands National Park National Park      300  1966
    ## 5 PW     CA    CHIS  Channel Islands National Park National Park    15700  1967
    ## 6 PW     CA    CHIS  Channel Islands National Park National Park    31000  1968

## Build

  - Adapt the first example. Plot the data ca, with year on x and
    visitors on y.
  - What relationship do you expect to see between year and the number
    of visitors?

<!-- end list -->

``` r
ggplot(data = ca, aes(x = year, y = visitors)) +
  geom_point()
```

![](03-visualize_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

  - Now map the values of the variable `park_name` to the `color`
    aesthetics.

<!-- end list -->

``` r
ggplot(ca, aes(year, visitors, color = park_name)) +
  geom_point()
```

![](03-visualize_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

## Customizing

  - <https://ggplot2.tidyverse.org/reference/index.html#section-scales>
  - <https://ggplot2.tidyverse.org/reference/index.html#section-themes>

<!-- end list -->

``` r
ggplot(ca, aes(year, visitors, color = park_name)) +
  geom_point() +
  labs(title = "Acadia National Park Visitation", y = "Visitation", x = "Year") +
  theme_bw()
```

![](03-visualize_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

## Faceting

Now using data from Southeast US National Parks.

``` r
ggplot(se, aes(year, visitors)) +
  geom_point() +
  facet_wrap(~ state)
```

![](03-visualize_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

## Geoms

### Discrete x

data = se

  - Create a scatterplot of `park_name` (x) versus `visitors` (y).
  - Is this a good plot?

<!-- end list -->

``` r
ggplot(data = se, aes(x = park_name, y = visitors)) + 
  geom_point()
```

![](03-visualize_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

  - Create a jitter plot.

<!-- end list -->

``` r
ggplot(se, aes(park_name, visitors)) + 
  geom_jitter()
```

![](03-visualize_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

  - Create a boxplot.

<!-- end list -->

``` r
ggplot(se, aes(x = park_name, y = visitors)) + 
  geom_boxplot()
```

![](03-visualize_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

### Time series

data = acadia

  - Create a scatter plot
  - Add lines
  - Add a smoothed mean
  - Move the smoothed mean to become the second layer. What subtle thing
    happened?

<!-- end list -->

``` r
ggplot(acadia, aes(year, visitors)) + 
  geom_point() +
  geom_line() +
  geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](03-visualize_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

### Bar charts

data = visit\_16

  - Create a columns bar chart where the height of the columns represent
    `visotors` (y) per `state` (x).

<!-- end list -->

``` r
ggplot(visit_16, aes(state, visitors)) + 
  geom_col()
```

![](03-visualize_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

  - Map the bar fill (colour) to `park_name`.

<!-- end list -->

``` r
ggplot(visit_16, aes(state, visitors, fill = park_name)) + 
  geom_col()
```

![](03-visualize_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

### Position adjustments

  - Now dodge the position of the bars to compare them side by side.

<!-- end list -->

``` r
ggplot(visit_16, aes(state, visitors, fill = park_name)) + 
  geom_col(position = "dodge")
```

![](03-visualize_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

  - Dodge the bars to allow side by side comparison.

<!-- end list -->

``` r
ggplot(visit_16, aes(state, visitors, fill = park_name)) + 
  geom_col(position = "dodge")
```

![](03-visualize_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

## Arranging and exporting plots

data = mass

  - Export the last plot with RStudio and `ggsave()`.

<!-- end list -->

``` r
my_plot <- ggplot(visit_16, aes(state, visitors, fill = park_name)) + 
  geom_col(position = "dodge")

ggsave(filename = "03-my_plot.pdf", my_plot)
```

    ## Saving 7 x 5 in image

## Leftovers

## Set vs map

  - Set the colour of all points to blue.

<!-- end list -->

``` r
ggplot(data = ca) +
  geom_point(mapping = aes(x = year, y = visitors), color = "blue")
```

![](03-visualize_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

  - What is wrong in this code?

<!-- end list -->

``` r
ggplot(data = ca) +
  geom_point(mapping = aes(x = year, y = visitors, color = "blue"))
```

![](03-visualize_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

## Facet

  - Add `facet_wrap(~ park_name)` to facet (split) the data by
    `park_name`. The plot is now clear evern without colour.

(I’ll ommit the name of the first arguments. They are optional.)

``` r
ggplot(ca) +
  geom_point(aes(x = year, y = visitors)) +
  facet_wrap(~ park_name)
```

![](03-visualize_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

## Geoms

  - Instead of representing you data with points, we now use a smooth
    mean of the data.

<!-- end list -->

``` r
ggplot(ca) +
  geom_smooth(aes(x = year, y = visitors)) 
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](03-visualize_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

(Smoothers fit a model to your data and then plot predictions from the
model.)

  - Use `geom_line()` and `color = park_name` to compare each park
    against the overall trend.

<!-- end list -->

``` r
ggplot(ca) +
  geom_line(aes(x = year, y = visitors, color = park_name)) +
  geom_smooth(aes(x = year, y = visitors)) 
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](03-visualize_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

  - Use `geom_bar()` to create a bar chart FIXME

<!-- end list -->

``` r
ggplot(ca) +
  geom_bar(aes(x = park_name))
```

![](03-visualize_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

(Bar charts, histograms, and frequency polygons bin your data and then
plot bin counts, the number of points that fall in each bin.)

## Arranging and exporting plots

-----

# Take aways

You can use this code template to make thousands of graphs with
**ggplot2**.

``` r
ggplot(data = <DATA>) +
  <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>))
```
