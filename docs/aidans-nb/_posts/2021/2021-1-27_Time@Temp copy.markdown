---
layout: post
title:  "Data Exploration - Reading Madigan et al.2020"
date:   2021-1-27 11:10:00 -0800
categories: jekyll update
---
## Data Exploration (2)

Yesterday I made some perliminary Time-at-temperature figures using data from the get_pdt() function - these were good for getting a general sense of patterns in the data, however they did not provide the time specificity that I will need to make future figures, nor was there any way to separate night and day water column use.

Today, I expanded on my initial time at temperature plots, using interp_pdt(), add_series_temp(), and add_daynight() functions within Camrin's tags3etuff package to make a data frame with more specific data (smaller time resolution with more details). To do this, I used the following for loops:

```r
# MAKOS

for (i in 4:length(makos)) {
  etuff <- read_etuff(makos[i])
  hdr <- get_header(makos[i])
  temp <- get_pdt(etuff)
  interp <- interp_pdt(etuff)
  series <- get_series(etuff)
  series <- filter(series, !is.na(depth))
  series <- add_series_temp(series, temp, interp)
  series <- filter(series, !is.na(temperature))
  series$dn <- add_daynight(series, etuff)
  series$ptt <- hdr$ptt
  pdt <- rbind(pdt, series)
  rm(etuff, hdr, temp, interp, series)
  print(i)
}

# BLUES

for (i in 1:length(blues)) {
    etuff <- read_etuff(blues[i])
    hdr <- get_header(blues[i])
    temp <- get_pdt(etuff)
    interp <- interp_pdt(etuff)
    series <- get_series(etuff)
    series <- filter(series, !is.na(depth))
    series <- add_series_temp(series, temp, interp)
    series <- filter(series, !is.na(temperature))
    series$dn <- add_daynight(series, etuff)
    series$ppt <- hdr$ptt
    pdtb <- rbind(pdtb, series)
    rm(etuff, hdr, temp, interp, series)
    print(i)
  }
  
```

Next I wrote the following geom_histogram code to build more informative figures, in which daytime temperature use is displayed on the left and nighttime temperature use is on the right.

There are still some issues with these fitures, namely:

1. Bin size should be refined further
2. y-lab (proportions) should be adjusted so the extent is equal on both sides

```r
# MAKOS

ggplot(data = pdt) +
  geom_histogram(data = subset(pdt, dn == "d"), aes(x = temperature, y = -(..count..)/sum(..count..)), color = "black") +
  geom_histogram(data = subset(pdt, dn =="n"), aes(x = temperature, y = (..count..)/sum(..count..)), color = "black") +
  coord_flip() +
  ylab("Proportion") +
  xlab("Temperature (ºC)") +
  theme_classic()
  
#BLUES
  
ggplot() +
  geom_histogram(data = subset(pdtb, dn == "d"), aes(x = temperature, y = -(..count..)/sum(..count..)), color = "black") +
  geom_histogram(data = subset(pdtb, dn == "n"), aes(x = temperature, y = (..count..)/sum(..count..)), color = "black") +
  coord_flip() +
  ylab("Proportion") +
  xlab("Temperature (ºC)") +
  theme_classic()
  
```
  
Notes:

- Some series datasets contained as high as 50% NA values, interpolating series and pdt data only produced more and therefore a significant amount of data was excluded in this analysis. I need to talk to Cam about where all the NA values come from. 
There are >300,000 data points in the blues data set and ~70,000 in the makos dataset. 

- Using the fine-scale pdt data altered the mean and standard deviation of temperature occupied by makos slightly. Initially it was about 17 ºC using get_pdt data. After interpolation the mean was 20 ºC. Likely a product of using higher resolution data but worth noting

Goals for Tomorrow:
- Move on to Time-at-depth plots using same pipeline and data frames
- Attempt proportion of depth use over a single day (I think previous heatmaps were one column = one day)



