---
layout: post
title: TRMM rainfall - processes
modified: '2019-01-22 20:17'
categories: blog
excerpt: Processing TRMM precipitation data for a regional project
tags:
  - TRMM
  - Tropical Rainfall Measurement Mission
  - Sub Saharan Africa
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-01-22 20:17'
comments: true
share: true
movie1: rainfall_3b43_trmm_199801-201807_v7-f

TRMM-0160_tile_M: TRMM-0160_tile_M
TRMM-0161_tile_A: TRMM-0161_tile_A
TRMM-0310_trend_A_1998-2017: TRMM-0310_trend_A_1998-2017
TRMM-0310_trend_A_2003-2016: TRMM-0310_trend_A_2003-2016
TRMM-0320_changes_A_1998-2017: TRMM-0320_changes_A_1998-2017
TRMM-0320_changes_A_2003-2016: TRMM-0320_changes_A_2003-2016
TRMM-0380_index-x-corr_M: TRMM-0380_index-x-corr_M
TRMM-0610_mosaic_M: TRMM-0610_mosaic_M
TRMM-0620_mosaic_index-x-corr_M: TRMM-0620_mosaic_index-x-corr_M
TRMM-0630_mosaic_timespanA_1998-2017: TRMM-0630_mosaic_timespanA_1998-2017
TRMM-0630_mosaic_timespanA_2003-2016: TRMM-0630_mosaic_timespanA_2003-2016
TRMM-0900_ExporttoByte_M: TRMM-0900_ExporttoByte_M
TRMM-0910_ExporttoByte_timespanA_1998-2017: TRMM-0910_ExporttoByte_timespanA_1998-2017
TRMM-0910_ExporttoByte_timespanA_2003-2016: TRMM-0910_ExporttoByte_timespanA_2003-2016
TRMM-0920_ExporttoByte_crosscorr: TRMM-0920_ExporttoByte_crosscorr
TRMM-0950_movieframes_M: TRMM-0950_movieframes_M
TRMM-0960_movieclock_M: TRMM-0960_movieclock_M

---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post outlines a process chain for exploring and analysing rainfall and its change over Sub Saharan Africa using Karttur´s GeoImagine Framework. The results are presented in the [next](../trmm-results/) post.

# Prerequisites

To follow the process steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/), download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github, and [download and process the original TRMM data](https://karttur.github.io/geoimagine/blog/blog-TRMM/).

# TRMM

The Tropical Rainfall Measurement Mission (TRMM) ran for 17 years, from 1998 to 2017 (the radar ceased to function already in October 2014). The monthly precipitation product, [TRMM 3B43](https://mirador.gsfc.nasa.gov/collections/TRMM_3B43__007.shtml) developed from TRMM also makes use of other satellite borne precipitation estimates as well as ground based measurements. The product thus continues, despite that the TRMM instrument is no longer operational.

# Process chain

The principal steps for creating estimations, maps and animations of rainfall from TRMM data over Africa using Karttur's GeoImagine Framework include:

- Tile to region
- Time series processing
- Mosaic
- Export media

In the Framework a process chain can be built as a series of calls to xml coded instructions. This section contains the calls and the remaining parts of the post details each called xml. As noted above, the results are available in the [next](../trmm-results) post.

<button id= "toggleProcessChain" onclick="hiddencode('ProcessChain')">Hide/Show AfricaSubSahara_process_TRMM.txt</button>

<div id="ProcessChain" style="display:none">
{% capture text-capture %}
{% raw %}
```
###################################
###################################
###    TRMM data processing     ###
###################################
###################################

## The TRMM processing requires that the Tropical Rainfall Measurement Mission (TRMM) data are already processed and available ##

###################################
###       Tile to region        ###
###################################

## Tile monthly TRMM to region ##
AfricaSubSahara_TRMM-0160_tile_M.xml

## Tile annual TRMM to region ##
AfricaSubSahara_TRMM-0161_tile_A.xml

###################################
###   Time Series Processing    ###
###################################

## TRMM annual trends (1998-2017 is for the complete timeseries, 2003-2016 for overlap with GRACE
## should be done at tile level! Not by tiling original data. ##
AfricaSubSahara_TRMM-0310_trend_A_1998-2017.xml
AfricaSubSahara_TRMM-0310_trend_A_2003-2016.xml

## Changes and significant trends (1998-2017 is for the complete timeseries, 2003-2016 for overlap with GRACE ##
AfricaSubSahara_TRMM-0320_changes_A_1998-2017.xml
AfricaSubSahara_TRMM-0320_changes_A_2003-2016.xml

## Cross correlation climate indexes and TRMM  ##
AfricaSubSahara_TRMM-0380_index-x-corr_M.xml

###################################
###   	       Mosaic           ###
###################################

## Mosaic monthly TRMM ##
AfricaSubSahara_TRMM-0610_mosaic_M.xml

## Mosaic monthly climate Index vs TRMM cross correlation ##
AfricaSubSahara_TRMM-0620_mosaic_index-x-corr_M.xml

## Mosaic TRMM trends ##
AfricaSubSahara_TRMM-0630_mosaic_timespanA_1998-2017.xml
AfricaSubSahara_TRMM-0630_mosaic_timespanA_2003-2016.xml

###################################
###        Export media         ###
###################################

## Export monthly TRMM mosaics ##
AfricaSubSahara_TRMM-0900_ExporttoByte_M.xml

## Export TRMM annual trends #
AfricaSubSahara_TRMM-0910_ExporttoByte_timespanA_1998-2017.xml
AfricaSubSahara_TRMM-0910_ExporttoByte_timespanA_2003-2016.xml

# Export Climate Index vs TRMM Cross correlation ##
AfricaSubSahara_TRMM-0920_ExporttoByte_crosscorr.xml

## Create TRMM movieframes ##
AfricaSubSahara_TRMM-0950_movieframes_M.xml

## Create TRMM Movieclock and movie script ##
AfricaSubSahara_TRMM-0960_movieclock_M.xml
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

## Tile to region

In this project the dominating tile system is the MODIS SIN grid dividing the earth in 36 horizontal and 18 vertical tiles. For the TRMM data, the starting point is the monthly TRMM rainfall estimates. Also the annually aggregated rainfall estimates are captured by tiling.  Alternatively, the annually aggregated rainfall can be calculated using the tiled monthly data. The imported TRMM data are not the original data, but data that have been cleaned regarding nodata as described in [this](https://karttur.github.io/geoimagine/blog/blog-TRMM/) post.

### Tile monthly TRMM to region

Process: [tileRegionToModisAncillary](https://karttur.github.io/geoimagine/subprocess/subproc-tileRegionToModisAncillary/)

{% capture foo %}{{page.TRMM-0160_tile_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0160_tile_M.html foo=foo %}

### Tile annual TRMM to region

Process: [tileRegionToModisAncillary](https://karttur.github.io/geoimagine/subprocess/subproc-tileRegionToModisAncillary/)

{% capture foo %}{{page.TRMM-0161_tile_A}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0161_tile_A.html foo=foo %}

## Time Series Processing

In the process chain used here, the aggregation of monthly to annual rainfall was done using the global TRMM data, and the annual rainfall imported through tiling (above). Also the other time series processes can be produced and imported in the same manner. The aggregation of the TRMM data to other spatial resolutions, however, causes interpolation errors and thus it is strongly recommended to redo the time series analysis directly using the tiled (monthly or annual) data.

### TRMM annual trends

The annual trends are estimated using two methods, ordinary least square (OLS) regression, and a Mann-Kendall (MK) test together with a Theil-Sen regression. Also the period mean and standard deviations are calculated. These calculations are done for two different periods, 1998 - 2017 and 2003 - 2016. The longer period includes all years with complete coverage of TRMM data. The shorter period corresponds to the availability of data from the [Gravity Recovery And Climate Experiment (GRACE)](https://grace.jpl.nasa.gov) mission. The latter data is a direct estimate of the Earth's water reservoirs over land.

Process: [trendtsmodis](https://karttur.github.io/geoimagine/subprocess/subproc-trendtsmodis/)

#### 1998-2017

The complete TRMM time series is analysed at a spatial scale corresponding to the resolution of the original data (approximately 30 km).

{% capture foo %}{{page.TRMM-0310_trend_A_1998-2017}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0310_trend_A_1998-2017.html foo=foo %}

#### 2013-2016

The TRMM time series corresponding to the available GRACE data is processed at the 1 degree spatial scale of the GRACE data  (approximately 111 km).

{% capture foo %}{{page.TRMM-0310_trend_A_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0310_trend_A_2003-2016.html foo=foo %}

## Changes and significant trends

Regions with significant negative (precipitation decrease) or positive (increase) are calculated using the MK scores and with the strength of significant trends captured as the slope and absolute change in precipitation as estimated from the median Theil-Sen regression. Again the analysis covers two different periods, representing the complete TRMM time series (1998-2017) and the overlap with GRACE data (2003-2016). The former period is in a spatial resolution resembling the original TRMM data while the latter in the more coarse resolution of the GRACE data. The latter allows direct overlay with GRACE data as described in other posts belonging to this project.

Process: [signiftrendsmodis](https://karttur.github.io/geoimagine/subprocess/subproc-signiftrendsmodis/)

#### 1998-2017

{% capture foo %}{{page.TRMM-0320_changes_A_1998-2017}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0320_changes_A_1998-2017.html foo=foo %}

#### 2013-2016

{% capture foo %}{{page.TRMM-0320_changes_A_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0320_changes_A_2003-2016.html foo=foo %}

### Cross correlation climate indexes and TRMM

 Climate indexes capturing the key variability of the internal dynamics of the Earth´s climate system have been widely used for understanding and forecasting e.g. the El Nino Southern Oscillation (ENSO), the North Atlantic Oscillation (NAO) and Pacific Decadal Oscillation (PDO). In this section a set of global climate indexes are compared to the local TRMM rainfall.

 To run the cross correlation you must have [captured the climate indexes](https://karttur.github.io/geoimagine/blog/blog-climateindex/) into the Framework. You can also use the Framework to [visually explore the climate indexes](https://karttur.github.io/geoimagine/blog/blog-climate-graph/). Time series decomposition and smoothing, and other options are shown in [a post on cross corrleation between climate indexes and single location (pixel) TRMM](https://karttur.github.io/geoimagine/blog/blog-climate-trmm-crosscorr/).

The processes here generate maps of the correlations (expressed as the Pearson number) and the lag (expressed as number of months) between different climate index and the local rainfall. To test the stability of the cross correlation using different smoothing algorithms and filter lengths, five different parameterizations are tested in the xml below.

Process: [indexcrosstrendtsmodis](https://karttur.github.io/geoimagine/subprocess/subproc-indexcrosstrendtsmodis/)

 {% capture foo %}{{page.TRMM-0380_index-x-corr_M}}{% endcapture %}
 {% include xml/AfricaSubSahara_TRMM-0380_index-x-corr_M.html foo=foo %}

## Mosaic

In this projects, the mosaicking is only done for the exports in the next step. In the mosaic process, the tiles are first concatenated and then cut to the actual coordinates of the defining region. Cell values and data type remain the same, but the data can be reprojected on the fly.

Process: [MosaicModis](https://karttur.github.io/geoimagine/subprocess/subproc-MosaicModis/)

### Mosaic monthly TRMM

The monthly mosaics are primarily used for creating the movies of the rainfall dynamics.

{% capture foo %}{{page.TRMM-0610_mosaic_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0610_mosaic_M.html foo=foo %}

### Mosaic climate Index vs TRMM cross correlation

Because of the comparison of five (5) different parameter settings, six (6) different indexes and then also four (4) different time series components, a large number of layers have to be mosaicked if all are to be included. Clicking the <span class='nutton'>Hide/Show button</span> below might thus respond slowly.

{% capture foo %}{{page.TRMM-0620_mosaic_index-x-corr_M}}{% endcapture %}

{% include xml/AfricaSubSahara_TRMM-0620_mosaic_index-x-corr_M.html foo=foo %}

### Mosaic TRMM trends

The annual trends were calculated for two different periods (see above). The shorter period (2003-2016) was primarily done for comparing TRMM and GRACE, and need not be mosaicked and exported. It is, however, included to allow graphical comparisons of both different periods as well as the difference between TRMM and GRACE.

#### 1998-2018  

{% capture foo %}{{page.TRMM-0630_mosaic_timespanA_1998-2017}}{% endcapture %}

{% include xml/AfricaSubSahara_TRMM-0630_mosaic_timespanA_1998-2017.html foo=foo %}

### 2003-2016

{% capture foo %}{{page.TRMM-0630_mosaic_timespanA_2003-2016}}{% endcapture %}

{% include xml/AfricaSubSahara_TRMM-0630_mosaic_timespanA_2003-2016.html foo=foo %}

## Export Media

The main reason for exporting the mosaicked layer is to allow visualization of both the data and the results.

Process: [exporttobytemodisRegionToRegion](https://karttur.github.io/geoimagine/subprocess/subproc-exporttobytemodisRegionToRegion/)

### Export monthly TRMM mosaics

The monthly images of the precipitation are exported in order to use each date as a frame in animations (movies).

{% capture foo %}{{page.TRMM-0900_ExporttoByte_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0900_ExporttoByte_M.html foo=foo %}

### Export TRMM annual trends

The annual trends were calculated for two different periods (see above). The shorter period (2003-2016) was primarily done for comparing TRMM and GRACE, and need not be mosaicked and exported. It is, however, included to allow graphical comparisons of both different periods as well as the difference between TRMM and GRACE.

#### 1998-2017

{% capture foo %}{{page.TRMM-0630_mosaic_timespanA_1998-2017}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0630_mosaic_timespanA_1998-2017.html foo=foo %}

#### 2003-2016

{% capture foo %}{{page.TRMM-0630_mosaic_timespanA_2003-2016}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0630_mosaic_timespanA_2003-2016.html foo=foo %}

#### Export Climate Index vs TRMM Cross correlation

{% capture foo %}{{page.TRMM-0920_ExporttoByte_crosscorr}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0920_ExporttoByte_crosscorr.html foo=foo %}

### Movies

To create the animated movie showing the monthly rainfall over Sub Saharan Africa the monthly rainfall data must be mosaicked and exported as color maps as outlined above. The movie is created using two processes; the first process converts the exported color maps to movie frames and the the second process created a clock and a timeline that fits the frames. The second process also produces a shell script that must be executed (run) to produce the movie.

The movie creation requires that the command line applications [ImageMagick](https://karttur.github.io/setup-theme-blog/blog/install-imagemagick/) and [FFmpeg](https://karttur.github.io/setup-theme-blog/blog/ffmpeg-movie/) are installed.

#### Create TRMM movieframes

Process: [movieframeModisRegionToRegion](https://karttur.github.io/geoimagine/subprocess/subproc-movieframeModisRegionToRegion/)

{% capture foo %}{{page.TRMM-0950_movieframes_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0950_movieframes_M.html foo=foo %}

#### Create TRMM movieclock and movie script

Process: [movieclockModisRegionToRegion](https://karttur.github.io/geoimagine/subprocess/subproc-movieclockModisRegionToRegion/)

{% capture foo %}{{page.TRMM-0960_movieclock_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0960_movieclock_M.html foo=foo %}

__To view the maps and movies created in this posted, click the <span class='button'>Next</span> button below__.
