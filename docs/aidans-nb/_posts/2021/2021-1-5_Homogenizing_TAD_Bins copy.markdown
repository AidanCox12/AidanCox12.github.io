---
layout: post
title:  "Finding Environmental Metrics (1)"
date:   2021-1-4 18:00:00 -0800
categories: jekyll update
---
## Homogenizing TAD Bins

In order to make any reasonable comparisons between behavior clusters of blue and mako sharks, I need to be comparing them accross the same bin sizes (otherwise this difference will influence the clustering process and potentially introduce a type 2 error). 

Because the mako data is the limiting factor in terms of available depth bin summaries, I will need to restructure the blue bins to match the mako bins. 

The depth bins for mako sharks are as follows: 

Bin 1: 0-10 m
Bin 2: 10-50 m
Bin 3: 50-100 m
Biin 4: 100-200 m
Bin 5: 200-300 m
Bin 6: 300-400 m
Bin 7: 400 - 500 m

Comparatively, the bins for blue sharks are:

Bin 1: 0-2 m
Bin 2: 2-10 m
Bin 3: 10-20 m
Bin 4: 20-50 m
Bin 5: 50-100 m
Bin 6: 100-200 m
Bin 7: 200-300 m
Bin 8: 300-400 m
Bin 9: 400-500 m
Bin 10: 500-700 m

Thus to homogenize the two groups blue shark bins must be combined so that:

Bin 1 = (Bin 1 + Bin 2)
Bin 2 = (Bin 3 + Bin 4)
Bin 3 = Bin 5
Bin 4 = Bin 6
Bin 5 = Bin 7
Bin 6 = Bin 8
Bin 7 = (Bin 9 + Bin 10)


