---
layout: post
title:  "Finding Environmental Metrics (1)"
date:   2021-1-8 10:30:00 -0800
categories: jekyll update
---
## Homogenizing TAD Bins (2)

I used a quick mutate() function to combine the necessary time at depth bins for blue sharks using the code:

```r
tad_blue %>% 
  mutate(Bin_1 = TimeAtDepthBin01 + TimeAtDepthBin02, 
         Bin_2 = TimeAtDepthBin03 + TimeAtDepthBin04,
         Bin_3 = TimeAtDepthBin05,
         Bin_4 = TimeAtDepthBin06,
         Bin_5 = TimeAtDepthBin07,
         Bin_6 = TimeAtDepthBin08,
         Bin_7 = TimeAtDepthBin09 + TimeAtDepthBin10,
         .keep = "unused")
```

Next I took the mean percentage of TAD for each bin and found that blue sharks spend most time in Bin_1 (39.03%) with an almost linear decrease in time at depth as depth increases

Compared to mako sharks, which spent ~33% of time between 50-100m, blue sharks spent only 11% of time in this range. 

On average blue sharks spent 56.15% of each day above 50m

Comparatively, mako sharks spent only 38% of time in this range 

NOTE: This could be an important Figure for the paper - demonstrating that blue shark depth use decreases as depth increases while mako shark depth use spikes in the middle of the water column 

The average ild.5 depth for blue shark observations was 64 m while for mako observations it was 82 m
That said, it doesn't make sense to do a temperature at depth above these measurements, since the measurement would be above the thermocline. Thus, I think it makes the most sense to include a temperature measurement at or around 100m in this study. This is a depth above which both species spend >65 % of their total time each day. 

To Do:
- Re-make the omega_blue data frame with the updated tad_blue data

##  Meeting with Cam: ##
Consider Modelled data vs. Measured Date
- Climatology shoulded be used for oxygen data since it might not be super interesing...if it is, then we can consider going through the work to extract a more comprehensive dataset from an ocean model
(Salinity is the same deal over this sample sight, might want to pull from HYCOM and look since there but probably won't find much)
- We will use HYCOM data for temperature at depth profiles because it offers better temporal and spatial coverage than measurements
although it is important to note that the tags on the animals may offer temp. at depth profiles measured during the animals movements - this could be burried in the data somewhere and is worth looking for

HMMoce package:
Uses Hidden Markov Models to improve geologation for PSAT tags
Compates environmental data from tag to HYCOM models in order to build liklhood models of animal position
Because of this, it has built in functions that I can use to pull the temperature/depth profiles I need

Oxygen data was downloaded from the 2018 World Ocean Atlas and visualized using NASA's Panoply program

