---
layout: post
title:  "Data Exploration - Reading Madigan et al.2020"
date:   2021-2-5 20:10:00 -0800
categories: jekyll update
---
## Data Exploration (4)

The first think I did was re-do the clustering algorhithm for blue sharks using the 7 common TAD bins. This required me to refamiliarize myself with the clustering code I wrote over the summer. Here is a summary of the basic workflow for future reference:

1. Arrange the data 
      In a data frameach row should represent a different unit of observation (in this case days) and each column represents a distinct       depth bin. The content of the bin should probably be something simple and standard such as proportion of time spent at that depth       range

2. Create a distance matrix
      Use the dist() function in the base stats package to create a distance matrix of the data (matrix stating how similar each             observation is to every other observation). Specify the method, in this case manhattan or city-block. Smooth the data so that          extremely low distances are reduced to zero (essentially de-emphasizing rare behaviors/outliers)
      
3. Perform a heirarchical clustering
      Use the hclust() function to create a dendrogram from your distance matrix, specifying a linkage method (here, "average"). This        method groups the most similar observations based on the average of their distance to other observations

4. Test the clusters
      Use the various functions of the NbClust package to test the appropriate number of clusters

5. Visualize the clusters
      Create some figures to visualize your clusters and inspect them for accuracy 
      
---

While refamiliarizing myself with these procedures I realized that there may be a problem in how I have constructed my common bins, specifically with the depth range of the final bin. I think in some cases the data stop at 500 meters or so while in others they continue on down to 2000m. This could potentially create erronious behaviors just based on individual tag bias. - Need to talk more with Camrin about this... 

Transitioning away from the clusters, I also made some map-based summary figures to highlight geographic patterns within the data. Most of this work was done on Friday because earlier in the week I was finishing my REU application for Woods Hole. That said, here are the figures that I was able to make:

Chlorophyll - 

# Makos
Coastal individuals (141257, 163096, 163098) experienced much higher average and more variable cholorphyll values, pelagic individuals experienced relatively constant values - could produce unique coastal behavior in makos

# Blues
All sharks occupied more highly productive waters around 2016-09

Sea Surface Height and Eddy Kinetic Energy - 

# Makos
Mako bottom time doesn't seem to be closely associated with SSH or, geographically from what I know of the region, from temperature.
Instead, it looks like heavy depth use near the coast (curious) with largely surface use in pelagic zone - maybe migratory behavior... This is supported by the fact that points with low surface use seem to be more spread out suggesting directed movement

# Blues
No relationship between ssh and bottom time but lots and lots of surface-time right around cape cod - maybe because other shark species are moving in there. Interesting fun fact is that blue sharks are never closer to shore than at cape cod in this dataset. There seems to be greater surface use below gulf stream in warm sargasso sea

Sea Surface Temperature - 

# Makos
There might be a positive relationship between sst and bottom time but it's hard to tell, not very strong...

# Blues
Strong positive relationship between sst and bottom time





