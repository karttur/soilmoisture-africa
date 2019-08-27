---
layout: post
title: Rainfall, water balance and Earth´s water content - results
modified: '2019-01-28 20:17'
categories: blog
excerpt: Cross correlations between variations in rainfall, vertical water balance and equivalent water pillar depth
tags:
  - GRACE
  - Tropical Rainfall Measurement Mission
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2019-01-28 20:17'
comments: true
share: true

movie1: grace-trmm_xcorr_africasubsahara_200205-201612_RL05-f-1deg
movie2: grace-vwb_xcorr_africasubsahara_200205-201612_RL05-f-1deg
movie3: grace-vwbsurplus_xcorr_africasubsahara_200205-201612_RL05-f-1deg

fig1a: trendcomp_trmm-grace_africasubsahara_2003-2016_model@p-v7-RL05-1deg
fig1b: trendcomp_vwbsurplus-grace_africasubsahara_2003-2016_model@p-v7-RL05-1deg

fig2a: obs-lag_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig2b: obs-pearson_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig2c: obs-lag_vwb-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig2d: obs-pearson_vwb-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig2e: obs-lag_vwbsurplus-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig2f: obs-pearson_vwbsurplus-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1

fig3a: season-lag_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig3b: season-pearson_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig3c: tendency-lag_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig3d: tendency-pearson_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig3e: residual-lag_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig3f: residual-pearson_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1

fig4a: season-pearson-lag0_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig4b: season-pearson-lag1_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig4c: season-pearson-lag2_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1

fig5a: tendency-pearson-lag0_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig5b: tendency-pearson-lag1_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig5c: tendency-pearson-lag2_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig5d: tendency-pearson-lag3_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig5e: tendency-pearson-lag4_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig5f: tendency-pearson-lag5_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1

fig6a: residual-pearson-lag0_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig6b: residual-pearson-lag1_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1
fig6c: residual-pearson-lag2_trmm-xc-grace_africasubsahara_200301-201612M_v7-RL05-nadd-a1

---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

This post presents the graphical results of the analysis of the correlations between water input (rainfall or Vertical Water Balance [VWB]) and water storage (equivalent water pillar depth) for Sub-Saharan Africa. The processing for deriving the images and movies are presented in the [previous](../grace-trmm-vwb-crosscorr-methods/) post.

### Master vs slave movies

The movies below have the master (rainfall or VWB) as a smaller inset overlaying the slave (Earth's equivalent water pillar). All three movies clearly illustrate how the Intertropical Convergence Zone (ITCZ) governs the rainfall pattern, with the equivalent water pillar seemingly lagging behind. This is perhaps most clearly seen in the movie with the total VWB as master (the second movie).

#### Rainfall as master

<figure>
<iframe src="{{ site.commonurl }}/movies/{{ site.data.movies[page.movie1].file }}" width="{{ site.data.movies[page.movie1].width }}" height="{{ site.data.movies[page.movie1].height }}" frameborder="0">
</iframe>
<figcaption> {{ site.data.movies[page.movie1].caption }} </figcaption>
</figure>

#### Total VWB as master

<figure>
<iframe src="{{ site.commonurl }}/movies/{{ site.data.movies[page.movie2].file }}" width="{{ site.data.movies[page.movie2].width }}" height="{{ site.data.movies[page.movie2].height }}" frameborder="0">
</iframe>
<figcaption> {{ site.data.movies[page.movie2].caption }} </figcaption>
</figure>

#### Surplus VWB as master

<figure>
<iframe src="{{ site.commonurl }}/movies/{{ site.data.movies[page.movie3].file }}" width="{{ site.data.movies[page.movie3].width }}" height="{{ site.data.movies[page.movie3].height }}" frameborder="0">
</iframe>
<figcaption> {{ site.data.movies[page.movie3].caption }} </figcaption>
</figure>

### Trend comparisons

The comparison of trends in the figure below shows the congruence of the directions of significant (p<0.05) changes. The maps use the 9 classes defined in the [method](../grace-trmm-vwb-crosscorr-methods) post. The left panel shows the congruence between significant changes in rainfall and equivalent water pillar depth; the right panel the changes in surplus VWB and equivalent water pillar depth. The total VWB result is identical to the result for rainfall.

<figure class="half">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig1a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig1a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig1b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig1b].file }}" alt="image"></a>

	<figcaption>TO BE ADDED </figcaption>
</figure>

### Cross correlation water input vs water storage

The cross correlations capture the statistical relations of the movies above.

#### Observed cross correlations

The figure below shows the best lag and the corresponding Pearson number for observed (not decomposed) datasets. The slave (dependent) is the same in all panels: the equivalent water pillar depth depth estimates. From top to bottom the masters (drivers) are: rainfall, total VWB and surplus VWB.

<figure class="half">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2b].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2c].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2c].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2d].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2d].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2e].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2e].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig2f].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig2f].file }}" alt="image"></a>

	<figcaption> Best lag and corresponding Pearson number for observed (not decomposed) datasets. The slave (dependent) is the same in all panels: the equivalent water pillar depth depth estimates. From top to bottom the masters (drivers) are: rainfall, total VWB and surplus VWB </figcaption>
</figure>

The cross correlation results are almost identical when comparing rainfall and total VWB as the master or driver. The cross correlations then adopting surplus VWB as the driver are either equal to, or worse, compared to using total VWB (or rainfall).

#### Decomposed cross correlations of rainfall

The figure shows the best lag and the corresponding Pearson number for rainfall as master and equivalent water pillar depth as slave for three different time series components: top) season, center) trend (or tendency) and, bottom) residual.

<figure class="half">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3b].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3c].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3c].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3d].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3d].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3e].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3e].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig3f].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig3f].file }}" alt="image"></a>

	<figcaption>Best lag and corresponding Pearson number for rainfall as master and equivalent water pillar depth as slave for three different time series components, from top to bottom:  seasonal signal, trend (or tendency) and residual. </figcaption>
</figure>

The cross correlations for the decomposed data show highly varying results for the different components. The seasonal signals of rainfall and equivalent water pillar depth are highly correlated except along the equator and at some coastal regions. The lag between the rainfall and water pillar is between 1 and 2 months (see figure below). The correlation between the trends (tendencies) are strongly varying, including regions with negative correlations and with dominating longer lag times (see figure below). The correlations between the residuals are weak, but positive and with a lag of 1 month dominating  most of southern Africa (see below).

#### Seasonal lag correlations

The figure shows the Pearson number (correlation) for decomposed seasonal signals with rainfall as master and equivalent water pillar depth as slave, starting with no (0) lag and increasing with a lag of one month per map.

<figure class="third">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig4a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig4a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig4b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig4b].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig4c].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig4c].file }}" alt="image"></a>

	<figcaption>Pearson number (correlation) for decomposed seasonal signals with rainfall as master and equivalent water pillar depth as slave, the maps represent lags of 0, 1 and 2 months. </figcaption>
</figure>

#### Trend lag correlations

The figure shows the Pearson number (correlation) for decomposed trends (tendencies) with rainfall as master and equivalent water pillar depth as slave, starting with no (0) lag and increasing with a lag of one month per map.

<figure class="third">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig5a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig5a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig5b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig5b].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig5c].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig5c].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig5c].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig5c].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig5d].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig5d].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig5e].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig5e].file }}" alt="image"></a>

	<figcaption>Pearson number (correlation) for decomposed strends (endencies) with rainfall as master and equivalent water pillar depth as slave, the maps represent lags of 0, 1 and 2 months in the first row, and 3, 4 and 5 months in the second. </figcaption>
</figure>

#### Residual lag correlations

The figure shows the Pearson number (correlation) for decomposed residual with rainfall as master and equivalent water pillar depth as slave, starting with no (0) lag and increasing with a lag of one month per map.

<figure class="third">
  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig6a].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig6a].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig6b].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig6b].file }}" alt="image"></a>

  <a href="{{ site.commonurl }}/images/{{ site.data.images[page.fig6c].file }}"><img src="{{ site.commonurl }}/images/{{ site.data.images[page.fig6c].file }}" alt="image"></a>

	<figcaption>Pearson number (correlation) for decomposed residuals with rainfall as master and equivalent water pillar depth as slave, the maps represent lags of 0, 1 and 2 months. </figcaption>
</figure>
