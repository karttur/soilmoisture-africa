---
layout: post
title: SMAP soil moisture - methods
modified: '2019-02-03 20:17'
categories: blog
excerpt: Processing SMAP soil moisture for a regional project
tags:
  - SMAP
  - Soil Moisture Active Passive
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-02-03 20:17'
comments: true
share: true

---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post outlines a process chain for preparing data from the Soil Moisture Active Passive (SMAP) mission for a regional project over Sub Saharan Africa using Karttur´s GeoImagine Framework.

# Prerequisites

To follow the processing steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/), download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github and [download and process the SMAP data](https://karttur.github.io/geoimagine/blog/blog-SMAP/). As you are going to use the SMAP enhanced product () for assimialting soil moisture estimates from the Moderate Resolution Imaging Spectroradiometer (MODIS) sensor, you should adjust the SMAP soil moisture estimates adjacent to open water bodies as described in [this](https://karttur.github.io/geoimagine/blog/blog-SMAP-adjust/) post.

# SMAP

The Soil Moisture Active and Passive (SMAP) mission estimates the global top 5 cm soil moisture with approximately a weekly interval. The SMAP passive radiometer original spatial resolution is 36 km, and has been operational since March 2015. Recent algorithmic development has allowed a 9 km enhanced product. In this project the 36 km product has been used for comparing continental scale soil moisture with both rainfall and gravity estimated water content on land. The enhanced 9 km product is used for [adjusting the soil moisture estimates from the Moderate Resolution Imaging Spectroradiometer (MODIS) sensor](#).

# Process chain

The processing of SMAP as a dataset on its own is restricted to tiling the global SMAP data to the SINgrid tiles covering Sub Saharan Africa.

<button id= "toggleProcessChain" onclick="hiddencode('ProcessChain')">Hide/Show AfricaSubSahara_process_SMAP.txt</button>

<div id="ProcessChain" style="display:none">

{% capture text-capture %}
{% raw %}
```
###################################
###################################
###       SMAP processing       ###
###################################
###################################

## The processing requires that the SMAP data are already processed and available ##

#createscaling_SMAP_v80.xml

###################################
###       Tile to region        ###
###################################

## Tile monthly SMAP to region ##
#AfricaSubSahara_SMAP-0160_tile_M.xml

## Tile 16D SMAP to region ##
#AfricaSubSahara_SMAP-0162_tile_16D.xml

###################################
###           Archive           ###
###################################

## Archive monthly ##
#AfricaSubSahara_SMAP-0980_archive-zip_M.xml

## Archive 16D ##
#AfricaSubSahara_SMAP-0980_archive-zip_16D.xml

## Archive 16D seasons ##
#AfricaSubSahara_MODIS-SMAP-0980_zip-archive-seasons_16D_2015-2018.xml

```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

## SMAP preprocessing

For this project you need SMAP data resampled to fit the temporal resolution of the rainfall and climate data (monthly) and the MODIS estimated soil moisture (16 day interval). The monthly rainfall and climate data are at coarser resolution and should be prepared using the 36 km (original) SMAP passive product. The MODIS derived soil moisture estimate is at higher spatial and temporal resolution and the 9 km SMAP passive (enhanced) product should be preprocessed to 16 day interval average. The [preprocessing is better to do using the global SMAP data](https://karttur.github.io/geoimagine/blog/blog-SMAP/), and then imported to the project through tiling as included below.

## Tile to region

In this project the dominating tile system is the MODIS SIN grid dividing the earth in 36 horizontal and 18 vertical tiles. As stated above you need to import both monthly coarse data (36 km) and the higher resolution 9 km data at 16 day intervals.

### Tile monthly SMAP to region



### Tile 16 day SMAP to region
