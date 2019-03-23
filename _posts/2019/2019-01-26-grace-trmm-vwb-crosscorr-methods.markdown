---
layout: post
title: Rainfall, water balance and Earth´s water content - methods
modified: '2019-01-26 20:17'
categories: blog
excerpt: Cross correlations between variations in rainfall, vertical water balance and equivalent water pillar depth
tags:
  - GRACE
  - Tropical Rainfall Measurement Mission
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-01-26 20:17'
comments: true
share: true

TRMM-GRACE-0370_dualtrendcomp_2003-2016: TRMM-GRACE-0370_dualtrendcomp_2003-2016

TRMM-GRACE-0385_layer-x-corr_2003-2016: TRMM-GRACE-0385_layer-x-corr_2003-2016

TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016: TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016

TRMM-GRACE-0951_overlay-movieframes_M: TRMM-GRACE-0951_overlay-movieframes_M

TRMM-GRACE-0960_movieclock_M: TRMM-GRACE-0960_movieclock_M
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post outlines a process chain for comparing the variations between rainfall and Vertical Water Balance (VWB) on the one hand and the Earth´s land water content on the other. The results are presented in the [next](../grace-results/) post.

# Prerequisites

To follow the processing steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/), download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github. You must also have completed the processing of [Tropical Rainfall Measurement Mission (TRMM) rainfall](../trmm-methods), the [VWB](../vwb-methods), and the [equivalent water depth from the Gravity Recovery and Climate Experiment (GRACE)](../grace-methods), as described in earlier posts of this project.

# Drivers of Earth's water storage

In the water cycle, precipitation is the ultimate source for the water content in land areas. Not all precipitation that falls contributes towards filling the Earth's water content.
A fraction of the precipitated water is directly transferred back to the atmosphere by evapotranspiration. Theoretically the Vertical Water Balance (VWB) should thus be a better predictor for the variations in the equivalent water pillar depth compared to gross precipitation.

In this section, the correlation between precipitation and VWB as drivers (masters) and the equivalent water pillar as a slave is tested using graphics and local (per cell) cross correlation. The correlations ignore the redistribution of water over land from upstream to downstream.

# Process chain

The principal steps for creating estimations, maps and animations relating water input (precipitation and VWB) to water content (equivalent water pillar depth) over Africa using Karttur's GeoImagine Framework include:

- Overlay comparison
- Time series processing
- Mosaic
- Export media

In the Framework a process chain can be built as a series of calls to xml coded instructions. This section contains the calls and the remaining parts of the post details each called xml. As noted above, the results are available in the [next](../grace-trmm-vwb-crosscorr-results) post.

<button id= "toggleProcessChain" onclick="hiddencode('ProcessChain')">Hide/Show AfricaSubSahara_process_GRACE.txt</button>

<div id="ProcessChain" style="display:none">

{% capture text-capture %}
{% raw %}
```
###################################
###################################
###   TRMM vs GRACE analysis   ###
###################################
###################################

## The processing requires that the TRMM and GRACE processing above are completed ##

## trendcomp_createpalettes.xm

###################################
###     Overlay comparison      ###
###################################

## Compare trends from GRACE and TRMM  ##
#AfricaSubSahara_TRMM-GRACE-0370_dualtrendcomp_2003-2016.xml

###################################
###   Time Series Processing    ###
###################################

## Cross correlation between TRMM (master) and GRACE (slave) ##
AfricaSubSahara_TRMM-GRACE-0385_layer-x-corr_2003-2016.xml

###################################
###   	       Mosaic           ###
###################################

## Mosaic the TRMM-GRACE (Master-Slave) cross correlation results for Sub Saharan Africa ##
AfricaSubSahara_TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016.xml

## Mosaic the trend comparison TRMM-GRACE for Sub Saharan Africa ##
#AfricaSubSahara_TRMM-GRACE-0630_mosaic_trendcomp_2003-2016.xml

###################################
###        Export media         ###
###################################

## Export TRMM-GRACE (Master-Slave) cross correlation ##
#AfricaSubSahara050_TRMM-GRACE-ExporttoByte_crosscorr.xml

## Export trend comparison TRMM-GRACE results ##
#AfricaSubSahara050_TRMM-GRACE-ExporttoByte_trendcomp.xml

## Create TRMM-GRACE overlay movieframes ##
#AfricaSubSahara055_GRACE+TRMM-overlaymovieframes_M.xml
#AfricaSubSahara_TRMM-GRACE-0951_overlay-movieframes_M.xml

## Create Movieclock and scripts for TRMM + GRACE overlay movie with movieclock overlay
#AfricaSubSahara_TRMM-GRACE-0960_movieclock_M.xml

###################################
###################################
###   VWB vs GRACE analysis   ###
###################################
###################################

## The processing requires that the VWB and GRACE processing above are completed ##

###################################
###     Overlay comparison      ###
###################################

## Compare trends from GRACE and VWB  ##
#AfricaSubSahara_VWB-GRACE-0370_dualtrendcomp_2003-2016.xml

###################################
###   Time Series Processing    ###
###################################

## Cross correlation between TRMM (master) and GRACE (slave) ##
#AfricaSubSahara_VWB-GRACE-0385_layer-x-corr_2003-2016.xml

###################################
###   	       Mosaic           ###
###################################

## Mosaic the VWB-GRACE (Master-Slave) cross correlation results for Sub Saharan Africa ##
AfricaSubSahara_VWB-GRACE-0625_mosaic_layer-x-corr_2003-2016.xml

## Mosaic the trend comparison VWB-GRACE for Sub Saharan Africa ##
#AfricaSubSahara_VWB-GRACE-0630_mosaic_trendcomp_2003-2016.xml

###################################
###        Export media         ###
###################################

## Export VWB-GRACE (Master-Slave) cross correlation ##
AfricaSubSahara_VWB-GRACE-0925-ExporttoByte_layer-x-corr_2003-2016.xml

## Export trend comparison VWB-GRACE results ##
#AfricaSubSahara_VWB-GRACE-0930-ExporttoByte_trendcomp.xml

## Create VWB-GRACE overlay movieframes ##
#AfricaSubSahara_VWB-GRACE-0951_overlay-movieframes_M.xml

## Create Movieclock and scripts for TRMM + GRACE overlay movie with movieclock overlay
#AfricaSubSahara_VWB-GRACE-0960_movieclock_M.xml
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

## Overlay comparison

As part of the processing of [TRMM rainfall](../trmm-methods), [VWB](../vwb-methods) and [GRACE equivalent water pillar depth](..(grace-methods)) the absolute changes of each has already been calculated. Here, a special overlay process is applied comparing two overlapping layers depicting changes or trends. The overlay identifies the congruence between the two change layers in 9 classes:

||           |                                  |      1st layer      |                 |
||           |           Increase                       |      No change      |     Decrease            |
||:---------|:--------------------------------:|:-------------------:|:---------------:|
||       <b>Increase</b>   |         both increasing          |    1st no change<br>2nd increasing    | 1st decreasing<br>2nd increasing   |
|<b>2nd layer</b>| <b>No change</b> | 1st increasing<br>2nd no change | No change in either | 1st decreasing<br>2nd no change  |
||     <b>Decrease</b>      |             1st increasing<br>2nd decreasing            |         1st no change<br>2nd decreasing          | both decreasing |

The overlay can be done with any two change layers and here the overlay comparisons are done for layers including changes for all regions, and layers with only significant changes.

### TRMM vs GRACE

{% capture foo %}{{page.TRMM-GRACE-0370_dualtrendcomp_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-GRACE-0370_dualtrendcomp_2003-2016.html foo=foo %}

### VWB vs GRACE

{% capture foo %}{{page.TRMM-GRACE-0370_dualtrendcomp_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-GRACE-0370_dualtrendcomp_2003-2016.html foo=foo %}

## Time Series Processing

The time series process is restricted to cross correlations between monthly variations in a master (rainfall or VWB) driving a slave (equivalent water pillar depth). The cross correlations are done at pixel by pixel time series. Following the results from comparing different smoothing algorithms [cross correlating climate indexes and TRMM](../trmm-results), the layer to layer cross correlation was done using a 12 month naive kernel. The allowed lag was restricted to slave responses following 0 to 6 months after the master signal.

### Precipitation as driver of water content

{% capture foo %}{{page.TRMM-GRACE-0385_layer-x-corr_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-GRACE-0385_layer-x-corr_2003-2016.html foo=foo %}

### VWB as driver of water content

{% capture foo %}{{page.TRMM-GRACE-0385_layer-x-corr_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-GRACE-0385_layer-x-corr_2003-2016.html foo=foo %}

## Mosaic

In this projects, the mosaicking is only done for the exports in the next step. In the mosaic process, the tiles are first concatenated and then cut to the actual coordinates of the defining region. Cell values and data type remain the same, but the data can be reprojected on the fly.

### Mosaic TRMM vs GRACE cross correlation

{% capture foo %}{{page.TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016.html foo=foo %}

### Mosaic VWB vs GRACE cross correlation

{% capture foo %}{{page.TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016.html foo=foo %}

## Export Media

The main reason for exporting the mosaicked layer is to allow visualization of both the data and the results.

### Export TRMM vs GRACE cross correlation
NOT DONE
{% capture foo %}{{page.TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016.html foo=foo %}

### Export VWB vs GRACE cross correlation
NOT DONE
{% capture foo %}{{page.TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-GRACE-0625_mosaic_layer-x-corr_2003-2016.html foo=foo %}

### Movies

The animated movies for a master and a slave are created by overlaying a smaller master frame over a larger slave (the size and position can be set as process parameters). The master and slave frames must first be produced as separate frames and then combined. The clock and time line are then overlaid as for other movies.

The movie creation requires that the command line applications [ImageMagick](https://karttur.github.io/setup-theme-blog/blog/install-imagemagick/) and [FFmpeg](https://karttur.github.io/setup-theme-blog/blog/ffmpeg-movie/) are installed.

#### Create TRMM vs GRACE overlay movieframes

{% capture foo %}{{page.TRMM-GRACE-0951_overlay-movieframes_M}}{% endcapture %}

{% include xml/AfricaSubSahara_TRMM-GRACE-0951_overlay-movieframes_M.html foo=foo %}

#### Create TRMM movieclock and movie script

{% capture foo %}{{page.TRMM-GRACE-0960_movieclock_M}}{% endcapture %}

{% include xml/AfricaSubSahara_TRMM-GRACE-0960_movieclock_M.html foo=foo %}
