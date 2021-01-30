---
layout: post
title:  "Finding Environmental Metrics (1)"
date:   2021-1-4 18:00:00 -0800
categories: jekyll update
---
## Environmental Data ##
There are three environmental variables that I need to consider adding to my analysis in order to consider sub-surface conditions that may be driving different patterns of diving behaviors in these two species of sharks, blues and makos. They are as follows:

1. Bulk-Buoyancy Frequency:
Pulled from Hycom and listed as "n2"" in the resultant tables

2. Temp @ 300m depth: 
Here 300m is arbitrary decision, to choose a more specific depth for this metric I will compare the average depth occupied by each species (in each cluster?)

3. Oxygen @ 300m depth:
Cam mentioned that I should put more thought into whether or not to include this metric. It may not be very insightful for the study region since oxygen does not vary by a large amount in the Northwest Atlantic, over the depth range considered here. In addition, oxygen data must be measured in-situ or modeled and either case introduces uncertainty into your conclusion. If the gain is less than the cost, it might not be worth the effort to include. Solution could be to download and see if it offers significant explanatory power 
Note - I also need to include the standard deviations of SST and SSH as these will provide some insight as to whether ths sharks were occupying frontal regions where variability in temperature and sea-surface height are larger.

Temp data can be downloaded at regular intervals from the World Ocean Atlas here:
[World Ocean Atlas, Temp.](https://www.nodc.noaa.gov/cgi-bin/OC5/woa13/woa13.pl?parameter=t)
- Need to talk with Cam about best date range, bin scale, and retrieval 

Dissolved oxygen data can be downloaded from the same source at regular depth intervals:
[World Ocean Atlas, O<sub>2</sub>](https://www.nodc.noaa.gov/cgi-bin/OC5/woa13/woa13oxnu.pl?parameter=o)

# Finding the average depth usage of each species #
Based on the omega_mako tad table, it looks like makos spent the most time in depth bin 3 (33.27%) 

Need to homogenize blue bins before I can replicate this with blues


To Do Tomorrow:
1. Homogenize the tad bins for each species
2. Find average depth of occupancy for blue and mako sharks



Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
