---
layout: post
title: Water balance and Earth´s water content - methods
modified: '2019-01-27 20:17'
categories: blog
excerpt: Cross correlations between variations in vertical water balance and equivalent water pillar depth
tags:
  - GRACE
  - Vertical Water Balance
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-01-27 20:17'
comments: true
share: true

AfricaSubSahara_VWB-GRACE-0370_dualtrendcomp_2003-2016: AfricaSubSahara_VWB-GRACE-0370_dualtrendcomp_2003-2016
AfricaSubSahara_VWB-GRACE-0385_layer-x-corr_2003-2016: AfricaSubSahara_VWB-GRACE-0385_layer-x-corr_2003-2016
AfricaSubSahara_VWB-GRACE-0625_mosaic_layer-x-corr_2003-2016: AfricaSubSahara_VWB-GRACE-0625_mosaic_layer-x-corr_2003-2016
AfricaSubSahara_VWB-GRACE-0630_mosaic_trendcomp_2003-2016: AfricaSubSahara_VWB-GRACE-0630_mosaic_trendcomp_2003-2016
AfricaSubSahara_VWB-GRACE-0925-ExporttoByte_layer-x-corr_2003-2016: AfricaSubSahara_VWB-GRACE-0925-ExporttoByte_layer-x-corr_2003-2016
AfricaSubSahara_VWB-GRACE-0930-ExporttoByte_trendcomp: AfricaSubSahara_VWB-GRACE-0930-ExporttoByte_trendcomp
AfricaSubSahara_VWB-GRACE-0951_overlay-movieframes_M: AfricaSubSahara_VWB-GRACE-0951_overlay-movieframes_M
AfricaSubSahara_VWB-GRACE-0960_movieclock_M: AfricaSubSahara_VWB-GRACE-0960_movieclock_M
AfricaSubSahara_VWB-GRACE-0980-archive-zip_trendcomp: AfricaSubSahara_VWB-GRACE-0980-archive-zip_trendcomp
AfricaSubSahara_VWB-GRACE-0980_archive-zip_layer-x-corr_2003-2016: AfricaSubSahara_VWB-GRACE-0980_archive-zip_layer-x-corr_2003-2016

---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post outlines a process chain for comparing the variations between Vertical Water Balance (VWB) and the Earth´s land water content. The [previous](../grace-trmm-methods/) post instead compares rainfall and water content. The results are presented in the [next](../grace-trmm-vwb-results/) post.

# Prerequisites

To follow the processing steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/), download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github. You must also have completed the processing of [VWB](../vwb-methods) and the [equivalent water depth from the Gravity Recovery and Climate Experiment (GRACE)](../grace-methods), as described in earlier posts of this project.

# Drivers of Earth's water storage

In the water cycle, precipitation is the ultimate source for the water content in land areas. Not all precipitation that falls contributes towards filling the Earth's water content.

A fraction of the precipitated water is directly transferred back to the atmosphere by evapotranspiration. Theoretically the Vertical Water Balance (VWB) should thus be a better predictor for the variations in the equivalent water pillar depth compared to gross precipitation.

In this section, the correlation between precipitation as a driver (master) and the equivalent water pillar as a slave is tested using graphics and local (per cell) cross correlation. The correlations ignore the redistribution of water over land from upstream to downstream. The [previous](../grace-trmm-crosscorr-methods/) post instead uses rainfall as the master. The results of both comparisons, with rainfall and VWB as drivers, are presented together in [this](../grace-trmm-vwb-crosscorr-results/) post.

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
###   VWB vs GRACE analysis   ###
###################################
###################################

## The processing requires that the project VWB and GRACE processing are completed ##

###################################
###          Update db          ###
###################################

## If you have access to preprocessed data created by karttur's Geoimagine Framework ##
## you can access the data from your Framework installation by updating the db ##
## You can also use updatedb to clean your database and/or delete files from your Framework organized storage ##

###################################
###     Overlay comparison      ###
###################################

## Compare trends from VWB and GRACE ##
#AfricaSubSahara_VWB-GRACE-0370_dualtrendcomp_2003-2016.xml

###################################
###   Time Series Processing    ###
###################################

## Cross correlation between VWB (master) and GRACE (slave) ##
#AfricaSubSahara_VWB-GRACE-0385_layer-x-corr_2003-2016.xml

###################################
###   	       Mosaic           ###
###################################

## Mosaic cross correlation VWB-GRACE (Master-Slave) results for Sub Saharan Africa ##
#AfricaSubSahara_VWB-GRACE-0625_mosaic_layer-x-corr_2003-2016.xml

## Mosaic change comparison VWB-GRACE for Sub Saharan Africa ##
#AfricaSubSahara_VWB-GRACE-0630_mosaic_trendcomp_2003-2016.xml

###################################
###        Export media         ###
###################################

## Export cross correlation VWB-GRACE (Master-Slave)  ##
#AfricaSubSahara_VWB-GRACE-0925-ExporttoByte_layer-x-corr_2003-2016.xml

## Export change comparison VWB-GRACE results ##
#AfricaSubSahara_VWB-GRACE-0930-ExporttoByte_trendcomp.xml

###   	       Movie            ###

## Create overlay image frames VWB-GRACE ##
#AfricaSubSahara_VWB-GRACE-0951_overlay-movieframes_M.xml

## Create clock frames and movie for VWB + GRACE overlay movie with movieclock overlay ##
#AfricaSubSahara_VWB-GRACE-0960_movieclock_M.xml

###################################
###          Archive            ###
###################################

## Archive cross correlation ##
#AfricaSubSahara_VWB-GRACE-0980_archive-zip_layer-x-corr_2003-2016.xml

## Archive change comparison VWB-GRACE for Sub Saharan Africa ##
AfricaSubSahara_VWB-GRACE-0980-archive-zip_trendcomp.xml
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

## Overlay comparison

As part of the processing of [VWB](../vwb-methods) and [GRACE equivalent water pillar depth](..(grace-methods)) the absolute changes of each has already been calculated. Here, a special overlay process is applied comparing two overlapping layers depicting changes or trends. The overlay identifies the congruence between the two change layers in 9 classes:

||           |                                  |      1st layer      |                 |
||           |           Increase                       |      No change      |     Decrease            |
||:---------|:--------------------------------:|:-------------------:|:---------------:|
||       <b>Increase</b>   |         both increasing          |    1st no change<br>2nd increasing    | 1st decreasing<br>2nd increasing   |
|<b>2nd layer</b>| <b>No change</b> | 1st increasing<br>2nd no change | No change in either | 1st decreasing<br>2nd no change  |
||     <b>Decrease</b>      |             1st increasing<br>2nd decreasing            |         1st no change<br>2nd decreasing          | both decreasing |

The overlay can be done with any two change layers and here the overlay comparisons are done for layers including changes for all regions, and layers with only significant changes.

Process: [dualtrendscompmodistiles](https://karttur.github.io/geoimagine/subprocess/subproc-dualtrendscompmodistiles/)

{% capture foo %}{{page.AfricaSubSahara_VWB-GRACE-0370_dualtrendcomp_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-GRACE-0370_dualtrendcomp_2003-2016.html foo=foo %}

## Time Series Processing

The time series process is restricted to cross correlations between monthly variations in a master (rainfall) driving a slave (equivalent water pillar depth). The cross correlations are done at pixel by pixel time series. Following the results from comparing different smoothing algorithms [cross correlating climate indexes and TRMM](../trmm-results), the layer to layer cross correlation was done using a 12 month naive kernel. The allowed lag was restricted to slave responses following 0 to 6 months after the master signal.

Process: [imagecrosstrendtsmodis](https://karttur.github.io/geoimagine/subprocess/subproc-imagecrosstrendtsmodis/)

{% capture foo %}{{page.AfricaSubSahara_VWB-GRACE-0385_layer-x-corr_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-GRACE-0385_layer-x-corr_2003-2016.html foo=foo %}

## Mosaic

In the mosaic process, the tiles are first concatenated and then cut to the actual coordinates of the defining region. Cell values and data type remain the same, but the data can be reprojected on the fly.

Process: [MosaicModis](https://karttur.github.io/geoimagine/subprocess/subproc-MosaicModis/)

###  Mosaic cross correlation

{% capture foo %}{{page.AfricaSubSahara_VWB-GRACE-0625_mosaic_layer-x-corr_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-GRACE-0625_mosaic_layer-x-corr_2003-2016.html foo=foo %}

### Mosaic change comparison

{% capture foo %}{{page.AfricaSubSahara_VWB-GRACE-0630_mosaic_trendcomp_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-GRACE-0630_mosaic_trendcomp_2003-2016.html foo=foo %}

## Export Media

Process: [exporttobytemodisRegionToRegion](https://karttur.github.io/geoimagine/subprocess/subproc-exporttobytemodisRegionToRegion/)

### Export cross correlation

{% capture foo %}{{page.AfricaSubSahara_VWB-GRACE-0925-ExporttoByte_layer-x-corr_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-GRACE-0925-ExporttoByte_layer-x-corr_2003-2016.html foo=foo %}

### Export change comparison

{% capture foo %}{{page.AfricaSubSahara_VWB-GRACE-0930-ExporttoByte_trendcomp}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-GRACE-0930-ExporttoByte_trendcomp.html foo=foo %}

### Movies

The animated movies for a master and a slave are created by overlaying a smaller master frame over a larger slave (the size and position can be set as process parameters). The master and slave frames must first be produced as separate frames and then combined. The clock and time line are then overlaid as for other movies.

The movie creation requires that the command line applications [ImageMagick](https://karttur.github.io/setup-theme-blog/blog/install-imagemagick/) and [FFmpeg](https://karttur.github.io/setup-theme-blog/blog/ffmpeg-movie/) are installed.

#### Create overlay image frames

Process: [mmovieoverlayframeModisRegion](https://karttur.github.io/geoimagine/subprocess/subproc-movieoverlayframeModisRegion/)

{% capture foo %}{{page.AfricaSubSahara_VWB-GRACE-0951_overlay-movieframes_M}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-GRACE-0951_overlay-movieframes_M.html foo=foo %}

#### Create clock frames and movie

Process: [movieclockModisRegionToRegion](https://karttur.github.io/geoimagine/subprocess/subproc-movieclockModisRegionToRegion/)

{% capture foo %}{{page.AfricaSubSahara_VWB-GRACE-0960_movieclock_M}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-GRACE-0960_movieclock_M.html foo=foo %}

## Archive

Archiving is done by creating zip files of each individual layer and saving it in a hierarchical structure identical to the original.

Process: [ArchiveModisRegionTiles](https://karttur.github.io/geoimagine/subprocess/subproc-ArchiveModisRegionTiles/)

### Archive cross correlation

{% capture foo %}{{page.AfricaSubSahara_VWB-GRACE-0980-archive-zip_trendcomp}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-GRACE-0980-archive-zip_trendcomp.html foo=foo %}

### Archive change comparison

{% capture foo %}{{page.AfricaSubSahara_VWB-GRACE-0980_archive-zip_layer-x-corr_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_VWB-GRACE-0980_archive-zip_layer-x-corr_2003-2016.html foo=foo %}

__To view the maps and movies created in this and the previous post, click the <span class='button'>Next</span> button below__.
