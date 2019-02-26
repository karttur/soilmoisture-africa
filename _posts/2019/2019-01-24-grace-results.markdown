---
layout: post
title: GRACE water pillar - results
modified: '2019-01-24 20:17'
categories: blog
excerpt: Graphical results of GRACE water pillar processing for Sub-Saharan Africa
tags:
- GRACE
- Gravity Recovery and Climate Experiment
- Water pillar
- media
- figures
- movie
- animations
- Sub Saharan Africa
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-01-24 20:17'
comments: true
share: true

movie1: grace-ave_cmwater_africasubsahara_200205-201612_RL05-f-1deg

fig1a: avg-grace-ave_cmwater_africasubsahara_2003-2016_RL05-f-A-1deg
fig1b: std-grace-ave_cmwater_africasubsahara_2003-2016_RL05-f-A-1deg

fig2a: ols-sl-grace-ave_cmwater_africasubsahara_2003-2016_RL05-f-A-1deg
fig2b: ts-mdsl-grace-ave_cmwater_africasubsahara_2003-2016_RL05-f-A-1deg
fig2c: ts-losl-grace-ave_cmwater_africasubsahara_2003-2016_RL05-f-A-1deg
fig2d: ts-hisl-grace-ave_cmwater_africasubsahara_2003-2016_RL05-f-A-1deg

fig3a: grace-ave-change_cmwater_africasubsahara_2003-2016_model-RL05-f-A-1deg
fig3b: grace-ave-change_cmwater_africasubsahara_2003-2016_model@p-RL05-f-A-1deg
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post presents the graphical results of the analysis of Earth's water content (equivalent water pillar depth), as estimated from remotely sensed gravitation, for Sub-Saharan Africa. The processing for deriving the images and movies are presented in the [previous](../grace-methods/) post.

## Monthly GRACE

The movie below is constructed from all the GRACE dates over Sub-Saharan Africa used in this project.

<figure>
<iframe src="{{ site.commonurl }}/movies/{{ site.data.movies[page.movie1].file }}" width="{{ site.data.movies[page.movie1].width }}" height="{{ site.data.movies[page.movie1].height }}" frameborder="0">
</iframe>
<figcaption> {{ site.data.movies[page.movie1].caption }} </figcaption>
</figure>

Note how the water depth varies seasonally, with the Intertropical Convergence Zone (ITCZ) bringing summer rains to southern Africa.

## GRACE annual trends 2003-2016

The GRACE equivalent water pillar depth statistics and trends are calculated from annually aggregated data.

### GRACE mean and standard deviation

<figure class="half">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig1a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig1a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig1b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig1b].file }}" alt="image"></a>

	<figcaption>Equivalent water pillar depth over sub-saharan Africa estimated from GRACE gravitational data for the period 2003 to 2016; the left panel shows average and the right standard deviation. The scaling is different between the two panels. </figcaption>
</figure>

### GRACE trends

<figure class="half">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2b].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2c].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2c].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2d].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2d].file }}" alt="image"></a>

	<figcaption>Comparison of regression slopes for equivalent water pillar depth over sub-saharan Africa estimated from GRACE gravitational data; clockwise, starting with the upper left panel, the maps show ordinary least square (OLS), median Theil-Sen (TS), upper bound of the 95 % confidence interval of the median TS slope, and the lower left panel the lower bound of the 95 % confidence interval of the median TS slope. </figcaption>
</figure>

### GRACE changes and significant trends

<figure class="half">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3b].file }}" alt="image"></a>

	<figcaption>Estimated absolute changes in GRACE equivalnet water pillar depth 2003 to 2016: the left panel shows the change for all regions, the right only changes where the Mann-Kendall test indicates significant changes (p<0.05).  </figcaption>
</figure>

Note how the estimates of the Theil-Sen 95 % confidence level fits well with the map of significant changes as estimated from the Mann-Kendall test. Regions that show a negative (positive) trend at the 95 % upper (lower) confidence interval of the TS are also indicated as areas with significant negative (positive) trend using the MK test.
