---
layout: archive
permalink: /about/
title: "Home"
header:
  overlay_image: /assets/images/backgrounds/paris-skyline.jpg


last_modified_at: 2019-06-11T11:22:24-05:00
toc: false
---
<h2>Oh, hello!</h2>
<i>Welcome to my blog and my showroom of my own projects.</i>

I am a mechanical and mechatronic engineer by training and I also do software development.
I have worked on projects designing and developing electro-mechanical systems as well as mobile apps.
Right now I am studying robotics (Ecole EFREI, Master's in droides and drones, 2019-2021).
Today's technology is growing fast, and my preferred strategy is to develop solutions that empower users.
My previous projects have explored this topic: an [everyday consumer product](https://thomascarstens.github.io/tech-project/braai-tongs/), a [user-centred online platform](https://thomascarstens.github.io/tech-project/App-for-education/),
a [healthcare robot](https://thomascarstens.github.io/tech-project/Service-robot/). I write about personal projects and some tech news [on my blog](https://thomascarstens.github.io/tags/), and I am I am involved in some [tech business ventures](https://thomascarstens.github.io/business/). While I'm in Paris, I am financing my studies with work as a developer.
If you are interested in what I am doing please contact me

I am a mechanical and mechatronic engineer by training and I also do software development.
I have worked on projects designing and developing electro-mechanical systems as well as mobile apps.
Right now I am studying robotics (Ecole EFREI, Master's in droides and drones, 2019-2021).
Today's technology is growing fast, and my preferred strategy is to develop solutions that empower users.
My previous projects have explored this topic: an everyday consumer product, a user-centred online platform,
a healthcare robot. I write about personal projects and some tech news on my blog, and I am involved in some tech business ventures. While I'm in Paris, I am financing my studies with work as a developer.
If you are interested in what I am doing please contact me

{% for post in site.posts %}
  <article class="tile" itemscope itemtype="http://schema.org/Article">
  <!-- TITLE -->
    <h2 class="post-title" itemprop="name">
    <a href="{{ site.url }}{{ post.url }}">{{ post.title }} --- {% if post.date %} <time class="entry-date date published" datetime="{{ post.date | date: "%Y-%m-%d" }}" itemprop="datePublished">{{ post.date | date: "%B %d, %Y" }}</time>{% endif %} </a>
    </h2>
  <!-- DATE   
    <h5>{% if post.date %}<p class="entry-date date published"><time datetime="{{ post.date | date: "%Y-%m-%d" }}" itemprop="datePublished">{{ post.date | date: "%B %d, %Y" }}</time></p>{% endif %}</h5>-->
  <!-- DESCRIPTION -->  
    <h5 class="post-excerpt" itemprop="description">{{ post.excerpt | strip_html | truncate: 160 }}</h5>
  <!-- HEADER -->
    <a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}" class="post-teaser">{% if post.header.teaser %}<img src="../{{ post.header.teaser }}" alt="teaser" itemprop="image">
      {% else %}<img src="{{ site.url }}/images/{{ site.teaser }}" alt="teaser" itemprop="image">{% endif %}</a>
  </article><!-- /.tile -->
  _____________________________________________________________________________
{% endfor %}
---
