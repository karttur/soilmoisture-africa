---
layout: post
title: Vertical Water Balance - Results
modified: '2019-01-23 20:17'
categories: blog
excerpt: Graphical results of VWB processing for Sub-Saharan Africa
tags:
- VWB
- Vertical Water Balance
- media
- figures
- movie
- animations
- Sub Saharan Africa
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-01-23 20:17'
comments: true
share: true

movie1: trmm-fao-vwb_3b43_africasubsahara_199801-201807_v7-f-m-30km
movie2: trmm-fao-vwb-surplus_3b43_africasubsahara_199801-201807_v7-f-m-30km
movie3: trmm-fao-vwb-deficit_3b43_africasubsahara_199801-201807_v7-f-m-30km

fig1a: avg-trmm-fao-vwb_3b43_africasubsahara_1998-2017_v7-f-m-A-30km
fig1b: avg-trmm-fao-vwb-surplus_3b43_africasubsahara_1998-2017_v7-f-m-A-30km
fig1c: avg-trmm-fao-vwb-deficit_3b43_africasubsahara_1998-2017_v7-f-m-A-30km

fig2a: ts-mdsl-trmm-fao-vwb_3b43_africasubsahara_1998-2017_v7-f-m-A-30km
fig2b: ts-mdsl-trmm-fao-vwb-surplus_3b43_africasubsahara_1998-2017_v7-f-m-A-30km
fig2c: ts-mdsl-trmm-fao-vwb-deficit_3b43_africasubsahara_1998-2017_v7-f-m-A-30km

fig3a: trmm-fao-vwb-change_3b43_africasubsahara_1998-2017_model-v7-f-m-A-30km
fig3b: trmm-fao-vwb-surplus-change_3b43_africasubsahara_1998-2017_model-v7-f-m-A-30km
fig3c: trmm-fao-vwb-deficit-change_3b43_africasubsahara_1998-2017_model-v7-f-m-A-30km
fig3d: trmm-fao-vwb-change_3b43_africasubsahara_1998-2017_model@p-v7-f-m-A-30km
fig3e: trmm-fao-vwb-surplus-change_3b43_africasubsahara_1998-2017_model@p-v7-f-m-A-30km
fig3f: trmm-fao-vwb-deficit-change_3b43_africasubsahara_1998-2017_model@p-v7-f-m-A-30km
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>
# Results

This post presents the graphical results of the Vertical Water Balance (VWB) analysis for Sub-Saharan Africa. The processing for deriving the images and movies are presented in the [previous](../vwb-methods/) post.

## Monthly VWB

The three movies below are constructed from all the VWB dates over Sub-Saharan Africa used in this project. The first movie shows the overall VWB; the second movie the surplus VWB (rainfall exceeding evapotranspiration); and the third movie the deficit VWB (evapotranspiration exceeding rainfall).

<figure>
<iframe src="{{ site.commonurl }}/movies/{{ site.data.movies[page.movie1].file }}" width="{{ site.data.movies[page.movie1].width }}" height="{{ site.data.movies[page.movie1].height }}" frameborder="0">
</iframe>
<figcaption> {{ site.data.movies[page.movie1].caption }} </figcaption>
</figure>

<figure>
<iframe src="{{ site.commonurl }}/movies/{{ site.data.movies[page.movie2].file }}" width="{{ site.data.movies[page.movie2].width }}" height="{{ site.data.movies[page.movie2].height }}" frameborder="0">
</iframe>
<figcaption> {{ site.data.movies[page.movie2].caption }} </figcaption>
</figure>

<figure>
<iframe src="{{ site.commonurl }}/movies/{{ site.data.movies[page.movie3].file }}" width="{{ site.data.movies[page.movie3].width }}" height="{{ site.data.movies[page.movie3].height }}" frameborder="0">
</iframe>
<figcaption> {{ site.data.movies[page.movie3].caption }} </figcaption>
</figure>

## VWB annual trends 1998-2017

The VWB statistics and trends are calculated from annually aggregated data.

### VWB mean

The three panels of the figure of annual mean VWB below show overall VWB, surplus VWB and deficit VWB. Note that regions that have overall surplus VWB, can have periods with deficits (and vice versa) and thus appear in all three panels.

<figure class="third">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig1a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig1a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig1b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig1b].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig1c].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig1c].file }}" alt="image"></a>

	<figcaption>Mean Vertical Water Balance (VWB) for Sub-Saharan Africa 1998-2017, the left panel shows the overall VWB, the middle surplus VWB and the right deficit VWB. </figcaption>
</figure>

### VWB trends

The three panels of the figure of trends in annual VWB below show overall VWB, surplus VWB and deficit VWB. many regions show different trends in wetting/drying when comparing the changes when separating surplus and deficit dominated periods. This is more clearly seen if you click one of the images and view the sequential maps at larger resolution.  

<figure class="third">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2b].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2c].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2c].file }}" alt="image"></a>

	<figcaption>Trends in annual Vertical Water Balance (VWB) for Sub-Saharan Africa 1998-2017, the left panel shows the overall VWB, the middle surplus VWB and the right deficit VWB. </figcaption>
</figure>

### VWB changes and significant trends

In the double row of panels in the figure of changes below, the top row shows the change in VWB between 1998 and 2017 for all regions; the bottom row only shows regions where the change has been significant (Mann-Kendall p<0.05). From left to right the panels show overall VWB, surplus VWB and deficit VWB. The change are more clearly seen if you click one of the images and view the sequential maps at larger resolution. Perhaps the most apparent result is that the regions with significant drying are much larger than regions with significant wetting.

<figure class="third">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3b].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3c].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3c].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3d].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3d].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3e].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3e].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3f].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3f].file }}" alt="image"></a>

	<figcaption>Absolut changes in annual Vertical Water Balance (VWB) for Sub-Saharan Africa 1998-2017, the left panels shows the overall VWB, the middle surplus VWB and the right deficit VWB; the top row shows changes for all regions while the bottom row shows regions with signification changes (Mann-Kendall p<0.05).</figcaption>
</figure>
