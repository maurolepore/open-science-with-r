R, RStudio and RMarkdown
================

<https://github.com/maurolepore/open-science-with-r>

## R Notebooks

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you
execute code within the notebook, the results appear beneath the code.

R code goes in **code chunks**, denoted by three backticks. Try
executing this chunk by clicking the *Run* button within the chunk or by
placing your cursor inside it and pressing *Crtl+Shift+Enter* (Windows)
or *Cmd+Shift+Enter* (Mac).

## Setup

The “setup” chunk always runs before anything else.

``` r
# install.packages("tidyverse")
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

## Warm up

Explore the R console. What do you expect the following to output?

``` r
3 * 4
```

    ## [1] 12

You can assign the result of this calculation to an “object” `x`, using:

``` r
x <- 3 * 4
x
```

    ## [1] 12

What do you expect the following lines to output?

``` r
x + 8
```

    ## [1] 20

``` r
x ** 2
```

    ## [1] 144

Preview: What do you expect this to return?

``` r
x < 13
```

    ## [1] TRUE

## Comments

In R, lines that are preceded by a hash symbol, `#`, will not be run:

``` r
# If you execute this chunk, 
# nothing will happen
# This is a good way to write notes directly in your code to explain things

# Even if I write commands that look like R commands
# x <- 1 + 2
```

Notice that `x` hasn’t changed; it still has the value we initially
assigned it.

``` r
x
```

    ## [1] 12

## Naming Objects

Object names cannot start with a digit and cannot contain certain
characters such as a comma or a space. A common convention adopted in
naming R object is “snakecase” (<https://style.tidyverse.org/>).

``` r
this_object_is_named_using_snake_case <- 3 * 4

this_object_is_named_using_snake_case
```

    ## [1] 12

``` r
# other.people.use.periods
# evenOthersUseCamelCase
```

## Object types

So far we worked mostly with numbers, but R can handle many types of
objects:

``` r
some_text <- "this is called a string"
typeof(some_text)
```

    ## [1] "character"

``` r
a_number <- 12
typeof(a_number)
```

    ## [1] "double"

``` r
true_or_false <- TRUE
typeof(true_or_false)
```

    ## [1] "logical"

  - `strings` are where we store text, denoted by quotation marks.
  - `doubles` are where we store numeric data.
  - `logicals` are where we store the result of a logical operation.

These are the most common types of data; but you will see others, such
as matrices, as you progress through R\!

## Logical operators and expressions

We can ask true or false questions about objects in R.

### Exercise

  - Experiment to find out the meaning of each each logical operator.

<!-- end list -->

``` r
a_number <- 12
```

``` r
# `==` means 'is equal to'
a_number == 12
```

    ## [1] TRUE

``` r
a_number == 10
```

    ## [1] FALSE

`!=` means means ‘not equal to’

``` r
a_number != 12
```

    ## [1] FALSE

``` r
a_number != 10
```

    ## [1] TRUE

`<` means …

`>` means …

`<=` means …

`>=` means …

## Vectors

An object doesn’t need to have only one value in it. We can store
multiple values in a vector:

``` r
weight_kg <- 57.5
weight_lb <- weight_kg * 2.2

# a vector
weights <- c(weight_kg, weight_lb)
weights
```

    ## [1]  57.5 126.5

``` r
names <- c("Jamie", "Melanie", "Julie")
names
```

    ## [1] "Jamie"   "Melanie" "Julie"

``` r
names[1]
```

    ## [1] "Jamie"

## Exercise

1.  Create a vector that contains the different weights of four fish
    (you pick the object name\!):

<!-- end list -->

  - one fish: 12 kg
  - two fish: 34 kg
  - red fish: 20 kg
  - blue fish: 6.6 kg

<!-- end list -->

2.  Convert the vector of kilos to pounds (hint: 1 kg = 2.2 pounds).
3.  Calculate the total weight. (hint: type `?sum` in the console)

## Functions

There are many ways to calculate the sum of the vector you made above.
One of them is by using the `sum()` function.

  - Functions take arguments and return values.
  - Some functions take no arguments (e.g. `date()`)
  - Functions have help files which can be found by calling
    `?function()`

### Exercise

Using the code chunk below, call the documentation for the following
functions, and try to figure out what they do (I have done the first one
for you): \* `min()` \* `max()` \* `mean()` \* `log()`

``` r
# Hint, you can use the arrows above the help file viewer to scroll between each
# help file you've called.

# ?min
min(c(1,2,3,4,5))
```

    ## [1] 1

``` r
# ?max
max(c(1,2,3,4,5))
```

    ## [1] 5

``` r
# ?mean
mean(c(1,2,3,4,5))
```

    ## [1] 3

``` r
# ?log
# It defaults to the natural logarithm
log(exp(1))
```

    ## [1] 1

``` r
# If you want log base 10 use `log10()`
log10(10)
```

    ## [1] 1

## Packages

So far, the functions we have seen exist in “base R”. This means, they
are all installed automatically when you install R. You can install many
other packages from [CRAN](https://cran.r-project.org/) with the
function `install.packages()`. For example, you can install the package
praise with

``` r
install.packages("praise")
```

    ## Installing package into '/home/rstudio-user/R/x86_64-pc-linux-gnu-library/4.0'
    ## (as 'lib' is unspecified)

You can then use an installed package in the current R session with
`library()`. For example, you can use the package praise with

``` r
library(praise)

praise()
```

    ## [1] "You are solid!"

## R Markdown

This whole time, we have been editing an R Markdown file, and keeping
track of our code directly in this file. RMarkdown files allow you to
document and execute reproducible research.

### Exercise

Try clicking the `Knit` button at the top of the page, and see what
happens.

## Clearing your History

As you’ve made your way through this document, RStudio will now be
cluttered with various objects. For the sake of reproducibility, it is
always good to remove all objects (and prove that you can get back to
the same result from scratch).

The best way to do this by restarting your R sessionwith
*Ctrl+Shift+F10* or from the menu *Session \> Restart R*.

# Take aways

R, RStudio and RMarkdown can help you make your research reproducible:

  - R is like a car engine; it comes with some useful functions, known
    as base R.
  - RStudio is like a car body; it providing an interface to interact
    with R.
  - RMarkdown is like a map; it documents how you got where you are.
