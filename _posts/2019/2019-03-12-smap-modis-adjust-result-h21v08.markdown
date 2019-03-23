---
layout: post
title: MODIS TWI assimilated to SMAP - h21v08
modified: '2019-03-12 20:17'
categories: tileassim
excerpt: Movie result for assimilation of MODIS TWI to SMAP for tile h21v08.
tags:
  - MODIS
  - SMAP
  - comparison
  - MCD43A4
  - Sub Saharan Africa
  - Process chain
  - h21v08
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-03-12 20:17'
comments: true
share: true
movie1: SMAPvsTWIx4_h21v08_2015121-2018361_002-modfit-9km
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post includes a single movie, showing the assimilation of MODIS derived soil moisture estimates with soil moisture estimated from SMAP. The methods for deriving the images and movies are presented [here](../../blog/smap-modis-adjust-methods/).

In the animation below, SMAP and TWI are both resampled to a 9 km spatial resolution. Each frame represents a 16 day period, with data force filled by a combination of interpolation and seasonal cycle long term average. The upper frames show SMAP and the the original TWI soil moisture estimates, the lower frames show TWI completely assimilated to SMAP (left), and a 50 % assimilation for non-flooded cells and with cells indicated as flooded or very wet in TWI retaining their original TWI values (right).

<figure>
<iframe src="{{ site.commonurl }}/movies/{{ site.data.movies[page.movie1].file }}" width="{{ site.data.movies[page.movie1].width }}" height="{{ site.data.movies[page.movie1].height }}" frameborder="0">
</iframe>
<figcaption> {{ site.data.movies[page.movie1].caption }} </figcaption>
</figure>
