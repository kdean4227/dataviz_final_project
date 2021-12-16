---
title: "Mini-Project 02 Kyle Dean"
output: 
  html_document:
    keep_md: true
    toc: true
    toc_float: true
---

# Data Visualization Project 02

_revised version of mini-project 02 goes here_

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
library(gapminder)
```

```
## Warning: package 'gapminder' was built under R version 4.0.5
```

```r
library(plotly)
```

```
## 
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggplot2':
## 
##     last_plot
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```

```
## The following object is masked from 'package:graphics':
## 
##     layout
```

```r
library(sf)
```

```
## Warning: package 'sf' was built under R version 4.0.5
```

```
## Linking to GEOS 3.9.1, GDAL 3.2.1, PROJ 7.2.1
```


```r
Billboard <- read_csv("https://raw.githubusercontent.com/reisanar/datasets/master/all_billboard_summer_hits.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_double(),
##   key = col_character(),
##   mode = col_character(),
##   track_uri = col_character(),
##   key_mode = col_character(),
##   playlist_name = col_character(),
##   playlist_img = col_character(),
##   track_name = col_character(),
##   artist_name = col_character(),
##   album_name = col_character(),
##   album_img = col_character()
## )
```

```
## See spec(...) for full column specifications.
```


```r
Bill2001 <- filter(Billboard, playlist_name == "summer_hits_2001")
```

```r
Bill2001Plot <- ggplot(
  data = Bill2001,
  mapping = aes(x = danceability, y = loudness, 
                color = mode)) +
  geom_point(aes(text = key_mode), size = 5) +
  scale_x_log10() +
  theme_minimal()
```

```
## Warning: Ignoring unknown aesthetics: text
```

```r
ggplotly(Bill2001Plot)
```

<!--html_preserve--><div id="htmlwidget-320a078cefca1c4a5418" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-320a078cefca1c4a5418">{"x":{"data":[{"x":[-0.182434630440219,-0.274905478918531,-0.329754146925876,-0.151195298948196,-0.193141970481183],"y":[-4.938,-4.95,-5.862,-6.347,-4.98],"text":["F# major<br />danceability: 0.657<br />loudness: -4.938<br />mode: major","C# major<br />danceability: 0.531<br />loudness: -4.950<br />mode: major","C major<br />danceability: 0.468<br />loudness: -5.862<br />mode: major","G major<br />danceability: 0.706<br />loudness: -6.347<br />mode: major","C major<br />danceability: 0.641<br />loudness: -4.980<br />mode: major"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(248,118,109,1)","opacity":1,"size":18.8976377952756,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)"}},"hoveron":"points","name":"major","legendgroup":"major","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[-0.0414361167780325,-0.156144577376839,-0.0757207139381184,-0.224753740259764,-0.185086818724926],"y":[-4.278,-5.319,-4.386,-6.239,-7.519],"text":["G# minor<br />danceability: 0.909<br />loudness: -4.278<br />mode: minor","F minor<br />danceability: 0.698<br />loudness: -5.319<br />mode: minor","C# minor<br />danceability: 0.840<br />loudness: -4.386<br />mode: minor","F minor<br />danceability: 0.596<br />loudness: -6.239<br />mode: minor","B minor<br />danceability: 0.653<br />loudness: -7.519<br />mode: minor"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(0,191,196,1)","opacity":1,"size":18.8976377952756,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(0,191,196,1)"}},"hoveron":"points","name":"minor","legendgroup":"minor","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.2283105022831,"r":7.30593607305936,"b":40.1826484018265,"l":37.2602739726027},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.344170048433268,-0.0270202152706404],"tickmode":"array","ticktext":["0.5","0.6","0.7"],"tickvals":[-0.301029995663981,-0.221848749616356,-0.154901959985743],"categoryorder":"array","categoryarray":["0.5","0.6","0.7"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"danceability","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-7.68105,-4.11595],"tickmode":"array","ticktext":["-7","-6","-5"],"tickvals":[-7,-6,-5],"categoryorder":"array","categoryarray":["-7","-6","-5"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"loudness","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.93503937007874},"annotations":[{"text":"mode","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"3474764a6868":{"text":{},"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"3474764a6868","visdat":{"3474764a6868":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
interactive_plot <- ggplotly(
  Bill2001Plot, tooltip = "text"
) 
interactive_plot
```

<!--html_preserve--><div id="htmlwidget-6dfb22e3e36650154e95" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-6dfb22e3e36650154e95">{"x":{"data":[{"x":[-0.182434630440219,-0.274905478918531,-0.329754146925876,-0.151195298948196,-0.193141970481183],"y":[-4.938,-4.95,-5.862,-6.347,-4.98],"text":["F# major","C# major","C major","G major","C major"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(248,118,109,1)","opacity":1,"size":18.8976377952756,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)"}},"hoveron":"points","name":"major","legendgroup":"major","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[-0.0414361167780325,-0.156144577376839,-0.0757207139381184,-0.224753740259764,-0.185086818724926],"y":[-4.278,-5.319,-4.386,-6.239,-7.519],"text":["G# minor","F minor","C# minor","F minor","B minor"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(0,191,196,1)","opacity":1,"size":18.8976377952756,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(0,191,196,1)"}},"hoveron":"points","name":"minor","legendgroup":"minor","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.2283105022831,"r":7.30593607305936,"b":40.1826484018265,"l":37.2602739726027},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.344170048433268,-0.0270202152706404],"tickmode":"array","ticktext":["0.5","0.6","0.7"],"tickvals":[-0.301029995663981,-0.221848749616356,-0.154901959985743],"categoryorder":"array","categoryarray":["0.5","0.6","0.7"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"danceability","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-7.68105,-4.11595],"tickmode":"array","ticktext":["-7","-6","-5"],"tickvals":[-7,-6,-5],"categoryorder":"array","categoryarray":["-7","-6","-5"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"loudness","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.93503937007874},"annotations":[{"text":"mode","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"34742cad82e":{"text":{},"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"34742cad82e","visdat":{"34742cad82e":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
htmlwidgets::saveWidget(interactive_plot, "fancy_plot.html")
```



```r
Billboard_cor <- Billboard %>% 
  select(danceability, energy, speechiness, acousticness, instrumentalness) %>% 
  cor()
# only consider upper triangular part of
# correlation matrix
Billboard_cor[lower.tri(Billboard_cor)] <- NA
# format the matrix of correlation
Billboard_cor_long <- Billboard_cor %>% 
  as.data.frame() %>% 
  rownames_to_column("Variable2") %>% 
  pivot_longer(cols = -Variable2,
               names_to = "Variable1",
               values_to = "cor") %>% 
  mutate(nice_cor = round(cor, 2)) %>% 
  mutate(Variable1 = fct_inorder(Variable1),
         Variable2 = fct_inorder(Variable2)) %>% 
  filter(!is.na(cor)) %>% 
  filter(Variable2 != Variable1)
```


```r
ggplot(Billboard_cor_long, 
       aes(x = Variable2, 
           y = Variable1, 
           fill = cor)) +
  geom_tile() +
  geom_text(aes(label = nice_cor)) +
  scale_fill_gradient2(
    low = "#F63719", 
    mid = "white", 
    high = "#3B9AB2", 
    limits = c(-1, 1)
    ) +
  labs(x = NULL, y = NULL) +
  coord_equal() +
  theme_minimal() +
  theme(panel.grid = element_blank(), legend.position = "none")
```

![](lastname_project_02_files/figure-html/unnamed-chunk-8-1.png)<!-- -->












