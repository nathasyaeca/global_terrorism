world_terrorism
================
Nathasya Pramudita
2023-10-05

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.3.1

    ## Warning: package 'ggplot2' was built under R version 4.3.1

    ## Warning: package 'tibble' was built under R version 4.3.1

    ## Warning: package 'tidyr' was built under R version 4.3.1

    ## Warning: package 'readr' was built under R version 4.3.1

    ## Warning: package 'purrr' was built under R version 4.3.1

    ## Warning: package 'dplyr' was built under R version 4.3.1

    ## Warning: package 'stringr' was built under R version 4.3.1

    ## Warning: package 'forcats' was built under R version 4.3.1

    ## Warning: package 'lubridate' was built under R version 4.3.1

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.2     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.2     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.1     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(plotly)
```

    ## Warning: package 'plotly' was built under R version 4.3.1

    ## 
    ## Attaching package: 'plotly'
    ## 
    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     last_plot
    ## 
    ## The following object is masked from 'package:stats':
    ## 
    ##     filter
    ## 
    ## The following object is masked from 'package:graphics':
    ## 
    ##     layout

``` r
library(extrafont)
```

    ## Registering fonts with R

``` r
world_terrorism <- read.csv("~/Datasets/global_terorism_db/global_terrorism_clean.csv")
```

``` r
world_terrorism.v1 <- world_terrorism %>% 
  select(country, year, latitude, longitude, success, attack_type, target) %>%
  drop_na()
```

``` r
geo_properties = list(
  showland = TRUE,
  showsubunits = FALSE,
  landcolor = toRGB('gray10'),
  showlakes = TRUE,
  lakecolor = toRGB('white')
)
```

``` r
terrorism_graph <- plot_geo(world_terrorism.v1,
                            lat = ~latitude,
                            lon = ~longitude,
                            marker = list(size = 2, color = "#FF0000", opacity = 0.2)) %>%
  add_markers(hoverinfo = "none") %>%
  config(displayModeBar = FALSE) %>% 
  layout(font = list(family = "Retroica"),
         title = "Terrorism Across the World\nFrom 1970 - 2020",
         text = "National Consortium for the Study of Terrorism and Responses to Terrorism (START)",
         geo = geo_properties)
```
