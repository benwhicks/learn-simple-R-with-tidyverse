
# learn-simple-R-with-tidyverse

The goal of `learn-simple-R-with-tidyverse` is to provide a gentle
inroduction to R, focusing on utilising the `tidyverse` packages. To use
this guide you will need to install [R](https://www.r-project.org/) and
[RStudio](https://rstudio.com/).

## R, Packages and the Tidyverse

R is a statistical programming language supported that is free and
open-source. One of it’s biggest strengths is the community contribution
of ‘packages’, which are collections of code and data wrapped up and
freely distributed for people to use. Because of the freedom in how R is
written there are often multiple ways to do exactly the same thing. This
can be confusing.

The [tidyverse](https://www.tidyverse.org/) is a collection of packages
that follow a similar style of coding, which I find easier to understand
and harder to create weird errors within. There is a solid video
introduction [here](https://www.youtube.com/watch?v=WM2hctrlMts) - just
watch the first half, especially if you are not sure where to type stuff
in RStudio.

To install the tidyverse you need to run the code
`install.packages('tidyverse')`.

To use the tidyvese collection of packages you need to load the
tidyverse.

``` r
# Anything following a # is a comment
# Below we load the tidyverse collection of packages
library(tidyverse)
#> -- Attaching packages -------------------------------------------------------------------------------- tidyverse 1.3.0 --
#> <U+2713> ggplot2 3.2.1     <U+2713> purrr   0.3.3
#> <U+2713> tibble  2.1.3     <U+2713> dplyr   0.8.3
#> <U+2713> tidyr   1.0.0     <U+2713> stringr 1.4.0
#> <U+2713> readr   1.3.1     <U+2713> forcats 0.4.0
#> -- Conflicts ----------------------------------------------------------------------------------- tidyverse_conflicts() --
#> x dplyr::filter() masks stats::filter()
#> x dplyr::lag()    masks stats::lag()
```

Bonus package: You might want to try out the package `lubridate` as well
if you ever have to deal with dates and times. It is not part of the
tidyverse per se but is commonly included in tidyverse style workflow.

## Looking at data, tibbles

R automatically loads in some default data sets. If you type `mtcars` or
`iris` into the console then R will show you the data - which is just a
table of values (called a data frame). The first cool thing about the
tidyverse is the tibble; which is just a souped up version of a data
frame.

``` r
# create tibble versions of the mtcars and iris tables
tib_mtcars <- as_tibble(mtcars)
tib_iris <- as_tibble(iris)

# See how mtcars prints now...
tib_mtcars
#> # A tibble: 32 x 11
#>      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
#>    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
#>  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
#>  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
#>  3  22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
#>  4  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
#>  5  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
#>  6  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
#>  7  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
#>  8  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
#>  9  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
#> 10  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
#> # … with 22 more rows
```

You can also take a closer look in RStudio by typing `View(tib_mtcars)`.
See if you can test out the following examples, but use the `iris` data
set. The ‘pipe’ operator, `%>%`, work like saying ‘take this *and then*
do this’. It’s a bit tricky to type so you can use `Ctrl-Shift-M` to
type it instead.

``` r
names(mtcars) # gets the variable names
#>  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
#> [11] "carb"

mtcars %>% 
  names()  # does the same thing. 
#>  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
#> [11] "carb"

mtcars %>% 
  names   # you can skip the () if no other inputs to the 'names' function are needed
#>  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
#> [11] "carb"

tib_mtcars %>% 
  select(mpg, disp, hp)
#> # A tibble: 32 x 3
#>      mpg  disp    hp
#>    <dbl> <dbl> <dbl>
#>  1  21    160    110
#>  2  21    160    110
#>  3  22.8  108     93
#>  4  21.4  258    110
#>  5  18.7  360    175
#>  6  18.1  225    105
#>  7  14.3  360    245
#>  8  24.4  147.    62
#>  9  22.8  141.    95
#> 10  19.2  168.   123
#> # … with 22 more rows

tib_mtcars %>% 
  select(starts_with('c'))
#> # A tibble: 32 x 2
#>      cyl  carb
#>    <dbl> <dbl>
#>  1     6     4
#>  2     6     4
#>  3     4     1
#>  4     6     1
#>  5     8     2
#>  6     6     1
#>  7     8     4
#>  8     4     2
#>  9     4     2
#> 10     6     4
#> # … with 22 more rows

# get the first 3 rows
tib_mtcars %>% 
  slice(1:3)
#> # A tibble: 3 x 11
#>     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
#>   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
#> 1  21       6   160   110  3.9   2.62  16.5     0     1     4     4
#> 2  21       6   160   110  3.9   2.88  17.0     0     1     4     4
#> 3  22.8     4   108    93  3.85  2.32  18.6     1     1     4     1

# Order by 
```
