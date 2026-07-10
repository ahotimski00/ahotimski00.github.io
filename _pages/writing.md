---
layout: single
title: "Writing"
permalink: /writing/
author_profile: true
---

Notes on geospatial engineering, performance, and the gap between what's possible and what's standard practice.

---

{% for post in site.posts %}
## [{{ post.title }}]({{ post.url | relative_url }})

*{{ post.date | date: "%B %d, %Y" }}*

{% if post.excerpt %}{{ post.excerpt | strip_html }}{% endif %}

{% unless forloop.last %}---{% endunless %}
{% endfor %}