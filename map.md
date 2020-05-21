## Making Maps in R

We are going to make a map using ggplot2 and ggmap in R. R contains many fantastic packages to help create publication-worthy figures. 
You can find the manual for ggmap [here](https://cran.r-project.org/web/packages/ggmap/ggmap.pdf)

We're going to start with a map of the United States. Begin by installing the packages you need and loading the libraries:

```
# install and load devtools
install.packages("devtools")
library(devtools)

install.packages("ggplot2")
install.packages(c("maps", "mapdata"))
devtools::install_github("dkahle/ggmap")
install.packages("RgoogleMaps")
install.packages("tidyverse")
install.packages("maptools")
install.packages("ggrepel")

library(ggrepel)
library(maptools)
library(tidyverse)
library(RgoogleMaps)
library(ggplot2)
library(ggmap)
library(maps)
library(mapdata)
```

We also need to load our map data, convert it to a data frame and give shorthand names to the different variables:

```
locations<-read.csv("crayfish_lat_long.csv")

locations

map_data <- data.frame(
  long = locations$lon,
  lat = locations$lat,
  names = locations$name,
  sites = locations$site,
  stringsAsFactors = FALSE
  )  
  ```
  
Now we can use the map data to plot the US and highlight a region that we will zoom in on:

```
usa <- map_data("usa") 
states <- map_data("state")

USA<-ggplot(data = states) +
  theme_void()+
  geom_polygon(data = states, aes(x = long, y = lat, group = group),fill = "white", color = "gray") +
  geom_rect(xmin = -96, xmax = -88, ymin = 32, ymax = 38, fill = NA, colour = "black", size = 0.75)
USA
ggsave("USA_plot.pdf",scale = 1, width = 12, height = 8, units = c("in"), dpi = 300)
```
![USA_plot](/images/USA_plot.jpg)


> Reflection:
> 
>What do theme_void, geom_polygon, and geom_rect create in the map? What are the variables we're plotting?
<br/>

Now that we have a region of interest, we will use ggmap to highlight our area and plot our sampling sites
First, we'll set the frame of our map:


`base = get_map(location=c(-96,32,-88,38), zoom = 7, source = "stamen", maptype="toner-background")`

![base](/images/base.jpg)

Now that we have a base map, let's add our plot points, and "beautify" the map:

```
ark <- ggmap(base) +
    theme(axis.title.y = element_blank(), axis.title.x = element_blank(), panel.border = element_rect(colour = "black", fill=NA, size=2)) +
    geom_text(data = states, aes(x = long, y = lat, label ="" ), size = 5) +
    geom_point(data = map_data, aes(x = long, y = lat), color = "black", size = 2) +
    geom_label_repel(data = map_data, aes(x = long, y = lat,label = paste(as.character(sites), sep="")), stat = "unique", box.padding = 0.5, segment.color = 'black') +
  	annotate("text", x = -92, y = 36, label = "Arkansas") +
  	annotate("text", x = -89, y = 34.5, label = "Mississippi") 
ark
ggsave("ark_plot.pdf", scale = 0.75, width = 8,height = 7, units = c("in"), dpi = 300)
```
![ark](/images/ark_plot.jpg)

> Reflection:
> 
>We manually annotated the state labels, but what are some commands we could change to have the map automatically contain the state labels?
<br/>

**Troubleshooting:**
* If your Arkansas map is rendering as a green, topological map instead of the black/white theme, try reinstalling ggmap, restarting your R session, and then loading all the packages again.
