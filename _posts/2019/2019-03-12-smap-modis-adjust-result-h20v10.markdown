---
layout: post
title: Adjust MODIS TWI with SMAP - results MODIS tile h20v10
modified: '2019-03-12 20:17'
categories: blog
excerpt: SMAP Assimilation of TWI
tags:
  - MODIS
  - SMAP
  - MCD43A4
  - Sub Saharan Africa
  - Process chain
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-03-12 20:17'
comments: true
share: true
movie1: SMAPvsTWI_h20v10_2015121-2018361_002-modfit-9km
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post presents graphics for the assimilation of MODIS derived soil moisture estimates with soil moisture estimated from SMAP. The methods for deriving the images and movies are presented in the [previous](../smap-modis-adjust-methods/) post.

In the animation below, SMAP and TWI are both resampled to a 9 km spatial resolution. Each frame represents a 16 day period, with data force filled by a combination of interpolation and seasonal cycle long term average.

<figure>
<iframe src="{{ site.commonurl }}/movies/{{ site.data.movies[page.movie1].file }}" width="{{ site.data.movies[page.movie1].width }}" height="{{ site.data.movies[page.movie1].height }}" frameborder="0">
</iframe>
<figcaption> {{ site.data.movies[page.movie1].caption }} </figcaption>
</figure>
