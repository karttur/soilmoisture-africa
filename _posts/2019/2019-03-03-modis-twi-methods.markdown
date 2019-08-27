---
layout: post
title: MODIS Transformed Wetness Index (TWI)
modified: '2019-03-03 20:17'
categories: blog
excerpt: Calculate MODIS TWI for regional project
tags:
  - MODIS
  - TWI
  - MCD43A4
  - Sub Saharan Africa
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-03-03 20:17'
comments: true
share: true
movie1: rainfall_3b43_trmm_199801-201807_v7-f


---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post covers the calculations of a Transformed Wetness Index (TWI) from Moderate Resolution Imaging Spectroradiometer (MODIS) reflectance data. The calculations are done for MODIS tiles covering Sub Saharan Africa at 16 day intervals.  The downloading and organization of the MODIS data is covered in the [previous](../modis-getdata) post. The [next](../modis-twi-assimilation/) post details how to assimilate MODIS TWI to SMAP soil moisture estimates as an alternative to traditional downscaling. Graphical presentation of some of the results are in the [this](../modis-results) post.

# Prerequisites

To follow the process steps in this post you must set up a [Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/) and download and install [Karttur's GeoImagine Framework](https://karttur.github.io/geoimagine/blog/blog-import-project-eclipse/) from Github. You must also have imported and exploded the MODIS data as outlined in the [previous](../modis-getdata) post.

# TWI

The Transformed Wetness Index (TWI) is a non-linear normalized difference index that uses biophysical vectors representing the soil line and water derived from an orthogonal linear transformation of multi-spectral reflection data. I have used TWI for [mapping global tropical wetlands]( https://doi.org/10.1111/gcb.13689) and also for [wetland change detection](https://doi.org/10.3390/rs10040611). The advantage of TWI is its high spatial resolution compared to (passive) microwave data. TWI, however, suffers from biases due to both soil and vegetation conditions. In this project I thus use SMAP data to adjust TWI by assimilation as outlined in the [next](../modis-twi-assimilation/) post.

# Process chain

The principal steps for calculating TWI from reflectance data using Karttur's GeoImagine Framework include:

- Linear transformation
- Non-linear normalized difference
- Conversion of TWI to percentage

In the Framework a process chain can be built as a series of calls to xml coded instructions. This section contains the calls and the remaining parts of the post details each called xml.

<button id= "toggleProcessChain" onclick="hiddencode('ProcessChain')">Hide/Show AfricaSubSahara_process_TRMM.txt</button>

<div id="ProcessChain" style="display:none">
{% capture text-capture %}
{% raw %}
```
###################################
###    MODIS TWI calculations   ###
###################################


```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

## Linear transformation

A linear transformation converts the band data to biophysical indexes. In Remote Sensing circles this is known as a Tasseled Cap Transformation (TCT). TCTs are, however, usually defined using a fixed matrix. TWI is instead defined from a set of optimized vectors for identifying difference in soil moisture and derived using a Gram-Schmidt orthogonalization. The process for inferring the orthogonal (linear) transformation is [<span class='package'>LinearTransformMODISRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-TransformMODISRegion/):

{% capture foo %}{{page.TRMM-0160_tile_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0160_tile_M.html foo=foo %}

## Non-linear normalized difference

The non-linear normalized difference uses scale preserving transformation and rotation to combine two input vectors and produce a foreground (FG) and a background (BG) index. TWI is a FG index defined from the transformed vectors representing soil brightness and surface wetness. The Non-linear normalized difference transformation to derive TWI is calibrated to generate the largest difference between wet and dry regions. The process for the scale preserving transformation and rotation generating FG and BG is [<span class='package'>fgbgmodisRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-fgbgmodisRegion/):

{% capture foo %}{{page.TRMM-0160_tile_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0160_tile_M.html foo=foo %}

## Conversion of TWI to percentage

TWI derived from the scale preserving transformation and rotation above is arbitrary scaled, and also non-linearly related to soil-moisture expressed as vol/vol or percent. For comparing TWI with other measures of soil-moisture, usually expressed as vol/vol, TWI needs to be converted to vol/vol, or percentage. Comparing TWI with ground probed soil-moisture I have defined an algorithm for this, and it can be implemented in the Framework using the process [<span class='package'>twipercentmodisRegion</span>](https://karttur.github.io/geoimagine/subprocess/subproc-twipercentmodisRegion/)

{% capture foo %}{{page.TRMM-0160_tile_M}}{% endcapture %}
{% include xml/AfricaSubSahara_TRMM-0160_tile_M.html foo=foo %}

# Next steps

In the [<span class='button'>Next</span>](../modis-twi-assimilation/) step time series data from the Soil Moisture Active Passive (SMAP) mission are used for adjusting TWI.
