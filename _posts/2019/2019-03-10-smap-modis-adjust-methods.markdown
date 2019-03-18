---
layout: post
title: Adjust MODIS TWI with SMAP
modified: '2019-03-10 20:17'
categories: blog
excerpt: SMAP Assimilation of TWI
tags:
  - MODIS
  - SMAP
  - MCD43A4
  - Sub Saharan Africa
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-03-10 20:17'
comments: true
share: true
movie1: rainfall_3b43_trmm_199801-201807_v7-f
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>


This post outlines a process chain for assimilating MODIS derived soil moisture estimates with soil moisture estimated from SMAP. The processing chain is covered in this post and the results are divided into a set of posts.

# Prerequisites

To follow the process steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/) and download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github. You must also have imported an processed both the SMAP and the MODIS data.

# Assimilation and downscaling

# Process chain

The principal steps for assimilating the MODIS data to SMAP  using Karttur's GeoImagine Framework include:

- Tile to region
- Resample to matching fit
- Visual
- Analyese assimilation
- Infer assimilation

In the Framework a process chain can be built as a series of calls to xml coded instructions. This section contains the calls and the remaining parts of the post details each called xml. As noted above, the results are available in the [next](../trmm-results) post.

<button id= "toggleProcessChain" onclick="hiddencode('ProcessChain')">Hide/Show AfricaSubSahara_process_TRMM.txt</button>

<div id="ProcessChain" style="display:none">
{% capture text-capture %}
{% raw %}
```
###################################
###  MODIS + SMAP assimilation  ###
###################################


## Resample SMAP to MODIS ##
#AfricaSubSahara_SMAP-0160_resample-2-MODIS_16D.xml

#Resample SMAP to MODIS original
#AfricaSubSahara_SMAP-0162_tile_16D.xml

#Then resample SMAP back to 9km but using average
#AfricaSubSahara_SMAP-0170_resample-2-SMAP_16D.xml

#Export the 9km SMAP and the 9km MODIS, same period and palette
#AfricaSubSahara_MODIS-0900_ExporttoByte_16D_9km.xml

#
#AfricaSubSahara_SMAP-0610_mosaic_16D_9km.xml

#AfricaSubSahara_SMAP-0900_ExporttoByte_16D_9km.xml

## Create SMAP + TWI 9 km movieframes ##
#AfricaSubSahara_SMAP-0950_movieframes_16D_9km.xml

#AfricaSubSahara_SMAP-0960_movieclock_16D_9km.xml

#AfricaSubSahara_MODIS-0951_tile-movieframes_16D.xml

#AfricaSubSahara_MODIS-0952_append-movieframes_16D.xml

#AfricaSubSahara_SMAP-MODIS-0960_tile-movieclock_16D.xml
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

## Resampling

The assimilation is performed using MODIS Grid Tile system. The MODIS data is already in this system, but at a spatial resolution of 500 m compared the SMAP data at 9 km. To fit the two datasets together you need to resample the MODIS data to 9 km, and to avoid loosing (too much) information you need to resample the SMAP data in 2 steps. In the first step you resample the original SMAP (9 km) data to the 500 m spatial resolution of the MODIS data, and then you resample it back to 9 km over the smae regions and useing the same resampling methods as for the MODIS resampling. Resampling the SMAP directly to 9 km affects the spatial consistency. Alternatively the MODIS data could have been resampled to fit the SMAP original prejection. That is, however, not implemented in the Framework where most processing builds on predefined tiles.


__To view the maps and movies created in this posted, click the <span class='button'>Next</span> button below__.
