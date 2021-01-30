---
layout: post
title:  "Data Exploration - Reading Madigan et al.2020"
date:   2021-1-29 20:10:00 -0800
categories: jekyll update
---
## Data Exploration (3)

Today I finished up my general summary figures by making time-at-depth figures and graphics of proportional depth use by time of day...

Time-at-depth was very easy, I used the same data frames and switched up the code from my time-at temperature figures

```r
ggplot() +
  geom_histogram(data = subset(pdt, dn == "d"), aes(x = depth, y = -(..count..)/sum(..count..)), color = "black") +
  geom_histogram(data = subset(pdt, dn == "n"), aes(x = depth, y = (..count..)/sum(..count..)), color = "black") +
  scale_x_reverse() +
  coord_flip() +
  ylab("Proportion") +
  xlab("Depth (m)") +
  theme_classic()

# BLUES

ggplot() +
  geom_histogram(data = subset(pdtb, dn == "d"), aes(x = depth, y = -(..count..)/sum(..count..)), color = "black") +
  geom_histogram(data = subset(pdtb, dn == "n"), aes(x = depth, y = (..count..)/sum(..count..)), color = "black") +
  scale_x_reverse() +
  coord_flip() +
  ylab("Proportion") +
  xlab("Depth (m)") +
  theme_classic()
  
```

Next came the hard part, figuring out how to make the proportioal depth use figures. I decided that if I could group the data by individual time stamps I could use a grouped count() function to count the observations at each depth and use that as my fill category. This idea more or less panned out by using the stat_density_2d() function, which just takes the density of each depth observation listed without taking into account the number of times the animal was observed at that depth. For makos, this seems to work fine since there were relatively few (<10) observations at each depth, but for blues it's a problem because especially at the surface there are about 50 observations at each depth. 

Note for next time:
- The current figures are a close estimate, however they should be resolved so that the fill pattern actually represents proportion of depth use rather than density of observations

```r
# MAKOS

props <- pdt %>% separate(DateTime_local, c("Date", "Time_Local"), sep =  "([ ])") %>%
  group_by(Time_Local) %>%
  count(depth)

props$Time_Local <- as.hms(props$Time_Local)
props$Time_Local <- as.numeric(props$Time_Local)

ggplot(data = props, aes(x = Time_Local, y = depth) ) +
  stat_density_2d(aes(fill = ((..density..)*n)), geom = "raster", contour = FALSE) +
  scale_fill_distiller(palette = "Spectral") + 
  scale_y_reverse() +
  scale_x_continuous(breaks = c(0, 43200, 86400), labels = c("00:00:00", "12:00:00", "23:00:00")) +
  xlab("Time of Day") +
  ylab("Depth(m)") +
  theme_minimal()

# BLUES

propsb <- pdtb %>% separate(DateTime_local, c("Date", "Time_Local"), sep =  "([ ])") %>%
  group_by(Time_Local) %>%
  count(depth)

propsb$Time_Local <- as.hms(propsb$Time_Local)
propsb$Time_Local <- as.numeric(propsb$Time_Local)

ggplot(data = propsb, aes(x = Time_Local, y = depth) ) +
  stat_density_2d(aes(fill = ((..density..)*n)), geom = "raster", contour = FALSE) +
  scale_fill_distiller(palette = "Spectral") + 
  scale_y_reverse() +
  scale_x_continuous(breaks = c(0, 43200, 86400), labels = c("00:00:00", "12:00:00", "23:00:00")) +
  xlab("Time of Day") +
  ylab("Depth(m)") +
  theme_minimal()

  
```


Goals for Next Week:
- Make some maps
  - dive frequency
  - max depth
  - dive time
- Make some annimations of movement overlayed against environmental factors 
  - temperature
  - SSH
  - EKE
  - etc. 



