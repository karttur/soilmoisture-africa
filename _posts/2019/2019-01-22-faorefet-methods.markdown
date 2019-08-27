---
layout: post
title: FAO reference ET - processes
modified: '2019-01-22 20:17'
categories: blog
excerpt: Processing FAO reference evapotranspiration (ET) data for a regional project
tags:
  - FAO reference evapotranspiration
  - refET
  - Sub Saharan Africa
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-01-22 20:17'
comments: true
share: true
AfricaSubSahara_FAOrefET-0980_arcihive-zip_staticM: AfricaSubSahara_FAOrefET-0980_arcihive-zip_staticM
AfricaSubSahara_FAOrefET-0160_tile_staticM: AfricaSubSahara_FAOrefET-0160_tile_staticM
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post outlines a process chain for organising reference evapotranspiration data over Sub Saharan Africa using Karttur´s GeoImagine Framework. The results are used for calculating regional water balances as outlined in the [next](../vwb-methods/) post.

# Prerequisites

To follow the process steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/), download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github, and [download and process the FAO ref ET data](https://karttur.github.io/geoimagine/blog/blog-FAO-refevap/).

# FAO reference evapotranspiration (refET)

The FAO dataset on reference evapotranspiration (refET) is composed of monthly average layers representing 1961 to 1990. The refET varies dependent of many factors, including temperature, wind and atmospheric water vapor pressure, but for this study you will use monthly average data. The alternative, to calculate dynamic refET is complicated and the data demands exceeds the available.

# Process chain

In the Framework, a process chain can be built as a series of calls to xml coded instructions. The process chain calls are under the <span class='button'>Hide/Show</span> button below and the remaining parts of the post details each called xml.

<button id= "toggleProcessChain" onclick="hiddencode('ProcessChain')">Hide/Show AfricaSubSahara_process_FAOrefET.txt</button>

<div id="ProcessChain" style="display:none">
{% capture text-capture %}
{% raw %}
```
###################################
###################################
###    FAO refET processing     ###
###################################
###################################

## The processing requires that the FAO reference evapotranspiration is captured and organized ##

###################################
###          Update db          ###
###################################

## If you have access to TRMM data created by karttur's Geoimagine Framework ##
## you can access the data from your Framework installation by updating the db ##
## You can also use updatedb to clean your database and/or delete files from your Framework organized storage ##

## Update db for FAO refET, if needed ##
#FAOrefET-0190_udatedb.xml

###################################
###       Tile to region        ###
###################################

## Tile FAO refET to region ##
#AfricaSubSahara_FAOrefET-0160_tile_staticM.xml

###################################
###           Archive           ###
###################################

## Archive ##
#AfricaSubSahara_FAOrefET-0980_arcihive-zip_staticM.xml
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

## Tile to region

In this project the dominating tile system is the MODIS SIN grid dividing the earth in 36 horizontal and 18 vertical tiles.

### Tile static monthly refET

Process: [tileRegionToModisAncillary](https://karttur.github.io/geoimagine/subprocess/subproc-tileRegionToModisAncillary/)

{% capture foo %}{{page.AfricaSubSahara_FAOrefET-0160_tile_staticM}}{% endcapture %}
{% include xml/AfricaSubSahara_FAOrefET-0160_tile_staticM.html foo=foo %}

## Archive

Archiving is done by creating zip files of each individual layer and saving it in a hierarchical structure identical to the original.

Process: [ArchiveModisRegionTiles](https://karttur.github.io/geoimagine/subprocess/subproc-ArchiveModisRegionTiles/)

{% capture foo %}{{page.AfricaSubSahara_FAOrefET-0980_arcihive-zip_staticM}}{% endcapture %}
{% include xml/AfricaSubSahara_FAOrefET-0980_arcihive-zip_staticM.html foo=foo %}
