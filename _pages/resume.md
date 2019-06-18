---
layout: archive
title: "Project portfolio and CV"
breadcrumbs: true
permalink: /cv/
share: true
comments: false
document_path: /assets/docs/Thomas_Carstens_webCV_11june.pdf
---

## Project Portfolio
<div>
{% for post in site.categories.Projects %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->

## Current CV <a download href="{{ page.document_path }}">[pdf]</a>

<iframe src="{{ page.document_path }}" width="100%" height="1000px"></iframe>
