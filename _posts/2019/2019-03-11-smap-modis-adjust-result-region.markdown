---
layout: post
title: Adjust MODIS TWI with SMAP - results
modified: '2019-03-11 20:17'
categories: blog
excerpt: SMAP Assimilation of TWI
tags:
  - MODIS
  - SMAP
  - MCD43A4
  - Sub Saharan Africa
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-03-11 20:17'
comments: true
share: true
movie1: SMAPvsTWI_africasubsahara_2015121-2018361_002-modfit-9km
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post presents graphics for the assimilation of MODIS derived soil moisture estimates with soil moisture estimated from SMAP. The methods for deriving the images and movies are presented in the [previous](../smap-modis-adjust-methods/) post.

Below you can watch a movie that compares SMAP and TWI, both at approximately 9 km spatial resolution, for the whole of Sub Saharan Africa. Under the following links you can view movies representing each MODIS SINgrid tile. Each of these movies show SMAP and MODIS TWI and two versions of assimilation of MODIS TWI to SMAP.

- [h16v08](../../tileassim/smap-modis-adjust-result-h16v08)
- [h16v09](../../tileassim/smap-modis-adjust-result-h16v09)
- [h16v12](../../tileassim/smap-modis-adjust-result-h16v12)
- [h17v08](../../tileassim/smap-modis-adjust-result-h17v08)
- [h17v10](../../tileassim/smap-modis-adjust-result-h17v10)
- [h17v12](../../tileassim/smap-modis-adjust-result-h17v12)
- [h18v08](../../tileassim/smap-modis-adjust-result-h18v08)
- [h18v09](../../tileassim/smap-modis-adjust-result-h18v09)
- [h19v08](../../tileassim/smap-modis-adjust-result-h19v08)
- [h19v09](../../tileassim/smap-modis-adjust-result-h19v09)
- [h19v10](../../tileassim/smap-modis-adjust-result-h19v10)
- [h19v11](../../tileassim/smap-modis-adjust-result-h19v11)
- [h19v12](../../tileassim/smap-modis-adjust-result-h19v12)
- [h20v08](../../tileassim/smap-modis-adjust-result-h20v08)
- [h20v09](../../tileassim/smap-modis-adjust-result-h20v09)
- [h20v10](../../tileassim/smap-modis-adjust-result-h20v10)
- [h20v11](../../tileassim/smap-modis-adjust-result-h20v11)
- [h20v12](../../tileassim/smap-modis-adjust-result-h20v12)
- [h21v08](../../tileassim/smap-modis-adjust-result-h21v08)
- [h21v09](../../tileassim/smap-modis-adjust-result-h21v09)
- [h21v10](../../tileassim/smap-modis-adjust-result-h21v10)
- [h21v11](../../tileassim/smap-modis-adjust-result-h21v11)
- [h22v08](../../tileassim/smap-modis-adjust-result-h22v08)
- [h22v09](../../tileassim/smap-modis-adjust-result-h22v09)
- [h23v08](../../tileassim/smap-modis-adjust-result-h23v08)
- [h23v09](../../tileassim/smap-modis-adjust-result-h23v09)
- [h23v10](../../tileassim/smap-modis-adjust-result-h23v10)

<figure>
<iframe src="{{ site.commonurl }}/movies/{{ site.data.movies[page.movie1].file }}" width="{{ site.data.movies[page.movie1].width }}" height="{{ site.data.movies[page.movie1].height }}" frameborder="0">
</iframe>
<figcaption> {{ site.data.movies[page.movie1].caption }} </figcaption>
</figure>
