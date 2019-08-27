---
layout: post
title: Adjust TWI with SMAP
modified: '2019-03-05 20:17'
categories: blog
excerpt: Reduce estimated TWI soil moisture biases by assimilation to SMAP
tags:
  - MODIS
  - TWI
  - SMAP_16D
  - assimilation
  - Sub Saharan Africa
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-03-05 20:17'
comments: true
share: true
movie1: rainfall_3b43_trmm_199801-201807_v7-f
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

In this post data already produced as part of this project from the [Soil Moisture Active Passive (SMAP)](../smap-methods) mission are used for adjusting the [MODIS Transformed Wetness Index (TWI)](../modis-twi-methods/) using assimilation. The result is an adjusted (or downscaled) soil moisture estimation at 463 m spatial and 16 days temporal resolution. The [next](../../modis-twi-timeseries/) post outlines the processes for calculating trends and changes from the assimilated TWI. Graphical presentation of some of the results are summarised in the [this](../modis-results) post.

# Prerequisites

To follow the processing steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/) and download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github. You must also [download and process the SMAP data](https://karttur.github.io/geoimagine/blog/blog-SMAP/) and [download MODIS](../modis-getdata) data and [calculate TWI](../modis-twi-methods).

# Downscaling

Spatial downscaling is typically divided into dynamic and statistical methods. Dynamic downscaling is much more demanding and require spatiotemporal data at the finer target resolution. Statistical downscaling instead uses proxy data at the finer target resolution and statistical functions for distribution the coarser estimates to target resolution.

In this project, soil moisture estimates are captured at 9 km from SMAP and at 500 (463) m from MODIS. The MODIS soil moisture index (TWI) suffers from biases related to both mineral compositions and vegetation cover. Adjusting TWI by assimilation of the mean and standard deviation of ground observed soil moisture reduces the biases (see [Gumbricht, 2018](https://doi.org/10.3390/rs10040611)). Ground observations, however, are restricted to a few locations. SMAP, on the other hand, has a global coverage.

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

### Create coherent datasets

In this project you are going to use a temporal assimilation (adjusting the mean and standard deviation) for adjusting MODIS TWI to the temporal statistics of SMAP. This is a valid approach under the assumption that MODIS TWI captures both the spatial and temporal dynamics of variations in soil moisture but that the absolute accuracy of SMAP estimated soil moisture is better. To test the coherency of the two datasets, and to define the assimilation, the two datasets must cover the same spatial and temporal domains.

The spatial fitting of the SMAP data to MODIS tiles in the SINGrid projection is done in 2 steps. First the SMAP data is resampled (as MODIS SINgrid tiles) to a spatial resolution of 500 m (the original resolution of the MODS MCD43A4 product), and then the resampled 500 m data are used for creating a 9 km averaged SMAP soil moisture product. The two-step process assures the spatial coherence when comparing the two datasets. The MODIS data is converted to 9 km using the same averaged resampling.

#### Tile SMAP to MODIS @ 500 m

Process: [<span class='package'>imagecrosstrendtsmodis</span>](https://karttur.github.io/geoimagine/subprocess/subproc-imagecrosstrendtsmodis/).

The SMAP data used for adjusting TWI is the enhanced passive product (SPL3SMP_E version 002). In a [previous](../smap-methods) post this data was tiled to 9 km spatial resolution as part of this project. The tiling directly to 9 km, however, is less accurate compared to first tiling to 500 m using nearest neighbor and then resampling to 9 km using averaging. For the purpose of assimilation, the higher accuracy is recommended but also takes longer time and require more computer resources.

{% capture foo %}{{page.AfricaSubSahara_SMAP-0162_tile_16D}}{% endcapture %}
{% include xml/AfricaSubSahara_SMAP-0162_tile_16D.html foo=foo %}

#### Resample to 9km

If you choose to tile (resample) the SMAP data to 500 m you now need to resample both soil moisture estimates to the 9 km SMAP resolution. If you tiled the SMAP data directly to 9 km, you only need to resample the MODIS TWI data to 9 km. 

Process: [<span class='package'>imagecrosstrendtsmodis</span>](https://karttur.github.io/geoimagine/subprocess/subproc-imagecrosstrendtsmodis/).

The same resampling is applied to the SMAP and MODIS data to create datasets at 9 km spatial resolution.

{% capture foo %}{{page.AfricaSubSahara_SMAP-0170_resample-2-SMAP_16D}}{% endcapture %}
{% include xml/AfricaSubSahara_SMAP-0170_resample-2-SMAP_16D.html foo=foo %}

### Cross correlation

The cross correlation between SMAP and TWI reveals the consistency in capturing variations in soil moisture between the two datasets (see the [next](../modis-twi-results/) post for graphical results).

Process: [<span class='package'>imagecrosstrendtsmodis</span>](https://karttur.github.io/geoimagine/subprocess/subproc-imagecrosstrendtsmodis/).

{% capture foo %}{{page.AfricaSubSahara-MODIS-SMAP-0385_layer-x-cross_16D}}{% endcapture %}
{% include xml/AfricaSubSahara-MODIS-SMAP-0385_layer-x-cross_16D.html foo=foo %}

### Extraction of overlapping seasonal signals

The assimilation is done using seasonal signals extracted from overlapping spatial and temporal domains. Extract the corresponding seasonal signals with the process [<span class='package'>extractseasonModisRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-extractseasonModisRegion/).

{% capture foo %}{{page.AfricaSubSahara_MODIS-SMAP-0320_extract-seasons_16D_2015-2018}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-SMAP-0320_extract-seasons_16D_2015-2018.html foo=foo %}

### Define assimilation

The assimilation parameters are defined using the process [<span class='package'>setAssimilationModisRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-setAssimilationModisRegion/). The process requires two source layers, a master and a slave. The two layers must have exactly the same spatial and temporal resolution. In this project the seasonal signals 2015 to 2018 are used as source layers.

{% capture foo %}{{page.AfricaSubSahara_MODIS-SMAP-0380_setassimilation_16D}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-SMAP-0380_setassimilation_16D.html foo=foo %}

### Infer assimilation

Infer the assimilation with the process [<span class='package'>assimilateModisRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-assimilateModisRegion/).

#### @ 9 km spatial resolution

The xml commands below infer the assimilation on the reampled 9 km MODIS TWI. The results are used for direct comparisons of the SMAP, the original and assimilated TWI in the [next](../blog-smap-modis.adjust-result-region) post.

{% capture foo %}{{page.AfricaSubSahara_MODIS-SMAP-0390_assimilate_16D_9km}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-SMAP-0390_assimilate_16D_9km.html foo=foo %}

#### @ 500 m spatial Resolution

In the xml file hidden below, the assimilation parameters derived at 9 km are inferred to the full time series of MODIS TWI estimated at the original (500 m) spatial resolution.

Process: [<span class='package'>assimilateModisRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-assimilateModisRegion/).

{% capture foo %}{{page.AfricaSubSahara_MODIS-SMAP-0392_assimilate_16D}}{% endcapture %}
{% include xml/AfricaSubSahara_MODIS-SMAP-0392_assimilate_16D.html foo=foo %}
