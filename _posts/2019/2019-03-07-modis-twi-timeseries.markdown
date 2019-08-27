---
layout: post
title: MODIS Transformed Wetness Index (TWI)
modified: '2019-03-07 20:17'
categories: blog
excerpt: Calculate MODIS TWI for regional project
tags:
  - MODIS
  - TWI
  - MCD43A4
  - Sub Saharan Africa
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-03-07 20:17'
comments: true
share: true
movie1: rainfall_3b43_trmm_199801-201807_v7-f
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

In this post data already produced as part of this project from the [Soil Moisture Active Passive (SMAP)](../smap-methods) mission are used for assimilating the [MODIS Transformed Wetness Index (TWI)]. The result is an adjusted soil moisture estimation at 463 m spatial and 16 days temporal resolution. Graphical presentation of some of the results are summarised in the [next](../modis-results) post.

# Prerequisites

To follow the processing steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/) and download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github. You must also [download and process the SMAP data](https://karttur.github.io/geoimagine/blog/blog-SMAP/) and [download MODIS](../modis-getdata) data and [calculate TWI](../modis-twi-methods).

# Downscaling

Spatial downscaling is typically divided into dynamic and statistical methods. Dynamic downscaling is much more demanding and require spatiotemporal data at the finer target resolution. Statistical downscaling instead uses proxy data at the finer target resolution and statistical functions for distribution the coarser estimates to target resolution.

In this project, soil moisture estimates are captured at 9 km from SMAP and at 500 (463) m from MODIS. The MODIS soil moisture index (TWI) suffers from biases related to both mineral compositions and vegetation cover. Adjusting TWI by assimilation of the mean and standard deviation of ground observed soil moisture reduces the biases. Ground observations, however, are restricted to a few locations. SMAP, on the other hand, has a global coverage.

As an alternative to traditional downscaling, in this study SMAP is used for assimilating TWI. By using comparative seasonal signals for defining the assimilation, the shorter SMAP record is used for adjusting the longer record of MODIS TWI soil moisture. The result is an 18 year long soil moisture record at 500 m spatial resolution.

# Process chain

The principal steps for adjusting MODIS TWI using SMAP with Karttur's GeoImagine Framework include:

- Create coherent datasets
- Cross correlation
- Extraction of overlapping seasonal signals
- Define assimilation parameters
- Infer assimilation

In the Framework a process chain can be built as a series of calls to xml coded instructions. This section contains the calls and the remaining parts of the post details each called xml.

<button id= "toggleProcessChain" onclick="hiddencode('ProcessChain')">Hide/Show AfricaSubSahara_process_TRMM.txt</button>

<div id="ProcessChain" style="display:none">
{% capture text-capture %}
{% raw %}
```
###################################
###################################
###  MODIS + SMAP assimilation  ###
###################################
###################################

## Update db with assimilated TWI A ##
#AfricaSubSahara_MODIS-0190_updatedb_TWI-assimilated-A.xml

###################################
###   Create coherent datasets  ###
###################################

## Tile SMAP to MODIS original spatiotemporal resolution ##
#AfricaSubSahara_SMAP-0162_tile_16D.xml

## Resample SMAP SINgrid back to 9km but using average ##
#AfricaSubSahara_SMAP-0170_resample-2-SMAP_16D.xml

## Resample MODIS to fit the SMAP 9 km spatial resolution (overlapping dates) ##
#AfricaSubSahara_MODIS-0170_resample-2-SMAP_16D.xml

###################################
###      Cross correlation      ###
###################################

## Cross correlate SMAP and TWI at 9kk and overlapping period (both filled)
## At both 500 m and 9 km spatial resolution
#AfricaSubSahara-MODIS-SMAP-0385_layer-x-cross_16D.xml

##############################################
###  Extract overlapping seasonal signals  ###
##############################################

## Extract MODIS an SMAP seasonal signals at 9km for overlapping period ##
#AfricaSubSahara_MODIS-SMAP-0320_extract-seasons_16D_2015-2018.xml

###################################
###     Define assimilation     ###
###################################

## Set MODIS to SMAP Assimilation (mean and standard deviation from master and slave) ##
#AfricaSubSahara_MODIS-SMAP-0380_setassimilation_16D.xml

###################################
###      Infer assimilation     ###
###################################

## Assimilate MODIS to SMAP at 9 km (infer the assimilation)
#AfricaSubSahara_MODIS-SMAP-0390_assimilate_16D_9km.xml

## Assimilate MODIS to SMAP at full resolution (infer the assimilation)
#AfricaSubSahara_MODIS-SMAP-0392_assimilate_16D.xml

###################################
###   Time Series Processing    ###
###################################

## Resample assimilated MODIS TWI to annual ##
#AfricaSubSahara_MODIS-0290_resample-2-A.xml

## Trend analysis on assimilated TWI ##
#AfricaSubSahara_MODIS-0310_trend_A_2001-2017.xml

###################################
###         Export Media        ###
###################################

#Export 9km SMAP, TWI original and TWI assimilated, same period and palette
#AfricaSubSahara_MODIS-SMAP-0900_ExporttoByte_16D_9km.xml

#Export MODIS 16D tiles
#AfricaSubSahara_MODIS-0900_ExporttoByte_16D.xml

#Export MODIS annual tiles
#AfricaSubSahara_MODIS-0900_ExporttoByte_A.xml

#Export MODIS statistics, trends and changes
#AfricaSubSahara_MODIS-0900_ExporttoByte_A.xml

###################################
###     MODIS + SMAP MOVIES     ###
###################################

## Create movieframes for TWI, SMAP and 2 versions of TWI assimilated to SMAP ##
#AfricaSubSahara_MODIS-SMAP-0950_movieframes-tiles_16D_9km.xml

#Append to frames to combined movie (done in 3 steps to create a movie with 4 frames)
#AfricaSubSahara_MODIS-SMAP-0951_movieframes-append-tiles_16D_9km.xml

## Movie clock, overlay and movie generation for appended tile versions ##
#AfricaSubSahara_MODIS-SMAP-0960_movielock-append-tiles_16D_9km.xml
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

### Time Series Processing

The time series analysis of the MODIS soil moisture estimate (TWI) uses the assimilated TWI as starting point.

#### Resample to annual soil moisture

Process: [<span class='package'>resampletsModisRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-resampletsModisRegion/).

{% capture foo %}{{page.AfricaSubSahara_MODIS-0290_resample-2-A}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-0290_resample-2-A.html foo=foo %}

#### Annual statistics and trends

Process: [<span class='package'>trendtsmodis</span>](https://karttur.github.io/geoimagine/subprocess/subproc-trendtsmodis/).

{% capture foo %}{{page.AfricaSubSahara_MODIS-0310_trend_A_2001-2017}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-0310_trend_A_2001-2017.html foo=foo %}

#### Annual changes and significant trends

{% capture foo %}{{page.AfricaSubSahara_MODIS-0320_changes_A_2001-2018}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-0320_changes_A_2001-2018.html foo=foo %}

### Export Media

#### Export 9km SMAP, TWI original and TWI assimilated

{% capture foo %}{{page.AfricaSubSahara_MODIS-SMAP-0900_ExporttoByte_16D_9km}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-SMAP-0900_ExporttoByte_16D_9km.html foo=foo %}

#### Export MODIS 16D tiles

Exports assimilated MODIS 16 day tiles at original (500 m) spatial resolution.

{% capture foo %}{{page.AfricaSubSahara_MODIS-0900_ExporttoByte_16D}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-0900_ExporttoByte_16D.html foo=foo %}

#### Export MODIS annual tiles

{% capture foo %}{{page.AfricaSubSahara_MODIS-0900_ExporttoByte_A}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-0900_ExporttoByte_A.html foo=foo %}

#### Export MODIS statistics, trends and changes

#AfricaSubSahara_MODIS-0900_ExporttoByte_timespanA.xml

### Movies

The spatial resolution of the MODIS TWI (500m) means that a single tile at full spatial resolution is 2400 rows * 2400 columns. That is too large for a movie. At the spatial resolution of the SMAP enhanced product (9 km) each tile is 120 * 120. Combining 4 tiles in a square would then become 240 * 240.

The movies for illustrating SMAP, TWI and the assimilation of TWI to SMAP are thus created per tile and combining 4 movies. Below, the first step creates 4 single movie frames, the second step combined the 4 individual movie frames, and in the last step movie clocks are created and overlaid over the combined frame and the movie produced.

#### Single movie movieframes

The commands in the hidden xml file creates movieframes for TWI, SMAP and 2 versions of TWI assimilated to SMAP.

{% capture foo %}{{page.AfricaSubSahara_MODIS-SMAP-0950_movieframes-tiles_16D_9km}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-SMAP-0950_movieframes-tiles_16D_9km.html foo=foo %}

#### Concatenate frames

The concatenation of movie frames is done in three steps, first combining 2 horisontal frames twice, and then combining the horisontally concatenated frames vertically.

{% capture foo %}{{page.AfricaSubSahara_MODIS-SMAP-0951_movieframes-append-tiles_16D_9km}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-SMAP-0951_movieframes-append-tiles_16D_9km.html foo=foo %}

#### Movie clock and movie generation

Create a movie clock, overlay the clock-timeline on the 4-frame concatenated movie frames and generate the movie.

{% capture foo %}{{page.AfricaSubSahara_MODIS-SMAP-0960_movielock-append-tiles_16D_9km}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-SMAP-0960_movielock-append-tiles_16D_9km.html foo=foo %}
