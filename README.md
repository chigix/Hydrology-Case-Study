Hydrology Case Study
================

Attempt of Exploratory Data Analysis in Hydrology Case Studies.

## Initial Setup

[RENV
workflow](https://rstudio.github.io/renv/articles/renv.html#workflow-1)
is employed here:

``` r
# `renv.lock` is used to store and restore all library dependencies.
> renv::restore()

# Snapshot the environment everytime new packages are installed or updated.
> renv::snapshot()
```

## Data Sets

-   `map("lakes")`
    -   The World Lakes Database provided by [the R Package
        `maps`](https://search.r-project.org/CRAN/refmans/maps/html/lakes.html)
        available in CRAN.

``` r
map_data("world") %>%
ggplot(aes(long, lat)) +
  geom_polygon(aes(group=group)) +
  coord_quickmap()
```

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
lakes_data <- map_data("lakes")

lakes_data %>%
ggplot(aes(long, lat)) +
  geom_polygon(aes(group=group, fill=region)) +
  coord_quickmap()
```

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
lakes_data %>%
  dplyr::filter(dplyr::across(region, ~ grepl("Great Lakes", .))) %>%
  ggplot(aes(long, lat)) +
  geom_polygon(aes(group=group, fill=as.factor(group))) +
  # coord_quickmap()
  coord_map("albers",  lat0 = 45.5, lat1 = 29.5)
```

![](README_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->
