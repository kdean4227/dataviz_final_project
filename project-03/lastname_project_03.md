---
title: "Visualizing Text and Distributions Kyle Dean"
output: 
  html_document:
    keep_md: true
    toc: true
    toc_float: true
---

By Kyle Dean

# Data Visualization Project 03


In this exercise you will explore methods to visualize text data and practice how to recreate charts that show the distributions of a continuous variable. 


## Part 1: Density Plots

Using the dataset obtained from FSU's [Florida Climate Center](https://climatecenter.fsu.edu/climate-data-access-tools/downloadable-data), for a station at Tampa International Airport (TPA) from 2016 to 2017, attempt to recreate the charts shown below


```r
library(tidyverse)
weather_tpa <- read_csv("https://github.com/reisanar/datasets/raw/master/tpa_weather_16_17.csv")
# random sample 
weather_tpa
```

```
## # A tibble: 367 x 6
##     year month   day precipitation max_temp min_temp
##    <dbl> <dbl> <dbl>         <dbl>    <dbl>    <dbl>
##  1  2016     1     1          0          81       70
##  2  2016     1     2          0          73       59
##  3  2016     1     3          0.18       61       50
##  4  2016     1     4          0          66       49
##  5  2016     1     5          0          68       49
##  6  2016     1     6          0          67       54
##  7  2016     1     7          0          72       56
##  8  2016     1     8          0.54       76       63
##  9  2016     1     9          0.65       78       62
## 10  2016     1    10          0          72       56
## # ... with 357 more rows
```

See https://www.reisanar.com/slides/relationships-models#10 for a reminder on how to use this dataset with the `lubridate` package for dates and times.


```r
library(lubridate)
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(ggplot2)
library(ggridges)
```

```
## Warning: package 'ggridges' was built under R version 4.0.5
```

```r
library(dplyr)
```

(a) Recreate the plot below:

<img src="https://github.com/reisanar/figs/raw/master/tpa_max_temps_facet.png" width="80%" style="display: block; margin: auto;" />

```r
ggplot(weather_tpa, aes(x = max_temp, fill = month)) +
  geom_histogram(binwidth = 3, colour = "grey100", size = 1.3) +
  facet_wrap(vars(month)) +
  scale_fill_gradientn(colours = hcl.colors(12)) +
  theme(legend.position = "none") +
  labs(x = "Maximum Temperature", y = "Number of days")
```

![](lastname_project_03_files/figure-html/unnamed-chunk-5-1.png)<!-- -->


Hint: the option `binwidth = 3` was used with the `geom_histogram()` function.

(b) Recreate the plot below:

<img src="https://github.com/reisanar/figs/raw/master/tpa_max_temps_density.png" width="80%" style="display: block; margin: auto;" />


```r
ggplot(weather_tpa, aes(x = max_temp)) +
  geom_density(kernal = "cosine", adjust = 1/6.5, fill = "grey33", colour = "grey3", size = 1.3) +
  labs(x = "Maximum Temperature", y = "Density")
```

```
## Warning: Ignoring unknown parameters: kernal
```

![](lastname_project_03_files/figure-html/unnamed-chunk-7-1.png)<!-- -->


Hint: check the `kernel` parameter of the `geom_density()` function, and use `bw = 0.5`.

(c) Recreate the chart below:

<img src="https://github.com/reisanar/figs/raw/master/tpa_max_temps_density_facet.png" width="80%" style="display: block; margin: auto;" />


```r
ggplot(weather_tpa, aes(x = max_temp, fill = month)) +
  geom_density() +
  facet_wrap(vars(month)) +
  scale_fill_gradientn(colours = hcl.colors(12)) +
  theme(legend.position = "none") +
  labs(x = "Maximum Temperature", title = "Density Plots for each month in 2016")
```

![](lastname_project_03_files/figure-html/unnamed-chunk-9-1.png)<!-- -->


Hint: default options for `geom_density()` were used. 

(d) Recreate the chart below:

<img src="https://github.com/reisanar/figs/raw/master/tpa_max_temps_ridges.png" width="80%" style="display: block; margin: auto;" />


```r
ggplot(weather_tpa, aes(x = max_temp, y = as.factor(month))) +
  geom_density() +
  geom_density_ridges(aes(fill = month), quantile_lines = TRUE, quantiles = 2, bandwidth = 1.75) +
  scale_fill_gradientn(colours = hcl.colors(12)) +
  labs(x = "Maximum Temperature", y = "") +
  theme(legend.position = "none")
```

![](lastname_project_03_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

Hint: default options for `geom_density()` were used. 

(e) Recreate the plot below:

<img src="https://github.com/reisanar/figs/raw/master/tpa_max_temps_ridges.png" width="80%" style="display: block; margin: auto;" />


```r
ggplot(weather_tpa, aes(x = max_temp, y = as.factor(month))) +
  geom_density_ridges(aes(fill = month), quantile_lines = TRUE, quantiles = 2, bandwidth = 1.75) +
  scale_fill_gradientn(colours = hcl.colors(12)) +
  labs(x = "Maximum Temperature", y = "") +
  theme(legend.position = "none")
```

![](lastname_project_03_files/figure-html/unnamed-chunk-13-1.png)<!-- -->


Hint: use the`ggridges` package, and the `geom_density_ridges()` function paying close attention to the `quantile_lines` and `quantiles` parameters.

(f) Recreate the chart below:

<img src="https://github.com/reisanar/figs/raw/master/tpa_max_temps_ridges_plasma.png" width="80%" style="display: block; margin: auto;" />


```r
ggplot(weather_tpa, aes(x = max_temp, y = as.factor(month), fill = stat(x))) +
  geom_density_ridges_gradient(quantile_lines = TRUE, quantiles = 2, scale = 3, rel_min_height = 0.01) +
  scale_fill_viridis_c(name = "Temp. [F]", option = "plasma") +
  labs(x = 'Maximum Temperature (in Fahrenheit degree)')
```

```
## Picking joint bandwidth of 1.49
```

![](lastname_project_03_files/figure-html/unnamed-chunk-15-1.png)<!-- -->


Hint: this uses the `plasma` option (color scale) for the _viridis_ palette.




## Part 2: Visualizing Text Data

Review the set of slides (and additional resources linked in it) for visualizing text data: https://www.reisanar.com/slides/text-viz#1

Choose any dataset with text data, and create at least one visualization with it. For example, you can create a frequency count of most used bigrams, a sentiment analysis of the text data, a network visualization of terms commonly used together, and/or a visualization of a topic modeling approach to the problem of identifying words/documents associated to different topics in the text data you decide to use. 

Make sure to include a copy of the dataset in the `data/` folder, and reference your sources if different from the ones listed below:

- [Billboard Top 100 Lyrics](https://github.com/reisanar/datasets/blob/master/BB_top100_2015.csv)

- [RateMyProfessors comments](https://github.com/reisanar/datasets/blob/master/rmp_wit_comments.csv)

- [FL Poly News 2020](https://github.com/reisanar/datasets/blob/master/poly_news_FL20.csv)

- [FL Poly News 2019](https://github.com/reisanar/datasets/blob/master/poly_news_FL19.csv)

(to get the "raw" data from any of the links listed above, simply click on the `raw` button of the GitHub page and copy the URL to be able to read it in your computer using the `read_csv()` function)
