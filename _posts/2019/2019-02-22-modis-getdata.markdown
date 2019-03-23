---
layout: post
title: MODIS - get the data
modified: '2019-02-22 20:17'
categories: blog
excerpt: Downloading and organizing MODIS data for a regional project
tags:
  - MODIS
  - MCD43A4
  - Sub Saharan Africa
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-02-22 20:17'
comments: true
share: true
movie1: rainfall_3b43_trmm_199801-201807_v7-f
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>


This post outlines a process chain for downloading and organizing [Moderate Resolution Imaging Spectroradiometer (MODIS)](https://terra.nasa.gov/about/terra-instruments/modis) reflectance data (MODIS product MCD43A4) for a region covering Sub Saharan Africa using Karttur´s GeoImagine Framework. The processing of the MODIS data is covered in the [next](../modis-methods) post, and then follows posts with the [results](../modis-results).

# Prerequisites

To follow the process steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/) and download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github.

The [GeoImagine blog](https://karttur.github.io/geoimagine/) contains a post on [MODIS processing](https://karttur.github.io/geoimagine/blog/blog-MODIS-TWI/) that is more detailed compared to this post.

# MODIS

[MODIS](https://terra.nasa.gov/about/terra-instruments/modis) is an optical and thermal sensor carried on two satellites, [Terra](https://terra.nasa.gov/) (launched in 1999) and [Aqua](https://aqua.nasa.gov/) (launched in 2002). In this project you are going to use MODIS product MCD43A4 for estimating soil moisture dynamics at 465 m spatial resolution and 16 day intervals.

# Process chain

The principal steps for downloading and organizing MODIS data using Karttur's GeoImagine Framework include:

- Search online library for available tiles
- Register available tiles
- Download selected tiles
- Explode selected bands

In the Framework a process chain can be built as a series of calls to xml coded instructions. This section contains the calls and the remaining parts of the post details each called xml.

<button id= "toggleProcessChain" onclick="hiddencode('ProcessChain')">Hide/Show AfricaSubSahara_process_TRMM.txt</button>

<div id="ProcessChain" style="display:none">
{% capture text-capture %}
{% raw %}
```

```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

## Search online library

The way Karttur´s GeoImagine Framework is organized, you first have to search the online repository for available MODIS tiles, then register the search results in the Framework postgres database. Once the data is registered you can download and extract the actual MODIS data.

The MODIS online library is hosted by the [Land Processes Distributed Active Archive Center (LP DAAC) Data Pool](https://lpdaac.usgs.gov/data_access/data_pool). Users are required to log in with their [Earthdata](https://urs.earthdata.nasa.gov/home) login credentials to obtain data. The default solution within the Framework is to register your credentials in a <span class='file'>.netrc</span> file as described in [this](https://karttur.github.io/geoimagine/blog/blog-setup-dblink/) post.

The Framework solution for finding available tiles is to trawl the LP DDAC Data Pool using the commandline tool <span class ='terminalapp'>wget</span> ("web get"); if you need to install <span class ='terminalapp'>wget</span>, please consult [this](https://karttur.github.io/geoimagine/blog/) post. The process for searching the Data Pool holdings of MODIS products is [<span class='package'>searchdatapool</span>](https://karttur.github.io/geoimagine/subprocess/subproc-searchDataPool/).

{% capture foo %}{{page.TRMM-0160_tile_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0160_tile_M.html foo=foo %}

## Register available tiles

To transfer or register the search results to the GeoImagine Framework database you must run the process [<span class='package'>ModisSearchToDB</span>](https://karttur.github.io/geoimagine/subprocess/subproc-ModisSearchToDB/). This process reads the html files created by <span class ='terminalapp'>wget</span>, extracts the required information and inserts the information in the database.

{% capture foo %}{{page.TRMM-0160_tile_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0160_tile_M.html foo=foo %}

## Download selected tiles

With the available MODIS Data Pool holdings registered in the database you can download any of the registered data using [<span class='package'>downloadModisRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-downloadModisRegion/). When running the process you can either download the files on the fly, or write the download commands to a shell script file. The latter is the default. To change it you need to set the parameter _asscript_ to _False_.

{% capture foo %}{{page.TRMM-0160_tile_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0160_tile_M.html foo=foo %}

If you did not add the parameter _asscript_, including setting it to False, the process produces a script file that you must run manually. To run the shell script you must first make it executable, and then execute it:

<span class='terminal'>$ chmod 777 /path/to/script.sh</span>

<span class='terminal'>$ /path/to/script.sh</span>

If you choose to use batch scripting you have to re-run the same [<span class='package'>downloadModisRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-downloadModisRegion/) process to identify the downloaded tiles. Alternatively you can instead run the process [<span class='package'>CheckMODISRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-CheckMODISRegion/) but it does a more thorough database control and takes longer time.

## Explode selected bands

Each MODIS product contains several bands; which bands to explode are defined in the postgres table _modis.template_. When you installed Karttur's GeoImagine Framework some default bands were added to the table (see the [GeoImagine MODIS](https://karttur.github.io/geoimagine/blog/blog-MODIS-TWI/) post). The default for the product used here (MCD43A4) is to extract seven (7) spectral bands, which are the bands we are interested in. To eplode the MODIS hdf file, use the process
[<span class='package'>ExplodeMODISRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-ExplodeMODISRegion/).

{% capture foo %}{{page.TRMM-0161_tile_A}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0161_tile_A.html foo=foo %}

# Next steps

If you followed the tutorial you should now have a complete set of spectral images covering your region (Sub-Saharan Africa) for the defined period.
The [<span class='button'>Next</span>](#) step is to process the spectral bands and derive estimates of soil moisture.
