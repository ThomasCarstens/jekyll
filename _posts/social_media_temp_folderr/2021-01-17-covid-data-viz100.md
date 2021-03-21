---
layout: single
title: "Data visualizations for COVID in South Africa"
excerpt: "Handin for the DVIC Data Visualisation Course, Dec '20."
header:
  teaser: /assets/images/posts/covid-data-viz/police.jpg
  overlay_image: /assets/images/posts/covid-data-viz/police.jpg

#categories: Project

tags:
- Data visualisation

tags:
toc: true
toc_sticky: false
date: 2021-01-17
gallery:
  - image_path: /assets/images/posts/covid-data-viz/scatter_deaths.png
    alt: " Deaths in South Africa due to Covid-19 over December 2020"
    title: "Deaths in South Africa due to Covid-19 over December 2020"


gallery2:
  - image_path: /assets/images/posts/covid-data-viz/police.jpg
    alt: "Police in the streets of Alexandra Township, made up of over 20000 informal dwellings."
    title: "Subject categories, Try 2"
  - image_path: /assets/images/posts/covid-data-viz/military_covid.jpg
    alt: "Police in the streets of "
    title: "Subject categories, Try 2"
---
# Does human movement affects covid infections significantly?

My statistical analysis links up human mobility in South Africa to surges in infection.  I wish to have a data-driven idea whether significant human movement affects covid infections significantly. Using the Google Mobility Reports, I will be comparing the spikes in Virus infections to human movement in South Africa between 1 December 2020 and 29 December 2020.

## 1. infections

### Deaths in South Africa due to Covid-19 over December 2020

<div class="flourish-embed flourish-scatter" data-src="visualisation/4990187"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

<em> Adapted from the Coronavirus COVID-19 (2019-nCoV) Data Repository and Dashboard for South Africa (1) </em>

### Simple premise
My hypothesis H0 is: there is no significant correlation between human movement and virus propagation in South Africa of such period.

### Mobility data with Google location tracking over December 2020
Fortunately, Google supplies location-tracking data. As long as we consider this data to be representative of greater human mobility, we can try to see the story behind the data.

Here we look at how people moved between their workplace and residential areas. I chose this data because it brings out trends in human movement.

<div class="flourish-embed flourish-chart" data-src="visualisation/5007715"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

Interesting spikes of movement occurring around the 19th of December and the 26th of December. Perhaps when most people are travelling to see family and then to leave?

Let's get back to the question. Is there any evidence that human movement affects infection rates? Perhaps we could juxtapose these for any trends.

<div class="flourish-embed flourish-chart" data-src="visualisation/5007788"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

This data is interesting because the changes from the baseline are considerable (from 50 percent to -50 percent of the baseline). It's interesting how parks become more trendy, and... so does the virus.

Seen the incubation time for the virus is roughly 10 days, the 15 days prior to infection should be better examined for significant levels of human movement. This graph shows no evidence of a correlation.

## 3. Biggest takeaways

{% include gallery id="gallery2" caption="Was it worth bringing the police and the army into townships?" %}

Unfortunately this analysis did not reveal a correlation between significant human movement and the spread of the virus. This analysis is done on a national level, and seen the incubation time for the virus is roughly 10 days, the 15 days prior to infection should be better examined for significant levels of human movement.

# Bibliography

(1) the Coronavirus COVID-19 (2019-nCoV) Data Repository and Dashboard for South Africa, https://github.com/dsfsi/covid19za
