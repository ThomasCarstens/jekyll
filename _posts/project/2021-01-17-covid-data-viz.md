---
layout: single
title: "Data visualizations for COVID in South Africa"
excerpt: "Handin for the DVIC Data Visualisation Course, Dec '20'."
header:
  teaser: /assets/images/backgrounds/university-avenue.png
  overlay_image: /assets/images/backgrounds/university-avenue.png

categories: Project

tags:
- Data visualisation

tags:
toc: true
toc_sticky: false
date: 2021-01-17
gallery:
  - image_path: /assets/images/posts/covid-data-viz/scatter_deaths.png
    alt: " Deaths in South Africa due to Covid-19 over December 2020"
    title: " Deaths in South Africa due to Covid-19 over December 2020"


gallery2:
  - image_path: /assets/images/posts/drone-interactions/tutorials-at-the-dvic.PNG
    alt: "Subject categories, Try 2"
    title: "Subject categories, Try 2"

---
# Deaths in South Africa

My statistical analysis links up human mobility in South Africa to surges in infection.  I wish to have a data-driven idea whether significant human movement affects covid infections significantly. Using the Google Mobility Reports, I will be comparing the spikes in Virus infections to human movement in South Africa between 1 March 2020 and 4 January 2021.

{% include gallery id="gallery" caption="" %}

My hypothesis H0 is: there is no significant correlation between human movement and virus propagation in South Africa of such period.
This analysis is done on a national level, and seen the incubation time for the virus is roughly 10 days, the15 days prior to infection are examined for significant levels of human movement. Said otherwise, for each significant level of infection, we determine how often over 15 days the movement exceeded set bounds (in number of days). This information will be analysed in a final Poisson curve to determine if the spikes are in fact correlated or they are two random patterns.


<div class="flourish-embed flourish-chart" data-src="visualisation/4990512"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

<em>temporary</em>
Covid infections are analysed according to the gradient in the number of infections as a rough measure of infectability. Significant levels of infection are those that cross a certain threshold in gradient.
The nature of our location-tracking data is percentage according to a baseline. Therefore significant levels of movement could roughly be determined if it exceeds set bounds on a normal curve according to data available for South Africa.  
<em>temporary</em>

<div class="flourish-embed flourish-scatter" data-src="visualisation/4990187"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

Datasets: WHO information was not sufficient, more SA info here:
https://github.com/dsfsi/covid19za
