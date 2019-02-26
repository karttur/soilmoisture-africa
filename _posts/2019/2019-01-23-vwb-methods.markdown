---
layout: post
title: Vertical Water Balance - processes
modified: '2019-01-23 20:17'
categories: blog
excerpt: Processing the Vertical Water Balance for a regional project
tags:
  - VWB
  - Vertical Water Balance
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-01-23 20:17'
comments: true
share: true

VWB-0160_tile_M: VWB-0160_tile_M
VWB-0161_tile_A: VWB-0161_tile_A
VWB-0310_trend_A_1998-2017: VWB-0310_trend_A_1998-2017
VWB-0310_trend_A_2003-2016: VWB-0310_trend_A_2003-2016
VWB-0320_changes_A_1998-2017: VWB-0320_changes_A_1998-2017
VWB-0320_changes_A_2003-2016: VWB-0320_changes_A_2003-2016

VWB-0610_mosaic_M: VWB-0610_mosaic_M
VWB-0630_mosaic_timespanA_1998-2017: VWB-0630_mosaic_timespanA_1998-2017
VWB-0630_mosaic_timespanA_2003-2016: VWB-0630_mosaic_timespanA_2003-2016
VWB-0900_ExporttoByte_M: VWB-0900_ExporttoByte_M
VWB-0910_ExporttoByte_timespanA_1998-2017: VWB-0910_ExporttoByte_timespanA_1998-2017
VWB-0910_ExporttoByte_timespanA_2003-2016: VWB-0910_ExporttoByte_timespanA_2003-2016

VWB-0950_movieframes_M: VWB-0950_movieframes_M
VWB-0960_movieclock_M: VWB-0960_movieclock_M
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post outlines a process chain for exploring and analysing the Vertical Water Balance (VWB) and its change over Sub Saharan Africa using Karttur´s GeoImagine Framework. The results are presented in the [next](../vwb-results/) post.

# Prerequisites

To follow the processing steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/), download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github, and [calculate the Vertical Water balance](https://karttur.github.io/geoimagine/blog/blog-VWB-TRMM-FAOrefET/). The latter also requires that you [download and process the original TRMM data](https://karttur.github.io/geoimagine/blog/blog-TRMM/) and the [FAO reference evapotranspiration](https://karttur.github.io/geoimagine/blog/blog-FAO-refevap/).

# Introduction

The Vertical Water Balance (VWB) is the local difference between precipitation and evapotranspiration. Humid regions have precipitation exceeding evapotranspiration and in arid areas evapotranspiration exceed precipitation. Many regions have both wet and dry seasons, with humid conditions during the wet season and arid during the dry.

# Process chain

The principal steps for creating estimations, maps and animations from VWB data over Africa include:

- Tile to region
- Time series processing
- Mosaic
- Export media

In the Framework a process chaincan be built as a series of calls to xml coded instructions. This section contains the calls and the remaining parts of the post details each called xml. As noted above, the results are available in the [next](../vwb-results) post.

<button id= "toggleProcessChain" onclick="hiddencode('ProcessChain')">Hide/Show AfricaSubSahara_process_VWB.txt</button>

<div id="ProcessChain" style="display:none">
{% capture text-capture %}
{% raw %}
```
###################################
###################################
###     VWB data processing     ###
###################################
###################################

## The processing requires that the Vertical Water Balance (VWB) data are already processed and available ##

###################################
###       Tile to region        ###
###################################

## Tile monthly VWB to region ##
AfricaSubSahara_VWB-0160_tile_M.xml

## Tile annual VWB to region ##
AfricaSubSahara_VWB-0161_tile_A.xml

###################################
###   Time Series Processing    ###
###################################

## VWB annual trends (1998-2017 is for the complete timeseries, 2003-2016 for overlap with GRACE
## should be done at tile level! Not by tiling original data. ##
AfricaSubSahara_VWB-0310_trend_A_1998-2017.xml
AfricaSubSahara_VWB-0310_trend_A_2003-2016.xml

## Changes and significant trends (1998-2017 is for the complete timeseries, 2003-2016 for overlap with GRACE ##
AfricaSubSahara_VWB-0320_changes_A_1998-2017.xml
AfricaSubSahara_VWB-0320_changes_A_2003-2016.xml

###################################
###   	       Mosaic           ###
###################################

## Mosaic monthly VWB ##
AfricaSubSahara_VWB-0610_mosaic_M.xml

## Mosaic VWB trends ##
#AfricaSubSahara_VWB-0630_mosaic_timespanA_1998-2017.xml
AfricaSubSahara_VWB-0630_mosaic_timespanA_2003-2016.xml

###################################
###        Export media         ###
###################################

## Export monthly VWB mosaics ##
AfricaSubSahara_VWB-0900_ExporttoByte_M.xml

## Export VWB annual trends ##
AfricaSubSahara_VWB-0910_ExporttoByte_timespanA_1998-2017.xml
AfricaSubSahara_VWB-0910_ExporttoByte_timespanA_2003-2016.xml

## Create monthly VWB movieframes for Sub Saharan Africa ##
## To create individual movies for VWB-total, VWB-surplus and VWB-deficit
## Run this and the next script three times while only keeping one process each time
## and also deleting intermediate files in between each run and renaming the final movie
## There are alternatives, including running all scripts and change the the script files or the frame folders/frame names
AfricaSubSahara_VWB-0950_movieframes_M.xml

## Create Movieclock and scripts for VWB movie with movieclock overlay
AfricaSubSahara_VWB-0960_movieclock_M.xml
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

## Tile to region

In this project the dominating tile system is the MODIS SIN grid dividing the earth in 36 horizontal and 18 vertical tiles. For the VWB data, the starting point is the monthly VWB estimates (total VWB, surplus VWB and deficit VWB). Also the annually aggregated VWB estimates are captured by tiling.  Alternatively, the annually aggregations can be calculated using the tiled monthly data.

### Tile monthly VWB to region

{% capture foo %}{{page.VWB-0160_tile_M}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0160_tile_M.html foo=foo %}

### Tile annual VWB to region

{% capture foo %}{{page.VWB-0161_tile_A}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0161_tile_A.html foo=foo %}

## Time Series Processing

In the process chain used here, the annual VWB is imported through tiling (above). Also the other time series processes can be produced and imported in the same manner. The aggregation of the VWB data to other spatial resolutions, however, causes interpolation errors and thus it is strongly recommended to redo the time series analysis directly using the tiled (monthly or annual) data.

### VWB annual trends

The annual trends are estimated using two methods, ordinary least square (OLS) regression, and a Mann-Kendall (MK) test together with a Theil-Sen regression. Also the period mean and standard deviations are calculated. These calculations are done for two different periods, 1998 - 2017 and 2003 - 2016. The longer period includes all years with complete coverage of VWB (TRMM) data. The shorter period corresponds to the availability of data from the [Gravity Recovery and Climate Experiment (GRACE)](https://grace.jpl.nasa.gov) mission. The latter data is a direct estimate of the Earth's water reservoirs over land.

#### 1998-2017

The complete VWB time series is analysed at a spatial scale corresponding to the resolution of the original data (approximately 30 km).

{% capture foo %}{{page.VWB-0310_trend_A_1998-2017}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0310_trend_A_1998-2017.html foo=foo %}

#### 2013-2016

The VWB time series corresponding to the available GRACE data is processed at the 1 degree spatial scale of the GRACE data  (approximately 111 km)

{% capture foo %}{{page.VWB-0310_trend_A_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0310_trend_A_2003-2016.html foo=foo %}

## Changes and significant trends

Regions with significant negative (VWB decrease) or positive (increase) are calculated using the MK scores and with the strength of significant trends captured as the slope and absolute change in VWB as estimated from the median Theil-Sen regression. Again the analysis covers two different periods, representing the complete VWB time series (1998-2017) and the overlap with GRACE data (2003-2016). The former period is in a spatial resolution resembling the original VWB data while the latter is in the more coarse resolution of the GRACE data.

#### 1998-2017

{% capture foo %}{{page.VWB-0320_changes_A_1998-2017}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0320_changes_A_1998-2017.html foo=foo %}

#### 2013-2016

{% capture foo %}{{page.VWB-0320_changes_A_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0320_changes_A_2003-2016.html foo=foo %}

## Mosaic

In this projects, the mosaicking is only done for the exports in the next step. In the mosaic process, the tiles are first concatenated and then cut to the actual coordinates of the defining region. Cell values and data type remain the same, but the data can be reprojected on the fly.

### Mosaic monthly VWB

The monthly mosaics are primarily used for creating the movies of the rainfall dynamics.

{% capture foo %}{{page.VWB-0610_mosaic_M}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0610_mosaic_M.html foo=foo %}

### Mosaic VWB trends

The annual trends were calculated for two different periods (see above). The shorter period (2003-2016) was primarily done for comparing VWB and GRACE, and need not be mosaicked and exported.

#### 1998-2018  

{% capture foo %}{{page.VWB-0630_mosaic_timespanA_1998-2017}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0630_mosaic_timespanA_1998-2017.html foo=foo %}

### 2003-2016

{% capture foo %}{{page.VWB-0630_mosaic_timespanA_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0630_mosaic_timespanA_2003-2016.html foo=foo %}

## Export Media

The main reason for exporting the mosaicked layer is to allow visualization of both the data and the results.

### Export monthly VWB mosaics

The monthly images of the VWB are exported in order to use each date as a frame in animations (movies).

{% capture foo %}{{page.VWB-0900_ExporttoByte_M}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0900_ExporttoByte_M.html foo=foo %}

### Export VWB annual trends

The annual trends were calculated for two different periods (see above). The shorter period (2003-2016) was primarily done for comparing VWB and GRACE, and need not be mosaicked and exported.

#### 1998-2017

{% capture foo %}{{page.VWB-0910_ExporttoByte_timespanA_1998-2017}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0910_ExporttoByte_timespanA_1998-2017.html foo=foo %}

#### 2003-2016

{% capture foo %}{{page.VWB-0910_ExporttoByte_timespanA_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-0910_ExporttoByte_timespanA_2003-2016.html foo=foo %}

### Movies

To create the animated movie showing the monthly rainfall over Sub Saharan Africa the monthly rainfall data must be mosaicked and exported as color maps as outlined above. The movie is created using two processes; the first process converts the exported color maps to movie frames and the the second process created a clock and a timeline that fits the frames. The second process also produces a shell script that must be executed (run) to produce the movie.

The movie creation requires that the command line applications [ImageMagick](https://karttur.github.io/setup-theme-blog/blog/install-imagemagick/) and [FFmpeg](https://karttur.github.io/setup-theme-blog/blog/ffmpeg-movie/) are installed.

The movie scripts are prepared for producing separate movies, for total, surplus and deficit VWB. To actually produce the three movies, however, demands some manual editing between each. The key issue is that the scripts creating and assembling the frames look for all images in the source folder. This can be achieved using different approaches, including deleting all files after each movie production, editing the scripts, or moving source files to temporary folders.

#### Create VWB movieframes

{% capture foo %}{{page.VWB-0950_movieframes_M}}{% endcapture %}

{% include xml/AfricaSubSahara_VWB-0950_movieframes_M.html foo=foo %}

#### Create VWB movieclock and movie script

{% capture foo %}{{page.VWB-0960_movieclock_M}}{% endcapture %}

{% include xml/AfricaSubSahara_VWB-0960_movieclock_M.html foo=foo %}

__To view the maps and movies created in this posted, click the <span class='button'>Next</span> button below__.
