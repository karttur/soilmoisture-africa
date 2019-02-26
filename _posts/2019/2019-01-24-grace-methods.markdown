---
layout: post
title: GRACE water pillar - methods
modified: '2019-01-24 20:17'
categories: blog
excerpt: Processing GRACE equivalent water pillar depth data for a regional project
tags:
  - GRACE
  - Gravity Recovery and Climate Experiment
  - Water pillar
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-01-24 20:17'
comments: true
share: true

GRACE-0160_tile_M: GRACE-0160_tile_M
GRACE-0161_tile_A: GRACE-0161_tile_A
GRACE-0310_trend_A_2003-2016: GRACE-0310_trend_A_2003-2016
GRACE-0320_changes_A_2003-2016: GRACE-0320_changes_A_2003-2016
GRACE-0610_mosaic_M: GRACE-0610_mosaic_M
GRACE-0630_mosaic_timespanA_2003-2016: GRACE-0630_mosaic_timespanA_2003-2016
GRACE-0900_ExporttoByte_M: GRACE-0900_ExporttoByte_M
GRACE-0910_ExporttoByte_timespanA_2003-2016: GRACE-0910_ExporttoByte_timespanA_2003-2016
GRACE-0950_movieframes_M: GRACE-0950_movieframes_M
GRACE-0960_movieclock_M: GRACE-0960_movieclock_M

---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post outlines a process chain for exploring and analysing the variations in Earth's water content (equivalent water pillar depth), as estimated  rom remotely sensed gravitation, over Sub Saharan Africa using Karttur´s GeoImagine Framework. The results are presented in the [next](../grace-results/) post.

# Prerequisites

To follow the processing steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/), download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github, and [download and process the GRACE data](https://karttur.github.io/geoimagine/blog/blog-GRACE/).

# GRACE

The [Gravity Recovery And Climate Experiment (GRACE)](https://grace.jpl.nasa.gov) mission was built around two identical satellites orbiting the Earth. Traveling with a fixed distance in between them the gravitational pull caused minute changes in the vertical elevation difference between the two satellites. This change can be used for estimating the gravitational pull. Short term (days to months) changes in the gravitation is primarily related to the Earth's water reservoirs over land, ice and oceans, and earthquakes and crustal deformations.

# Process chain

The principal steps for creating estimations, maps and animations from gravity estimated water pillar depth over Africa using Karttur's GeoImagine Framework include:

- Tile to region
- Time series processing
- Mosaic
- Export media

In the Framework a process chain can be built as a series of calls to xml coded instructions. This section contains the calls and the remaining parts of the post details each called xml. As noted above, the results are available in the [next](../grace-results) post.

<button id= "toggleProcessChain" onclick="hiddencode('ProcessChain')">Hide/Show AfricaSubSahara_process_GRACE.txt</button>

<div id="ProcessChain" style="display:none">

{% capture text-capture %}
{% raw %}
```
###################################
###################################
###    GRACE data processing    ###
###################################
###################################

## The processing requires that the GRACE data are already processed and available ##

###################################
###       Tile to region        ###
###################################

## Tile monthly GRACE to region ##
AfricaSubSahara_GRACE-0160_tile_M.xml

## Tile annual GRACE to region ##
AfricaSubSahara_GRACE-0161_tile_A.xml

###################################
###   Time Series Processing    ###
###################################

## GRACE annual trends  
AfricaSubSahara_GRACE-0310_trend_A_2003-2016.xml

## Changes and significant trends  ##
AfricaSubSahara_GRACE-0320_changes_A_2003-2016.xml

###################################
###   	       Mosaic           ###
###################################

## Mosaic monthly GRACE ##
AfricaSubSahara_GRACE-0610_mosaic_M.xml

## Mosaic VWB trends ##
AfricaSubSahara_GRACE-0630_mosaic_timespanA_2003-2016.xml

###################################
###        Export media         ###
###################################

## Export monthly GRACE ##
AfricaSubSahara_GRACE-0900_ExporttoByte_M.xml

## Export GRACE annual trends ##
AfricaSubSahara_GRACE-0910_ExporttoByte_timespanA_2003-2016.xml

## Create GRACE movieframes ##
AfricaSubSahara_GRACE-0950_movieframes_M.xml

## Create GRACE Movieclock and movie script ##
AfricaSubSahara_GRACE-0960_movieclock_M.xml
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

## Tile to region

In this project the dominating tile system is the MODIS SIN grid dividing the earth in 36 horizontal and 18 vertical tiles. For the GRACE data, the starting point is the [monthly average equivalent water depth estimates](https://karttur.github.io/geoimagine/blog/blog-GRACE/), created within Karttur¨s GeoImagine Framework. Also the annually aggregated water depth estimates are captured by tiling. Alternatively, the annually aggregated gravity depth can be calculated using the tiled monthly data. The imported GRACE data are not the original data, but the [average of the three product solutions available for download](https://karttur.github.io/geoimagine/blog/blog-GRACE/).

### Tile monthly GRACE to region

{% capture foo %}{{page.GRACE-0160_tile_M}}{% endcapture %}
{% include xml/AfricaSubSahara_GRACE-0160_tile_M.html foo=foo %}

### Tile annual GRACE to region

{% capture foo %}{{page.GRACE-0161_tile_A}}{% endcapture %}
{% include xml/AfricaSubSahara_GRACE-0161_tile_A.html foo=foo %}

## Time Series Processing

In the process chain used here, the aggregation of average monthly to annual gravity water depth was done using the global GRACE data, and the annual average signal imported through tiling (above). Also the other time series processes can be produced and imported in the same manner. As the spatial resolution of the global GRACE data and the tiled data is approximately equal, the difference between tiling the global statistical data and calculating trends and other statistics from the tiled monthly or annual data is negligible.

### GRACE annual trends

The annual trends are estimated using two methods, ordinary least square (OLS) regression, and a Mann-Kendall (MK) test together with a Theil-Sen regression. The trends and other statistics are calculated included all years with complete data from the complete GRACE mission (2003-2016).

#### 2003-2016

{% capture foo %}{{page.GRACE-0310_trend_A_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_GRACE-0310_trend_A_2003-2016.html foo=foo %}

## Changes and significant trends

Regions with significant negative (water storage decrease) or positive (water storage increase) are calculated using the MK scores and with the strength of significant trends captured as the slope and absolute change in water pillar depth as estimated from the median Theil-Sen regression.

#### 2003-2016

{% capture foo %}{{page.GRACE-0320_changes_A_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_GRACE-0320_changes_A_2003-2016.html foo=foo %}

## Mosaic

In the mosaic process, the tiles are first concatenated and then cut to the actual coordinates of the defining region. Cell values and data type remain the same, but the data can be reprojected on the fly.

### Mosaic monthly GRACE

The monthly mosaics are primarily used for creating the movies of the rainfall dynamics.

{% capture foo %}{{page.GRACE-0610_mosaic_M}}{% endcapture %}

{% include xml/AfricaSubSahara_GRACE-0610_mosaic_M.html foo=foo %}

### Mosaic GRACE trends

#### 2003-2016

{% capture foo %}{{page.GRACE-0630_mosaic_timespanA_2003-2016}}{% endcapture %}

{% include xml/AfricaSubSahara_GRACE-0630_mosaic_timespanA_2003-2016.html foo=foo %}

## Export Media

The main reason for exporting the mosaicked layer is to allow visualization of both the data and the results.

### Export monthly GRACE mosaics

The monthly images of the GRACE water pillar depth are exported in order to use each date as a frame in animations (movies).

{% capture foo %}{{page.GRACE-0900_ExporttoByte_M}}{% endcapture %}

{% include xml/AfricaSubSahara_GRACE-0900_ExporttoByte_M.html foo=foo %}

### Export GRACE annual trends

#### 2003-2016

{% capture foo %}{{page.GRACE-0630_mosaic_timespanA_2003-2016}}{% endcapture %}

{% include xml/AfricaSubSahara_GRACE-0630_mosaic_timespanA_2003-2016.html foo=foo %}

### Movies

To create the animated movie showing the monthly variations in gravity induced equivalent water pillar depth over Sub Saharan Africa the monthly data must be mosaicked and exported as color maps as outlined above. The movie is created using two processes; the first process converts the exported color maps to movie frames and the the second process created a clock and a timeline that fits the frames. The second process also produces a shell script that must be executed (run) to produce the movie.

The movie creation requires that the command line applications [ImageMagick](https://karttur.github.io/setup-theme-blog/blog/install-imagemagick/) and [FFmpeg](https://karttur.github.io/setup-theme-blog/blog/ffmpeg-movie/) are installed.

#### Create GRACE movieframes

{% capture foo %}{{page.GRACE-0950_movieframes_M}}{% endcapture %}

{% include xml/AfricaSubSahara_GRACE-0950_movieframes_M.html foo=foo %}

#### Create GRACE movieclock and movie script

{% capture foo %}{{page.GRACE-0960_movieclock_M}}{% endcapture %}

{% include xml/AfricaSubSahara_GRACE-0960_movieclock_M.html foo=foo %}

__To view the maps and movies created in this posted, click the <span class='button'>Next</span> button below__.
