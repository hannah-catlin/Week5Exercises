---
title: 'Weekly Exercises #5'
author: "Hannah"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
---





```r
library(tidyverse)     # for data cleaning and plotting
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
library(openintro)     # for the abbr2state() function
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
library(ggmap)         # for mapping points on maps
library(gplots)        # for col2hex() function
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
library(gifski)        # need the library for creating gifs but don't need to load each time
library(shiny)         # for creating interactive apps
theme_set(theme_minimal())
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 

# Lisa's garden data
data("garden_harvest")

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)

# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")

panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")

panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")

#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

## Put your homework on GitHub!

Go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) or to previous homework to remind yourself how to get set up. 

Once your repository is created, you should always open your **project** rather than just opening an .Rmd file. You can do that by either clicking on the .Rproj file in your repository folder on your computer. Or, by going to the upper right hand corner in R Studio and clicking the arrow next to where it says Project: (None). You should see your project come up in that list if you've used it recently. You could also go to File --> Open Project and navigate to your .Rproj file. 

## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  

```r
root_veg_harvest <- garden_harvest %>% 
  filter(vegetable %in% c("radish", "beets", "rutabaga", 
                          "carrots", "kohlrabi", "potatoes")) %>% 
  mutate(veg_caps = str_to_title(vegetable)) %>% 
  ggplot(aes(x = date, y = fct_infreq(veg_caps), color = vegetable)) +
  geom_point(aes(size = weight)) +
  scale_color_manual(values = c("red4", "darkorange1", "olivedrab1", 
                                "darkgoldenrod4", "indianred2", "navajowhite")) +
  labs(title = "Root Vegetable Harvests", size = "weight (g)") +
  xlab("") + ylab ("") +
  guides(color = FALSE)

ggplotly(root_veg_harvest)
```

```{=html}
<div id="htmlwidget-5f32bf8737646ce755b2" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-5f32bf8737646ce755b2">{"x":{"data":[{"x":[18424,18431,18432,18434,18450,18450,18451,18452,18455,18461,18463,18470,18470,18473,18487,18487,18487,18487],"y":[3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3],"text":["weight:    8<br />date: 2020-06-11<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:   25<br />date: 2020-06-18<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:   11<br />date: 2020-06-19<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:   57<br />date: 2020-06-21<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:   62<br />date: 2020-07-07<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:   10<br />date: 2020-07-07<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:   83<br />date: 2020-07-08<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:   69<br />date: 2020-07-09<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:   89<br />date: 2020-07-12<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:  172<br />date: 2020-07-18<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:  107<br />date: 2020-07-20<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:   49<br />date: 2020-07-27<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:  149<br />date: 2020-07-27<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:  101<br />date: 2020-07-30<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:  198<br />date: 2020-08-13<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight:  308<br />date: 2020-08-13<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight: 2209<br />date: 2020-08-13<br />fct_infreq(veg_caps): Beets<br />vegetable: beets","weight: 2476<br />date: 2020-08-13<br />fct_infreq(veg_caps): Beets<br />vegetable: beets"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(139,0,0,1)","opacity":1,"size":[3.77952755905512,5.34793684080615,4.43839124330731,6.44229343729102,6.57484943312878,4.31748750454448,7.07384598031608,6.7505084644133,7.20308368821556,8.65096205435268,7.56441126877068,6.2152448067039,8.29646940703584,7.44792530019736,9.02291251348455,10.368164401577,21.6256950383063,22.6771653543307],"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(139,0,0,1)"}},"hoveron":"points","name":"beets","legendgroup":"beets","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18466,18467,18467,18470,18471,18473,18473,18480,18480,18481,18484,18495,18503,18503,18522,18522,18532,18532,18549,18549],"y":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],"text":["weight:   56<br />date: 2020-07-23<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  178<br />date: 2020-07-24<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:   80<br />date: 2020-07-24<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  174<br />date: 2020-07-27<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  160<br />date: 2020-07-28<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  116<br />date: 2020-07-30<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  107<br />date: 2020-07-30<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  164<br />date: 2020-08-06<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  442<br />date: 2020-08-06<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  255<br />date: 2020-08-07<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  221<br />date: 2020-08-10<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  457<br />date: 2020-08-21<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  888<br />date: 2020-08-29<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  169<br />date: 2020-08-29<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  160<br />date: 2020-09-17<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  168<br />date: 2020-09-17<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  883<br />date: 2020-09-27<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight:  449<br />date: 2020-09-27<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight: 1500<br />date: 2020-10-14<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots","weight: 1023<br />date: 2020-10-14<br />fct_infreq(veg_caps): Carrots<br />vegetable: carrots"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(255,127,0,1)","opacity":1,"size":[6.41498229606389,8.73927319273712,7.00728723199127,8.68057591067601,8.46935363517665,7.73270966456827,7.56441126877068,8.5306611532799,11.7041724053778,9.75790622843011,9.33121164267086,11.8399557556511,15.0638705748626,8.60620060449217,8.46935363517665,8.59118758820027,15.0317671157401,11.7678251937628,18.4728278554957,15.8985604514764],"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(255,127,0,1)"}},"hoveron":"points","name":"carrots","legendgroup":"carrots","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18522],"y":[6],"text":"weight:  191<br />date: 2020-09-17<br />fct_infreq(veg_caps): Kohlrabi<br />vegetable: kohlrabi","type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(192,255,62,1)","opacity":1,"size":8.92541743545246,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(192,255,62,1)"}},"hoveron":"points","name":"kohlrabi","legendgroup":"kohlrabi","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18480,18480,18484,18484,18493,18493,18503,18503,18514,18521,18537,18537,18543,18543,18550,18550,18550,18550,18552],"y":[2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2],"text":["weight:  317<br />date: 2020-08-06<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  439<br />date: 2020-08-06<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  272<br />date: 2020-08-10<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  168<br />date: 2020-08-10<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  323<br />date: 2020-08-19<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  278<br />date: 2020-08-19<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  262<br />date: 2020-08-29<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  716<br />date: 2020-08-29<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  843<br />date: 2020-09-09<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  629<br />date: 2020-09-16<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight: 1596<br />date: 2020-10-02<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  101<br />date: 2020-10-02<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  372<br />date: 2020-10-08<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  436<br />date: 2020-10-08<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight: 1527<br />date: 2020-10-15<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  272<br />date: 2020-10-15<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight: 1718<br />date: 2020-10-15<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  295<br />date: 2020-10-15<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes","weight:  293<br />date: 2020-10-17<br />fct_infreq(veg_caps): Potatoes<br />vegetable: potatoes"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(139,101,8,1)","opacity":1,"size":[10.4662636467078,11.6767355837891,9.96021677543873,8.59118758820027,10.5308712930661,10.0300572884759,9.84202825388115,13.9011835324927,14.7715645396155,13.258925238563,18.9381659195091,7.44792530019736,11.0370040031827,11.6492031071,18.6051805224568,9.96021677543873,19.5096824223434,10.2238296604045,10.2013363907244],"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(139,101,8,1)"}},"hoveron":"points","name":"potatoes","legendgroup":"potatoes","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18419,18424,18426,18433,18434,18446,18450,18456,18470],"y":[5,5,5,5,5,5,5,5,5],"text":["weight:   36<br />date: 2020-06-06<br />fct_infreq(veg_caps): Radish<br />vegetable: radish","weight:   67<br />date: 2020-06-11<br />fct_infreq(veg_caps): Radish<br />vegetable: radish","weight:   53<br />date: 2020-06-13<br />fct_infreq(veg_caps): Radish<br />vegetable: radish","weight:   16<br />date: 2020-06-20<br />fct_infreq(veg_caps): Radish<br />vegetable: radish","weight:   37<br />date: 2020-06-21<br />fct_infreq(veg_caps): Radish<br />vegetable: radish","weight:   88<br />date: 2020-07-03<br />fct_infreq(veg_caps): Radish<br />vegetable: radish","weight:   43<br />date: 2020-07-07<br />fct_infreq(veg_caps): Radish<br />vegetable: radish","weight:   50<br />date: 2020-07-13<br />fct_infreq(veg_caps): Radish<br />vegetable: radish","weight:   39<br />date: 2020-07-27<br />fct_infreq(veg_caps): Radish<br />vegetable: radish"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(238,99,99,1)","opacity":1,"size":[5.79238936288389,6.70139795950959,6.33129563558472,4.85544745003384,5.82801800150006,7.18188499442792,6.02997547039211,6.24476973011442,5.89747798239821],"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(238,99,99,1)"}},"hoveron":"points","name":"radish","legendgroup":"radish","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18551,18551,18552,18552,18552,18553,18553,18553,18553,18553,18553,18553,18553,18553,18553,18553,18553],"y":[4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4],"text":["weight:  883<br />date: 2020-10-16<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight:  740<br />date: 2020-10-16<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight:  932<br />date: 2020-10-17<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight: 1096<br />date: 2020-10-17<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight: 1101<br />date: 2020-10-17<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight: 2001<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight:  673<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight:  144<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight:  366<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight: 1393<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight:  903<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight:  419<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight: 1026<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight: 1350<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight:  297<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight:   52<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga","weight:  114<br />date: 2020-10-18<br />fct_infreq(veg_caps): Rutabaga<br />vegetable: rutabaga"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(255,222,173,1)","opacity":1,"size":[15.0317671157401,14.0713073118498,15.342538289973,16.3268018130633,16.3555998180188,20.7615180133743,13.5890025822752,8.21565891426341,10.9769410964457,17.936155875625,15.159637579197,11.4913292652982,15.9164571379072,17.7146632196816,10.2462446919137,6.30278336553216,7.69593507824901],"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(255,222,173,1)"}},"hoveron":"points","name":"rutabaga","legendgroup":"rutabaga","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":57.716894977169},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Root Vegetable Harvests","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[18412.3,18559.7],"tickmode":"array","ticktext":["Jun","Jul","Aug","Sep","Oct"],"tickvals":[18414,18444,18475,18506,18536],"categoryorder":"array","categoryarray":["Jun","Jul","Aug","Sep","Oct"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,6.6],"tickmode":"array","ticktext":["Carrots","Potatoes","Beets","Rutabaga","Radish","Kohlrabi"],"tickvals":[1,2,3,4,5,6],"categoryorder":"array","categoryarray":["Carrots","Potatoes","Beets","Rutabaga","Radish","Kohlrabi"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.913385826771654},"annotations":[{"text":"weight (g)","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"70944d2693cc":{"size":{},"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"70944d2693cc","visdat":{"70944d2693cc":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

```r
length_v_depth <- penguins %>% 
  ggplot(aes(x = bill_length_mm, y = bill_depth_mm, color = species)) +
  geom_point() +
  theme_minimal()

ggplotly(length_v_depth)
```

```{=html}
<div id="htmlwidget-ed95aa69a7adc80490ea" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-ed95aa69a7adc80490ea">{"x":{"data":[{"x":[39.1,39.5,40.3,null,36.7,39.3,38.9,39.2,34.1,42,37.8,37.8,41.1,38.6,34.6,36.6,38.7,42.5,34.4,46,37.8,37.7,35.9,38.2,38.8,35.3,40.6,40.5,37.9,40.5,39.5,37.2,39.5,40.9,36.4,39.2,38.8,42.2,37.6,39.8,36.5,40.8,36,44.1,37,39.6,41.1,37.5,36,42.3,39.6,40.1,35,42,34.5,41.4,39,40.6,36.5,37.6,35.7,41.3,37.6,41.1,36.4,41.6,35.5,41.1,35.9,41.8,33.5,39.7,39.6,45.8,35.5,42.8,40.9,37.2,36.2,42.1,34.6,42.9,36.7,35.1,37.3,41.3,36.3,36.9,38.3,38.9,35.7,41.1,34,39.6,36.2,40.8,38.1,40.3,33.1,43.2,35,41,37.7,37.8,37.9,39.7,38.6,38.2,38.1,43.2,38.1,45.6,39.7,42.2,39.6,42.7,38.6,37.3,35.7,41.1,36.2,37.7,40.2,41.4,35.2,40.6,38.8,41.5,39,44.1,38.5,43.1,36.8,37.5,38.1,41.1,35.6,40.2,37,39.7,40.2,40.6,32.1,40.7,37.3,39,39.2,36.6,36,37.8,36,41.5],"y":[18.7,17.4,18,null,19.3,20.6,17.8,19.6,18.1,20.2,17.1,17.3,17.6,21.2,21.1,17.8,19,20.7,18.4,21.5,18.3,18.7,19.2,18.1,17.2,18.9,18.6,17.9,18.6,18.9,16.7,18.1,17.8,18.9,17,21.1,20,18.5,19.3,19.1,18,18.4,18.5,19.7,16.9,18.8,19,18.9,17.9,21.2,17.7,18.9,17.9,19.5,18.1,18.6,17.5,18.8,16.6,19.1,16.9,21.1,17,18.2,17.1,18,16.2,19.1,16.6,19.4,19,18.4,17.2,18.9,17.5,18.5,16.8,19.4,16.1,19.1,17.2,17.6,18.8,19.4,17.8,20.3,19.5,18.6,19.2,18.8,18,18.1,17.1,18.1,17.3,18.9,18.6,18.5,16.1,18.5,17.9,20,16,20,18.6,18.9,17.2,20,17,19,16.5,20.3,17.7,19.5,20.7,18.3,17,20.5,17,18.6,17.2,19.8,17,18.5,15.9,19,17.6,18.3,17.1,18,17.9,19.2,18.5,18.5,17.6,17.5,17.5,20.1,16.5,17.9,17.1,17.2,15.5,17,16.8,18.7,18.6,18.4,17.8,18.1,17.1,18.5],"text":["bill_length_mm: 39.1<br />bill_depth_mm: 18.7<br />species: Adelie","bill_length_mm: 39.5<br />bill_depth_mm: 17.4<br />species: Adelie","bill_length_mm: 40.3<br />bill_depth_mm: 18.0<br />species: Adelie","bill_length_mm:   NA<br />bill_depth_mm:   NA<br />species: Adelie","bill_length_mm: 36.7<br />bill_depth_mm: 19.3<br />species: Adelie","bill_length_mm: 39.3<br />bill_depth_mm: 20.6<br />species: Adelie","bill_length_mm: 38.9<br />bill_depth_mm: 17.8<br />species: Adelie","bill_length_mm: 39.2<br />bill_depth_mm: 19.6<br />species: Adelie","bill_length_mm: 34.1<br />bill_depth_mm: 18.1<br />species: Adelie","bill_length_mm: 42.0<br />bill_depth_mm: 20.2<br />species: Adelie","bill_length_mm: 37.8<br />bill_depth_mm: 17.1<br />species: Adelie","bill_length_mm: 37.8<br />bill_depth_mm: 17.3<br />species: Adelie","bill_length_mm: 41.1<br />bill_depth_mm: 17.6<br />species: Adelie","bill_length_mm: 38.6<br />bill_depth_mm: 21.2<br />species: Adelie","bill_length_mm: 34.6<br />bill_depth_mm: 21.1<br />species: Adelie","bill_length_mm: 36.6<br />bill_depth_mm: 17.8<br />species: Adelie","bill_length_mm: 38.7<br />bill_depth_mm: 19.0<br />species: Adelie","bill_length_mm: 42.5<br />bill_depth_mm: 20.7<br />species: Adelie","bill_length_mm: 34.4<br />bill_depth_mm: 18.4<br />species: Adelie","bill_length_mm: 46.0<br />bill_depth_mm: 21.5<br />species: Adelie","bill_length_mm: 37.8<br />bill_depth_mm: 18.3<br />species: Adelie","bill_length_mm: 37.7<br />bill_depth_mm: 18.7<br />species: Adelie","bill_length_mm: 35.9<br />bill_depth_mm: 19.2<br />species: Adelie","bill_length_mm: 38.2<br />bill_depth_mm: 18.1<br />species: Adelie","bill_length_mm: 38.8<br />bill_depth_mm: 17.2<br />species: Adelie","bill_length_mm: 35.3<br />bill_depth_mm: 18.9<br />species: Adelie","bill_length_mm: 40.6<br />bill_depth_mm: 18.6<br />species: Adelie","bill_length_mm: 40.5<br />bill_depth_mm: 17.9<br />species: Adelie","bill_length_mm: 37.9<br />bill_depth_mm: 18.6<br />species: Adelie","bill_length_mm: 40.5<br />bill_depth_mm: 18.9<br />species: Adelie","bill_length_mm: 39.5<br />bill_depth_mm: 16.7<br />species: Adelie","bill_length_mm: 37.2<br />bill_depth_mm: 18.1<br />species: Adelie","bill_length_mm: 39.5<br />bill_depth_mm: 17.8<br />species: Adelie","bill_length_mm: 40.9<br />bill_depth_mm: 18.9<br />species: Adelie","bill_length_mm: 36.4<br />bill_depth_mm: 17.0<br />species: Adelie","bill_length_mm: 39.2<br />bill_depth_mm: 21.1<br />species: Adelie","bill_length_mm: 38.8<br />bill_depth_mm: 20.0<br />species: Adelie","bill_length_mm: 42.2<br />bill_depth_mm: 18.5<br />species: Adelie","bill_length_mm: 37.6<br />bill_depth_mm: 19.3<br />species: Adelie","bill_length_mm: 39.8<br />bill_depth_mm: 19.1<br />species: Adelie","bill_length_mm: 36.5<br />bill_depth_mm: 18.0<br />species: Adelie","bill_length_mm: 40.8<br />bill_depth_mm: 18.4<br />species: Adelie","bill_length_mm: 36.0<br />bill_depth_mm: 18.5<br />species: Adelie","bill_length_mm: 44.1<br />bill_depth_mm: 19.7<br />species: Adelie","bill_length_mm: 37.0<br />bill_depth_mm: 16.9<br />species: Adelie","bill_length_mm: 39.6<br />bill_depth_mm: 18.8<br />species: Adelie","bill_length_mm: 41.1<br />bill_depth_mm: 19.0<br />species: Adelie","bill_length_mm: 37.5<br />bill_depth_mm: 18.9<br />species: Adelie","bill_length_mm: 36.0<br />bill_depth_mm: 17.9<br />species: Adelie","bill_length_mm: 42.3<br />bill_depth_mm: 21.2<br />species: Adelie","bill_length_mm: 39.6<br />bill_depth_mm: 17.7<br />species: Adelie","bill_length_mm: 40.1<br />bill_depth_mm: 18.9<br />species: Adelie","bill_length_mm: 35.0<br />bill_depth_mm: 17.9<br />species: Adelie","bill_length_mm: 42.0<br />bill_depth_mm: 19.5<br />species: Adelie","bill_length_mm: 34.5<br />bill_depth_mm: 18.1<br />species: Adelie","bill_length_mm: 41.4<br />bill_depth_mm: 18.6<br />species: Adelie","bill_length_mm: 39.0<br />bill_depth_mm: 17.5<br />species: Adelie","bill_length_mm: 40.6<br />bill_depth_mm: 18.8<br />species: Adelie","bill_length_mm: 36.5<br />bill_depth_mm: 16.6<br />species: Adelie","bill_length_mm: 37.6<br />bill_depth_mm: 19.1<br />species: Adelie","bill_length_mm: 35.7<br />bill_depth_mm: 16.9<br />species: Adelie","bill_length_mm: 41.3<br />bill_depth_mm: 21.1<br />species: Adelie","bill_length_mm: 37.6<br />bill_depth_mm: 17.0<br />species: Adelie","bill_length_mm: 41.1<br />bill_depth_mm: 18.2<br />species: Adelie","bill_length_mm: 36.4<br />bill_depth_mm: 17.1<br />species: Adelie","bill_length_mm: 41.6<br />bill_depth_mm: 18.0<br />species: Adelie","bill_length_mm: 35.5<br />bill_depth_mm: 16.2<br />species: Adelie","bill_length_mm: 41.1<br />bill_depth_mm: 19.1<br />species: Adelie","bill_length_mm: 35.9<br />bill_depth_mm: 16.6<br />species: Adelie","bill_length_mm: 41.8<br />bill_depth_mm: 19.4<br />species: Adelie","bill_length_mm: 33.5<br />bill_depth_mm: 19.0<br />species: Adelie","bill_length_mm: 39.7<br />bill_depth_mm: 18.4<br />species: Adelie","bill_length_mm: 39.6<br />bill_depth_mm: 17.2<br />species: Adelie","bill_length_mm: 45.8<br />bill_depth_mm: 18.9<br />species: Adelie","bill_length_mm: 35.5<br />bill_depth_mm: 17.5<br />species: Adelie","bill_length_mm: 42.8<br />bill_depth_mm: 18.5<br />species: Adelie","bill_length_mm: 40.9<br />bill_depth_mm: 16.8<br />species: Adelie","bill_length_mm: 37.2<br />bill_depth_mm: 19.4<br />species: Adelie","bill_length_mm: 36.2<br />bill_depth_mm: 16.1<br />species: Adelie","bill_length_mm: 42.1<br />bill_depth_mm: 19.1<br />species: Adelie","bill_length_mm: 34.6<br />bill_depth_mm: 17.2<br />species: Adelie","bill_length_mm: 42.9<br />bill_depth_mm: 17.6<br />species: Adelie","bill_length_mm: 36.7<br />bill_depth_mm: 18.8<br />species: Adelie","bill_length_mm: 35.1<br />bill_depth_mm: 19.4<br />species: Adelie","bill_length_mm: 37.3<br />bill_depth_mm: 17.8<br />species: Adelie","bill_length_mm: 41.3<br />bill_depth_mm: 20.3<br />species: Adelie","bill_length_mm: 36.3<br />bill_depth_mm: 19.5<br />species: Adelie","bill_length_mm: 36.9<br />bill_depth_mm: 18.6<br />species: Adelie","bill_length_mm: 38.3<br />bill_depth_mm: 19.2<br />species: Adelie","bill_length_mm: 38.9<br />bill_depth_mm: 18.8<br />species: Adelie","bill_length_mm: 35.7<br />bill_depth_mm: 18.0<br />species: Adelie","bill_length_mm: 41.1<br />bill_depth_mm: 18.1<br />species: Adelie","bill_length_mm: 34.0<br />bill_depth_mm: 17.1<br />species: Adelie","bill_length_mm: 39.6<br />bill_depth_mm: 18.1<br />species: Adelie","bill_length_mm: 36.2<br />bill_depth_mm: 17.3<br />species: Adelie","bill_length_mm: 40.8<br />bill_depth_mm: 18.9<br />species: Adelie","bill_length_mm: 38.1<br />bill_depth_mm: 18.6<br />species: Adelie","bill_length_mm: 40.3<br />bill_depth_mm: 18.5<br />species: Adelie","bill_length_mm: 33.1<br />bill_depth_mm: 16.1<br />species: Adelie","bill_length_mm: 43.2<br />bill_depth_mm: 18.5<br />species: Adelie","bill_length_mm: 35.0<br />bill_depth_mm: 17.9<br />species: Adelie","bill_length_mm: 41.0<br />bill_depth_mm: 20.0<br />species: Adelie","bill_length_mm: 37.7<br />bill_depth_mm: 16.0<br />species: Adelie","bill_length_mm: 37.8<br />bill_depth_mm: 20.0<br />species: Adelie","bill_length_mm: 37.9<br />bill_depth_mm: 18.6<br />species: Adelie","bill_length_mm: 39.7<br />bill_depth_mm: 18.9<br />species: Adelie","bill_length_mm: 38.6<br />bill_depth_mm: 17.2<br />species: Adelie","bill_length_mm: 38.2<br />bill_depth_mm: 20.0<br />species: Adelie","bill_length_mm: 38.1<br />bill_depth_mm: 17.0<br />species: Adelie","bill_length_mm: 43.2<br />bill_depth_mm: 19.0<br />species: Adelie","bill_length_mm: 38.1<br />bill_depth_mm: 16.5<br />species: Adelie","bill_length_mm: 45.6<br />bill_depth_mm: 20.3<br />species: Adelie","bill_length_mm: 39.7<br />bill_depth_mm: 17.7<br />species: Adelie","bill_length_mm: 42.2<br />bill_depth_mm: 19.5<br />species: Adelie","bill_length_mm: 39.6<br />bill_depth_mm: 20.7<br />species: Adelie","bill_length_mm: 42.7<br />bill_depth_mm: 18.3<br />species: Adelie","bill_length_mm: 38.6<br />bill_depth_mm: 17.0<br />species: Adelie","bill_length_mm: 37.3<br />bill_depth_mm: 20.5<br />species: Adelie","bill_length_mm: 35.7<br />bill_depth_mm: 17.0<br />species: Adelie","bill_length_mm: 41.1<br />bill_depth_mm: 18.6<br />species: Adelie","bill_length_mm: 36.2<br />bill_depth_mm: 17.2<br />species: Adelie","bill_length_mm: 37.7<br />bill_depth_mm: 19.8<br />species: Adelie","bill_length_mm: 40.2<br />bill_depth_mm: 17.0<br />species: Adelie","bill_length_mm: 41.4<br />bill_depth_mm: 18.5<br />species: Adelie","bill_length_mm: 35.2<br />bill_depth_mm: 15.9<br />species: Adelie","bill_length_mm: 40.6<br />bill_depth_mm: 19.0<br />species: Adelie","bill_length_mm: 38.8<br />bill_depth_mm: 17.6<br />species: Adelie","bill_length_mm: 41.5<br />bill_depth_mm: 18.3<br />species: Adelie","bill_length_mm: 39.0<br />bill_depth_mm: 17.1<br />species: Adelie","bill_length_mm: 44.1<br />bill_depth_mm: 18.0<br />species: Adelie","bill_length_mm: 38.5<br />bill_depth_mm: 17.9<br />species: Adelie","bill_length_mm: 43.1<br />bill_depth_mm: 19.2<br />species: Adelie","bill_length_mm: 36.8<br />bill_depth_mm: 18.5<br />species: Adelie","bill_length_mm: 37.5<br />bill_depth_mm: 18.5<br />species: Adelie","bill_length_mm: 38.1<br />bill_depth_mm: 17.6<br />species: Adelie","bill_length_mm: 41.1<br />bill_depth_mm: 17.5<br />species: Adelie","bill_length_mm: 35.6<br />bill_depth_mm: 17.5<br />species: Adelie","bill_length_mm: 40.2<br />bill_depth_mm: 20.1<br />species: Adelie","bill_length_mm: 37.0<br />bill_depth_mm: 16.5<br />species: Adelie","bill_length_mm: 39.7<br />bill_depth_mm: 17.9<br />species: Adelie","bill_length_mm: 40.2<br />bill_depth_mm: 17.1<br />species: Adelie","bill_length_mm: 40.6<br />bill_depth_mm: 17.2<br />species: Adelie","bill_length_mm: 32.1<br />bill_depth_mm: 15.5<br />species: Adelie","bill_length_mm: 40.7<br />bill_depth_mm: 17.0<br />species: Adelie","bill_length_mm: 37.3<br />bill_depth_mm: 16.8<br />species: Adelie","bill_length_mm: 39.0<br />bill_depth_mm: 18.7<br />species: Adelie","bill_length_mm: 39.2<br />bill_depth_mm: 18.6<br />species: Adelie","bill_length_mm: 36.6<br />bill_depth_mm: 18.4<br />species: Adelie","bill_length_mm: 36.0<br />bill_depth_mm: 17.8<br />species: Adelie","bill_length_mm: 37.8<br />bill_depth_mm: 18.1<br />species: Adelie","bill_length_mm: 36.0<br />bill_depth_mm: 17.1<br />species: Adelie","bill_length_mm: 41.5<br />bill_depth_mm: 18.5<br />species: Adelie"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(248,118,109,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)"}},"hoveron":"points","name":"Adelie","legendgroup":"Adelie","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[46.5,50,51.3,45.4,52.7,45.2,46.1,51.3,46,51.3,46.6,51.7,47,52,45.9,50.5,50.3,58,46.4,49.2,42.4,48.5,43.2,50.6,46.7,52,50.5,49.5,46.4,52.8,40.9,54.2,42.5,51,49.7,47.5,47.6,52,46.9,53.5,49,46.2,50.9,45.5,50.9,50.8,50.1,49,51.5,49.8,48.1,51.4,45.7,50.7,42.5,52.2,45.2,49.3,50.2,45.6,51.9,46.8,45.7,55.8,43.5,49.6,50.8,50.2],"y":[17.9,19.5,19.2,18.7,19.8,17.8,18.2,18.2,18.9,19.9,17.8,20.3,17.3,18.1,17.1,19.6,20,17.8,18.6,18.2,17.3,17.5,16.6,19.4,17.9,19,18.4,19,17.8,20,16.6,20.8,16.7,18.8,18.6,16.8,18.3,20.7,16.6,19.9,19.5,17.5,19.1,17,17.9,18.5,17.9,19.6,18.7,17.3,16.4,19,17.3,19.7,17.3,18.8,16.6,19.9,18.8,19.4,19.5,16.5,17,19.8,18.1,18.2,19,18.7],"text":["bill_length_mm: 46.5<br />bill_depth_mm: 17.9<br />species: Chinstrap","bill_length_mm: 50.0<br />bill_depth_mm: 19.5<br />species: Chinstrap","bill_length_mm: 51.3<br />bill_depth_mm: 19.2<br />species: Chinstrap","bill_length_mm: 45.4<br />bill_depth_mm: 18.7<br />species: Chinstrap","bill_length_mm: 52.7<br />bill_depth_mm: 19.8<br />species: Chinstrap","bill_length_mm: 45.2<br />bill_depth_mm: 17.8<br />species: Chinstrap","bill_length_mm: 46.1<br />bill_depth_mm: 18.2<br />species: Chinstrap","bill_length_mm: 51.3<br />bill_depth_mm: 18.2<br />species: Chinstrap","bill_length_mm: 46.0<br />bill_depth_mm: 18.9<br />species: Chinstrap","bill_length_mm: 51.3<br />bill_depth_mm: 19.9<br />species: Chinstrap","bill_length_mm: 46.6<br />bill_depth_mm: 17.8<br />species: Chinstrap","bill_length_mm: 51.7<br />bill_depth_mm: 20.3<br />species: Chinstrap","bill_length_mm: 47.0<br />bill_depth_mm: 17.3<br />species: Chinstrap","bill_length_mm: 52.0<br />bill_depth_mm: 18.1<br />species: Chinstrap","bill_length_mm: 45.9<br />bill_depth_mm: 17.1<br />species: Chinstrap","bill_length_mm: 50.5<br />bill_depth_mm: 19.6<br />species: Chinstrap","bill_length_mm: 50.3<br />bill_depth_mm: 20.0<br />species: Chinstrap","bill_length_mm: 58.0<br />bill_depth_mm: 17.8<br />species: Chinstrap","bill_length_mm: 46.4<br />bill_depth_mm: 18.6<br />species: Chinstrap","bill_length_mm: 49.2<br />bill_depth_mm: 18.2<br />species: Chinstrap","bill_length_mm: 42.4<br />bill_depth_mm: 17.3<br />species: Chinstrap","bill_length_mm: 48.5<br />bill_depth_mm: 17.5<br />species: Chinstrap","bill_length_mm: 43.2<br />bill_depth_mm: 16.6<br />species: Chinstrap","bill_length_mm: 50.6<br />bill_depth_mm: 19.4<br />species: Chinstrap","bill_length_mm: 46.7<br />bill_depth_mm: 17.9<br />species: Chinstrap","bill_length_mm: 52.0<br />bill_depth_mm: 19.0<br />species: Chinstrap","bill_length_mm: 50.5<br />bill_depth_mm: 18.4<br />species: Chinstrap","bill_length_mm: 49.5<br />bill_depth_mm: 19.0<br />species: Chinstrap","bill_length_mm: 46.4<br />bill_depth_mm: 17.8<br />species: Chinstrap","bill_length_mm: 52.8<br />bill_depth_mm: 20.0<br />species: Chinstrap","bill_length_mm: 40.9<br />bill_depth_mm: 16.6<br />species: Chinstrap","bill_length_mm: 54.2<br />bill_depth_mm: 20.8<br />species: Chinstrap","bill_length_mm: 42.5<br />bill_depth_mm: 16.7<br />species: Chinstrap","bill_length_mm: 51.0<br />bill_depth_mm: 18.8<br />species: Chinstrap","bill_length_mm: 49.7<br />bill_depth_mm: 18.6<br />species: Chinstrap","bill_length_mm: 47.5<br />bill_depth_mm: 16.8<br />species: Chinstrap","bill_length_mm: 47.6<br />bill_depth_mm: 18.3<br />species: Chinstrap","bill_length_mm: 52.0<br />bill_depth_mm: 20.7<br />species: Chinstrap","bill_length_mm: 46.9<br />bill_depth_mm: 16.6<br />species: Chinstrap","bill_length_mm: 53.5<br />bill_depth_mm: 19.9<br />species: Chinstrap","bill_length_mm: 49.0<br />bill_depth_mm: 19.5<br />species: Chinstrap","bill_length_mm: 46.2<br />bill_depth_mm: 17.5<br />species: Chinstrap","bill_length_mm: 50.9<br />bill_depth_mm: 19.1<br />species: Chinstrap","bill_length_mm: 45.5<br />bill_depth_mm: 17.0<br />species: Chinstrap","bill_length_mm: 50.9<br />bill_depth_mm: 17.9<br />species: Chinstrap","bill_length_mm: 50.8<br />bill_depth_mm: 18.5<br />species: Chinstrap","bill_length_mm: 50.1<br />bill_depth_mm: 17.9<br />species: Chinstrap","bill_length_mm: 49.0<br />bill_depth_mm: 19.6<br />species: Chinstrap","bill_length_mm: 51.5<br />bill_depth_mm: 18.7<br />species: Chinstrap","bill_length_mm: 49.8<br />bill_depth_mm: 17.3<br />species: Chinstrap","bill_length_mm: 48.1<br />bill_depth_mm: 16.4<br />species: Chinstrap","bill_length_mm: 51.4<br />bill_depth_mm: 19.0<br />species: Chinstrap","bill_length_mm: 45.7<br />bill_depth_mm: 17.3<br />species: Chinstrap","bill_length_mm: 50.7<br />bill_depth_mm: 19.7<br />species: Chinstrap","bill_length_mm: 42.5<br />bill_depth_mm: 17.3<br />species: Chinstrap","bill_length_mm: 52.2<br />bill_depth_mm: 18.8<br />species: Chinstrap","bill_length_mm: 45.2<br />bill_depth_mm: 16.6<br />species: Chinstrap","bill_length_mm: 49.3<br />bill_depth_mm: 19.9<br />species: Chinstrap","bill_length_mm: 50.2<br />bill_depth_mm: 18.8<br />species: Chinstrap","bill_length_mm: 45.6<br />bill_depth_mm: 19.4<br />species: Chinstrap","bill_length_mm: 51.9<br />bill_depth_mm: 19.5<br />species: Chinstrap","bill_length_mm: 46.8<br />bill_depth_mm: 16.5<br />species: Chinstrap","bill_length_mm: 45.7<br />bill_depth_mm: 17.0<br />species: Chinstrap","bill_length_mm: 55.8<br />bill_depth_mm: 19.8<br />species: Chinstrap","bill_length_mm: 43.5<br />bill_depth_mm: 18.1<br />species: Chinstrap","bill_length_mm: 49.6<br />bill_depth_mm: 18.2<br />species: Chinstrap","bill_length_mm: 50.8<br />bill_depth_mm: 19.0<br />species: Chinstrap","bill_length_mm: 50.2<br />bill_depth_mm: 18.7<br />species: Chinstrap"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(0,186,56,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(0,186,56,1)"}},"hoveron":"points","name":"Chinstrap","legendgroup":"Chinstrap","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[46.1,50,48.7,50,47.6,46.5,45.4,46.7,43.3,46.8,40.9,49,45.5,48.4,45.8,49.3,42,49.2,46.2,48.7,50.2,45.1,46.5,46.3,42.9,46.1,44.5,47.8,48.2,50,47.3,42.8,45.1,59.6,49.1,48.4,42.6,44.4,44,48.7,42.7,49.6,45.3,49.6,50.5,43.6,45.5,50.5,44.9,45.2,46.6,48.5,45.1,50.1,46.5,45,43.8,45.5,43.2,50.4,45.3,46.2,45.7,54.3,45.8,49.8,46.2,49.5,43.5,50.7,47.7,46.4,48.2,46.5,46.4,48.6,47.5,51.1,45.2,45.2,49.1,52.5,47.4,50,44.9,50.8,43.4,51.3,47.5,52.1,47.5,52.2,45.5,49.5,44.5,50.8,49.4,46.9,48.4,51.1,48.5,55.9,47.2,49.1,47.3,46.8,41.7,53.4,43.3,48.1,50.5,49.8,43.5,51.5,46.2,55.1,44.5,48.8,47.2,null,46.8,50.4,45.2,49.9],"y":[13.2,16.3,14.1,15.2,14.5,13.5,14.6,15.3,13.4,15.4,13.7,16.1,13.7,14.6,14.6,15.7,13.5,15.2,14.5,15.1,14.3,14.5,14.5,15.8,13.1,15.1,14.3,15,14.3,15.3,15.3,14.2,14.5,17,14.8,16.3,13.7,17.3,13.6,15.7,13.7,16,13.7,15,15.9,13.9,13.9,15.9,13.3,15.8,14.2,14.1,14.4,15,14.4,15.4,13.9,15,14.5,15.3,13.8,14.9,13.9,15.7,14.2,16.8,14.4,16.2,14.2,15,15,15.6,15.6,14.8,15,16,14.2,16.3,13.8,16.4,14.5,15.6,14.6,15.9,13.8,17.3,14.4,14.2,14,17,15,17.1,14.5,16.1,14.7,15.7,15.8,14.6,14.4,16.5,15,17,15.5,15,13.8,16.1,14.7,15.8,14,15.1,15.2,15.9,15.2,16.3,14.1,16,15.7,16.2,13.7,null,14.3,15.7,14.8,16.1],"text":["bill_length_mm: 46.1<br />bill_depth_mm: 13.2<br />species: Gentoo","bill_length_mm: 50.0<br />bill_depth_mm: 16.3<br />species: Gentoo","bill_length_mm: 48.7<br />bill_depth_mm: 14.1<br />species: Gentoo","bill_length_mm: 50.0<br />bill_depth_mm: 15.2<br />species: Gentoo","bill_length_mm: 47.6<br />bill_depth_mm: 14.5<br />species: Gentoo","bill_length_mm: 46.5<br />bill_depth_mm: 13.5<br />species: Gentoo","bill_length_mm: 45.4<br />bill_depth_mm: 14.6<br />species: Gentoo","bill_length_mm: 46.7<br />bill_depth_mm: 15.3<br />species: Gentoo","bill_length_mm: 43.3<br />bill_depth_mm: 13.4<br />species: Gentoo","bill_length_mm: 46.8<br />bill_depth_mm: 15.4<br />species: Gentoo","bill_length_mm: 40.9<br />bill_depth_mm: 13.7<br />species: Gentoo","bill_length_mm: 49.0<br />bill_depth_mm: 16.1<br />species: Gentoo","bill_length_mm: 45.5<br />bill_depth_mm: 13.7<br />species: Gentoo","bill_length_mm: 48.4<br />bill_depth_mm: 14.6<br />species: Gentoo","bill_length_mm: 45.8<br />bill_depth_mm: 14.6<br />species: Gentoo","bill_length_mm: 49.3<br />bill_depth_mm: 15.7<br />species: Gentoo","bill_length_mm: 42.0<br />bill_depth_mm: 13.5<br />species: Gentoo","bill_length_mm: 49.2<br />bill_depth_mm: 15.2<br />species: Gentoo","bill_length_mm: 46.2<br />bill_depth_mm: 14.5<br />species: Gentoo","bill_length_mm: 48.7<br />bill_depth_mm: 15.1<br />species: Gentoo","bill_length_mm: 50.2<br />bill_depth_mm: 14.3<br />species: Gentoo","bill_length_mm: 45.1<br />bill_depth_mm: 14.5<br />species: Gentoo","bill_length_mm: 46.5<br />bill_depth_mm: 14.5<br />species: Gentoo","bill_length_mm: 46.3<br />bill_depth_mm: 15.8<br />species: Gentoo","bill_length_mm: 42.9<br />bill_depth_mm: 13.1<br />species: Gentoo","bill_length_mm: 46.1<br />bill_depth_mm: 15.1<br />species: Gentoo","bill_length_mm: 44.5<br />bill_depth_mm: 14.3<br />species: Gentoo","bill_length_mm: 47.8<br />bill_depth_mm: 15.0<br />species: Gentoo","bill_length_mm: 48.2<br />bill_depth_mm: 14.3<br />species: Gentoo","bill_length_mm: 50.0<br />bill_depth_mm: 15.3<br />species: Gentoo","bill_length_mm: 47.3<br />bill_depth_mm: 15.3<br />species: Gentoo","bill_length_mm: 42.8<br />bill_depth_mm: 14.2<br />species: Gentoo","bill_length_mm: 45.1<br />bill_depth_mm: 14.5<br />species: Gentoo","bill_length_mm: 59.6<br />bill_depth_mm: 17.0<br />species: Gentoo","bill_length_mm: 49.1<br />bill_depth_mm: 14.8<br />species: Gentoo","bill_length_mm: 48.4<br />bill_depth_mm: 16.3<br />species: Gentoo","bill_length_mm: 42.6<br />bill_depth_mm: 13.7<br />species: Gentoo","bill_length_mm: 44.4<br />bill_depth_mm: 17.3<br />species: Gentoo","bill_length_mm: 44.0<br />bill_depth_mm: 13.6<br />species: Gentoo","bill_length_mm: 48.7<br />bill_depth_mm: 15.7<br />species: Gentoo","bill_length_mm: 42.7<br />bill_depth_mm: 13.7<br />species: Gentoo","bill_length_mm: 49.6<br />bill_depth_mm: 16.0<br />species: Gentoo","bill_length_mm: 45.3<br />bill_depth_mm: 13.7<br />species: Gentoo","bill_length_mm: 49.6<br />bill_depth_mm: 15.0<br />species: Gentoo","bill_length_mm: 50.5<br />bill_depth_mm: 15.9<br />species: Gentoo","bill_length_mm: 43.6<br />bill_depth_mm: 13.9<br />species: Gentoo","bill_length_mm: 45.5<br />bill_depth_mm: 13.9<br />species: Gentoo","bill_length_mm: 50.5<br />bill_depth_mm: 15.9<br />species: Gentoo","bill_length_mm: 44.9<br />bill_depth_mm: 13.3<br />species: Gentoo","bill_length_mm: 45.2<br />bill_depth_mm: 15.8<br />species: Gentoo","bill_length_mm: 46.6<br />bill_depth_mm: 14.2<br />species: Gentoo","bill_length_mm: 48.5<br />bill_depth_mm: 14.1<br />species: Gentoo","bill_length_mm: 45.1<br />bill_depth_mm: 14.4<br />species: Gentoo","bill_length_mm: 50.1<br />bill_depth_mm: 15.0<br />species: Gentoo","bill_length_mm: 46.5<br />bill_depth_mm: 14.4<br />species: Gentoo","bill_length_mm: 45.0<br />bill_depth_mm: 15.4<br />species: Gentoo","bill_length_mm: 43.8<br />bill_depth_mm: 13.9<br />species: Gentoo","bill_length_mm: 45.5<br />bill_depth_mm: 15.0<br />species: Gentoo","bill_length_mm: 43.2<br />bill_depth_mm: 14.5<br />species: Gentoo","bill_length_mm: 50.4<br />bill_depth_mm: 15.3<br />species: Gentoo","bill_length_mm: 45.3<br />bill_depth_mm: 13.8<br />species: Gentoo","bill_length_mm: 46.2<br />bill_depth_mm: 14.9<br />species: Gentoo","bill_length_mm: 45.7<br />bill_depth_mm: 13.9<br />species: Gentoo","bill_length_mm: 54.3<br />bill_depth_mm: 15.7<br />species: Gentoo","bill_length_mm: 45.8<br />bill_depth_mm: 14.2<br />species: Gentoo","bill_length_mm: 49.8<br />bill_depth_mm: 16.8<br />species: Gentoo","bill_length_mm: 46.2<br />bill_depth_mm: 14.4<br />species: Gentoo","bill_length_mm: 49.5<br />bill_depth_mm: 16.2<br />species: Gentoo","bill_length_mm: 43.5<br />bill_depth_mm: 14.2<br />species: Gentoo","bill_length_mm: 50.7<br />bill_depth_mm: 15.0<br />species: Gentoo","bill_length_mm: 47.7<br />bill_depth_mm: 15.0<br />species: Gentoo","bill_length_mm: 46.4<br />bill_depth_mm: 15.6<br />species: Gentoo","bill_length_mm: 48.2<br />bill_depth_mm: 15.6<br />species: Gentoo","bill_length_mm: 46.5<br />bill_depth_mm: 14.8<br />species: Gentoo","bill_length_mm: 46.4<br />bill_depth_mm: 15.0<br />species: Gentoo","bill_length_mm: 48.6<br />bill_depth_mm: 16.0<br />species: Gentoo","bill_length_mm: 47.5<br />bill_depth_mm: 14.2<br />species: Gentoo","bill_length_mm: 51.1<br />bill_depth_mm: 16.3<br />species: Gentoo","bill_length_mm: 45.2<br />bill_depth_mm: 13.8<br />species: Gentoo","bill_length_mm: 45.2<br />bill_depth_mm: 16.4<br />species: Gentoo","bill_length_mm: 49.1<br />bill_depth_mm: 14.5<br />species: Gentoo","bill_length_mm: 52.5<br />bill_depth_mm: 15.6<br />species: Gentoo","bill_length_mm: 47.4<br />bill_depth_mm: 14.6<br />species: Gentoo","bill_length_mm: 50.0<br />bill_depth_mm: 15.9<br />species: Gentoo","bill_length_mm: 44.9<br />bill_depth_mm: 13.8<br />species: Gentoo","bill_length_mm: 50.8<br />bill_depth_mm: 17.3<br />species: Gentoo","bill_length_mm: 43.4<br />bill_depth_mm: 14.4<br />species: Gentoo","bill_length_mm: 51.3<br />bill_depth_mm: 14.2<br />species: Gentoo","bill_length_mm: 47.5<br />bill_depth_mm: 14.0<br />species: Gentoo","bill_length_mm: 52.1<br />bill_depth_mm: 17.0<br />species: Gentoo","bill_length_mm: 47.5<br />bill_depth_mm: 15.0<br />species: Gentoo","bill_length_mm: 52.2<br />bill_depth_mm: 17.1<br />species: Gentoo","bill_length_mm: 45.5<br />bill_depth_mm: 14.5<br />species: Gentoo","bill_length_mm: 49.5<br />bill_depth_mm: 16.1<br />species: Gentoo","bill_length_mm: 44.5<br />bill_depth_mm: 14.7<br />species: Gentoo","bill_length_mm: 50.8<br />bill_depth_mm: 15.7<br />species: Gentoo","bill_length_mm: 49.4<br />bill_depth_mm: 15.8<br />species: Gentoo","bill_length_mm: 46.9<br />bill_depth_mm: 14.6<br />species: Gentoo","bill_length_mm: 48.4<br />bill_depth_mm: 14.4<br />species: Gentoo","bill_length_mm: 51.1<br />bill_depth_mm: 16.5<br />species: Gentoo","bill_length_mm: 48.5<br />bill_depth_mm: 15.0<br />species: Gentoo","bill_length_mm: 55.9<br />bill_depth_mm: 17.0<br />species: Gentoo","bill_length_mm: 47.2<br />bill_depth_mm: 15.5<br />species: Gentoo","bill_length_mm: 49.1<br />bill_depth_mm: 15.0<br />species: Gentoo","bill_length_mm: 47.3<br />bill_depth_mm: 13.8<br />species: Gentoo","bill_length_mm: 46.8<br />bill_depth_mm: 16.1<br />species: Gentoo","bill_length_mm: 41.7<br />bill_depth_mm: 14.7<br />species: Gentoo","bill_length_mm: 53.4<br />bill_depth_mm: 15.8<br />species: Gentoo","bill_length_mm: 43.3<br />bill_depth_mm: 14.0<br />species: Gentoo","bill_length_mm: 48.1<br />bill_depth_mm: 15.1<br />species: Gentoo","bill_length_mm: 50.5<br />bill_depth_mm: 15.2<br />species: Gentoo","bill_length_mm: 49.8<br />bill_depth_mm: 15.9<br />species: Gentoo","bill_length_mm: 43.5<br />bill_depth_mm: 15.2<br />species: Gentoo","bill_length_mm: 51.5<br />bill_depth_mm: 16.3<br />species: Gentoo","bill_length_mm: 46.2<br />bill_depth_mm: 14.1<br />species: Gentoo","bill_length_mm: 55.1<br />bill_depth_mm: 16.0<br />species: Gentoo","bill_length_mm: 44.5<br />bill_depth_mm: 15.7<br />species: Gentoo","bill_length_mm: 48.8<br />bill_depth_mm: 16.2<br />species: Gentoo","bill_length_mm: 47.2<br />bill_depth_mm: 13.7<br />species: Gentoo","bill_length_mm:   NA<br />bill_depth_mm:   NA<br />species: Gentoo","bill_length_mm: 46.8<br />bill_depth_mm: 14.3<br />species: Gentoo","bill_length_mm: 50.4<br />bill_depth_mm: 15.7<br />species: Gentoo","bill_length_mm: 45.2<br />bill_depth_mm: 14.8<br />species: Gentoo","bill_length_mm: 49.9<br />bill_depth_mm: 16.1<br />species: Gentoo"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(97,156,255,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(97,156,255,1)"}},"hoveron":"points","name":"Gentoo","legendgroup":"Gentoo","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.2283105022831,"r":7.30593607305936,"b":40.1826484018265,"l":48.9497716894977},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[30.725,60.975],"tickmode":"array","ticktext":["40","50","60"],"tickvals":[40,50,60],"categoryorder":"array","categoryarray":["40","50","60"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"bill_length_mm","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[12.68,21.92],"tickmode":"array","ticktext":["15.0","17.5","20.0"],"tickvals":[15,17.5,20],"categoryorder":"array","categoryarray":["15.0","17.5","20.0"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"bill_depth_mm","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.913385826771654},"annotations":[{"text":"species","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"709451e06a52":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"709451e06a52","visdat":{"709451e06a52":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```
  
  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).


```r
train_delays2018 <- small_trains %>% 
  filter(year %in% c(2018)) %>% 
  ggplot(aes(x = month, y = num_arriving_late)) +
  geom_bar(stat = 'identity') +
  labs(title = "Number of Late Arriving Trains by Month (2018)",
       subtitle = "Arrival_Station: {closest_state}",
       x = "",
       y = "") +
  transition_states(arrival_station, 
                    transition_length = 2, 
                    state_length = 2)

animate(train_delays2018, duration = 20)

anim_save("traindelays.gif")
```

![](traindelays.gif)<!-- -->

## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. You should do the following:
  * From the `garden_harvest` data, filter the data to the tomatoes and find the *daily* harvest in pounds for each variety.  
  * Then, for each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each vegetable and arranged (HINT: `fct_reorder()`) from most to least harvested (most on the bottom).  
  * Add animation to reveal the plot over date. 

I have started the code for you below. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0.


```r
tomatoes <- garden_harvest %>% 
  filter(vegetable == "tomatoes") %>% 
  group_by(date, variety) %>% 
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>% 
  group_by(variety) %>% 
  mutate(variety = str_to_upper(variety)) %>% 
  mutate(cumtotharvest = cumsum(daily_harvest_lb)) %>% 
  ungroup() %>% 
  complete(variety, date, fill = list(daily_harvest_lb = 0))
```

```r
tomato_animate <- tomatoes %>% 
  ggplot(aes(x = date, 
             y = cumtotharvest)) +
  geom_area(aes(fill = variety)) +
  labs(title = "Cumulative tomato harvest (lb)", 
       subtitle = "Date: {frame_along}",
       x = "",
       y = "") +
  theme(legend.title = element_blank()) + 
  transition_reveal(date)


animate(tomato_animate)

anim_save("tomatoeos.gif")
```

![](tomatoeos.gif)<!-- -->
## Maps, animation, and movement!

  4. Map my `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.


```r
mallorca <- get_stamenmap(
    bbox = c(left = 2.34, bottom = 39.52, right = 2.70, top = 39.70), 
    maptype = "terrain",
    zoom = 11)

bikeride <- ggmap(mallorca) + 
  geom_point(data = mallorca_bike_day7, 
             aes(x = lon, y = lat), 
             size = .8, color = "red") +
  geom_path(data = mallorca_bike_day7,
            aes(x = lon, y = lat, color = ele),
            alpha = 0.8, size = .8) +
  scale_color_viridis_c(option = "magma") +
  labs(x="",
       y="",
       title="Mallorca Bike Ride - Day 7", 
       subtitle = "Time: {frame_along}") +
  theme(plot.title = element_text(hjust = 0.5)) +
  theme_map() +
  theme(legend.background = element_blank()) +
  transition_reveal(time)

animate(bikeride)

anim_save("mallorcaride.gif")
```

![](mallorcaride.gif)<!-- -->


  5. In this exercise, you get to meet my sister, Heather! She is a proud Mac grad, currently works as a Data Scientist at 3M where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files (HINT: `bind_rows()`, 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

```r
trail <- panama_swim %>% 
  bind_rows(list(panama_run, panama_bike))

panama <- get_stamenmap(
    bbox = c(left = -79.56, bottom = 8.88, right = -79.41, top = 9.001), 
    maptype = "terrain",
    zoom = 13)

race <- ggmap(panama) + 
  geom_point(data = trail, 
             aes(x = lon, y = lat, color = event, shape = event), 
             size = 2) +
  geom_path(data = trail,
            aes(x = lon, y = lat, color = event),
            alpha = 0.8, size = .5) +
  labs(x="",
       y="",
       title="Race Map", 
       subtitle = "Time: {frame_along}") +
  theme_map() +
  theme(legend.background = element_blank()) +
  transition_reveal(time)

animate(race)

anim_save("panamarace.gif")
```

![](panamarace.gif)<!-- -->
 
## COVID-19 data

  6. In this exercise, you are going to replicate many of the features in [this](https://aatishb.com/covidtrends/?region=US) visualization by Aitish Bhatia but include all US states. Requirements:
 * Create a new variable that computes the number of new cases in the past week (HINT: use the `lag()` function you've used in a previous set of exercises). Replace missing values with 0's using `replace_na()`.  
  * Filter the data to omit rows where the cumulative case counts are less than 20.  
  * Create a static plot with cumulative cases on the x-axis and new cases in the past 7 days on the y-axis. Connect the points for each state over time. HINTS: use `geom_path()` and add a `group` aesthetic.  Put the x and y axis on the log scale and make the tick labels look nice - `scales::comma` is one option. This plot will look pretty ugly as is.
  * Animate the plot to reveal the pattern by date. Display the date as the subtitle. Add a leading point to each state's line (`geom_point()`) and add the state name as a label (`geom_text()` - you should look at the `check_overlap` argument).  
  * Use the `animate()` function to have 200 frames in your animation and make it 30 seconds long. 
  * Comment on what you observe.
  

```r
covid_2 <- covid19 %>% 
  group_by(state) %>% 
  mutate(sevendaylag = lag(cases, 7, order_by = date)) %>% 
  replace_na(list(sevendaylag = 0)) %>% 
  mutate(weeklydailycases = cases - sevendaylag) %>% 
  filter(cases >= 20)

 covidanimate <- covid_2 %>%
  ggplot(aes(x = cases, y = weeklydailycases, group = state)) +
  geom_path(color = "darkblue")+
  geom_point(color = "indianred") +
  geom_text(aes(label = state)) +
  labs(title = "Trajectory of Confrimed Covid Cases", 
       subtitle = "Date: {frame_along}",
       x = "Total Confirmed Cases",
       y = "New Confirmed Cases (Past Week)") +
  theme(legend.position = "none") +
  transition_reveal(date)

animate(covidanimate, nframes = 200, duration = 20)

anim_save("covidbystate.gif")
```

![](covidbystate.gif)<!-- -->

  7. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. The code below gives the population estimates for each state and loads the `states_map` data. Here is a list of details you should include in the plot:
  
  * Put date in the subtitle.   
  * Because there are so many dates, you are going to only do the animation for all Fridays. So, use `wday()` to create a day of week variable and filter to all the Fridays.   
  * Use the `animate()` function to make the animation 200 frames instead of the default 100 and to pause for 10 frames on the end frame.   
  * Use `group = date` in `aes()`.   
  * Comment on what you see.  



```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))

states_map <- map_data("state")
```


```r
states_map <- map_data("state")


covidper10k <- covid19 %>% 
  mutate(state = str_to_lower(state)) %>% 
  left_join(census_pop_est_2018,
            by = c("state" = "state")) %>% 
  group_by(state, est_pop_2018, date) %>% 
  summarise(cumulativecases = max(cases)) %>% 
  mutate(cases_per_cap = (cumulativecases/est_pop_2018)*10000)
  

mycovidmap <- covidper10k %>% 
  mutate(str_to_lower(state), weekday = wday(date, label = TRUE)) %>% 
  filter(weekday == "Fri") %>% 
  ggplot() +
  geom_map(map = states_map,
           aes(map_id = state,
               fill = cases_per_cap,
               group = date))  + 

  expand_limits(x = states_map$long, y = states_map$lat) + 
  theme_map() +
  theme(legend.position = "right",
        legend.key.size = unit(1.5, "line")) +
  labs(title = "US COVID-19 Cases per 10,000 People", 
       subtitle = "State: {next_state}",
       caption = "By Hannah",
       fill = "Cases per 10,000") +
  scale_fill_viridis_c() +
  transition_states(date, transition_length = 0) 

animate(mycovidmap, duration = 30)

anim_save("covidbystate.gif")
```

![](covidbystate.gif)<!-- -->
## Your first `shiny` app (for next week!)

NOT DUE THIS WEEK! If any of you want to work ahead, this will be on next week's exercises.

  8. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' cumulative number of COVID cases over time. The x-axis will be number of days since 20+ cases and the y-axis will be cumulative cases on the log scale (`scale_y_log10()`). We use number of days since 20+ cases on the x-axis so we can make better comparisons of the curve trajectories. You will have an input box where the user can choose which states to compare (`selectInput()`) and have a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
## GitHub link

  9. Below, provide a link to your GitHub page with this set of Weekly Exercises. Specifically, if the name of the file is 05_exercises.Rmd, provide a link to the 05_exercises.md file, which is the one that will be most readable on GitHub. If that file isn't very readable, then provide a link to your main GitHub page.


**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
