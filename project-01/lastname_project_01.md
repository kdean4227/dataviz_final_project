---
title: "Mini-Project 01 Kyle Dean"
output: 
  html_document:
    keep_md: true
    toc: true
    toc_float: true
---

# Data Visualization Project 01

_revised version of mini-project 01 goes here_

By Kyle Dean


```r
library(tidyverse)
```

```
## -- Attaching packages -------------------------------------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.2     v purrr   0.3.4
## v tibble  3.0.3     v dplyr   1.0.2
## v tidyr   1.1.2     v stringr 1.4.0
## v readr   1.3.1     v forcats 0.5.0
```

```
## -- Conflicts ----------------------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(ggplot2)
library(dplyr)
```



```r
fuel <- read_csv("https://raw.githubusercontent.com/reisanar/datasets/master/fuel.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_double(),
##   make = col_character(),
##   model = col_character(),
##   class = col_character(),
##   drive = col_character(),
##   transmission = col_character(),
##   transmission_type = col_character(),
##   engine_descriptor = col_character(),
##   turbocharger = col_logical(),
##   supercharger = col_logical(),
##   fuel_type = col_character(),
##   fuel_type_1 = col_character(),
##   fuel_type_2 = col_logical(),
##   gas_guzzler_tax = col_logical(),
##   my_mpg_data = col_character(),
##   start_stop_technology = col_logical(),
##   alternative_fuel_technology = col_character(),
##   electric_motor = col_logical(),
##   manufacturer_code = col_logical(),
##   gasoline_electricity_blended_cd = col_logical(),
##   vehicle_charger = col_logical()
##   # ... with 2 more columns
## )
```

```
## See spec(...) for full column specifications.
```

```r
fuel
```

```
## # A tibble: 38,113 x 81
##    vehicle_id  year make  model class drive transmission transmission_ty~
##         <dbl> <dbl> <chr> <chr> <chr> <chr> <chr>        <chr>           
##  1      26587  1984 Alfa~ GT V~ Mini~ <NA>  Manual 5-Sp~ <NA>            
##  2      27705  1984 Alfa~ GT V~ Mini~ <NA>  Manual 5-Sp~ <NA>            
##  3      26561  1984 Alfa~ Spid~ Two ~ <NA>  Manual 5-Sp~ <NA>            
##  4      27681  1984 Alfa~ Spid~ Two ~ <NA>  Manual 5-Sp~ <NA>            
##  5      27550  1984 AM G~ DJ P~ Spec~ 2-Wh~ Automatic 3~ <NA>            
##  6      28426  1984 AM G~ DJ P~ Spec~ 2-Wh~ Automatic 3~ <NA>            
##  7      27549  1984 AM G~ FJ8c~ Spec~ 2-Wh~ Automatic 3~ <NA>            
##  8      28425  1984 AM G~ FJ8c~ Spec~ 2-Wh~ Automatic 3~ <NA>            
##  9      27593  1984 Amer~ Eagl~ Spec~ 4-Wh~ Automatic 3~ <NA>            
## 10      28455  1984 Amer~ Eagl~ Spec~ 4-Wh~ Automatic 3~ <NA>            
## # ... with 38,103 more rows, and 73 more variables: engine_index <dbl>,
## #   engine_descriptor <chr>, engine_cylinders <dbl>, engine_displacement <dbl>,
## #   turbocharger <lgl>, supercharger <lgl>, fuel_type <chr>, fuel_type_1 <chr>,
## #   fuel_type_2 <lgl>, city_mpg_ft1 <dbl>, unrounded_city_mpg_ft1 <dbl>,
## #   city_mpg_ft2 <dbl>, unrounded_city_mpg_ft2 <dbl>,
## #   city_gasoline_consumption_cd <dbl>, city_electricity_consumption <dbl>,
## #   city_utility_factor <dbl>, highway_mpg_ft1 <dbl>,
## #   unrounded_highway_mpg_ft1 <dbl>, highway_mpg_ft2 <dbl>,
## #   unrounded_highway_mpg_ft2 <dbl>, highway_gasoline_consumption_cd <dbl>,
## #   highway_electricity_consumption <dbl>, highway_utility_factor <dbl>,
## #   unadjusted_city_mpg_ft1 <dbl>, unadjusted_highway_mpg_ft1 <dbl>,
## #   unadjusted_city_mpg_ft2 <dbl>, unadjusted_highway_mpg_ft2 <dbl>,
## #   combined_mpg_ft1 <dbl>, unrounded_combined_mpg_ft1 <dbl>,
## #   combined_mpg_ft2 <dbl>, unrounded_combined_mpg_ft2 <dbl>,
## #   combined_electricity_consumption <dbl>,
## #   combined_gasoline_consumption_cd <dbl>, combined_utility_factor <dbl>,
## #   annual_fuel_cost_ft1 <dbl>, annual_fuel_cost_ft2 <dbl>,
## #   gas_guzzler_tax <lgl>, save_or_spend_5_year <dbl>,
## #   annual_consumption_in_barrels_ft1 <dbl>,
## #   annual_consumption_in_barrels_ft2 <dbl>, tailpipe_co2_ft1 <dbl>,
## #   tailpipe_co2_in_grams_mile_ft1 <dbl>, tailpipe_co2_ft2 <dbl>,
## #   tailpipe_co2_in_grams_mile_ft2 <dbl>, fuel_economy_score <dbl>,
## #   ghg_score <dbl>, ghg_score_alt_fuel <dbl>, my_mpg_data <chr>,
## #   x2d_passenger_volume <dbl>, x2d_luggage_volume <dbl>,
## #   x4d_passenger_volume <dbl>, x4d_luggage_volume <dbl>,
## #   hatchback_passenger_volume <dbl>, hatchback_luggage_volume <dbl>,
## #   start_stop_technology <lgl>, alternative_fuel_technology <chr>,
## #   electric_motor <lgl>, manufacturer_code <lgl>,
## #   gasoline_electricity_blended_cd <lgl>, vehicle_charger <lgl>,
## #   alternate_charger <lgl>, hours_to_charge_120v <dbl>,
## #   hours_to_charge_240v <dbl>, hours_to_charge_ac_240v <dbl>,
## #   composite_city_mpg <dbl>, composite_highway_mpg <dbl>,
## #   composite_combined_mpg <dbl>, range_ft1 <dbl>, city_range_ft1 <dbl>,
## #   highway_range_ft1 <dbl>, range_ft2 <lgl>, city_range_ft2 <dbl>,
## #   highway_range_ft2 <dbl>
```


```r
fuelMake <- fuel %>%
  count(make)
```



```r
fuelMake1 <- fuelMake[c(1:round(nrow(fuelMake)/3),digits = 0),]
fuelMake2 <- fuelMake[c((round(nrow(fuelMake)/3)+1):floor(nrow(fuelMake)*2/3)),]
fuelMake3 <- fuelMake[c((floor(nrow(fuelMake)*2/3)+1):nrow(fuelMake)),]
```


```r
ggplot(fuelMake1, aes(x = make, y = n)) +
  geom_col() +
  coord_flip() +
  theme(legend.position = "none") +
  labs(x = "Maker of car", y = "Count")
```

![](lastname_project_01_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
ggplot(fuelMake2, aes(x = make, y = n)) +
  geom_col() +
  coord_flip() +
  theme(legend.position = "none") +
  labs(x = "Maker of car", y = "Count")
```

![](lastname_project_01_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

```r
ggplot(fuelMake3, aes(x = make, y = n)) +
  geom_col() +
  coord_flip() +
  theme(legend.position = "none") +
  labs(x = "Maker of car", y = "Count")
```

![](lastname_project_01_files/figure-html/unnamed-chunk-7-1.png)<!-- -->
Made a clearner version of the columns


```r
fuelAnnual <- fuel %>%
  count(annual_fuel_cost_ft1)
```

```r
fuelAnnual$PriceBracket <- c(1:60)
```

```r
fuelAnnual$CostCount <- c(1:60)
```


```r
CostVec <- c(1:60)
for(i in 1:60){
  CostVec[i] <- fuelAnnual$annual_fuel_cost_ft1[i] * fuelAnnual$n[i]
}
CostVec
```

```
##  [1]     500    9900   20400   16250   20300   38250   16000  114750   45000
## [10]   66500   66000  259350  216700  685400  520800  642500  820300 1225800
## [19] 1734600 2045950 2497500  280550 2664000 3986400  476000 4278750    5400
## [28] 4704550 1328100 4580550 2204000 4044650 2452800  172000 3724600 3426750
## [37]   46000 7463600  268800 5210000   76500   57200 1653600 2524500   13750
## [46] 1288000 1502200 1200000    3100 1008000 1114750   13800 1099000  569800
## [55]  159900  229500  134850   28200   21200   30250
```

```r
fuelAnnual$CostCount <- CostVec
```

```r
fuelAnnual
```

```
## # A tibble: 60 x 4
##    annual_fuel_cost_ft1     n PriceBracket CostCount
##                   <dbl> <int>        <int>     <dbl>
##  1                  500     1            1       500
##  2                  550    18            2      9900
##  3                  600    34            3     20400
##  4                  650    25            4     16250
##  5                  700    29            5     20300
##  6                  750    51            6     38250
##  7                  800    20            7     16000
##  8                  850   135            8    114750
##  9                  900    50            9     45000
## 10                  950    70           10     66500
## # ... with 50 more rows
```



```r
Vec <- c(1:60)
for(i in 1:nrow(fuelAnnual)){
  if(fuelAnnual$CostCount[i] < (sum((fuelAnnual$CostCount))/60)){
    Vec <- replace(Vec, i, "Below Average")
  }
  if(fuelAnnual$CostCount[i] >= (mean((fuelAnnual$CostCount))/60)){
    Vec <- replace(Vec, i, "Above Average")
  }
}
Vec
```

```
##  [1] "Below Average" "Below Average" "Below Average" "Below Average"
##  [5] "Below Average" "Above Average" "Below Average" "Above Average"
##  [9] "Above Average" "Above Average" "Above Average" "Above Average"
## [13] "Above Average" "Above Average" "Above Average" "Above Average"
## [17] "Above Average" "Above Average" "Above Average" "Above Average"
## [21] "Above Average" "Above Average" "Above Average" "Above Average"
## [25] "Above Average" "Above Average" "Below Average" "Above Average"
## [29] "Above Average" "Above Average" "Above Average" "Above Average"
## [33] "Above Average" "Above Average" "Above Average" "Above Average"
## [37] "Above Average" "Above Average" "Above Average" "Above Average"
## [41] "Above Average" "Above Average" "Above Average" "Above Average"
## [45] "Below Average" "Above Average" "Above Average" "Above Average"
## [49] "Below Average" "Above Average" "Above Average" "Below Average"
## [53] "Above Average" "Above Average" "Above Average" "Above Average"
## [57] "Above Average" "Above Average" "Above Average" "Above Average"
```

```r
fuelAnnual$PriceBracket <- Vec
```


```r
max(fuelAnnual$CostCount)
```

```
## [1] 7463600
```


```r
ggplot(fuelAnnual, aes(x = annual_fuel_cost_ft1, y = n, color = CostCount)) + 
  geom_point(size = 3) +
  facet_wrap(~ PriceBracket) +
  scale_color_gradientn(colours = hcl.colors(25)) +
  theme(legend.position = "none") +
  labs(y = "", x = "")
```

![](lastname_project_01_files/figure-html/unnamed-chunk-17-1.png)<!-- -->
Got a much better color for the map, made the points bigger, and removed the ugly legend




