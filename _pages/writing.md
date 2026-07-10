---
layout: single
title: "Writing"
permalink: /writing/
author_profile: true
---

Half field notes, half opinions on maps, data, and geospatial workflows.

---

{% for post in site.posts %}
## [{{ post.title }}]({{ post.url | relative_url }})

*{{ post.date | date: "%B %d, %Y" }}*

{% if post.excerpt %}{{ post.excerpt | strip_html }}{% endif %}

{% unless forloop.last %}---{% endunless %}
{% endfor %}